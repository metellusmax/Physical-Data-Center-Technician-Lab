# Phase 4: RAM Upgrade & Validation

**Project:** Physical Data Center Technician Lab  
**System:** Dell OptiPlex 7010 SFF  
**Asset ID:** PHY-SRV01  
**Status:** ✅ Completed

## 🎯 Objective

Upgrade the physical server's memory capacity to support future infrastructure exercises and gain hands-on experience with hardware installation, component identification, and Linux hardware validation.

This exercise focuses on installing additional DDR3 memory modules and verifying that the operating system recognizes the upgraded hardware.

---

## ⚙️ 1. Hardware Configuration

### System Specifications

| Component | Configuration |
|-----------|---------------|
| Server | Dell OptiPlex 7010 SFF |
| Processor | Intel Core i5-3470 @ 3.20 GHz |
| Operating System | Ubuntu Server 24.04 LTS |
| Memory Type | DDR3 SDRAM |
| Memory Speed | 1333 MT/s |
| Total DIMM Slots | 4 |

### Memory Upgrade

| Configuration | Before | After |
|---------------|--------|-------|
| Installed RAM | 4 GB | 10 GB |
| Usable Memory | 3.7 GiB | 9.6 GiB |
| Installed DIMMs | 2 | 4 |
| Available DIMM Slots | 2 | 0 |

**Upgrade:** Installed an additional 6 GB of DDR3 RAM using one 4 GB module and one 2 GB module.

The original memory modules remained installed.

---

## 🔧 2. RAM Installation

### Equipment Used

- Dell OptiPlex 7010 SFF
- 4 GB DDR3 DIMM
- 2 GB DDR3 DIMM
- Anti-static wrist strap
- Phillips screwdriver

### Installation Procedure

1. Shut down Ubuntu Server.
2. Disconnected the system from power.
3. Opened the Dell OptiPlex chassis.
4. Located the four motherboard DIMM slots.
5. Identified the two available memory slots.
6. Aligned the additional DDR3 modules with the DIMM slots.
7. Installed the 4 GB and 2 GB memory modules.
8. Verified that the retention clips were secured.
9. Reassembled the system.
10. Powered on the server.

**Result:** The system successfully booted after the memory upgrade.

### 📸 Evidence

**RAM Installation**

<img width="312" height="475" alt="image" src="https://github.com/user-attachments/assets/ccd97c2f-343d-4fae-88df-6f93c49cb793" />



## 🧪 3. Memory Verification

After installation, verified the upgraded memory configuration using Ubuntu Server.

### Check Available Memory

Executed:

```bash
free -h
```

### Results

| Metric | Before Upgrade | After Upgrade |
|--------|----------------|---------------|
| Total Memory | 3.7 GiB | 9.6 GiB |
| Installed Capacity | 4 GB | 10 GB |
| Available Memory | Approximately 3.2 GiB | Approximately 9.2 GiB |

**Result:** Ubuntu successfully recognized the additional memory.

### 📸 Evidence

**Memory Before Upgrade**

<img width="855" height="95" alt="image" src="https://github.com/user-attachments/assets/00240d56-fd83-4d63-8f91-f65a395985e7" />


**Memory After Upgrade**

<img width="908" height="88" alt="image png (2)" src="https://github.com/user-attachments/assets/b5b5db49-d4b0-42e5-bf84-9892f4ccb01f" />


---

## 🔍 4. Memory Module Identification

Used Linux hardware inventory tools to verify the installed memory modules.

### DMI Memory Information

Executed:

```bash
sudo dmidecode -t memory
```

This command displays memory hardware information reported by the system firmware.

### Hardware Inventory

Executed:

```bash
sudo lshw -class memory
```

This command displays information about the system's memory hardware.

### Verified Memory Configuration

| DIMM Slot | Capacity | Manufacturer | Configured Speed |
|-----------|----------|--------------|------------------|
| DIMM1 | 2 GB | Samsung | 1333 MT/s |
| DIMM2 | 2 GB | Samsung | 1333 MT/s |
| DIMM3 | 4 GB | Samsung | 1333 MT/s |
| DIMM4 | 2 GB | Samsung | 1333 MT/s |
| **Total** | **10 GB** | | |

### Validation Results

- All four DIMM slots populated.
- All four memory modules detected.
- Total installed memory confirmed at 10 GB.
- Memory operating at 1333 MT/s.
- Ubuntu successfully booted with the upgraded configuration.




## 🛠️ 5. Memory Error Investigation

Reviewed Linux kernel messages to identify potential memory-related hardware errors following the upgrade.

### Diagnostic Command

Executed:

```bash
sudo journalctl -k -b | grep -Ei 'edac|mce|hardware error'
```

### Observed Output

```text
EDAC MC: Ver: 3.0.0
EDAC ie31200: No ECC support
```

### Findings

**EDAC MC: Ver: 3.0.0**

Indicates that the Linux Error Detection and Correction subsystem initialized.

**EDAC ie31200: No ECC support**

Indicates that ECC memory functionality is not supported by the current hardware configuration.

These messages are informational and do not indicate a memory failure.

### Result

No actual memory faults were identified in the displayed kernel messages.

> The absence of reported errors does not guarantee
> that all memory modules are error-free.
> A dedicated memory diagnostic can provide additional validation.



## ✅ 6. Final Validation

| Validation Check | Result |
|------------------|--------|
| Physical RAM Installation | PASS |
| System Boot | PASS |
| Ubuntu Memory Detection | PASS |
| Total Installed RAM | 10 GB |
| DIMM Detection | 4 of 4 |
| Memory Speed | 1333 MT/s |
| Kernel Message Review | No memory faults identified |

**Overall Result:** RAM upgrade successfully completed and validated.

---

## 🏁 Outcome

Successfully upgraded the Dell OptiPlex 7010 SFF from 4 GB to 10 GB of DDR3 RAM.

The server recognized all four memory modules and successfully booted into Ubuntu Server following the hardware upgrade.

The upgrade increased installed memory capacity by **150%**, providing additional resources for future infrastructure and Linux administration exercises.

## 🛠️ Skills Demonstrated

- Physical hardware maintenance
- DDR3 memory installation
- DIMM slot identification
- ESD safety practices
- Hardware compatibility verification
- Linux memory administration
- Hardware inventory using `dmidecode` and `lshw`
- Kernel log inspection
- Post-upgrade system validation


