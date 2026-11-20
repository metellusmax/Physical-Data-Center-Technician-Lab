# Phase 5: Linux Storage Administration

**Project:** Physical Data Center Technician Lab  
**System:** Dell OptiPlex 7010 SFF  
**Asset ID:** PHY-SRV01  
**Status:** ✅ Completed

## 🎯 Objective

Configure and validate a secondary SATA SSD on a physical Ubuntu Server.

This phase focuses on disk identification, GPT partitioning, ext4 filesystem creation, storage mounting, and persistent filesystem configuration.

---

## ⚙️ 1. Storage Environment

| Component | Configuration |
|-----------|---------------|
| Operating System | Ubuntu Server 24.04 LTS |
| Primary SSD | Samsung PM851 128 GB |
| Secondary SSD | Patriot P210 128 GB |
| Primary Storage | LVM |
| Secondary Storage | GPT / ext4 |
| Mount Point | `/mnt/lab-storage` |
| Administration | SSH |

The secondary SSD was configured independently of the existing Ubuntu operating system and LVM configuration.

---

## 🔍 2. Disk Identification

**Why This Step Matters:**

Before modifying storage, it is important to identify the correct physical disk to prevent accidental data loss or changes to the operating system drive.

### Commands Executed

```bash
lsblk -o NAME,SIZE,MODEL,TYPE,MOUNTPOINTS
```

Lists detected storage devices, including their capacity, model, device type, and mount points.

```bash
sudo fdisk -l
```

Displays physical disks, partition tables, and existing partitions.

```bash
sudo wipefs -n /dev/sdb
```

Checks for existing filesystem or partition-table signatures without modifying the disk.

### Results

| Device | Model | Capacity | Purpose |
|--------|-------|----------|---------|
| `/dev/sda` | Samsung PM851 | 119.2 GiB | Ubuntu OS |
| `/dev/sdb` | Patriot P210 | 119.2 GiB | Secondary Storage |

**Result:** Both SSDs were detected, and the Patriot P210 was identified as the secondary storage device.

### 📸 Evidence

<img width="758" height="760" alt="image png (3)" src="https://github.com/user-attachments/assets/6065037a-17b4-446b-b0c6-252709fbbfad" />


---

## 💾 3. GPT Partition Configuration

**Why This Step Matters:**

Partitioning defines how storage space is organized on a physical disk. Creating a GPT partition table prepares the secondary SSD for filesystem creation and future storage management.

### Command Executed

```bash
sudo fdisk /dev/sdb
```

Opens the `fdisk` utility to manage the partition table on the selected disk.

### fdisk Commands

| Command | Purpose |
|---------|---------|
| `g` | Creates a GPT partition table |
| `n` | Creates a new partition |
| `p` | Displays the proposed partition layout |
| `w` | Writes the partition table to disk |

The default partition number and sector boundaries were accepted to allocate nearly the entire SSD.

### Verification

```bash
lsblk -o NAME,SIZE,MODEL,TYPE,FSTYPE,MOUNTPOINTS
```

Confirms that the new partition exists and displays its filesystem and mount status.

**Result:** Successfully created `/dev/sdb1`, a 119.2 GiB Linux partition.

### 📸 Evidence

<img width="742" height="518" alt="image png (4)" src="https://github.com/user-attachments/assets/3fee5756-c56e-4112-b424-12fc446ac96b" />
<img width="761" height="296" alt="image png (5)" src="https://github.com/user-attachments/assets/1632a019-9528-4355-a8fb-1580bc526440" />



---

## 🛠️ 4. ext4 Filesystem Creation

**Why This Step Matters:**

A partition defines an area of storage, but a filesystem is required to organize and store files.

The ext4 filesystem was selected because it is widely supported in Linux and suitable for general-purpose storage.

### Command Executed

```bash
sudo mkfs.ext4 -L lab-storage /dev/sdb1
```

### Command Explanation

| Component | Purpose |
|-----------|---------|
| `sudo` | Executes with administrative privileges |
| `mkfs.ext4` | Creates an ext4 filesystem |
| `-L lab-storage` | Assigns the filesystem label |
| `/dev/sdb1` | Specifies the partition to format |

### Verification

```bash
lsblk -f
```

Displays filesystem types, labels, UUIDs, and mount points.

**Result:** Successfully created an ext4 filesystem labeled `lab-storage`.

### 📸 Evidence

<img width="756" height="742" alt="image png (6)" src="https://github.com/user-attachments/assets/34704389-9027-492b-980a-30c991dd9f8f" />


---

## 📂 5. Filesystem Mounting & Validation

**Why This Step Matters:**

Linux requires a filesystem to be mounted before its contents can be accessed through the directory structure.

Mounting the secondary SSD at `/mnt/lab-storage` provides a dedicated location for additional storage without modifying the operating system's root filesystem.

### Create Mount Point

```bash
sudo mkdir -p /mnt/lab-storage
```

Creates the directory used to access the SSD. The `-p` option creates missing parent directories if necessary.

### Mount the Filesystem

```bash
sudo mount /dev/sdb1 /mnt/lab-storage
```

Attaches the ext4 filesystem to the specified directory.

### Verify Mount and Capacity

```bash
lsblk -f
df -h /mnt/lab-storage
```

- `lsblk -f` confirms the filesystem is mounted.
- `df -h` displays filesystem capacity, used space, and available storage.

