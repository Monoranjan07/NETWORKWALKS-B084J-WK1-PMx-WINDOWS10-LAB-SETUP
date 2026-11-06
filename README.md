<div align="center">

# 🪟 Windows 10 Cybersecurity Lab Setup

### Building and Configuring a Windows 10 Virtual Machine in an Isolated NAT Network Environment

NetworkWalks Cybersecurity Internship Program · Batch B084J · Week 01 · Extra Project – Windows 10 Lab Setup

![VMware](https://img.shields.io/badge/Hypervisor-VMware%20Workstation%2017%20Player-607078?style=for-the-badge&logo=vmware&logoColor=white)
![Windows 10](https://img.shields.io/badge/Guest%20OS-Windows%2010%2022H2-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Network](https://img.shields.io/badge/Network-VMnet2%20NAT-blue?style=for-the-badge)
![IPv4](https://img.shields.io/badge/Windows%20IP-10.0.0.10%2F24-informational?style=for-the-badge)
![Program](https://img.shields.io/badge/NetworkWalks-B084J-orange?style=for-the-badge)

[![GitHub](https://img.shields.io/badge/GitHub-Monoranjan07-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Monoranjan07)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Monoranjan%20Banik-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/monoranjan-banik-3a0092335/)

</div>

---

## 📑 Table of Contents

1. [Project Overview](#-project-overview)
2. [Project Objectives](#-project-objectives)
3. [Purpose of the Lab](#-purpose-of-the-lab)
4. [Lab Architecture](#-lab-architecture)
5. [Lab Configuration](#-lab-configuration)
6. [Prerequisites and Tools Used](#-prerequisites-and-tools-used)
7. [Step-by-Step Lab Setup Procedure](#-step-by-step-lab-setup-procedure)
8. [Lab Verification](#-lab-verification)
9. [Project Demonstration Video](#-project-demonstration-video)
10. [Problems Encountered and Solutions](#-problems-encountered-and-solutions)
11. [What I Learned](#-what-i-learned)
12. [Security and Ethical Use](#-security-and-ethical-use)
13. [Tools and Resources](#-tools-and-resources)
14. [Author](#-author)
15. [Project Information](#-project-information)

---

## 📌 Project Overview

This repository documents an **additional Week 1 project** in the NetworkWalks Cybersecurity Internship Program: deploying a **Windows 10** virtual machine in **VMware Workstation 17 Player** and connecting it to the same isolated lab network as my Kali Linux machine.

In this project I:

- Deployed a Windows 10 (22H2, English ISO) virtual machine.
- Used a custom NAT network, **VMnet2**, on the `10.0.0.0/24` subnet.
- Configured a **static IPv4 address** (`10.0.0.10`), the default gateway (`10.0.0.1`) and DNS (`8.8.8.8`).
- Tested communication with the Kali Linux lab machine (`10.0.0.2`), then tested internet and DNS connectivity.

This project complements my [Kali Linux lab setup](https://github.com/Monoranjan07/NETWORKWALKS-B084J-WK1-PM1-CYBERSECURITY-LAB-SETUP). Together they form a two-machine virtual lab.

---

## 🎯 Project Objectives

- Deploy Windows 10 in VMware Workstation.
- Configure the virtual machine hardware.
- Configure the custom NAT network (VMnet2).
- Assign a static IPv4 address.
- Configure the default gateway and DNS server.
- Establish communication with the Kali Linux VM.
- Verify network connectivity.
- Document the lab professionally.

---

## 🧪 Purpose of the Lab

A cybersecurity learner needs a safe place to practise. This Windows 10 VM adds a Windows target/client environment to my lab:

- **Isolation:** the VMs sit on their own virtual network, separate from the host's other networks.
- **Repeatability:** documented values (addresses, gateway, DNS) let me rebuild the lab consistently.
- **Networking fundamentals:** static addressing, subnets, gateways, DNS and NAT are all exercised in practice.
- **VM-to-VM communication:** a Windows machine and a Kali machine on one subnet is the basis for later exercises.
- **Practical learning:** later modules can build on a working, verified environment.

---

## 🏗️ Lab Architecture

```text
┌────────────────────────────────────────────────────────────────┐
│  Windows Host                                                  │
│                                                                │
│   ┌──────────────────────────────────────────────────────┐     │
│   │  VMware Workstation 17 Player                        │     │
│   │                                                      │     │
│   │   ┌──────────────────────────────────────────────┐   │     │
│   │   │  Custom NAT Network – VMnet2 ("Network Walks")│  │     │
│   │   │  Subnet: 10.0.0.0/24   Gateway: 10.0.0.1      │  │     │
│   │   └───────────────┬───────────────┬──────────────┘   │     │
│   │                   │               │                  │     │
│   │        ┌──────────┴───────┐ ┌─────┴────────────┐     │     │
│   │        │ Windows 10 VM    │ │ Kali Linux VM    │     │     │
│   │        │ 10.0.0.10        │ │ 10.0.0.2         │     │     │
│   │        │ (this project)   │ │ (other lab VM)   │     │     │
│   │        └──────────────────┘ └──────────────────┘     │     │
│   └──────────────────────────────────────────────────────┘     │
└────────────────────────────────────────────────────────────────┘
                              │ NAT via 10.0.0.1
                              ▼
                   External network / Internet
```

The two virtual machines have **different** addresses: Windows 10 is `10.0.0.10` and Kali Linux is `10.0.0.2`.

---

## ⚙️ Lab Configuration

### Hypervisor

| Setting | Value |
|---|---|
| Hypervisor | VMware Workstation 17 Player |
| Network management | VMware Virtual Network Editor |
| Lab network | VMnet2 (custom NAT) |

### Windows 10 VM Hardware

| Setting | Value |
|---|---|
| Guest operating system | Windows 10 |
| ISO | Windows 10 22H2, English |
| Memory (RAM) | 8 GB |
| Processors | 4 |
| Hard disk | 20 GB NVMe |
| Network adapter | Custom – Network Walks (VMnet2) |

### NAT Network (VMnet2)

| Setting | Value |
|---|---|
| Network | VMnet2 |
| Type | Custom NAT |
| Subnet IP | 10.0.0.0 |
| Subnet mask | 255.255.255.0 |
| Gateway IP | 10.0.0.1 |
| Port forwarding | No entries configured |
| Allow active FTP | Enabled |
| Allow any Organizationally Unique Identifier | Enabled |
| UDP timeout | 30 seconds |
| Config port | 0 |
| IPv6 | Disabled |

### Windows 10 IPv4 Configuration

| Setting | Value |
|---|---|
| IPv4 method | Static (manual) configuration |
| IP address | 10.0.0.10 |
| Subnet mask | 255.255.255.0 |
| Default gateway | 10.0.0.1 |
| Preferred DNS server | 8.8.8.8 |

> **Address note:** `10.0.0.10` is the Windows 10 VM. `10.0.0.2` is the **Kali Linux** lab machine used as the VM-to-VM test target.

The host operating system is not established by my evidence, so it is not specified in the configuration tables.

---

## 🧰 Prerequisites and Tools Used

| Tool / Requirement | Purpose |
|---|---|
| Windows 10 22H2 English ISO | Installation media for the VM |
| VMware Workstation 17 Player | Virtualization platform |
| VMware Virtual Network Editor | Configuring VMnet2 NAT |
| Windows Network Connections | Setting the static IPv4 address and DNS |
| Windows Command Prompt | Running `ipconfig` and `ping` |
| Windows networking utilities | Verifying addressing and connectivity |
| Kali Linux VM (from my earlier project) | VM-to-VM connectivity test target |

---

## 🪜 Step-by-Step Lab Setup Procedure

### Step 1 — Windows 10 ISO Download

I downloaded the Windows 10 22H2 English ISO as installation media for the virtual machine.

<p align="center">
  <img src="images/01-windows-10-iso-download.png" alt="Windows 10 English International ISO download page" width="800"><br>
  <em>Figure 1 – Windows 10 English International ISO download page.</em>
</p>

### Steps 2 and 3 — Creating the VM and Configuring Hardware

I created the Windows 10 virtual machine in VMware Workstation 17 Player and configured its hardware: 8 GB RAM, 4 processors and a 20 GB NVMe virtual disk. Its network adapter was set to the custom network (Network Walks / VMnet2).

<p align="center">
  <img src="images/02-windows10-vm-settings.png" alt="VMware Workstation Windows 10 virtual machine settings" width="800"><br>
  <em>Figure 2 – VMware Workstation virtual machine configuration for the Windows 10 VM.</em>
</p>

### Step 4 — Configuring the Custom NAT Network (VMnet2)

In the Virtual Network Editor, VMnet2 is a custom NAT network with subnet `10.0.0.0`, mask `255.255.255.0` and gateway `10.0.0.1`. No port forwarding entries are configured. Allow active FTP and Allow any OUI are enabled, the UDP timeout is 30 seconds, the config port is 0, and IPv6 is disabled.

<p align="center">
  <img src="images/03-vmware-vmnet2-nat-settings.png" alt="VMware Virtual Network Editor VMnet2 NAT settings" width="800"><br>
  <em>Figure 3 – VMware Virtual Network Editor showing the VMnet2 NAT settings.</em>
</p>

### Step 5 — Configuring the Windows 10 Network Adapter

The VM's network adapter is attached to the custom network **Network Walks (VMnet2)**, so Windows 10 shares a subnet with the Kali Linux VM. This setting is shown in the VM settings in Figure 2.

### Step 6 — Setting Static IPv4 and DNS

Inside Windows 10, I configured a static IPv4 address instead of relying on DHCP, so the machine keeps a predictable address in the lab:

| Setting | Value |
|---|---|
| IP address | 10.0.0.10 |
| Subnet mask | 255.255.255.0 |
| Default gateway | 10.0.0.1 |
| Preferred DNS | 8.8.8.8 |

<p align="center">
  <img src="images/04-windows10-static-ip-configuration.png" alt="Windows 10 static IPv4 configuration and connectivity testing" width="800"><br>
  <em>Figure 4 – Windows 10 static IPv4 configuration and connectivity testing.</em>
</p>

### Steps 7 and 8 — Testing VM-to-VM, Internet and DNS Connectivity

From Command Prompt, I used `ipconfig` to confirm the addressing and `ping` to test the Kali Linux VM (`10.0.0.2`), a public IP (`8.8.8.8`), and two domain names (`google.com`, `networkwalks.com`). Results are summarised in [Lab Verification](#-lab-verification).

<p align="center">
  <img src="images/05-windows10-network-verification.png" alt="Command Prompt network connectivity verification" width="800"><br>
  <em>Figure 5 – Command Prompt network connectivity verification.</em>
</p>

---

## ✅ Lab Verification

### Captured verification (shown in the project screenshots)

| Command | Purpose | Expected result | Project evidence |
|---|---|---|---|
| `ipconfig` | Confirm the Windows VM's IPv4 settings | `10.0.0.10`, mask `255.255.255.0`, gateway `10.0.0.1` | ✅ Captured (Figures 4–5) |
| `ping 10.0.0.2` | Test VM-to-VM connectivity with the Kali Linux machine | Replies from `10.0.0.2` | ✅ Captured, successful replies |
| `ping 8.8.8.8` | Test internet reachability through the NAT gateway without DNS | Replies from `8.8.8.8` | ✅ Captured, successful replies |
| `ping google.com` | Test DNS resolution and internet access | Name resolves; replies received | ✅ Captured, successful replies |
| `ping networkwalks.com` | Test DNS resolution for the program's domain | Name resolves; replies received | ✅ Captured, successful replies |

```cmd
ipconfig
ping 10.0.0.2
ping 8.8.8.8
ping google.com
ping networkwalks.com
```

### Recommended additional checks (not claimed as completed)

```cmd
ipconfig /all          :: confirm DNS server and adapter details
ping 10.0.0.1          :: test the NAT gateway directly
nslookup google.com    :: test DNS resolution separately
tracert 8.8.8.8        :: view the path through the gateway
```

---

## 🎬 Project Demonstration Video

<div align="center">

[![Watch Windows 10 Lab Demonstration](https://img.shields.io/badge/▶%20Watch%20Windows%2010%20Lab%20Demonstration-LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/feed/update/urn:li:activity:7524488966579089408/)

</div>

**🔗 Video link:** https://www.linkedin.com/feed/update/urn:li:activity:7524488966579089408/

The demonstration video is hosted on LinkedIn. It shows the Windows 10 lab setup: the VM configuration, the VMnet2 NAT network, the static IPv4 settings, and the connectivity checks.

---

## 🧩 Problems Encountered and Solutions

This section lists the troubleshooting topics relevant to this setup and how each is handled in the final configuration.

| Topic | How it is handled |
|---|---|
| **VM network adapter selection** | The adapter must be set to the custom network (Network Walks / VMnet2), or the VM will not share a subnet with the Kali VM. |
| **NAT network configuration** | VMnet2 uses subnet `10.0.0.0`, mask `255.255.255.0` and gateway `10.0.0.1`; Windows addressing must fit this subnet. |
| **Static IPv4 configuration** | Windows uses `10.0.0.10/24`, a different address from Kali (`10.0.0.2`), to avoid an address conflict. |
| **Gateway configuration** | The default gateway is set to the NAT gateway `10.0.0.1` so traffic can leave the subnet. |
| **DNS resolution** | DNS is set to `8.8.8.8`; successful pings to domain names confirm names resolve. |
| **VM-to-VM connectivity** | Pinging `10.0.0.2` confirms the Windows VM can reach the Kali VM on the same subnet. |

---

## 📚 What I Learned

- **Windows virtualization:** deploying and sizing a Windows 10 VM in VMware Workstation.
- **VMware networking:** using the Virtual Network Editor and custom virtual networks.
- **NAT networking:** how a NAT network gives VMs outside access through a gateway.
- **IPv4 addressing:** planning unique host addresses inside a `/24` subnet.
- **Subnet masks:** how `255.255.255.0` defines the lab subnet.
- **Default gateways:** why `10.0.0.1` is needed to reach other networks.
- **DNS configuration:** the role of a DNS server in name resolution.
- **VM-to-VM communication:** connecting Windows and Kali on one subnet.
- **Troubleshooting:** testing in layers (local, gateway, internet IP, domain name) with `ipconfig` and `ping`.

---

## ⚖️ Security and Ethical Use

- This lab is for **educational and authorized cybersecurity practice only**.
- Security tools and techniques must only be used on systems I own or have **explicit written permission** to test.
- No testing against third-party systems is part of this project.
- Cybersecurity knowledge must be used lawfully and responsibly.

---

## 🔗 Tools and Resources

- [Microsoft – Download Windows 10](https://www.microsoft.com/software-download/windows10)
- [VMware Workstation Player](https://www.vmware.com/products/workstation-player.html)
- [Kali Linux](https://www.kali.org/)
- [My Kali Linux lab setup](https://github.com/Monoranjan07/NETWORKWALKS-B084J-WK1-PM1-CYBERSECURITY-LAB-SETUP)
- [NetworkWalks](https://networkwalks.com)

---

## 👤 Author

<div align="center">

### Monoranjan Banik

**Cybersecurity Intern – NetworkWalks Cybersecurity Internship Program, Batch B084J**

[![GitHub](https://img.shields.io/badge/GitHub-Monoranjan07-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Monoranjan07)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Monoranjan%20Banik-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/monoranjan-banik-3a0092335/)

</div>

---

## 📋 Project Information

| Item | Details |
|---|---|
| **Project title** | Windows 10 Cybersecurity Lab Setup |
| **Program** | NetworkWalks Cybersecurity Internship Program |
| **Batch** | B084J |
| **Week** | 01 |
| **Module** | Extra Project – Windows 10 Lab Setup |
| **Author** | Monoranjan Banik |
| **Hypervisor** | VMware Workstation 17 Player |
| **Guest OS** | Windows 10 |
| **VM RAM** | 8 GB |
| **Processors** | 4 |
| **Virtual disk** | 20 GB NVMe |
| **Lab network** | Custom NAT – VMnet2 |
| **Windows IP** | 10.0.0.10/24 |
| **Kali Linux IP** | 10.0.0.2 |
| **Gateway** | 10.0.0.1 |
| **DNS** | 8.8.8.8 |
| **Repository** | [NETWORKWALKS-B084J-WK1-PMx-WINDOWS10-LAB-SETUP](https://github.com/Monoranjan07/NETWORKWALKS-B084J-WK1-PMx-WINDOWS10-LAB-SETUP) |
| **Status** | Completed, based on the supplied project evidence |

<div align="center">

⭐ *Documented by Monoranjan Banik as part of the NetworkWalks Cybersecurity Internship Program.*

</div>
