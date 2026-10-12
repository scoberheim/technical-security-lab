# Technical Security Lab

## Contents

- [Proxmox Setup](#proxmox-setup)
- [Network Diagram](#network-diagram)
- [Security Controls](#security-controls)
- [Virtual Machines](#virtual-machines)
- [Asset Management](#asset-management)
- [GRC Projects](#grc-projects)

This repository documents how I designed, built and run my cybersecurity homelab.

I use the lab to practise security architecture, network segmentation, system administration, vulnerability management and risk assessment. It runs on **Proxmox VE** with an **OPNsense** firewall, and the virtual machines stand in for common enterprise systems and a security testing platform. Testing happens on an isolated network so it can't affect my home network.

The lab is also the environment behind my [GRC case study](https://github.com/scoberheim/Risk-Assessment-For-Small-Technology-Environment), where I carry out an asset register, risk assessment and control mapping against it.

### Lab objectives

* Build practical cybersecurity and infrastructure skills
* Document the network architecture and security controls
* Set up network segmentation and firewall policies
* Keep an inventory of lab assets, classified by criticality
* Run security tests in a controlled environment
* Apply risk assessment and security governance to a real setup
* Keep clear technical documentation

I add to the lab as I take on new security and GRC projects.

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

I installed Proxmox VE directly onto the server hardware as a Type 1 hypervisor, using a bootable USB made with Rufus and the Proxmox VE ISO. Running it on bare metal gives the lab dedicated resources and lets me manage the network, storage and virtual machines from one place.


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

These controls reduce the risk of unauthorised access and limit the damage if something goes wrong.

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
The diagram shows how the homelab is built with Proxmox VE and OPNsense.

Internet traffic comes in through an OPNsense virtual firewall, with separate WAN (vmbr1) and LAN (vmbr0) bridges configured in Proxmox. The primary LAN connects physical devices and wireless clients. An isolated Cyber Lab network (VLAN 30) holds the security testing machines: Kali Linux, Windows 11 and Ubuntu.

Firewall policies control traffic between the two networks, so I can try out security tools and techniques without putting the primary network at risk. I use the lab to practise firewall administration, network architecture, vulnerability assessment, incident investigation and Microsoft security tools.


<img width="641" height="501" alt="Network Diagram drawio" src="https://github.com/user-attachments/assets/2bbe3e9d-68f4-4414-9042-1fc7a46794da" />

---
# Asset Management

I keep an asset inventory for the lab to support risk assessment and security management. The full asset register is in the [GRC case study](https://github.com/scoberheim/Risk-Assessment-For-Small-Technology-Environment/blob/main/asset-register.md).

| Asset | Type | Environment | Criticality |
|---|---|---|---|
| Proxmox | Hypervisor | Infrastructure | High |
| OPNsense | Firewall | Network | High |
| Windows Server | Server | Lab | High |
| Windows 11 | Endpoint | Lab | Medium |
| Ubuntu | Server | Lab | Medium |
| Kali Linux | Security Testing | Lab | Low |

---
# GRC Projects

- [Information security risk assessment and risk register](https://github.com/scoberheim/Risk-Assessment-For-Small-Technology-Environment): 16 risks assessed using NIST SP 800-30, including AI-related risks
- [Control mapping to NIST CSF 2.0](https://github.com/scoberheim/Risk-Assessment-For-Small-Technology-Environment/blob/main/control-mapping.md), with ISO/IEC 27001:2022 Annex A in progress
