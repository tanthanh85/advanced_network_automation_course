# Advanced Network Automation Course
## Course Introduction

---

## Course Overview

Modern enterprise networks are no longer managed through isolated scripts or manual configuration. They are **software‑driven systems** composed of automation platforms, APIs, controllers, data sources, and observability pipelines that must operate reliably at scale. As a result, network automation has evolved from task automation into a **software engineering discipline**.

This course is an **advanced, production‑focused network automation program** designed for engineers who already possess strong Python and automation fundamentals and are ready to move into **automation architecture, system design, and operational excellence**. Rather than focusing on individual tools in isolation, the course emphasizes **how automation systems are designed, integrated, deployed, observed, and evolved in real enterprise environments**.

Learners will work with object‑oriented automation architectures, Infrastructure as Code systems, enterprise network controllers, testing and validation frameworks, container platforms, observability tools, and AI‑assisted operational techniques. Throughout the course, emphasis is placed on **design trade‑offs, real‑world constraints, and practical decision‑making**, ensuring that learners can build automation systems that are robust, maintainable, and production‑ready.

This course is **not certification‑driven**. It is intended for engineers who want to **think and operate like network automation architects**.

---

## Target Audience

This course is intended for experienced practitioners, including:

- Senior network engineers transitioning into automation and NetDevOps roles
- Network automation engineers and developers
- Site Reliability Engineers (SREs) working with networked systems
- Network architects responsible for large‑scale, automated environments
- Technical professionals designing or operating enterprise automation platforms

The course assumes professional experience with networking and automation and is not suitable for beginners.

---

## Prerequisites

Learners are expected to have completed prior training or possess equivalent experience in the following areas:

- Python programming for network automation
- Managing Python development environments
- Concurrency using threading and asyncio
- CLI automation using Netmiko and Paramiko
- API‑based automation using REST and NETCONF/YANG
- Infrastructure as Code concepts and workflows
- Ansible for device provisioning and configuration management
- Automation of network security policies (ACLs, firewalls)
- Building Python‑based network management tools
- Centralized configuration management, monitoring, and alerting
- Evaluating and selecting appropriate automation tools

This course **does not** cover Python basics, introductory automation concepts, or networking fundamentals.

---

## Course Content Outline

### Phase 1 – Automation Architecture & Object‑Oriented Design  
**Module 1: Software Architecture for Network Automation**

- Automation as a software system
- Object‑oriented domain modeling for networks
- Protocol abstraction and multi‑vendor design
- Reliability, performance, and observability by design
- Git and CI/CD as the automation control plane  

**Lab:** Build an object‑oriented automation core

---

### Phase 2 – Intent, State & Infrastructure as Code  
**Module 2: Source of Truth & IaC Systems**

- Desired vs observed state
- NetBox as Source of Truth
- Declarative and imperative automation patterns
- Advanced use of Ansible and Terraform  

**Lab:** Build an IaC control system with drift detection

---

### Phase 3 – Network Controllers & Domain Automation  
**Module 3: Controller‑Driven Automation**

- DNAC, ACI, and SD‑WAN architectures
- Automation boundaries and controller APIs
- Avoiding double sources of truth  

**Lab:** Automate workflows using enterprise controllers

---

### Phase 4 – Testing, Validation & Assurance  
**Module 4: Network Testing & Validation**

- Automation testing strategies
- Python unit testing for automation systems
- pyATS for pre‑ and post‑change validation  

**Lab:** Build a validation pipeline integrated with CI/CD

---

### Phase 5 – Runtime Platforms & Scale  
**Module 5: Containers & Kubernetes for Automation**

- Containerizing automation platforms
- Docker and Kubernetes deployment models
- Scaling, resilience, and runtime troubleshooting  

**Lab:** Deploy and scale the automation platform

---

### Phase 6 – Observability, Analytics & Assurance  
**Module 6: Observability with ThousandEyes & Splunk**

- Logs, metrics, traces, and OpenTelemetry
- Network path visibility with ThousandEyes
- Event correlation and analytics with Splunk  

**Lab:** Build an observable automation system

---

### Phase 7 – AI in Network Automation  
**Module 7: AI‑Assisted Network Automation**

- Practical use cases for AI in network operations
- LLM‑assisted diagnostics and decision support
- Edge AI and closed‑loop automation  

**Lab:** Implement AI‑assisted operational workflows

---

### Capstone Project  
**Production‑Grade Network Automation Platform**

- Integrate all course components
- Operate, observe, scale, and secure the automation system
- Demonstrate architectural and operational maturity

---

## Key Learning Outcomes

By the end of this course, learners will be able to:

- Design network automation systems using object‑oriented software architecture
- Manage network intent and state safely using Source of Truth and IaC principles
- Integrate automation with enterprise network controllers and platforms
- Implement robust testing, validation, and assurance pipelines for network changes
- Deploy and scale automation platforms using containers and Kubernetes
- Build observability pipelines to diagnose and correlate automation and network issues
- Apply AI techniques responsibly to assist network operations and decision‑making
- Operate, troubleshoot, and evolve production‑grade network automation systems