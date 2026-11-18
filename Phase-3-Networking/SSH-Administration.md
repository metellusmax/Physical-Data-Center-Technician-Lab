# Phase 3: SSH Remote Administration

**Project:** Physical Data Center Technician Lab  
**System:** Dell OptiPlex 7010 SFF  
**Asset ID:** PHY-SRV01  
**Status:** ✅ Completed

## 🎯 Objective

Establish secure remote command-line access to a physical Ubuntu Server from a Windows laptop using Secure Shell (SSH).

This exercise focuses on SSH service verification, remote authentication, Linux system administration, and package management over a network connection.

---

## ⚙️ 1. Environment

| Component | Configuration |
|-----------|---------------|
| Server | Dell OptiPlex 7010 SFF |
| Operating System | Ubuntu Server 24.04 LTS |
| Hostname | `dct-lab-server` |
| SSH Server | OpenSSH |
| SSH Client | Windows PowerShell |
| Network Interface | `eno1` |
| Server IPv4 Address | `10.0.0.164` |
| Client IPv4 Address | `10.0.0.53` |
| Authentication | Username and Password |
| SSH Port | TCP 22 |

> IP addresses were assigned through DHCP and may change.

---

## 🔐 2. SSH Server Configuration

OpenSSH Server was selected during the initial Ubuntu Server installation.

Password authentication was enabled for initial remote administration within the home lab.

### SSH Service Verification

Executed:

```bash
systemctl status ssh
```

The output indicated that the SSH service was inactive but configured for socket activation.

```text
Active: inactive (dead)
TriggeredBy: ssh.socket
```

### SSH Socket Verification

Executed:

```bash
systemctl status ssh.socket
```

The output confirmed:

```text
Active: active (listening)
Listen: 0.0.0.0:22
        [::]:22
```

### Result

- OpenSSH Server successfully installed.
- SSH socket activation enabled.
- TCP port 22 available for incoming SSH connections.
- Server prepared for remote administration.

> Ubuntu Server 24.04 supports socket-activated SSH,
> allowing the SSH service to start when a connection is received.

### 📸 Evidence

**SSH Service Status and SSH Socket Verification**

<img width="1197" height="612" alt="image" src="https://github.com/user-attachments/assets/8015e9d7-8cda-4d0a-b7ec-a1b8f7fed189" />




## 💻 3. Remote SSH Connection

After configuring Ethernet networking and verifying connectivity, established an SSH connection from a Windows laptop.

### Connection Procedure

1. Connected the Windows laptop to the home network.
2. Opened Windows PowerShell.
3. Initiated an SSH connection to the Ubuntu Server.
4. Accepted the server's SSH host key after verification.
5. Authenticated using the Ubuntu administrator account.
6. Successfully accessed the remote Linux shell.

### SSH Connection Command

Executed from Windows PowerShell:

```powershell
ssh max@10.0.0.164
```

### Successful Authentication

After authentication, the remote terminal displayed:

```bash
max@dct-lab-server:~$
```

This confirmed that the Windows laptop successfully established a remote SSH session with the physical Ubuntu Server.

### 📸 Evidence

**Successful Remote SSH Connection**

<img width="658" height="713" alt="image png (1)" src="https://github.com/user-attachments/assets/56119c3d-95d2-449b-95d6-8c6b0013a74c" />


---

## ✅ 4. Ubuntu Package Management

After establishing the SSH session,  Ubuntu package updates through the established SSH session.


### Update Package Information

Executed:

```bash
sudo apt update
```

This refreshed the available package information from configured Ubuntu repositories.

### Upgrade Installed Packages

Executed:

```bash
sudo apt upgrade
```

This upgraded installed packages to available versions from the configured repositories.

### Result

- Package information successfully refreshed.
- Available package upgrades applied.
- Ubuntu package maintenance completed remotely.
- SSH connectivity remained operational during administration.





## 🛡️ 5. Security Considerations

The initial SSH configuration uses password authentication for remote access within the home lab.

### Current Security Practices

- SSH access restricted to the trusted home network.
- Authentication required for remote access.
- Administrative commands executed using `sudo`.
- Ubuntu packages updated.
- No intentional public internet exposure of SSH.

### Planned Security Improvements

- [ ] Configure SSH key-based authentication.
- [ ] Verify key-based login.
- [ ] Disable password authentication after validating SSH keys.
- [ ] Review SSH configuration and access controls.
- [ ] Evaluate firewall rules for SSH access.

> Password authentication will remain enabled until
> key-based authentication is successfully configured
> and tested.

---

## ✅ 6. Final Validation

| Validation Check | Result |
|------------------|--------|
| OpenSSH Installation | PASS |
| SSH Socket Activation | PASS |
| TCP Port 22 Listening | PASS |
| Remote SSH Connection | PASS |
| User Authentication | PASS |
| Remote Linux Shell | PASS |
| Remote Package Updates | PASS |

**Overall Result:** Successfully established and validated SSH remote administration.



## 🏁 Outcome

Successfully configured and verified remote administration of a physical Ubuntu Server from a Windows laptop using OpenSSH.

The server can now be administered remotely over the local network without requiring direct keyboard and monitor access.

This exercise demonstrated practical Linux server administration, SSH authentication, remote troubleshooting, and operating system maintenance.

## 🛠️ Skills Demonstrated

- SSH remote administration
- OpenSSH service verification
- SSH socket activation
- Remote authentication
- Linux command-line administration
- Linux resource monitoring
- Ubuntu package management
- Secure remote access fundamentals


