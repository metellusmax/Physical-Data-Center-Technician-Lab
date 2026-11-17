# Phase 2: Bare-Metal Ubuntu Server Deployment

**Project:** Physical Data Center Technician Lab  
**System:** Dell OptiPlex 7010 SFF  
**Asset ID:** PHY-SRV01  
**Status:** ✅ Completed

## 🎯 Objective

Deploy Ubuntu Server directly onto physical hardware to establish a Linux server environment for infrastructure administration, networking, and storage management.

This phase focuses on bootable media creation, BIOS configuration, operating system installation, storage provisioning, and system validation.



## ⚙️ Deployment Environment

| Component | Configuration |
|-----------|---------------|
| Server | Dell OptiPlex 7010 SFF |
| Processor | Intel Core i5-3470 @ 3.20 GHz |
| Memory | 4 GB DDR3 (Initial Configuration) |
| Primary Storage | Samsung PM851 128 GB SSD |
| Operating System | Ubuntu Server 24.04.3 LTS |
| Boot Mode | Legacy BIOS |
| Installation Media | 16 GB USB Flash Drive |
| USB Creation Tool | Rufus |
| Hostname | `dct-lab-server` |
| Administrator Account | `max` |

> The server was initially deployed with 4 GB RAM.
> Memory was subsequently upgraded to 10 GB during Phase 4.


## 🔧 1. Bootable USB Preparation

Downloaded the Ubuntu Server 24.04.3 LTS ISO and used Rufus to create bootable installation media.

### Rufus Configuration

| Setting | Configuration |
|---------|---------------|
| Boot Selection | Ubuntu Server ISO |
| Partition Scheme | MBR |
| Target System | BIOS or UEFI |
| Persistence | Disabled |
| Installation Media | 16 GB USB |
| Image Writing Mode | DD Image Mode |

**Result:** Successfully created bootable installation media and loaded the Ubuntu Server installer.

### 📸 Evidence

**Rufus Bootable USB Configuration**

<img width="417" height="543" alt="image" src="https://github.com/user-attachments/assets/bb0ae4d6-f234-4753-b9e0-cfd59de17eb0" />


**Successful Ubuntu Installer Boot**

<img width="1134" height="504" alt="image" src="https://github.com/user-attachments/assets/2bbb42fa-c8c4-4730-97da-37c9bcc731a9" />





## 🖥️ 2. Ubuntu Server Installation

Booted the Dell OptiPlex 7010 SFF using the installation USB and completed the Ubuntu Server setup.

### Installation Steps

1. Selected English as the installation language.
2. Configured the keyboard layout.
3. Selected the standard Ubuntu Server installation.
4. Continued installation without Ethernet connectivity.
5. Skipped proxy configuration.
6. Continued past the Ubuntu archive mirror configuration.
7. Selected the Samsung 128 GB SSD as the installation target.
8. Enabled Logical Volume Manager (LVM).
9. Configured the server hostname and administrator account.
10. Selected OpenSSH Server for remote administration.
11. Completed installation and rebooted from the SSD.

### Installation Configuration

| Setting | Configuration |
|---------|---------------|
| Installation Type | Bare Metal |
| Operating System | Ubuntu Server 24.04.3 LTS |
| Hostname | `dct-lab-server` |
| Username | `max` |
| Network During Installation | Offline |
| Storage Configuration | Guided Installation |
| Volume Management | LVM |
| Disk Encryption | Disabled |
| SSH | OpenSSH Server |

**Result:** Ubuntu Server successfully installed and booted from the physical SSD.

### 📸 Evidence


**First Successful Boot**

<img width="296" height="157" alt="image" src="https://github.com/user-attachments/assets/8bb4621b-0209-4610-a9d3-4760bfb83513" />



## 💾 3. Storage Configuration

Configured the Samsung PM851 128 GB SSD using Ubuntu's guided storage installation with LVM.

### Physical Disk Layout

