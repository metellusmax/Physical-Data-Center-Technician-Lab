
# Phase 1: Hardware Inspection & Inventory

**Project:** Physical Data Center Technician Lab  
**System:** Dell OptiPlex 7010 SFF  
**Asset ID:** PHY-SRV01  
**Inspection Date:** November 13, 2026  
**Status:** ✅ Completed

## 🎯 Objective

Perform an initial hardware inspection of a Dell OptiPlex 7010 SFF to identify installed components, verify system functionality, and establish a hardware inventory before deploying Ubuntu Server.

This phase focuses on hardware identification, BIOS diagnostics, component handling, and physical system validation.

## 🔧 Equipment Used

- Dell OptiPlex 7010 SFF
- Anti-static wrist strap
- Phillips screwdriver
- Monitor and keyboard
- Power cable

## 🖥️ Initial Hardware Configuration

| Component | Specification |
|-----------|---------------|
| Manufacturer | Dell |
| Model | OptiPlex 7010 SFF |
| Processor | Intel Core i5-3470 @ 3.20 GHz |
| Memory | 4 GB DDR3 (1333 MT/s) |
| Memory Slots | 4 DIMM slots |
| Primary Storage | Samsung PM851 128 GB SSD |
| Optical Drive | MATSHITA DVD+/-RW UJ8E1 |
| Network | Integrated Gigabit Ethernet |
| BIOS Version | A29 |
| Boot Mode | Legacy BIOS |

## 🔍 Physical Inspection

### Chassis & Components

- Inspected the external chassis and I/O ports.
- Opened the system chassis using ESD precautions.
- Identified the motherboard, CPU heatsink, cooling fan, and DIMM slots.
- Inspected SATA data and power connections.
- Identified the primary SSD and optical drive.
- Removed the storage assembly for inspection.
- Checked for visible physical damage.

**Result:** No visible physical damage identified during the initial inspection.

### Memory Inspection

Inspected the two original Samsung DDR3 memory modules.

| Slot | Capacity | Manufacturer | Type |
|------|----------|--------------|------|
| DIMM 1 | 2 GB | Samsung | DDR3 |
| DIMM 2 | 2 GB | Samsung | DDR3 |

**Total Installed Memory:** 4 GB

### Component Servicing

Performed basic hardware servicing procedures:

- Removed DIMM 1.
- Reinstalled DIMM 1.
- Removed DIMM 2.
- Reinstalled DIMM 2.
- Inspected the storage assembly.
- Reassembled the system.

## ✅ Hardware Validation

| Test | Result |
|------|--------|
| Initial Power-On | PASS |
| Power-On Self-Test (POST) | PASS |
| BIOS Access | PASS |
| CPU Detection | PASS |
| Memory Detection | PASS |
| Storage Detection | PASS |
| Dell Diagnostics | PASS |

The system successfully completed initial hardware validation.

## 📸 Inspection Evidence

### Initial System Inspection

[INSERT PHOTO: Dell OptiPlex exterior]

### Internal Component Inspection

[INSERT PHOTO: Open chassis and motherboard]

### Memory Module Inspection

[INSERT PHOTO: Original DDR3 memory modules]

### BIOS Verification

[INSERT SCREENSHOT: BIOS system information]

## 📝 Outcome

Successfully completed the initial hardware inspection, identified installed components, performed basic component servicing, and verified system functionality.

The system was confirmed operational and ready for bare-metal Ubuntu Server deployment.

