Lab 1 – Team‑Based Network Automation
=====================================================

Secure, Reviewed, and CI/CD‑Driven Deployment
-------------------------------------------------

* * *

1\. Lab Purpose
---------------

This lab introduces learners to enterprise‑style network automation, where changes are:

*   Designed by an architect
*   Implemented by specialists
*   Reviewed and approved by a manager
*   Executed automatically via CI/CD
*   Secured using centralized secrets management

Unlike traditional labs, no single learner performs all tasks. Each learner takes a role, collaborates through GitLab, and follows a controlled workflow.

* * *

2\. Learning Objectives
-----------------------

By the end of this lab, learners will be able to:

*   Apply object‑oriented design to network automation
*   Use YAML as a Source of Truth (SoT)
*   Render the configuration using Jinja2
*   Retrieve credentials securely from HashiCorp Vault
*   Deploy configuration using Netmiko
*   Use GitLab branching, merge requests, and approvals
*   Trigger network changes via CI/CD pipelines
*   Perform safe rollback using Git

* * *

3\. Lab Duration and Format
---------------------------

*   Duration: 90–120 minutes
*   Format: Team‑based (5 learners)
*   Difficulty: Advanced
*   Target audience: Network / automation engineers

* * *

4\. Team Roles (Mandatory)
--------------------------

Each learner must assume one role only.

### Role 1 – Network Automation Architect

*   Designs repository structure and workflow
*   Assigns tasks
*   Owns architectural decisions
*   Writes `README.md`

* * *

### Role 2 – Network Intent Owner (SoT Owner)

*   Defines ACL intent in YAML
*   Does not write Python
*   Does not manage credentials

* * *

### Role 3 – Automation Developer

*   Writes Python automation code
*   Uses Netmiko, Jinja2, Vault
*   Does not define intent values

* * *

### Role 4 – Vault & Security Owner

*   Configures HashiCorp Vault
*   Stores credentials securely
*   Enforces least‑privilege access

* * *

### Role 5 – Project Manager / Approver

*   Owns the `main` branch
*   Reviews merge requests
*   Approves or rejects changes

* * *

5\. Lab Architecture
--------------------

Copy Code

    lab1-iosxe-acl/
    ├── intent/
    │   └── acl.yaml
    ├── templates/
    │   └── iosxe_acl.j2
    ├── automation/
    │   ├── main.py
    │   ├── device.py
    │   └── vault_client.py
    ├── .gitlab-ci.yml
    └── README.md
    

* * *

6\. Environment Setup
---------------------

### Cisco IOS XE (DevNet Sandbox)

Use the Cisco IOS XE on Cisco Developer Sandbox.  


* * *

### GitLab Requirements

*   GitLab project created
*   `main` branch protected
*   Merge requests required
*   GitLab Runner available

* * *

### Vault Requirements

*   HashiCorp Vault (dev mode acceptable)
*   Vault address and token available to CI runner

* * *

7\. Step‑by‑Step Lab Tasks
--------------------------

* * *

Step 1 – Project Initialization
-------------------------------

Owner: Architect + Project Manager

1.  Create a new GitLab repository
2.  Protect the `main` branch
3.  Require merge request approval
4.  Create initial `README.md` describing:
    *   Architecture
    *   Workflow
    *   Roles

✅ No automation code yet

* * *

Step 2 – Vault Setup
--------------------

Owner: Vault & Security Owner

Start Vault (example):

```bash
    vault server -dev
```   

Store router credentials:

```bash
    vault kv put network/iosxe
      host=ios-xe-mgmt.cisco.com
      username=developer
      password=Cisco123!
```

Configure GitLab Runner environment variables:

```text
    VAULT_ADDR=http://vault:8200
    VAULT_TOKEN=s.xxxxx
```  

✅ No secrets in Git  
✅ No secrets in pipeline logs

* * *

Step 3 – Define Network Intent (SoT)
------------------------------------

Owner: Network Intent Owner

Create file `intent/acl.yaml`:

```yaml
    device:
      name: iosxe-sandbox
      acl:
        name: LAB_ACL
        interface: GigabitEthernet1
        direction: in
        entries:
          - seq: 10
            action: permit
            protocol: ip
            source: 10.10.10.0 0.0.0.255
            destination: any
          - seq: 20
            action: deny
            protocol: ip
            source: any
            destination: any
```   

