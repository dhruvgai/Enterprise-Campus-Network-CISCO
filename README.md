Redundant Multi-Floor Enterprise Campus Network

 📌 Project Overview

This project presents the design, configuration, implementation, and testing of a **Redundant Multi-Floor Enterprise Campus Network** using **Cisco Packet Tracer**.

The network is designed using a hierarchical enterprise architecture with **Distribution and Access layers**, VLAN segmentation, Layer 3 routing, gateway redundancy, link redundancy, dynamic routing, secure device management, and ACL-based traffic control.



🎯 Project Objectives

The main objectives of this project are:

- Design a scalable and reliable enterprise campus network.
- Implement VLAN-based network segmentation.
- Configure Inter-VLAN routing.
- Implement HSRP for gateway redundancy.
- Configure EtherChannel using LACP.
- Implement Rapid PVST+ for Layer 2 loop prevention.
- Configure OSPF for dynamic routing.
- Configure DHCP services for end devices.
- Implement SSH for secure device management.
- Configure ACLs to control and restrict network traffic.
- Test, verify, and troubleshoot the complete network.

🏗️ Network Architecture

The project follows a hierarchical enterprise campus network design.

Distribution Layer

- DSW1
- DSW2

 Access Layer

- ASW1
- ASW2
- ASW3

Campus Routing

- R-CAMP1
- R-CAMP2

The distribution switches provide Layer 3 services, routing, gateway redundancy, VLAN interfaces, DHCP services, and network security controls.


📡 Network Topology

The complete network topology is available in the `Diagrams` directory.

![Enterprise Campus Network Topology](Diagrams/Network_Topology.png)


 🔹 VLAN and IP Addressing Plan

| VLAN | Department / Purpose | Network |
|------|----------------------|---------|
| 10 | ADMIN | 10.10.10.0/24 |
| 20 | HR | 10.10.20.0/24 |
| 30 | FINANCE | 10.10.30.0/24 |
| 40 | DEVELOPMENT | 10.10.40.0/24 |
| 50 | TRAINING | 10.10.50.0/24 |
| 60 | SERVER | 10.10.60.0/24 |
| 99 | MANAGEMENT | 192.168.99.0/24 |

The network uses separate VLANs to provide logical segmentation between departments and services.



 🔄 High Availability and Redundancy

Network availability is improved using multiple redundancy mechanisms.

## HSRP

HSRP provides default-gateway redundancy between the distribution switches.

If one distribution switch becomes unavailable, the other distribution switch can continue providing gateway services.
 EtherChannel

EtherChannel is configured between DSW1 and DSW2 using **LACP**.

Benefits include:

- Increased available bandwidth
- Link redundancy
- Improved resilience
- Reduced dependency on a single physical link

## Rapid PVST+

Rapid PVST+ is used to prevent Layer 2 switching loops while providing faster Spanning Tree convergence.



## 🌐 Routing

### Inter-VLAN Routing

Layer 3 Switch Virtual Interfaces (SVIs) are configured for the required VLANs.

Example DSW1 SVI addressing:

| Interface | IP Address |
|-----------|------------|
| VLAN 10 | 10.10.10.2/24 |
| VLAN 20 | 10.10.20.2/24 |
| VLAN 30 | 10.10.30.2/24 |
| VLAN 40 | 10.10.40.2/24 |
| VLAN 50 | 10.10.50.2/24 |
| VLAN 60 | 10.10.60.2/24 |
| VLAN 99 | 192.168.99.2/24 |

### OSPF

OSPF is used as the dynamic routing protocol for communication between the Layer 3 network devices.

The project uses router IDs including:

- R-CAMP1 — `1.1.1.1`
- DSW1 — `2.2.2.2`
- Additional network devices use their configured OSPF router IDs.



## 🖥️ DHCP

DHCP services are configured to provide IP addresses to hosts in the required VLANs.

DHCP configuration includes:

- Address pools
- Default gateways
- Network addresses
- Excluded addresses
- DNS configuration where required

This reduces the need for manual IP configuration on client devices.

---

## 🔐 Network Security

Several security mechanisms are implemented.

### SSH Management

SSH is configured for secure remote management of network devices.

Management access is restricted using an SSH management ACL.

The management networks include:

- `10.10.10.0/24`
- `10.10.99.0/24`

### Access Control Lists

ACLs are used to control communication between network segments.

Important ACL functions include:

- Restricting Training VLAN access to the Server VLAN.
- Protecting Server VLAN resources.
- Allowing authorized management traffic.
- Allowing required web traffic.
- Controlling ICMP traffic.
- Denying unauthorized traffic.

Example ACL:

text
ACL_RESTRICT_TRAINING

This ACL restricts traffic from:

text
10.10.50.0/24

to:

10.10.60.0/24


while allowing other permitted traffic according to the configured policy.

