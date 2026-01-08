Advanced Network Automation Course
==================================

Module 0 – Course Introduction & Foundations
--------------------------------------------

### Hands‑On Lab Guide

* * *

Lab Overview
------------

This lab validates that your development environment, workflows, and foundational automation skills are ready for expert‑level work. Rather than building complex automation, you will:

*   Prepare a professional automation workspace
*   Validate Python environment isolation
*   Use Git as a system of record
*   Execute a basic CI/CD‑style workflow
*   Interact with network devices using:
    *   REST APIs
    *   RESTCONF
    *   NETCONF
    *   Netmiko
*   Practice expert‑level troubleshooting techniques

> Important:  
> This lab mirrors the DevNet Expert Practical Exam mindset. You are expected to:
> 
> *   Read errors carefully
> *   Diagnose issues independently
> *   Validate results explicitly

* * *

Lab Objectives
--------------

By completing this lab, you will be able to:

*   Build and validate a Python automation environment
*   Use Git as the authoritative source of automation logic
*   Execute and troubleshoot automation scripts
*   Interact programmatically with network devices using multiple interfaces
*   Explain when and why to use REST, RESTCONF, NETCONF, or CLI automation
*   Demonstrate disciplined troubleshooting methodology

* * *

Lab Environment Requirements
----------------------------

You will need one of the following:

*   Cisco IOS XE device (physical or virtual), or
*   Cisco DevNet Sandbox (IOS XE on CSR1000v)

### Required Tools

*   Python 3.9+
*   Git
*   pip
*   Docker (optional but recommended)
*   Python libraries:
    *   requests
    *   ncclient
    *   netmiko
    *   pyyaml

* * *

Lab Topology (Logical)
----------------------
```text
[ Your Laptop ]
     |
     |  (HTTPS / SSH)
     |
[ IOS XE Device ]
```
  
Section 1 – Project Workspace and Python Environment
-------------------------------------------------------

### Objective

Create a reproducible, isolated automation workspace.

* * *

### Step 1.1 – Create Project Directory
```bash
mkdir devnet-expert-module0
cd devnet-expert-module0
```
### Step 1.2 – Create Python Virtual Environment
```bash
python3 -m venv venv
source venv/bin/activate
```
Validate:
```bash
which python
```
### Step 1.3 – Create requirements.txt
```text
requests==2.31.0
ncclient==0.6.15
netmiko==4.3.0
pyyaml==6.0.1
```
Install dependencies:
```bash
pip install -r requirements.txt
```
Section 2 – Git as the Source of Truth
--------------------------------------

### Objective

Use Git to track all automation artifacts.

* * *

### Step 2.1 – Initialize Git Repository
```bash
git init
git status
```
### Step 2.2 – Create Initial Project Structure
```text
devnet-expert-module0/
├── rest/
├── restconf/
├── netconf/
├── cli/
├── requirements.txt
└── README.md
```
### Step 2.3 – Initial Commit
```bash
git add .
git commit -m "Initial project structure and dependencies"
```
Validation Checkpoint
```bash
git log --oneline
```
Section 3 – Python REST API Interaction
---------------------------------------

### Objective

Validate basic REST API interaction and error handling.

* * *

### Step 3.1 – Create REST API Script

File: `rest/rest_api_test.py`
```python
import requests

url = "https://api.example.com/status"
headers = {"Accept": "application/json"}

try:
    response = requests.get(url, headers=headers, timeout=5)
    response.raise_for_status()
    print("API Response:", response.json())
except requests.exceptions.RequestException as e:
    print("API request failed:", e)
```
### Step 3.2 – Execute Script
```bash
python rest/rest_api_test.py
```
Section 4 – RESTCONF Interaction
--------------------------------

### Objective

Retrieve and configure YANG‑modeled data using RESTCONF.

* * *

### Step 4.1 – RESTCONF GET Interfaces

