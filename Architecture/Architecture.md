## Current Architecture

The current lab consists of a physical Ubuntu Server connected
to the home network through Gigabit Ethernet.

The server is remotely administered from a Windows laptop
using SSH.

```mermaid
flowchart TB
    Internet((Internet))
    Router["Home Router<br/>Gateway: 10.0.0.1"]
    Server["Dell OptiPlex 7010 SFF<br/>Ubuntu Server 24.04 LTS<br/>10.0.0.164"]
    Laptop["Windows Laptop<br/>SSH Administration"]

    Internet --- Router
    Router ---|"Cat6 Ethernet"| Server
    Router -.-|"Home LAN"| Laptop
    Laptop -.->|"SSH TCP/22"| Server
```

### Current Configuration

| Component | Configuration |
|---|---|
| Server | Dell OptiPlex 7010 SFF |
| Operating System | Ubuntu Server 24.04 LTS |
| Memory | 10 GB DDR3 |
| Storage | Samsung 128 GB SSD |
| Network | Gigabit Ethernet |
| IP Address | 10.0.0.164/24 (DHCP) |
| Gateway | 10.0.0.1 |
| Remote Access | OpenSSH |



--- 

## Target Architecture

The planned architecture introduces a NETGEAR GS308E managed
switch to support VLAN configuration, network segmentation,
and additional infrastructure troubleshooting exercises.

```mermaid
flowchart TB
    Internet((Internet))
    Router["Home Router / Gateway<br/>VLAN Routing: To Be Determined"]
    Switch["NETGEAR GS308E<br/>8-Port Gigabit Managed Switch"]

    Server["VLAN 10 - Server<br/>Dell OptiPlex 7010 SFF<br/>Ubuntu Server"]
    Laptop["VLAN 20 - Management<br/>Windows Laptop"]
    Test["VLAN 30 - Testing<br/>Future Lab Endpoint"]

    Internet --- Router
    Router ---|"Network Uplink"| Switch

    Switch ---|"Access Port - VLAN 10"| Server
    Switch ---|"Access Port - VLAN 20"| Laptop
    Switch -.->|"Optional - VLAN 30"| Test
```

### Planned Network Configuration

| VLAN | Purpose | Status |
|---|---|---|
| VLAN 10 | Server Infrastructure | Planned |
| VLAN 20 | Management | Planned |
| VLAN 30 | Network Testing | Optional |

### Planned Implementation

- [ ] Install secondary SSD.
- [ ] Integrate NETGEAR GS308E.
- [ ] Document switch port assignments.
- [ ] Configure VLAN membership.
- [ ] Test VLAN connectivity and isolation.
- [ ] Configure inter-VLAN routing if supported.
- [ ] Verify SSH access across the intended management path.
- [ ] Document final network configuration.

**Status:** Planned architecture. Configuration subject to hardware
capabilities and connectivity testing.
