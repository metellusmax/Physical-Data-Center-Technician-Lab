# Phase 3: Ubuntu Server Network Configuration

**Project:** Physical Data Center Technician Lab  
**System:** Dell OptiPlex 7010 SFF  
**Asset ID:** PHY-SRV01  
**Status:** ✅ Completed

## 🎯 Objective

Configure wired Ethernet connectivity on a physical Ubuntu Server using Netplan and DHCP.

This exercise focuses on network interface identification, IPv4 configuration, routing, DNS resolution, and connectivity validation.

---

## ⚙️ 1. Network Environment

| Component | Configuration |
|-----------|---------------|
| Server | Dell OptiPlex 7010 SFF |
| Operating System | Ubuntu Server 24.04 LTS |
| Network Adapter | Intel 82579LM Gigabit Ethernet |
| Interface | `eno1` |
| Connection Type | Wired Ethernet |
| IPv4 Configuration | DHCP |
| Observed IPv4 Address | `10.0.0.164/24` |
| Default Gateway | `10.0.0.1` |
| Network Configuration Tool | Netplan |
| Network Renderer | systemd-networkd |

> The IP address was assigned dynamically through DHCP and may change.

---

## 🔌 2. Ethernet Interface Identification

Ubuntu Server was initially installed without network connectivity.

After completing the physical Ethernet cabling exercise, the server was connected to the home network.

### Interface Verification

Executed:

```bash
ip -br link
```

The output confirmed:

```text
eno1    UP    <BROADCAST,MULTICAST,UP,LOWER_UP>
```

### Result

- Ubuntu recognized the integrated Ethernet adapter.
- The Ethernet interface was enabled.
- A physical network link was established.
- The terminated Cat6 cable provided working connectivity.

### IP Address Verification

Executed:

```bash
ip -br addr
```

The interface initially had IPv6 addressing but no DHCP-assigned IPv4 address.

**Finding:** The physical Ethernet connection was operational, but IPv4 configuration was required.



---

## 🛠️ 3. Network Configuration Using Netplan

Netplan was used to configure the Ethernet interface to obtain an IPv4 address automatically through DHCP.

### Initial Configuration Inspection

Executed:

```bash
ls /etc/netplan/
```

```bash
sudo cat /etc/netplan/*.yaml
```

No existing Netplan YAML configuration files were found.
### Create Network Configuration

Created the following file:

```bash
sudo nano /etc/netplan/01-ethernet.yaml
```

Added:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eno1:
      dhcp4: true
```

### Configuration Explanation

| Setting | Purpose |
|---------|---------|
| `network` | Defines the network configuration |
| `version: 2` | Specifies the Netplan configuration format |
| `renderer: networkd` | Uses systemd-networkd to manage networking |
| `ethernets` | Defines Ethernet interfaces |
| `eno1` | Identifies the physical Ethernet adapter |
| `dhcp4: true` | Enables automatic IPv4 configuration through DHCP |

### Secure the Configuration File

Executed:

```bash
sudo chmod 600 /etc/netplan/01-Ethernet.yaml
```

This restricted access to the configuration file.

### Generate and Apply Configuration

Executed:

```bash
sudo netplan generate
sudo netplan apply
```

The configuration was successfully applied.

### 📸 Evidence

**Netplan Configuration**

<img width="972" height="420" alt="image" src="https://github.com/user-attachments/assets/cfd71d55-d1f4-4505-8473-1c374f9ed0fd" />


---
### 🌐 4. DHCP Configuration Verification

After applying the Netplan configuration, verified the network interface using:

```bash
ip -br addr
```

### Results

| Setting | Verified Value |
|---------|----------------|
| Interface | `eno1` |
| Interface Status | UP |
| IPv4 Address | `10.0.0.164` |
| Subnet Prefix | `/24` |
| Address Assignment | DHCP |

**Result:** Ubuntu Server successfully obtained an IPv4 address from the home network.



---

### 🧪 5. Network Connectivity Testing

Performed connectivity tests to verify local network communication, internet access, and DNS resolution.

### Test 1: Default Gateway Verification

Executed:

```bash
ip route
```

Verified the default gateway:

```text
default via 10.0.0.1 dev eno1
```

**Result:** The server had a valid default route through the home router.

### Test 2: Gateway Connectivity

Executed:

```bash
ping -c 4 10.0.0.1
```

Results:

- 4 packets transmitted
- 4 packets received
- 0% packet loss
- Average latency: 1.191 ms

**Status:** PASS

### Test 3: Internet Connectivity

Executed:

```bash
ping -c 4 1.1.1.1
```

Results:

- 4 packets transmitted
- 4 packets received
- 0% packet loss
- Average latency: 12.257 ms.
**Status:** PASS

### Test 4: DNS Resolution

Executed:

```bash
ping -c 4 google.com
```

Results:

- Domain name successfully resolved.
- 4 packets transmitted.
- 4 packets received.
- 0% packet loss.
- Average latency: 13.538 ms.

**Status:** PASS

### Connectivity Test Summary

| Test | Result | Status |
|------|--------|--------|
| Ethernet Link | Established | PASS |
| DHCP Assignment | Successful | PASS |
| Default Gateway | Detected | PASS |
| Gateway Connectivity | 0% Packet Loss | PASS |
| Internet Connectivity | 0% Packet Loss | PASS |
| DNS Resolution | Successful | PASS |

### 📸 Evidence

**Routing Table and Network Connectivity Test**
<img width="730" height="618" alt="image" src="https://github.com/user-attachments/assets/8725ba92-cdaf-414f-8f89-deb6299c90ca" />


---

## ✅ 6. Final Validation

The network configuration was successfully completed.

### Verified Results

- Physical Ethernet connection established.
- Integrated network adapter detected by Ubuntu.
- Netplan configuration created and applied.
- DHCP successfully assigned an IPv4 address.
- Default gateway verified.
- Internet connectivity confirmed.
- DNS resolution confirmed.

The server was prepared for remote administration using OpenSSH.

---

## 🏁 Outcome

Successfully configured wired Ethernet networking on a physical Ubuntu Server using Netplan and DHCP.

The server established connectivity with the home network, received an IPv4 address, and successfully communicated with the default gateway and external network resources.

This configuration enabled subsequent remote administration through SSH.

## 🛠️ Skills Demonstrated

- Linux network interface identification
- Ethernet connectivity validation
- Netplan configuration
- DHCP administration
- IPv4 addressing and subnetting
- Routing table inspection
- Network connectivity testing
- DNS troubleshooting
- Linux network administration



