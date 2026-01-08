Advanced Network Automation Course
==================================

Module 0 – Course Introduction and Foundations
----------------------------------------------

* * *

Module Objectives
-----------------

This module 0 is to review basic network automation topics then followed by an introduction to some advanced network automation topics.

*   Review on how modern networks are engineered and operated as software systems
*   Review on how to build and manage a professional automation development environment
*   Review on how to apply Git as the single source of truth for automation systems
*   Understand CI/CD pipelines and their role in network automation
*   Review on how to write and analyze Python code interacting with:
    *   RESTful APIs
    *   RESTCONF
    *   NETCONF
    *   CLI devices using Netmiko/Scapli...
    *   JSON/XML/YAML data representation
*   Introduction to an expert‑level troubleshooting and systems mindset
*   (Optional) Describe the structure and expectations of the Cisco DevNet Expert (v1.1) 

* * *

0.1 The Evolution of Network Automation
---------------------------------------

### 0.1.1 From Manual Operations to Software Systems

Traditional network operations relied heavily on:

*   Interactive CLI sessions
*   Manual change tracking
*   Post‑change verification

While effective at small scale, this approach does not scale to modern environments involving:

*   Hybrid and multi‑cloud connectivity
*   Large numbers of devices
*   Continuous application changes

Modern networks are now software‑controlled systems, where:

*   APIs replace CLI as the primary interface
*   Desired state replaces imperative commands
*   Automation pipelines replace manual workflows

Network engineers must therefore think and operate as software engineers with networking expertise.

* * *

### 0.1.2 Automation as a First‑Class System

Automation is no longer a collection of scripts. It is:

*   Designed
*   Versioned
*   Tested
*   Deployed
*   Monitored

Failure to treat automation as a system leads to fragile solutions that break under scale or change.

* * *

0.2 DevNet Expert Practical Exam Context
----------------------------------------

### 0.2.1 Exam Philosophy

The DevNet Expert Practical Exam is:

*   Fully hands‑on
*   Scenario‑based
*   Time‑constrained
*   Integration‑focused

You are evaluated on your ability to:

*   Understand requirements quickly
*   Modify existing systems
*   Debug failures
*   Make sound design decisions

The exam assumes prior knowledge and does not provide tutorials.

* * *

### 0.2.2 Example Exam Scenario

You are given:

*   A Git repository with automation code
*   A failing CI/CD pipeline
*   A brief requirement:  
    _“Fix the pipeline and ensure the service deploys successfully.”_

You must:

1.  Inspect the code
2.  Understand the failure
3.  Apply a minimal fix
4.  Validate end‑to‑end behavior

This course is structured to mirror that experience.

* * *

0.3 Engineering the Development Environment
-------------------------------------------

### 0.3.1 Python as the Automation Language

Python is used because it offers:

*   Rich networking libraries
*   Native HTTP and data handling
*   Broad industry adoption

However, Python requires discipline to avoid dependency and environment issues.

* * *

### 0.3.2 Virtual Environments

Always isolate project dependencies.
```bash
python3 -m venv venv
source venv/bin/activate
```
This ensures:

*   Reproducibility
*   Predictable behavior
*   CI/CD compatibility

* * *

### 0.3.3 Dependency Management

Use pinned dependencies.
```text
# requirements.txt
requests==2.31.0
ncclient==0.6.15
netmiko==4.3.0
pyyaml==6.0.1
```
Install dependencies:
```bash
pip install -r requirements.txt
```
0.4 Git as the Single Source of Truth
-------------------------------------

### 0.4.1 Git Beyond Version Control

At expert level, Git is:

*   A system of record
*   A deployment trigger
*   A rollback mechanism

If a change is not in Git, it should not exist in production.

* * *

### 0.4.2 Repository Structure Example
```text
automation-project/
├── api/
│   └── app.py
├── netconf/
│   └── config.xml
├── restconf/
│   └── payload.json
├── cli/
│   └── netmiko_script.py
├── tests/
│   └── test_api.py
├── requirements.txt
└── Dockerfile
```
### 0.4.3 Safe Rollback with Git
```bash
git log --oneline
git revert <commit-hash>
```
This creates a new commit that undoes a change without rewriting history.

* * *

0.5 CI/CD Pipelines for Automation
----------------------------------

### 0.5.1 Why CI/CD Matters

CI/CD ensures that:

*   Changes are validated automatically
*   Errors are caught early
*   Deployments are repeatable

Automation without CI/CD is fragile.

* * *

### 0.5.2 Typical Pipeline Stages

1.  Validate (linting, syntax checks)
2.  Test (unit tests, API tests)
3.  Build (containers)
4.  Deploy (automation execution)
5.  Verify (post‑checks)

* * *

### 0.5.3 Example Pipeline (Conceptual)
```yaml
stages:
  - validate
  - test
  - deploy

validate:
  script:
    - python -m py_compile api/app.py

test:
  script:
    - pytest tests/

deploy:
  script:
    - python deploy.py
```
* * *

0.6 Python REST API Fundamentals
--------------------------------