## 🛡️ Server Protection

The Server VLAN is:


10.10.60.0/24


Access to server resources is controlled through the configured server-protection ACL.

Authorized administrative and management networks can access required server resources, while unauthorized access is restricted.



## 🔧 Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- IPv4
- VLAN
- Inter-VLAN Routing
- HSRP
- OSPF
- EtherChannel
- LACP
- Rapid PVST+
- DHCP
- SSH
- Standard ACL
- Extended ACL
- Trunking
- Layer 3 Switching

---




## 🧪 Network Verification

The following Cisco IOS commands were used to verify the configuration and operation of the network.

### VLAN Verification

```cisco
show vlan brief
```

### Trunk Verification

```cisco
show interfaces trunk
```

### EtherChannel Verification

```cisco
show etherchannel summary
```

### Spanning Tree Verification

```cisco
show spanning-tree
```

### HSRP Verification

```cisco
show standby
```

### Routing Table Verification

```cisco
show ip route
```

### OSPF Neighbor Verification

```cisco
show ip ospf neighbor
```

### DHCP Verification

```cisco
show ip dhcp binding
```

### ACL Verification

```cisco
show access-lists
```

### SSH Verification

```cisco
show ip ssh
```

### Interface ACL Verification

```cisco
show ip interface vlan 50
show ip interface vlan 60
```

### Configuration Verification

```cisco
show running-config
```

---

## 📡 Connectivity Testing

Network connectivity was tested using:

```text
ping
traceroute
```

Testing was performed between relevant VLANs, network devices, servers, and management hosts.

The testing verified:

- VLAN connectivity
- Inter-VLAN routing
- OSPF routing
- HSRP gateway availability
- Server accessibility
- ACL restrictions
- SSH management access

---

## 🛠️ Troubleshooting

During implementation, an ACL application issue was identified on DSW1.

### Issue

The ACLs existed correctly, but the required ACLs were initially not applied to the VLAN interfaces.

The following verification showed:

```text
Inbound/Outgoing access list is not set
```

### Troubleshooting Process

1. Checked the ACL configuration.
2. Verified the ACL entries using:

```cisco
show access-lists
```

3. Checked the VLAN interface configuration:

```cisco
show ip interface vlan 50
show ip interface vlan 60
```

4. Identified that the ACL was not applied to the required interface.
5. Reapplied the ACL using the appropriate `ip access-group` command.
6. Verified the interface again.
7. Performed connectivity testing to confirm the security policy.

### Result

The ACL application issue was resolved and the required traffic restrictions were successfully implemented.

---

## 📄 Project Documentation

The complete project report contains detailed information about:

- Network requirements
- Network topology
- Device inventory
- VLAN configuration
- IP addressing
- HSRP configuration
- EtherChannel configuration
- STP configuration
- OSPF configuration
- DHCP configuration
- SSH configuration
- ACL configuration
- Security implementation
- Testing and verification
- Troubleshooting
- Project results
- Conclusion

The complete report is available in:

```text
Documentation/
```

---

## 📦 Packet Tracer Project

The complete Cisco Packet Tracer project file is available in:

```text
Packet_Tracer/
```

Open the `.pkt` file using Cisco Packet Tracer to inspect the topology and configurations.

---


## 📈 Project Outcomes

The completed project demonstrates the implementation of an enterprise campus network with:

- Department-based VLAN segmentation
- Redundant default gateways
- Dynamic routing
- Redundant network links
- Layer 2 loop prevention
- Centralized DHCP services
- Secure SSH management
- ACL-based network security
- Server protection
- Network troubleshooting and verification

---

## 🎓 Skills Demonstrated

This project demonstrates practical skills in:

- Enterprise Network Design
- Cisco IOS Configuration
- VLAN Configuration
- Switching
- Routing
- OSPF
- HSRP
- EtherChannel / LACP
- STP
- DHCP
- SSH
- Network Security
- ACL Configuration
- Network Troubleshooting
- Cisco Packet Tracer

---

## 👨‍💻 Project Information

**Project:** Redundant Multi-Floor Enterprise Campus Network

**Platform:** Cisco Packet Tracer

**Network Type:** Enterprise Campus Network

**Status:** Completed

---

## ⚠️ Security Note

Configuration files uploaded to this repository should not contain real passwords, private keys, API keys, cloud credentials, or other sensitive information.

Any credentials shown in demonstration configurations should be replaced with placeholders before publishing the repository publicly.

---

## 📌 Conclusion

The project successfully demonstrates the design and implementation of a redundant and secure enterprise campus network using Cisco Packet Tracer.

The combination of VLAN segmentation, Inter-VLAN routing, HSRP, EtherChannel, Rapid PVST+, OSPF, DHCP, SSH, and ACLs provides a scalable, resilient, manageable, and secure network architecture suitable for an enterprise environment.
