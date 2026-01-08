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