Steps:

1.  Create feature branch: `feature/acl-intent`
2.  Commit with clear message
3.  Open merge request

* * *

Step 4 – Create Jinja2 Template
-------------------------------

Owner: Automation Developer

Create `templates/iosxe_acl.j2`:

```jinja2

    ip access-list extended {{ acl.name }}
    {% for entry in acl.entries %}
     {{ entry.seq }} {{ entry.action }} {{ entry.protocol }} {{ entry.source }} {{ entry.destination }}
    {% endfor %}
    !
    interface {{ acl.interface }}
     ip access-group {{ acl.name }} {{ acl.direction }}
```   

* * *

Step 5 – Implement Vault Client
-------------------------------

Owner: Automation Developer

Create `automation/vault_client.py`:

```python

    import hvac
    import os
    
    def get_router_credentials():
        client = hvac.Client(
            url=os.environ["VAULT_ADDR"],
            token=os.environ["VAULT_TOKEN"]
        )
    
        secret = client.secrets.kv.v2.read_secret_version(
            path="network/iosxe"
        )
    
        return secret["data"]["data"]
```   

* * *

Step 6 – Implement Device Abstraction
-------------------------------------

Owner: Automation Developer

Create `automation/device.py`:

```python

    from netmiko import ConnectHandler
    
    class IOSXEDevice:
        def __init__(self, host, username, password):
            self.params = {
                "device_type": "cisco_ios",
                "host": host,
                "username": username,
                "password": password
            }
    
        def push_config(self, commands):
            with ConnectHandler(**self.params) as conn:
                output = conn.send_config_set(commands)
                conn.save_config()
            return output
```    

* * *

Step 7 – Implement Main Automation Script
-----------------------------------------

Owner: Automation Developer

Create `automation/main.py`:

```python

    import yaml
    from jinja2 import Environment, FileSystemLoader
    from vault_client import get_router_credentials
    from device import IOSXEDevice
    
    def load_intent():
        with open("intent/acl.yaml") as f:
            return yaml.safe_load(f)
    
    def render_acl(acl):
        env = Environment(loader=FileSystemLoader("templates"))
        template = env.get_template("iosxe_acl.j2")
        return template.render(acl=acl).splitlines()
    
    def main():
        intent = load_intent()
        acl = intent["device"]["acl"]
    
        creds = get_router_credentials()
    
        device = IOSXEDevice(
            host=creds["host"],
            username=creds["username"],
            password=creds["password"]
        )
    
        commands = render_acl(acl)
        output = device.push_config(commands)
    
        print(output)
    
    if __name__ == "__main__":
        main()
```    

* * *

Step 8 – GitLab CI/CD Pipeline
------------------------------

Owner: Architect + Project Manager

Create `.gitlab-ci.yml`:

```yaml
    stages:
      - validate
      - deploy
    
    validate:
      stage: validate
      image: python:3.11
      script:
        - pip install pyyaml
        - python -c "import yaml; yaml.safe_load(open('intent/acl.yaml'))"
      only:
        - merge_requests
    
    deploy:
      stage: deploy
      image: python:3.11
      script:
        - pip install netmiko hvac pyyaml jinja2
        - python automation/main.py
      only:
        - main
      when: manual
```   

✅ Deployment only after merge  
✅ Manual trigger for safety

* * *

Step 9 – Review and Approval
----------------------------

Owner: Project Manager (with Architect input)

Approval checklist:

*   ✅ Intent is clear
*   ✅ No secrets in Git
*   ✅ Vault integration works
*   ✅ CI validation passed
*   ✅ Rollback plan documented

Approve merge request.

* * *

Step 10 – Deployment and Rollback
---------------------------------

1.  Trigger deploy job manually
2.  Verify ACL on router
3.  Revert commit to demonstrate rollback
4.  Re‑run pipeline

* * *

8\. Assessment Criteria
-----------------------

Learners are assessed on:

*   Architecture correctness
*   Role discipline
*   Security practices
*   Git collaboration
*   CI/CD usage
*   Rollback capability

* * *

9\. Key Takeaways
-----------------

*   Automation is a team sport
*   Security is architectural
*   CI/CD is the execution engine
*   Approval is evidence‑based
*   Rollback is mandatory