# Advanced Network Automation  
## Course Introduction

---

## Course Overview

Modern enterprise networks are no longer managed through isolated scripts or manual configuration. They are **software‑driven systems** composed of automation platforms, APIs, controllers, data sources, and observability pipelines that must operate reliably at scale. As a result, network automation has evolved from task automation into a **software engineering discipline**.

This course is an **advanced, production‑focused network automation program** designed for engineers who already possess strong Python and automation fundamentals and are ready to move into **automation architecture, system design, and operational excellence**. Rather than focusing on individual tools in isolation, the course emphasizes **how automation systems are designed, integrated, deployed, observed, secured, and evolved in real enterprise environments**.

Throughout the course, learners will build and evolve a **single automation platform**, progressively enhancing it with object‑oriented design, Infrastructure as Code workflows, enterprise network controllers, testing and validation pipelines, containerized runtime environments, observability systems, and AI‑assisted operational capabilities.

This course adopts **GitLab as the standard code repository and CI/CD platform** and **HashiCorp Vault as the centralized secrets management system**, reflecting real‑world enterprise automation practices.

This course is **not certification‑driven**. It is intended for engineers who want to **think and operate like network automation architects**.

---

## Target Audience

This course is intended for experienced practitioners, including:

- Senior network engineers transitioning into automation and NetDevOps roles
- Network automation engineers and software developers
- Site Reliability Engineers (SREs) working with networked systems
- Network architects responsible for large‑scale, automated environments
- Engineers designing or operating enterprise automation platforms

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
- GitLab as the automation control plane
- Secure credential handling using HashiCorp Vault  

**Lab:** Build an object‑oriented automation core with secure credential access

---

### Phase 2 – Intent, State & Infrastructure as Code  
**Module 2: Source of Truth & IaC Systems**

- Desired vs observed state
- NetBox as Source of Truth
- Declarative and imperative automation patterns
- Advanced use of Ansible and Terraform
- Secure secrets retrieval from Vault in IaC workflows  

**Lab:** Build an IaC control system with drift detection and Vault‑backed secrets

---

### Phase 3 – Network Controllers & Domain Automation  
**Module 3: Controller‑Driven Automation**

- DNAC, ACI, and SD‑WAN architectures
- Automation boundaries and controller APIs
- Avoiding double sources of truth
- Secure API authentication using Vault‑managed credentials  

**Lab:** Automate workflows using enterprise controllers with Vault‑integrated authentication

---

### Phase 4 – Testing, Validation & Assurance  
**Module 4: Network Testing & Validation**

- Automation testing strategies
- Python unit testing for automation systems
- pyATS for pre‑ and post‑change validation
- Testing automation behavior in CI pipelines  

**Lab:** Build a validation pipeline integrated with GitLab CI/CD

---

### Phase 5 – Runtime Platforms & Scale  
**Module 5: Containers & Kubernetes for Automation**

- Containerizing automation platforms
- Docker and Kubernetes deployment models
- Secure secrets injection using Vault
- Scaling, resilience, and runtime troubleshooting  

**Lab:** Deploy and scale the automation platform with Vault‑backed secrets

---

### Phase 6 – Observability, Analytics & Assurance  
**Module 6: Observability with ThousandEyes & Splunk**

- Logs, metrics, traces, and OpenTelemetry
- Network path visibility with ThousandEyes
- Event correlation and analytics with Splunk
- Observability for both automation and network behavior  

**Lab:** Build an observable automation system and correlate network and automation data

---

### Phase 7 – AI in Network Automation  
**Module 7: AI‑Assisted Network Automation**

- Practical use cases for AI in network operations
- LLM‑assisted diagnostics and decision support
- Edge AI and closed‑loop automation
- Security and governance considerations for AI‑driven systems  

**Lab:** Implement AI‑assisted operational workflows with guardrails

---

### Capstone Project  
**Production‑Grade Network Automation Platform**

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
- **Automation & Orchestration:** Python, Ansible, Terraform  
- **Runtime Platforms:** Docker, Kubernetes  
- **Observability:** ThousandEyes, Splunk, OpenTelemetry  

These standards are used throughout the course to reflect **real‑world enterprise automation environments**.