| Device | Size | Purpose |
|--------|------|---------|
| `/dev/sda` | 119.2 GiB | Physical Samsung SSD |
| `/dev/sda1` | 1 MiB | BIOS Boot Partition |
| `/dev/sda2` | 2 GiB | `/boot` |
| `/dev/sda3` | 117.2 GiB | LVM Physical Volume |

### LVM Configuration

| Component | Configuration |
|-----------|---------------|
| Physical Volume | `/dev/sda3` |
| Volume Group | `ubuntu-vg` |
| Logical Volume | `ubuntu-lv` |
| Root Filesystem | ext4 |
| Root Logical Volume | 58.6 GiB |
| Unallocated LVM Space | Approximately 58.6 GiB |

The remaining space within the volume group was retained for future LVM administration exercises.

### Storage Validation Commands

```bash
lsblk
df -h
sudo pvs
sudo vgs
sudo lvs
```

### Validation Results

- Samsung SSD successfully detected.
- BIOS boot partition configured.
- `/boot` filesystem mounted.
- Root filesystem mounted through LVM.
- Volume group and logical volume successfully recognized.
- Approximately 58.6 GiB remained available within the LVM volume group.

### 📸 Evidence

**Storage Partition Layout, Filesystem Utilization and LVM Verification**

<img width="953" height="701" alt="image" src="https://github.com/user-attachments/assets/adfe503a-877e-484f-b302-1e4c147c79a1" />





## ✅ 4. Operating System & Hardware Validation

After installation, verified that Ubuntu Server recognized the physical hardware.

### Validation Commands

```bash
hostnamectl
lscpu
free -h
lsblk
```

### System Verification

| Component | Verified Result |
|-----------|-----------------|
| Operating System | Ubuntu Server 24.04.3 LTS |
| Hostname | `dct-lab-server` |
| Kernel | Linux 6.8.0-71-generic |
| Architecture | x86-64 |
| Manufacturer | Dell Inc. |
| Model | OptiPlex 7010 |
| Processor | Intel Core i5-3470 |
| CPU Cores | 4 |
| Initial Memory | 4 GB DDR3 |
| Primary Storage | Samsung 128 GB SSD |
| BIOS Version | A29 |

### Validation Results

- Ubuntu Server successfully booted from the SSD.
- Operating system and hostname verified.
- Processor and memory recognized.
- Storage partitions and LVM configuration validated.
- No installation-related hardware issues identified.

### 📸 Evidence

**Operating System, Processor and Memory Verification**

<img width="1222" height="781" alt="image" src="https://github.com/user-attachments/assets/5cc10692-e33c-4c13-ab16-9c7c99a1afc0" />






## 🔐 5. OpenSSH Installation

Selected OpenSSH Server during the Ubuntu installation process to prepare the system for remote administration.

### SSH Verification

```bash
systemctl status ssh
```

The SSH service was configured to use socket activation.

Verified the socket using:

```bash
systemctl status ssh.socket
```

### Result

```text
Active: active (listening)
```

OpenSSH was successfully installed and configured to accept connections.

Remote SSH connectivity was subsequently established and validated during Phase 3.

### 📸 Evidence

**SSH Socket Verification**

<img width="1163" height="371" alt="image" src="https://github.com/user-attachments/assets/e78d778b-6e8b-4fe0-8a1b-d141e72f0e9d" />




## 🏁 Outcome

Successfully deployed Ubuntu Server 24.04.3 LTS directly onto a Dell OptiPlex 7010 SFF.

The deployment established a functional Linux server with:

- Bare-metal Ubuntu Server installation
- Legacy BIOS boot configuration
- LVM-based storage management
- Verified CPU, memory, and SSD detection
- OpenSSH Server installation
- Successful operating system validation

The system was prepared for network configuration, remote administration, and future hardware expansion.

---

## 🛠️ Skills Demonstrated

- Bare-metal operating system deployment
- BIOS and boot configuration
- Bootable USB creation
- Linux installation
- Disk partitioning
- Logical Volume Manager (LVM)
- Linux hardware validation
- SSH service configuration
- Technical documentation

