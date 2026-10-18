# Lab 01 – Windows Server Installation & Initial Configuration

## Scenario

You are a Junior IT Administrator working for a small company that is preparing a new Windows Server environment for centralised user and computer management.

Before implementing Active Directory Domain Services (AD DS), you must deploy and verify a Windows Server virtual machine.

## Objective

Install and configure Windows Server 2022 using Oracle VirtualBox, verify system resources and network connectivity, and prepare the environment for future Active Directory administration and IT Support troubleshooting exercises.

## Tasks

1. Download the official Windows Server 2022 Evaluation ISO.
2. Create a new virtual machine using Oracle VirtualBox.
3. Configure virtual hardware resources, storage, and networking.
4. Install Windows Server 2022 Standard Evaluation with Desktop Experience.
5. Configure the built-in Administrator account.
6. Verify server performance and operating system information.
7. Investigate the network configuration and test connectivity.
8. Create a clean installation snapshot.

---

## 1. Virtual Machine Configuration

The virtual machine was created using Oracle VirtualBox 7.2.6 and the official Windows Server 2022 Evaluation ISO.

The following configuration was used:

| Component | Configuration |
|---|---|
| Virtual Machine | WIN-SRV2022-LAB |
| Operating System | Windows Server 2022 Standard Evaluation |
| Installation Type | Desktop Experience |
| Memory | 3072 MB |
| Virtual CPUs | 2 |
| Virtual Disk | 60 GB, dynamically allocated |
| Disk Format | VDI |
| Network Adapter | Intel PRO/1000 MT Desktop |
| Network Mode | NAT |
| Host Operating System | Windows 10 Home |

The virtual disk was stored on a separate internal partition to avoid using the host operating system's primary storage.

01-vm-hardware.png

02-virtual-disk.png

**Evidence – Screenshot 1:** VirtualBox virtual hardware and disk configuration.

## 2. Windows Server Installation

The Windows Server 2022 Evaluation ISO was attached to the virtual machine.

A clean installation was performed using the following options:

- Windows Server 2022 Standard Evaluation (Desktop Experience)
- Custom installation
- 60 GB unallocated virtual disk

Windows Setup automatically created the required system partitions and completed the operating system installation.

The built-in Administrator account was configured with a password.

Following installation, the server successfully booted into the Windows desktop, and Server Manager launched.

**Result:** Windows Server 2022 was installed successfully.

## 3. System and Performance Verification

The server configuration was inspected using Server Manager and Windows Task Manager.

The following results were recorded:

| Property | Result |
|---|---|
| Computer Name | WIN-CJ8TTMHJDKA |
| Workgroup | WORKGROUP |
| Operating System | Windows Server 2022 Standard Evaluation |
| Installed RAM | 3 GB |
| Memory Usage | Approximately 1.1 GB (37%) |
| Available Memory | Approximately 1.9 GB |
| Virtual Processors | 2 |
| CPU Utilisation | Approximately 3% during observation |
| Remote Management | Enabled |
| Windows Defender Firewall | Enabled |

File Explorer and Server Manager opened normally, with no significant performance issues observed inside the virtual machine.

The host computer experienced minor delays when running the virtual machine alongside other applications, but remained usable.

![Server Properties](screenshots/03-server-properties.png)

**Evidence – Screenshot 2:** Server Manager – Local Server properties.

## 4. Network Configuration Investigation

The following command was executed to investigate the server's network configuration:

```cmd
ipconfig /all
```

The results confirmed that the server received its IPv4 configuration through DHCP.

| Network Property | Result |
|---|---|
| IPv4 Address | 10.0.2.15 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 10.0.2.2 |
| DHCP Server | 10.0.2.2 |
| DNS Server | 192.168.18.1 |
| DHCP Enabled | Yes |

The configuration was consistent with a VirtualBox NAT networking environment.

No static IP address was configured during this laboratory.

## 5. Network Connectivity Testing

Three connectivity tests were performed using Command Prompt.

### Test 1 – Default Gateway Connectivity

```cmd
ping 10.0.2.2
```

**Result:**
- Packets sent: 4
- Packets received: 4
- Packet loss: 0%

The server successfully communicated with its virtual default gateway.

**Status: PASS**

### Test 2 – External Network Connectivity

```cmd
ping 1.1.1.1
```

**Result:**
- Packets sent: 4
- Packets received: 4
- Packet loss: 0%
- Average response time: approximately 11 ms

The successful responses confirmed external IP connectivity through the NAT network.

**Status: PASS**

### Test 3 – DNS Resolution

```cmd
nslookup microsoft.com
```

**Result:**

The configured DNS server, 192.168.18.1, successfully resolved microsoft.com to IPv4 and IPv6 addresses.

Although the DNS server name appeared as "Unknown", the query returned valid results, indicating successful forward DNS resolution.

**Status: PASS**

![Network Connectivity Tests](screenshots/04-network-tests.png)
**Evidence – Screenshot 3:** Command Prompt showing gateway, external connectivity, and DNS test results.

## 6. Virtual Machine Snapshot

After completing the installation and verification tasks, Windows Server was shut down.

A VirtualBox snapshot was created with the following name:

`Clean Windows Server 2022 Installation`

The snapshot preserves the initial server state before installing Active Directory Domain Services or making further administrative changes.

**Result:** Snapshot created successfully.

![Clean Installation Snapshot](screenshots/05-clean-snapshot.png)
**Evidence – Screenshot 4:** VirtualBox Snapshots showing the clean installation snapshot.

## 7. Final Results

| Requirement | Status |
|---|---|
| Windows Server installation | PASS |
| Administrator account configuration | PASS |
| Server Manager access | PASS |
| System resources verification | PASS |
| IPv4 configuration investigation | PASS |
| Default gateway connectivity | PASS |
| External network connectivity | PASS |
| DNS resolution | PASS |
| Clean installation snapshot | PASS |

## 8. Conclusion

Windows Server 2022 Standard Evaluation was successfully deployed in Oracle VirtualBox and verified through system administration and network troubleshooting tools.

The server operated with 3 GB of allocated RAM and two virtual CPUs. Network connectivity and DNS resolution tests were successful, and Server Manager was accessible.

A clean installation snapshot was created to provide a recovery point for subsequent practical exercises.

The environment is ready for the next laboratory, which will focus on server naming, network configuration, and deployment of Active Directory Domain Services.
