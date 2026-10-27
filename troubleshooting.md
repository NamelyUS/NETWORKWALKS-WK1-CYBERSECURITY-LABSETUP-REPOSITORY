# Network Troubleshooting — Week 1

## Issue 1: NAT Network Connection Failed

### Problem

Kali Linux failed to activate the `NAT-eth0` NetworkManager connection after configuring the static IPv4 address `10.0.0.2/24`.

The error reported:

```
IP configuration could not be reserved
```

NetworkManager logs also reported that `10.0.0.2` was already in use.

### Investigation

The following steps were performed:

1. Verified the VirtualBox NAT Network subnet was `10.0.0.0/24`.
2. Confirmed the gateway was `10.0.0.1`.
3. Disabled DHCP on the NAT Network.
4. Checked the VirtualBox VM network adapters.
5. Reviewed NetworkManager logs to identify the IP conflict.
6. Checked the running virtual machines and host-only adapter configuration.

The conflict persisted after DHCP was disabled.

### Resolution Attempt

To restore network connectivity, the Kali network connection was changed to use `10.0.0.3/24`.

Command:

```
sudo nmcli connection modify "NAT-eth0" ipv4.method manual ipv4.addresses 10.0.0.3/24 ipv4.gateway 10.0.0.1 ipv4.dns "1.1.1.1 8.8.8.8"
```

The connection was then activated:

```
sudo nmcli connection up "NAT-eth0"
```

Result: The connection activated successfully.

### Verification

Gateway connectivity:

```
ping -c 4 10.0.0.1
```

Result: 4 packets received, 0% packet loss.

Internet connectivity:

```
ping -c 4 1.1.1.1
```

Result: 4 packets received, 0% packet loss.

DNS resolution:

```
ping -c 4 google.com
```

Result: Successful.

### Current Status

Network and internet connectivity are working with the temporary static address `10.0.0.3/24`.

The originally required address `10.0.0.2/24` has not yet been configured successfully. Further investigation is needed to identify the device or VirtualBox network component responding to that address.

## Key Takeaways

- Read the complete error message before changing network settings.
- NetworkManager logs can help identify IP address conflicts.
- Verify gateway, external IP, and DNS connectivity separately.
- Record temporary workarounds honestly and distinguish them from the final required configuration.

---

*Documented as part of my Week 1 cybersecurity internship lab setup at NetworkWalks.*
