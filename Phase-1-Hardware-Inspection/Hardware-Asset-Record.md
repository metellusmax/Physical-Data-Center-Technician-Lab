# Hardware Asset Record

**Project:** Physical Data Center Technician Lab  
**Asset ID:** PHY-SRV01  
**Asset Type:** Physical Linux Server  
**Asset Status:** Operational - Upgrades In Progress

## 1. Asset Information

| Field | Information |
|-------|-------------|
| Asset Name | PHY-SRV01 |
| Manufacturer | Dell |
| Model | OptiPlex 7010 |
| Form Factor | Small Form Factor (SFF) |
| Service Tag | [REDACTED] |
| Acquisition Date | November 13, 2026 |
| Purchase Price | Not Recorded |
| Operating System | Ubuntu Server 24.04 LTS |
| Hostname | dct-lab-server |
| Asset Status | Operational |

> Sensitive asset identifiers have been removed from this public record.

## 2. Processor

| Specification | Value |
|---------------|-------|
| Processor | Intel Core i5-3470 |
| Base Clock | 3.20 GHz |
| Cores | 4 |
| Threads | 4 |
| Hyper-Threading | No |
| Architecture | x86-64 |
| L3 Cache | 6 MB |

## 3. Memory

### Initial Configuration

| Component | Specification |
|-----------|---------------|
| Installed RAM | 4 GB |
| Memory Type | DDR3 |
| Operating Speed | 1333 MT/s |
| Populated Slots | 2 of 4 |
| DIMM 1 | 2 GB |
| DIMM 2 | 2 GB |

### Current Configuration

**Upgrade:** Added 6 GB DDR3 RAM.

| Slot | Capacity | Manufacturer | Speed |
|------|----------|--------------|-------|
| DIMM1 | 2 GB | Samsung | 1333 MT/s |
| DIMM2 | 2 GB | Samsung | 1333 MT/s |
| DIMM3 | 4 GB | Samsung | 1333 MT/s |
| DIMM4 | 2 GB | Samsung | 1333 MT/s |
| **Total** | **10 GB** | | |

**Validation:** Ubuntu successfully detected approximately 9.6 GiB of usable memory.

Validation commands:

```bash
free -h
sudo dmidecode -t memory
sudo lshw -class memory
```

**Status:** Upgrade completed and verified.

## 4. Storage

### Current Storage

| Component | Specification |
|-----------|---------------|
| Primary SSD | Samsung PM851 |
| Capacity | 128 GB |
| Interface | SATA |
| SATA Port | SATA-0 (initial inventory) |
| Operating System | Ubuntu Server 24.04 LTS |
| Filesystem | ext4 |
| Volume Management | LVM |

### Optical Drive

| Component | Specification |
|-----------|---------------|
| Manufacturer | MATSHITA |
| Model | DVD+/-RW UJ8E1 |
| Interface | SATA |
| SATA Port | SATA-1 (initial inventory) |

### Planned Storage Expansion

| Component | Specification |
|-----------|---------------|
| Secondary SSD | 128 GB SATA SSD |
| Installation Status | Pending |
| Mounting Bracket | Acquired |
| SATA Data Cable | Longer cable ordered |
| Planned SATA Port | SATA-2 |

**Next Action:** Install the secondary SSD and verify detection through BIOS and Ubuntu.

## 5. Network Hardware

| Component | Configuration |
|-----------|---------------|
| Integrated NIC | Intel 82579LM Gigabit Ethernet |
| Interface Name | eno1 |
| Network Connection | Wired Ethernet |
| IPv4 Configuration | DHCP |
| Observed IPv4 Address | 10.0.0.164/24 |
| Default Gateway | 10.0.0.1 |
| Remote Administration | OpenSSH |
| USB Wi-Fi Adapter | Included |

### Network Equipment

**NETGEAR GS308E**

- 8-Port Gigabit Easy Smart Managed Switch
- Status: Acquired, integration pending
- Planned Use: VLANs, network segmentation, and switch management

## 6. BIOS Configuration

| Setting | Value |
|---------|-------|
| BIOS Version | A29 |
| Boot Mode | Legacy |
| Secure Boot | Disabled |
| Integrated NIC | Enabled |
| PXE | Enabled (initial inventory) |

## 7. Initial Physical Inspection

| Inspection Item | Result |
|-----------------|--------|
| Chassis Condition | Good |
| Front Ports | Good |
| Rear Ports | Good |
| Power Cord | Included |
| Visible Physical Damage | None Observed |
| Internal Components | Identified |
| Original RAM | 4 GB |
| Primary SSD | Samsung PM851 |

## 8. Hardware Validation

| Test | Result |
|------|--------|
| Initial Power-On | PASS |
| POST | PASS |
| BIOS Access | PASS |
| CPU Detection | PASS |
| Memory Detection | PASS |
| Storage Detection | PASS |
| Dell Diagnostics | PASS |
| Ubuntu Installation | PASS |
| Ethernet Connectivity | PASS |
| SSH Remote Access | PASS |
| RAM Upgrade Detection | PASS |
| Secondary SSD Detection | PENDING |

## 9. Hardware Maintenance Log

| Date | Activity | Result |
|------|----------|--------|
| 2026-11-13 | Initial hardware inspection | Completed |
| 2026-11 | DIMM removal and reinstallation | Completed |
| 2026-11 | Bare-metal Ubuntu deployment | Completed |
| 2026-11 | Network configuration and SSH validation | Completed |
| 2026-11 | RAM upgraded from 4 GB to 10 GB | Completed |
| Pending | Secondary SSD installation | Awaiting longer SATA cable |
| Planned | NETGEAR GS308E integration | Not Started |

## 10. Current System Configuration

| Component | Current Configuration |
|-----------|----------------------|
| Asset ID | PHY-SRV01 |
| System | Dell OptiPlex 7010 SFF |
| CPU | Intel Core i5-3470 |
| RAM | 10 GB DDR3 |
| Primary SSD | Samsung 128 GB |
| Secondary SSD | Pending |
| Operating System | Ubuntu Server 24.04 LTS |
| Hostname | dct-lab-server |
| Networking | Gigabit Ethernet |
| Remote Administration | SSH |
| Managed Switch | NETGEAR GS308E (Pending Integration) |

## 11. Planned Maintenance

- [x] Complete initial hardware inspection.
- [x] Validate original components.
- [x] Install Ubuntu Server.
- [x] Configure Ethernet and SSH.
- [x] Upgrade RAM to 10 GB.
- [ ] Install secondary SSD.
- [ ] Validate secondary storage.
- [ ] Configure additional Linux storage.
- [ ] Integrate NETGEAR GS308E.
- [ ] Configure and test VLANs.
- [ ] Complete final system validation.

---

**Asset Record Status:** Active  
**Last Updated:** November 2026

[Return to Hardware Inspection](Hardware-Inspection.md)
