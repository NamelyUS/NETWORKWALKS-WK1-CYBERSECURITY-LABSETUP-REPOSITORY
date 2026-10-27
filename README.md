# NETWORKWALKS-WK1-CYBERSECURITY-LABSETUP-REPOSITORY

# NetworkWalks — Week 1 Cybersecurity Lab Setup

## Overview

This repository documents my Week 1 cybersecurity lab setup as part of my internship at NetworkWalks, under the guidance of Waqas Karim, CCIE.

The objective was to configure a Kali Linux virtual machine in Oracle VirtualBox, establish network connectivity, and troubleshoot configuration issues encountered during setup.

## Objectives

- Configure a VirtualBox NAT Network.
- Connect Kali Linux to the configured network.
- Configure a static IPv4 address.
- Verify gateway connectivity and internet access.
- Document troubleshooting steps and results.

## Lab Environment

| Component | Configuration |
|---|---|
| Host OS | Windows 10 |
| Virtualization | Oracle VirtualBox |
| Attacker VM | Kali Linux |
| Network mode | NAT Network |
| NAT Network name | NatNetwork |
| Network subnet | `10.0.0.0/24` |
| Gateway | `10.0.0.1` |
| Kali IPv4 address | `10.0.0.3/24` |
| DNS servers | `1.1.1.1`, `8.8.8.8` |
| DHCP | Disabled |

### Virtual Network Configuration

- **Adapter 1:** NAT Network (`NatNetwork`)
- **Adapter 2:** Host-only Adapter
- **Shared folder:** Configured in VirtualBox
- **Shared clipboard and drag-and-drop:** Enabled

## Network Verification

### 1. Gateway Connectivity

Command:

```
ping -c 4 10.0.0.1
```

Result: 4 packets received, 0% packet loss.

### 2. Internet Connectivity

Command:

```
ping -c 4 1.1.1.1
```

Result: 4 packets received, 0% packet loss.

### 3. DNS Resolution

Command:

```
ping -c 4 google.com
```

Result: Successful, confirming that hostname resolution and internet connectivity were working.

## Troubleshooting

During configuration, Kali Linux failed to activate its network connection when I assigned the required address `10.0.0.2/24`.

NetworkManager logs reported that `10.0.0.2` was already in use. Disabling DHCP on the NAT Network did not resolve the conflict.

To restore connectivity, I temporarily configured Kali with the static address `10.0.0.3/24`, retaining the gateway `10.0.0.1`.

After activating the connection, I successfully verified communication with the gateway and external internet connectivity.

**Note:** The lab's current working address is 10.0.0.3/24. The originally specified `10.0.0.2/24` address remains unresolved and requires further investigation.

## Lessons Learned

- Configuring a virtual network requires careful IP address planning.
- NetworkManager logs are useful for diagnosing connection failures.
- A successful gateway ping and an external IP ping help verify network connectivity.
- Troubleshooting systematically is more effective than repeatedly changing settings without examining the error messages.

## Repository Structure

```
NETWORKWALKS-WK1-CYBERSECURITY-LAB/
├── README.md
├── troubleshooting.md
└── screenshots/
    └── README.md
```

## Acknowledgment

This lab setup was completed as part of my Week 1 cybersecurity internship tasks at NetworkWalks.

Special thanks to Waqas Karim, CCIE, for the guidance and learning opportunity.

---

*This repository documents my hands-on learning, configuration process, verification results, and troubleshooting experience.*