### 0.6.1 Generic REST API Example
```python
import requests

url = "https://api.example.com/devices"
headers = {"Authorization": "Bearer TOKEN"}

response = requests.get(url, headers=headers, timeout=5)
response.raise_for_status()

devices = response.json()
for device in devices:
    print(device["hostname"])
```
Key concepts:

*   HTTP methods
*   Status codes
*   JSON parsing
*   Error handling

* * *

0.7 RESTCONF with Python
------------------------

### 0.7.1 RESTCONF Basics

RESTCONF provides RESTful access to YANG‑modeled data.

Base URL:
```text
https://<device>/restconf/data
```
Headers:
```text
Accept: application/yang-data+json
Content-Type: application/yang-data+json
```
### 0.7.2 RESTCONF GET Example
```python
from requests.auth import HTTPBasicAuth
import requests

url = "https://10.10.10.1/restconf/data/ietf-interfaces:interfaces"
headers = {"Accept": "application/yang-data+json"}

response = requests.get(
    url,
    headers=headers,
    auth=HTTPBasicAuth("admin", "password"),
    verify=False
)

print(response.json())
```
### 0.7.3 RESTCONF PUT Example
```python
payload = {
  "ietf-interfaces:interface": {
    "name": "Loopback10",
    "description": "RESTCONF interface",
    "type": "iana-if-type:softwareLoopback",
    "enabled": True
  }
}

url = "https://10.10.10.1/restconf/data/ietf-interfaces:interfaces/interface=Loopback10"

response = requests.put(
    url,
    json=payload,
    headers=headers,
    auth=HTTPBasicAuth("admin", "password"),
    verify=False
)

print(response.status_code)
```
RESTCONF enforces:

*   YANG structure
*   Idempotent configuration

* * *

0.8 NETCONF with Python
-----------------------

### 0.8.1 NETCONF Overview

NETCONF uses:

*   SSH
*   XML
*   RPC operations

Python library:

*   `ncclient`

* * *

### 0.8.2 NETCONF Connection Example
```python
from ncclient import manager

with manager.connect(
    host="10.10.10.1",
    port=830,
    username="admin",
    password="password",
    hostkey_verify=False
) as m:
    print(m.server_capabilities)
```
### 0.8.3 NETCONF edit‑config Example
```python
config = """
<config>
  <interfaces xmlns="urn:ietf:params:xml:ns:yang:ietf-interfaces">
    <interface>
      <name>Loopback20</name>
      <description>NETCONF Interface</description>
      <enabled>true</enabled>
    </interface>
  </interfaces>
</config>
"""

with manager.connect(
    host="10.10.10.1",
    port=830,
    username="admin",
    password="password",
    hostkey_verify=False
) as m:
    response = m.edit_config(target="running", config=config)
    print(response)
```
0.9 Netmiko for CLI Automation
------------------------------

### 0.9.1 When to Use Netmiko

Netmiko is useful for:

*   Legacy devices
*   CLI‑only features
*   Quick imperative changes

* * *

### 0.9.2 Netmiko Example
```python
from netmiko import ConnectHandler

device = {
    "device_type": "cisco_ios",
    "host": "10.10.10.1",
    "username": "admin",
    "password": "password",
}

connection = ConnectHandler(**device)
output = connection.send_command("show ip interface brief")
print(output)

commands = [
    "interface Loopback30",
    "description Netmiko Interface",
    "ip address 10.30.30.1 255.255.255.255"
]

connection.send_config_set(commands)
connection.save_config()
connection.disconnect()
```
0.10 Tool Selection: Expert Perspective
---------------------------------------


| Tool       | Primary Use                         |
|------------|-------------------------------------|
| REST APIs  | Controllers, applications           |
| RESTCONF  | YANG-based declarative configuration |
| NETCONF   | Transactional configuration         |
| Netmiko   | CLI-based imperative changes        |

Expert engineers choose tools intentionally.

* * *

0.11 Troubleshooting Discipline
-------------------------------

### 0.11.1 Systematic Debugging

1.  Identify failure
2.  Read logs
3.  Reproduce locally
4.  Apply minimal fix
5.  Validate end‑to‑end

Example error:
```text
ModuleNotFoundError: No module named 'ncclient'
```
Fix:

*   Add dependency
*   Commit
*   Re‑run pipeline

* * *

0.12 Summary
------------

Module 0 established the foundational knowledge and professional practices required for expert‑level network automation. It framed networks as software systems, emphasized Git‑driven workflows and CI/CD pipelines, and introduced Python‑based interaction with REST APIs, RESTCONF, NETCONF, and CLI devices. These foundations are essential for all subsequent modules and for success in the Cisco DevNet Expert Practical Exam.

* * *

Review Questions
----------------

1.  Why is Git considered a control plane for automation?
2.  When should RESTCONF be preferred over Netmiko?
3.  How does CI/CD reduce automation risk?
4.  Why are virtual environments critical?
5.  What distinguishes expert‑level troubleshooting?

* * *

### Next Module

Module 1 – Software Design, Development, and Deployment