### Results

| Metric | Result |
|--------|--------|
| Filesystem | ext4 |
| Mount Point | `/mnt/lab-storage` |
| Total Capacity | 117 GiB |
| Available Capacity | 111 GiB |
| Mount Status | Successful |

### Read/Write Test

**Why This Test Matters:**

A successfully mounted filesystem does not automatically confirm that data can be written and retrieved. A read/write test verifies basic storage functionality.

Created a test file:

```bash
echo "Physical Data Center Technician Lab - Storage Test" | sudo tee /mnt/lab-storage/storage-test.txt
```

The `echo` command generates text, while `sudo tee` writes that text to a file on the mounted SSD.

Verified the contents:

```bash
cat /mnt/lab-storage/storage-test.txt
```

The `cat` command reads the file to confirm the stored contents.

**Result:** Successfully created and retrieved data from the secondary SSD.

### 📸 Evidence

<img width="942" height="271" alt="Screenshot 2026-11-18 234401 png" src="https://github.com/user-attachments/assets/662fb6de-5ccc-49bc-89f1-61b3ed0a09d3" />
<img width="945" height="668" alt="Screenshot 2026-11-18 234200 png" src="https://github.com/user-attachments/assets/634a0fd8-74ac-49b8-b62b-6eb397683c9a" />


---

## 🔄 6. Persistent Mount Configuration

**Why This Step Matters:**

A manually mounted filesystem does not automatically remain mounted after a reboot.

Configuring `/etc/fstab` ensures the secondary SSD is mounted during system startup, allowing the storage to remain accessible after restarts.

### Back Up fstab

```bash
sudo cp /etc/fstab /etc/fstab.bak
```

Creates a backup of the existing filesystem configuration before making changes.

### Edit fstab

```bash
sudo nano /etc/fstab
```

Opens the filesystem table, which defines filesystems that Linux should mount automatically.

Added the following entry:

```fstab
UUID=a37242de-7949-4ded-af1a-6800872bb6ac /mnt/lab-storage ext4 defaults,nofail 0 2
```

### Configuration Explanation

| Setting | Purpose |
|---------|---------|
| UUID | Identifies the filesystem |
| `/mnt/lab-storage` | Mount directory |
| `ext4` | Filesystem type |
| `defaults` | Standard mount options |
| `nofail` | Allows boot to continue if the drive is unavailable |
| `0` | Disables dump backup |
| `2` | Filesystem check priority |

Using the filesystem UUID provides a more reliable reference than `/dev/sdb1`, since Linux device names can change.

### Validate Configuration

```bash
sudo systemctl daemon-reload
```

Reloads systemd configuration after modifying `/etc/fstab`.

```bash
sudo findmnt --verify --verbose
```

Checks the filesystem table for configuration errors.

**Result:**

```text
0 parse errors, 0 errors, 1 warning
```

The warning referenced Ubuntu's existing swap file and was unrelated to the secondary SSD.

### Test Persistent Mounting

```bash
sudo umount /mnt/lab-storage
```

Unmounts the secondary filesystem.

```bash
sudo mount -a
```

Mounts eligible filesystems defined in `/etc/fstab`, allowing the new configuration to be tested.

```bash
findmnt /mnt/lab-storage
```

Confirms the SSD was successfully remounted.

**Result:** Persistent mount configuration validated.

### 📸 Evidence

<img width="754" height="580" alt="image png (7)" src="https://github.com/user-attachments/assets/c7c4f5fd-6711-4d98-b1fe-d869458de27e" />


---

## ✅ 7. Post-Reboot Validation

**Why This Step Matters:**

Testing `/etc/fstab` manually confirms the configuration can mount the filesystem, but a reboot verifies that the SSD is automatically mounted during normal system startup.

This final check ensures the storage remains accessible without manual intervention.

### Commands Executed

```bash
findmnt /mnt/lab-storage
```

Confirms that the filesystem is mounted at the expected location.

```bash
cat /mnt/lab-storage/storage-test.txt
```

Verifies that the previously created test file remains accessible after reboot.

```bash
lsblk -o NAME,SIZE,MODEL,FSTYPE,MOUNTPOINTS
```

Displays both physical SSDs, their filesystems, and mount points.

### Final Results

| Validation | Status |
|------------|--------|
| Secondary SSD Detection | PASS |
| GPT Partition | PASS |
| ext4 Filesystem | PASS |
| Read/Write Test | PASS |
| Persistent Mount | PASS |
| Automatic Mount After Reboot | PASS |
| Test File Persistence | PASS |

### 📸 Evidence

<img width="746" height="346" alt="image png (8)" src="https://github.com/user-attachments/assets/929d5248-df04-4077-a3ae-51bce7c736d3" />

---

## 🏁 Outcome

Successfully configured the Patriot P210 128 GB SSD as additional storage on Ubuntu Server.

The secondary SSD was partitioned using GPT, formatted with ext4, and mounted at `/mnt/lab-storage`.

Persistent mounting was configured through `/etc/fstab` and successfully validated after reboot.

The existing Ubuntu operating system and LVM configuration remained intact.

## 🛠️ Skills Demonstrated

- Linux disk identification
- GPT partition management
- ext4 filesystem creation
- Filesystem mounting
- Linux storage validation
- UUID-based persistent mounting
- `/etc/fstab` administration
- Storage read/write testing
- Post-reboot system validation
