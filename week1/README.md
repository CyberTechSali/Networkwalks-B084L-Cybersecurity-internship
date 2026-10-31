# Week 1: Cybersecurity Lab Setup

**Networkwalks - B084L**

## Objective

Build a small virtual network with **VirtualBox** made of two machines (Kali Linux and Windows 10), and verify that they can communicate with each other.

## Environment

| Item | Detail |
|---|---|
| Hypervisor | Oracle VirtualBox |
| VM 1 | Kali Linux (`kali vm`) |
| VM 2 | Windows 10 (`vm-win10`) |
| Network type | NAT Network (`NatNetwork`) |
| Network range | `10.0.0.0/24` |
| DHCP | Enabled |

## 1. Creating the NAT Network

In VirtualBox: **File > Tools > Network Manager > NAT Networks > Create**

- **Name**: `NatNetwork`
- **IPv4 Prefix**: `10.0.0.0/24`
- **Enable DHCP**: checked
- **Enable IPv6**: unchecked

![NAT Network configuration](images/1.png)

## 2. Configuring the VM Network Adapters

For each VM: **Settings > Network > Adapter 1**

- **Attached to**: `NAT Network`
- **Name**: `NatNetwork`
- **Promiscuous Mode**: `Allow All`
- **Virtual Cable Connected**: checked

![vm-win10 network settings](images/2.png)

> `Allow All` promiscuous mode lets a VM see all traffic on the virtual network, which will be useful for packet analysis later.

## 3. IP Addresses (assigned via DHCP)

| Machine | IPv4 Address | Subnet Mask | Gateway |
|---|---|---|---|
| Kali Linux | `10.0.0.4` | `255.255.255.0` | `10.0.0.1` |
| Windows 10 | `10.0.0.3` | `255.255.255.0` | `10.0.0.1` |

**Kali** (`ifconfig` command):

![Kali IP address](images/3.png)

**Windows 10** (`ipconfig` command):

![Windows IP address](images/4.png)

## 4. Connectivity Test

From Windows 10, ping Kali:

```
ping 10.0.0.4
```

Result: 4 packets sent, 4 received, **0% loss**, response time < 1 ms. TTL = 64, which is consistent with a Linux system.

![Ping from Windows to Kali](images/5.png)

## Network Diagram

```
            NatNetwork (10.0.0.0/24)
                     |
        +------------+------------+
        |                         |
  Kali Linux                 Windows 10
  10.0.0.4                   10.0.0.3
        \                         /
         \---- Gateway 10.0.0.1 ----/
```

## Conclusion

Both machines are on the same `10.0.0.0/24` network, receive their IP addresses automatically via DHCP, and communicate successfully. The lab is ready for the coming weeks.

## Useful Commands

```bash
# Linux
ifconfig          # or: ip a
ping <ip>

# Windows
ipconfig
ping <ip>
```