File: `restconf/get_interfaces.py`
```python
import requests
from requests.auth import HTTPBasicAuth

url = "https://<DEVICE_IP>/restconf/data/ietf-interfaces:interfaces"
headers = {"Accept": "application/yang-data+json"}

response = requests.get(
    url,
    headers=headers,
    auth=HTTPBasicAuth("admin", "password"),
    verify=False
)

print(response.json())
```
### Step 4.2 – RESTCONF PUT Loopback Interface

File: restconf/config_loopback.py
```python
payload = {
  "ietf-interfaces:interface": {
    "name": "Loopback10",
    "description": "RESTCONF Lab Interface",
    "type": "iana-if-type:softwareLoopback",
    "enabled": True
  }
}

url = "https://<DEVICE_IP>/restconf/data/ietf-interfaces:interfaces/interface=Loopback10"

response = requests.put(
    url,
    headers={"Content-Type": "application/yang-data+json"},
    auth=HTTPBasicAuth("admin", "password"),
    json=payload,
    verify=False
)

print("Status Code:", response.status_code)
```
Validation Checkpoint
```text
show ip interface brief
```
Section 5 – NETCONF Interaction
-------------------------------

### Objective

Use NETCONF to perform transactional configuration.

* * *

### Step 5.1 – NETCONF Capability Discovery

File: `netconf/netconf_capabilities.py`
```python
from ncclient import manager

with manager.connect(
    host="<DEVICE_IP>",
    port=830,
    username="admin",
    password="password",
    hostkey_verify=False
) as m:
    for cap in m.server_capabilities:
        print(cap)
```
### Step 5.2 – NETCONF edit‑config

File: netconf/config_loopback.xml
```xml
<config>
  <interfaces xmlns="urn:ietf:params:xml:ns:yang:ietf-interfaces">
    <interface>
      <name>Loopback20</name>
      <description>NETCONF Lab Interface</description>
      <enabled>true</enabled>
    </interface>
  </interfaces>
</config>
```
File: netconf/edit_config.py
```python
from ncclient import manager

with open("config_loopback.xml") as f:
    config = f.read()

with manager.connect(
    host="<DEVICE_IP>",
    port=830,
    username="admin",
    password="password",
    hostkey_verify=False
) as m:
    response = m.edit_config(target="running", config=config)
    print(response)
```
Section 6 – CLI Automation with Netmiko
---------------------------------------

### Objective

Automate CLI‑based configuration safely.

* * *

### Step 6.1 – Netmiko Script

File: `cli/netmiko_loopback.py`
```python
from netmiko import ConnectHandler

device = {
    "device_type": "cisco_ios",
    "host": "<DEVICE_IP>",
    "username": "admin",
    "password": "password"
}

connection = ConnectHandler(**device)

commands = [
    "interface Loopback30",
    "description Netmiko Lab Interface",
    "ip address 10.30.30.1 255.255.255.255"
]

connection.send_config_set(commands)
connection.save_config()
connection.disconnect()
```
Section 7 – Git‑Driven Workflow Validation
------------------------------------------

### Objective

Demonstrate Git‑based change tracking and rollback.

* * *

### Step 7.1 – Commit Changes
```bash
git add .
git commit -m "Module 0 automation lab completed"
```
### Step 7.2 – Simulate a Bad Change and Rollback
```bash
git revert HEAD
```
Section 8 – Troubleshooting Exercise
------------------------------------

### Scenario

Uninstall ncclient.
```bash
pip uninstall ncclient
python netconf/netconf_capabilities.py
```
Expected failure:
```bash
ModuleNotFoundError: No module named 'ncclient'
```
Resolution

* Identify missing dependency
* Reinstall
* Re‑run script

Lab Completion Criteria
-----------------------

You have successfully completed this lab if you can:

*   Run all scripts without errors
*   Explain tool selection decisions
*   Recover from dependency failures
*   Validate configuration changes on the device
*   Use Git to manage and rollback changes

* * *

Lab Summary
-----------

This lab validated your readiness for expert‑level automation by ensuring you can build, execute, troubleshoot, and version automation workflows using industry‑standard tools and protocols. These skills are foundational for all subsequent modules and mirror the expectations of the Cisco DevNet Expert Practical Exam.

