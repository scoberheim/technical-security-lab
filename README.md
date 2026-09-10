# Technical Security Lab

## Contents

- [Proxmox Setup](#proxmox-setup)
- [Network Diagram](#network-diagram)
- [Security Controls](#security-controls)
- [Virtual Machines](#virtual-machines)
- [Asset Management](#asset-management)
- [GRC Projects](#grc-projects)

This repository documents the design, implementation and ongoing development of my technical cybersecurity homelab.

The lab provides a controlled environment for developing practical skills in **security architecture, network segmentation, system administration, vulnerability management, security controls and risk assessment**.

The environment is built using **Proxmox VE** and **OPNsense**, with multiple virtual machines representing common enterprise systems and security testing platforms. The lab is intentionally segmented to allow security testing and experimentation while protecting the primary network.

The lab also serves as the technical foundation for my **Governance, Risk and Compliance (GRC) portfolio**, providing a realistic environment in which to apply concepts such as asset identification, risk assessment, security controls, network security and business impact.

### Lab Objectives

* Develop practical cybersecurity and infrastructure security skills
* Understand and document network architecture and security controls
* Implement network segmentation and firewall policies
* Maintain an inventory and classification of lab assets
* Conduct security testing in a controlled environment
* Apply risk assessment and security governance principles
* Produce professional technical documentation suitable for a cybersecurity portfolio

The lab is continuously evolving as new security and GRC projects are developed.

---

# Proxmox Setup

### Hardware

| Component | Specification | Purpose |
|---|---|---|
| CPU | Intel Core i5 5th Gen | Virtual machine processing |
| RAM | 16 GB | VM allocation and hypervisor operation |
| Network | Intel I350-T4 | Dedicated network interfaces |
| Network | Realtek RTL8111 | Additional network connectivity |
| Storage | 256 GB SSD | Proxmox and virtual machine storage |


### Installation

Proxmox VE was installed directly onto the physical server hardware, providing a dedicated Type 1 hypervisor platform for hosting the cybersecurity lab.

A bootable USB installation media was created using Rufus and the Proxmox VE ISO. Installing Proxmox directly onto the hardware provides dedicated resources for the virtualised lab environment and allows the network, storage and virtual machines to be centrally managed.


### Network Architecture

| Component | Interface | Network | Purpose |
|---|---|---|---|
| OPNsense | WAN | ISP Network | Internet connectivity |
| OPNsense | LAN | 192.168.0.0/24 | Primary LAN |
| OPNsense | VLAN 30 | 192.168.30.0/24 | Cyber Lab |
| Proxmox | vmbr1 | WAN | OPNsense WAN |
| Proxmox | vmbr0 | LAN | Internal networking |

---

# Security Controls

The lab implements several security controls designed to reduce the risk of unauthorised access and limit the impact of security incidents.

### Network Segmentation
- Primary LAN separated from Cyber Lab environment
- VLAN 30 used for security testing
- Firewall policies control traffic between networks

### Firewall
- OPNsense provides network perimeter security
- Traffic between network segments is controlled through firewall rules
- NAT provides controlled Internet access to lab systems

### Access Control
- Administrative access restricted to authorised systems
- Management interfaces separated from testing environments

### Security Testing
- Kali Linux provides a controlled security testing platform
- Windows 11 provides a target endpoint for security testing
- Testing is performed within the isolated lab environment

# Virtual Machines

| VM / Asset                  | Role                            | Category | Security / GRC Purpose                                      |
| --------------------------- | ------------------------------- | -------- | ----------------------------------------------------------- |
| OPNsense Firewall            | Network Security                | IT       | Internet gateway, firewall and network security             |
| Ubuntu Desktop               | Endpoint                        | IT       | Linux workstation / security testing                        |
| Windows 11 Desktop           | Endpoint                        | IT       | Windows workstation / general computing                     |
| Kali Linux Desktop           | Security Workstation            | IT       | Security testing and vulnerability assessment               |
| Ubuntu Server                | Server                          | IT       | File / application server                                   |
| Proxmox                      | Infrastructure / Virtualisation | IT       | Hosts and manages virtual machines                          |
| Azure Storage Account        | Cloud Storage                   | IT       | Cloud storage for Azure-hosted data                         |
| Microsoft Sentinel Workspace | Security Service                | Security | Centralised security monitoring, logging and incident management |

---
# Network Diagram
This diagram illustrates the architecture of my cybersecurity homelab, built using Proxmox VE and OPNsense. The environment is designed to provide hands-on experience with network security, system administration, virtualization, and security operations concepts.
Internet connectivity is provided through an OPNsense virtual firewall, with separate WAN (vmbr1) and LAN (vmbr0) bridges configured within Proxmox. The primary LAN provides connectivity to physical devices and wireless clients, while an isolated Cyber Lab network (VLAN 30) hosts security testing systems including Kali Linux, Windows 11 and Ubuntu virtual machines.

Network segmentation and firewall policies are used to control traffic between environments, allowing safe experimentation with security tools and techniques while protecting the primary network. This lab serves as a platform for developing practical skills in firewall administration, network architecture, vulnerability assessment, incident investigation, and Microsoft security technologies.


<img width="641" height="501" alt="Network Diagram drawio" src="https://github.com/user-attachments/assets/2bbe3e9d-68f4-4414-9042-1fc7a46794da" />

---
# Asset Management

The lab maintains an asset inventory to support risk assessment and security management.

| Asset | Type | Environment | Criticality |
|---|---|---|---|
| Proxmox | Hypervisor | Infrastructure | High |
| OPNsense | Firewall | Network | High |
| Windows Server | Server | Lab | High |
| Windows 11 | Endpoint | Lab | Medium |
| Ubuntu | Server | Lab | Medium |
| Kali Linux | Security Testing | Lab | Low |
