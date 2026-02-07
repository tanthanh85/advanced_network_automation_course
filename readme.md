# Advanced Network Automation Course
## Course Introduction

---

## Course Overview

Modern enterprise networks are still too often operated through isolated scripts, manual configuration, or tool‑centric workflows. At scale, these approaches fail. Today’s networks must be treated as software‑driven systems—composed of automation platforms, APIs, controllers, data sources, CI/CD pipelines, security controls, and observability layers that operate continuously and reliably. As a result, network automation has evolved from task execution into a full software engineering and operations discipline, increasingly augmented by AI‑driven insights.

This course is an advanced, production‑focused network automation program designed for engineers and teams who already have strong Python and automation fundamentals and are ready to move into automation architecture, system design, and operational excellence. Rather than teaching tools in isolation, the course focuses on how real enterprise automation systems are designed, integrated, tested, secured, deployed, observed, and evolved over time.

Throughout the course, learners will collaboratively design and evolve a single end‑to‑end automation platform. This platform is progressively enhanced using:

*   Object‑oriented software architecture and domain modeling
*   Intent‑based automation and Infrastructure as Code (IaC) workflows
*   Enterprise network controllers and their APIs
*   CI/CD‑driven testing, validation, and safe deployment
*   Containerized and reproducible runtime environments
*   Observability pipelines for telemetry, logs, and events
*   AIOps capabilities, including anomaly detection, correlation, and AI‑assisted troubleshooting and decision support

Automation is treated as a team sport. The course also emphasizes collaboration between architects, developers, operators, security owners, and approvers, reflecting how automation actually functions inside large enterprises.

To mirror real‑world practice, the course standardizes on:

*   GitLab as the system of record and CI/CD control plane
*   HashiCorp Vault for centralized, secure secrets management

This course is not certification‑driven. It is designed for engineers and teams who want to think, design, and operate like network automation and AIOps architects, building systems that are scalable, observable, secure, and ready for AI‑assisted operations in production environments.

---

## Target Audience

This course is intended for experienced practitioners, including:

- Senior network engineers/teams transitioning into network automation and NetDevOps roles  
- Network automation engineers and software developers  
- Network architects responsible for large‑scale, automated environments  
- Engineers designing or operating enterprise automation platforms  

The course assumes professional experience with networking and automation and is not suitable for beginners.

---

## Prerequisites

Learners are expected to have completed prior training or possess equivalent experience in the following areas:

- Basic Python programming for network automation  
- Managing Python development environments  
- Hands-on concurrency using threading and asyncio
- CLI automation using Netmiko and Paramiko  
- API‑based automation using RESTful APIs, RESTCONF/YANG, and NETCONF/YANG  
- Infrastructure as Code concepts and workflows  
- Basic knowledge of Ansible for configuration management  
- Experience on building Python‑based network management and monitoring tools  
- Evaluating and selecting appropriate automation tools  

This course **does not** cover Python fundamentals, introductory automation concepts, or networking basics.

---

## Course Content Outline

### Module 1 – Software Architecture for Network Automation

- Automation as a software system  
- Object‑oriented domain modeling for networks  
- Protocol abstraction and multi‑vendor design  
- Reliability, performance, and observability by design  
- GitLab as the automation control plane  
- Secure credential handling using HashiCorp Vault  

**Lab:** Build an object‑oriented automation core with secure credential access

---

### Module 2 – Source of Truth & Infrastructure as Code Systems

- Desired state vs observed state  
- NetBox as a Source of Truth  
- Declarative and imperative automation patterns  
- Advanced use of Ansible, Terraform, and Cisco NSO  
- Secure secrets retrieval from Vault in IaC workflows  

**Lab:** Build an IaC control system with drift detection and Vault‑backed secrets

---

### Module 3 – Controller‑Driven Network Automation

- Cisco DNAC, ACI, and SD‑WAN architectures  
- Automation boundaries and controller APIs  
- Avoiding double sources of truth  
- Secure API authentication using Vault‑managed credentials  

**Lab:** Automate workflows using enterprise controllers with Vault‑integrated authentication

---

### Module 4 – Network Testing, Validation & Assurance

- Automation testing strategies  
- Python unit testing for automation systems  
- pyATS for pre‑ and post‑change validation  
- Testing automation behavior in CI pipelines  

**Lab:** Build a validation pipeline integrated with GitLab CI/CD

---

### Module 5 – Containers & Kubernetes for Network Automation

- Containerizing automation platforms  
- Docker and Kubernetes deployment models  
- Secure secrets injection using HashiCorp Vault  
- Scaling, resilience, and runtime troubleshooting  

**Lab:** Deploy and scale the automation platform with Vault‑backed secrets

---

### Module 6 – Observability, Analytics & Assurance

- Logs, metrics, traces, and OpenTelemetry  
- Network path visibility with ThousandEyes  
- Event correlation and analytics with Splunk  
- Observability for both automation platforms and network behavior  

**Lab:** Build an observable automation system and correlate network and automation data

---

### Module 7 – AI‑Assisted Network Automation

- Practical use cases for AI in network operations  
- LLM‑assisted diagnostics and decision support  
- Edge AI and closed‑loop automation  
- Security and governance considerations for AI‑driven systems  

**Lab:** Implement AI‑assisted operational workflows with guardrails

---

### Capstone Project – Production‑Grade Network Automation Platform

- Integrate all course components  
- Operate, observe, scale, and secure the automation system  
- Use GitLab CI/CD as the deployment backbone  
- Manage secrets centrally with HashiCorp Vault  
- Demonstrate architectural and operational maturity  

---

## Key Learning Outcomes

By the end of this course, learners will be able to:

- Design network automation systems using object‑oriented software architecture  
- Manage network intent and state safely using Source of Truth and IaC principles  
- Securely manage credentials and secrets using HashiCorp Vault  
- Integrate automation workflows with GitLab CI/CD pipelines  
- Automate and operate enterprise network controllers and platforms  
- Implement robust testing, validation, and assurance pipelines  
- Deploy and scale automation platforms using containers and Kubernetes  
- Build observability pipelines to diagnose and correlate automation and network issues  
- Apply AI techniques responsibly to assist network operations and decision‑making  
- Operate, troubleshoot, and evolve production‑grade network automation systems  

---

## Repository and Workflow Standards

- **Source Control & CI/CD:** GitLab  
- **Secrets Management:** HashiCorp Vault  
- **Infrastructure Modeling:** NetBox  
- **Automation & Orchestration:** Python, Ansible, Terraform, Cisco NSO  
- **Runtime Platforms:** Docker, Kubernetes  
- **Observability:** ThousandEyes, Splunk, OpenTelemetry  

These standards are used throughout the course to reflect **real‑world enterprise automation environments**.