# 🖥️ Physical Data Center Technician Lab

A hands-on infrastructure lab focused on developing practical skills in hardware maintenance, Linux server administration, networking, and data center operations.

This project documents the deployment, configuration, troubleshooting, and maintenance of a physical Linux server using a Dell OptiPlex 7010 SFF.

## ⚙️ Lab Environment

| Component | Specifications |
|-----------|----------------|
| Server | Dell OptiPlex 7010 SFF |
| Processor | Intel Core i5-3470 @ 3.20 GHz |
| Memory | 10 GB DDR3 (1333 MT/s) |
| Primary Storage | Samsung 128 GB SATA SSD |
| Secondary Storage | Patriot P210 128 GB SATA SSD |
| Operating System | Ubuntu Server 24.04 LTS |
| Network Switch | NETGEAR GS308E 8-Port Gigabit |
| Networking | Gigabit Ethernet, DHCP |
| Remote Administration | OpenSSH |

## 🌐 Current Architecture

The lab currently operates as a physical Ubuntu Server connected to a home network through Ethernet.

The server supports remote administration through SSH, Linux system management, and hardware maintenance.

The NETGEAR GS308E managed switch will be integrated to support VLAN configuration, network segmentation, and additional networking exercises.

**Current Configuration**
- Physical Ubuntu Server running on Dell OptiPlex 7010 SFF
- Ethernet connectivity with DHCP
- Remote administration through SSH
- 10 GB DDR3 RAM
- 128 GB SATA SSD
- Secondary SSD installation and configuration

**Planned Expansion**
- NETGEAR GS308E switch integration
- VLAN configuration and network segmentation
- Additional network troubleshooting exercises

📁 [View Architecture Documentation](Architecture/Architecture.md)

## 📋 Project Roadmap

| Phase | Description | Status |
|-------|-------------|--------|
| [Phase 1](Phase-1-Hardware-Inspection/) | Hardware Inspection & Inventory | ✅ Complete |
| [Phase 2](Phase-2-Ubuntu-Deployment/) | Bare-Metal Ubuntu Deployment | ✅ Complete |
| [Phase 3](Phase-3-Networking/) | Network Cabling & Remote Administration | ✅ Complete |
| [Phase 4](Phase-4-Hardware-Upgrades/) | RAM & Storage Upgrades | ✅ Complete |
| [Phase 5](Phase-5-Storage-Administration/) | Linux Storage Administration | ✅ Complete |
| [Phase 6](Phase-6-Switching-and-VLANs/) | Managed Switching & VLANs | ⏳ Planned |
| [Phase 7](Phase-7-Final-Validation/) | Final Validation & Documentation | ⏳ Planned |

## 🛠️ Technical Skills

**Hardware**
- Component identification and inspection
- RAM installation and validation
- SATA storage maintenance
- BIOS configuration and troubleshooting

**Networking**
- Cat6 cable termination (T568B)
- Ethernet connectivity testing
- DHCP and TCP/IP configuration
- SSH remote administration

**Linux Administration**
- Bare-metal Ubuntu Server deployment
- Linux command-line administration
- LVM and filesystem management
- System updates and troubleshooting

**Infrastructure Operations**
- Hardware inventory
- System validation
- Technical documentation
- Troubleshooting and problem resolution

## 🚀 Current Status

Successfully deployed and configured a physical Ubuntu Server
on a Dell OptiPlex 7010 SFF.

**Next Milestone:** Integrate the NETGEAR GS308E 8-Port Gigabit
Easy Smart Managed Switch and begin VLAN configuration,
network segmentation, and switch management exercises.
