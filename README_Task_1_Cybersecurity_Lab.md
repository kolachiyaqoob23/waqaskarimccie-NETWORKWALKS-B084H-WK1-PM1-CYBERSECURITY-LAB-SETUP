# 🔐 Task 1: Cybersecurity Lab Environment Setup

**Project:** Virtualized Cybersecurity and Penetration Testing Lab  
**Author:** Muhammad Yaqoob  
**Degree:** BS Cybersecurity  
**University:** Aror University of Art, Architecture, Design and Heritage  
**Environment:** Kali Linux on Oracle VirtualBox  
**Purpose:** Ethical hacking, networking, reconnaissance, and authorized security testing

---

## 📌 1. Project Overview

This project involves setting up a virtual cybersecurity laboratory using Kali Linux and Oracle VirtualBox on my personal laptop.

The lab provides a controlled environment for learning cybersecurity fundamentals, understanding virtual networking, practicing network reconnaissance, and conducting security assessments against systems that I own or have explicit permission to test.

A dedicated VirtualBox NAT Network has been created to support communication between virtual machines and provide outbound network connectivity. The environment can be extended in future tasks by adding intentionally vulnerable target machines.

## 🎯 2. Project Objectives

The objectives of this task are to:

- Install and run Oracle VirtualBox on my laptop.
- Import and start the Kali Linux virtual machine.
- Create a dedicated NAT Network for the cybersecurity lab.
- Configure Kali Linux network settings.
- Understand DHCP, IPv4 addressing, gateways, and DNS.
- Verify local network and internet connectivity.
- Learn how virtual machines communicate through a virtual network.
- Create a clean snapshot for recovery before practical security exercises.
- Document the setup and troubleshooting process.

## 💻 3. Laptop and Lab Specifications

| Component | Configuration |
|---|---|
| Host device | Personal laptop |
| Host operating system | Windows 11 (as shown in the screenshot) |
| Processor | Intel Core i7 |
| Physical RAM | 8 GB |
| Virtualization software | Oracle VirtualBox |
| Guest operating system | Kali Linux |
| Virtual machine RAM | Verify in VirtualBox settings |
| Network type | NAT Network |
| Network name | `NatNetwork` |
| IPv4 network prefix | `10.0.0.0/24` |
| DHCP server | Enabled |
| IPv6 | Disabled for this NAT Network |
| Kali connection | `Wired connection 1` |
| IPv4 configuration | Automatic (DHCP) |
| DNS shown in Kali settings | `10.0.0.1` |

*Note: Confirm exact Windows, VirtualBox, and Kali Linux versions and allocated VM memory before publishing the final report.*

## 🏗️ 4. Lab Architecture

```text
              Personal Laptop
                 Windows 11
                  8 GB RAM
                      |
                      v
             Oracle VirtualBox
                      |
                      v
                 Kali Linux
             (Cybersecurity VM)
                      |
                      v
                  NatNetwork
                 10.0.0.0/24
                 DHCP: Enabled
                      |
             +--------+--------+
             |                 |
             v                 v
       Future Target VM   Future Target VM
       (Authorized Lab)   (Authorized Lab)
```

The additional target machines are planned extensions and are not claimed to be configured yet.

A NAT Network can allow connected virtual machines to communicate with one another while providing outbound connectivity through network address translation. Actual connectivity depends on the VM adapter configuration and network settings.

## ⚙️ 5. Implementation Procedure

### Step 1: Install the Required Software

The following software is required for this laboratory:

- **7-Zip:** Extracts compressed virtual-machine archives.
- **Oracle VirtualBox:** Runs virtual machines on the host laptop.
- **Kali Linux:** Provides cybersecurity and penetration-testing tools.

Official resources:

- [7-Zip Downloads](https://www.7-zip.org/download.html)
- [Oracle VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads)
- [Official Kali Linux Downloads](https://www.kali.org/get-kali/)

### Step 2: Import and Start Kali Linux

The Kali Linux virtual machine was imported into Oracle VirtualBox and started successfully.

The VM's CPU allocation, RAM allocation, and other hardware settings should be checked in VirtualBox before running resource-intensive tools, especially because the host laptop has 8 GB of RAM.

### Step 3: Create the NAT Network

A dedicated NAT Network named `NatNetwork` was created in VirtualBox.

| Setting | Value |
|---|---|
| Network name | `NatNetwork` |
| IPv4 prefix | `10.0.0.0/24` |
| DHCP | Enabled |
| IPv6 | Disabled |

This network provides a foundation for connecting multiple virtual machines to the same private lab network.

**Screenshot evidence:** VirtualBox Network Manager showing `NatNetwork`, the IPv4 prefix, and the enabled DHCP server.

### Step 4: Configure the Kali Linux Network

The network settings for Kali Linux were opened through the NetworkManager graphical interface.

| Setting | Observed value |
|---|---|
| Connection name | `Wired connection 1` |
| IPv4 method | Automatic (DHCP) |
| Additional DNS server | `10.0.0.1` |
| Network | `NatNetwork` configured in VirtualBox |

The connection is currently configured to obtain its IPv4 address automatically through DHCP.

**Important:** DHCP is not the same as a manually assigned static IP address. A DHCP reservation or static configuration should only be documented after the actual assigned address and network settings have been verified.

### Step 5: Verify Network Connectivity

Run these commands in Kali Linux and record the actual results.

Check network interfaces and IPv4 addresses:

```bash
ip -br addr
```

Check the routing table and default gateway:

```bash
ip route
```

Inspect DNS configuration:

```bash
cat /etc/resolv.conf
```

Test gateway connectivity, if `10.0.0.1` is confirmed as the gateway:

```bash
ping -c 4 10.0.0.1
```

Test connectivity to a public IP address:

```bash
ping -c 4 8.8.8.8
```

Test DNS resolution:

```bash
getent hosts kali.org
```

Check the installed Nmap version:

```bash
nmap --version
```

These commands are verification steps; do not report them as successful until you have run them and observed the results. A failed ping alone does not always prove connectivity is unavailable, because ICMP may be filtered.

### Step 6: Create a Recovery Snapshot

After verifying the network configuration, create a clean snapshot in VirtualBox.

Suggested name: `Clean Kali - Task 1 Baseline`

1. Shut down Kali Linux cleanly or use an appropriate snapshot procedure.
2. Open the VM's **Snapshots** section in VirtualBox.
3. Create a snapshot with the suggested name.
4. Add a description of the verified network configuration.
5. Confirm the snapshot appears in the VM's snapshot list.

The snapshot provides a recovery point before future experiments. Snapshot creation and restoration should be tested rather than assumed complete.

## 🔎 6. Lab Verification Checklist

- [ ] Kali Linux starts successfully.
- [ ] VirtualBox NAT Network exists.
- [ ] NAT Network prefix is `10.0.0.0/24`.
- [ ] DHCP is enabled on the NAT Network.
- [ ] Kali Linux obtains an IPv4 address.
- [ ] Default gateway has been verified.
- [ ] Gateway connectivity has been tested.
- [ ] Outbound network connectivity has been tested.
- [ ] DNS resolution works.
- [ ] Nmap is installed and its version has been checked.
- [ ] Clean recovery snapshot has been created.
- [ ] Snapshot restoration has been tested.

## 🐞 7. Troubleshooting and Lessons Learned

### Problem 1: Internet Connectivity Issues

Incorrect network settings, DNS configuration, or virtual adapter selection can prevent internet connectivity.

**Troubleshooting approach:**

1. Confirm that the VM is connected to the intended `NatNetwork`.
2. Inspect the assigned address with `ip -br addr`.
3. Inspect the default route with `ip route`.
4. Test gateway connectivity.
5. Check DNS resolution separately.
6. Review NetworkManager connection settings before changing them.

Avoid applying random network commands or changing multiple settings simultaneously. Identify the cause before modifying the configuration.

### Problem 2: Incorrect or Unexpected IP Address

Because the network uses DHCP, the address assigned to Kali Linux may vary unless a reservation or persistent configuration is established.

**Solution:** Inspect the assigned address and DHCP configuration. If a stable address is required, configure a suitable DHCP reservation or a correctly planned static address without conflicting with the DHCP pool.

### Problem 3: Virtualization Errors

If a virtual machine fails to start because hardware virtualization is unavailable, check the firmware virtualization settings and VirtualBox diagnostics.

On supported Intel systems, the firmware option is commonly called Intel Virtualization Technology (VT-x). The exact procedure depends on the laptop manufacturer.

## 🧠 8. What I Learned

1. **Virtualization:** Running a separate operating system without replacing the host operating system.
2. **NAT Network:** Connecting multiple virtual machines to a shared virtual network with outbound connectivity.
3. **DHCP:** Automatically obtaining network configuration from a DHCP server.
4. **IPv4 addressing:** Understanding network prefixes, host addresses, and subnet masks.
5. **Default gateway:** Understanding how traffic reaches destinations outside the local network.
6. **DNS:** Translating domain names into IP addresses.
7. **Network troubleshooting:** Using Linux commands to inspect interfaces, routing, and name resolution.
8. **Snapshots:** Maintaining a recovery point before risky experiments.
9. **Technical documentation:** Recording configuration details, evidence, and troubleshooting steps accurately.

## 🔐 9. Security and Ethical Use

This laboratory is intended for educational purposes and authorized security testing only.

- Test only systems that I own or have explicit permission to assess.
- Use intentionally vulnerable virtual machines for exploitation practice.
- Keep target systems isolated from unnecessary external access.
- Review shared-folder settings and avoid exposing sensitive host files to the guest VM.
- Take recovery snapshots before potentially disruptive experiments.
- Do not scan or attack third-party systems without authorization.

**Important:** A NAT Network is not a guarantee of complete isolation. Virtual-machine networking, shared folders, host integration, and port-forwarding settings should be reviewed before running vulnerable targets.

## 🚀 10. Future Improvements

- Add an intentionally vulnerable target VM, such as Metasploitable, in the authorized lab.
- Configure and document a consistent IP-addressing plan.
- Learn Nmap host discovery and port scanning against lab targets.
- Capture and inspect traffic with Wireshark.
- Practice vulnerability assessment and report writing.
- Introduce a local web application for authorized web-security testing.
- Maintain a documented snapshot and recovery strategy.
- Create a network diagram and save command outputs as evidence.

## 📚 11. Tools and References

- [Kali Linux](https://www.kali.org/)
- [Oracle VirtualBox](https://www.virtualbox.org/)
- [7-Zip](https://www.7-zip.org/)
- [Nmap Documentation](https://nmap.org/book/man.html)
- [Wireshark](https://www.wireshark.org/)

## 👤 12. Project Information

| Field | Details |
|---|---|
| Student | Muhammad Yaqoob |
| Program | BS Cybersecurity |
| University | Aror University |
| Task | Task 1 — Cybersecurity Lab Environment Setup |
| Project category | Cybersecurity / Virtualization / Networking |
| Host platform | Windows laptop |
| Guest platform | Kali Linux |
| Virtual network | `NatNetwork` |
| Network prefix | `10.0.0.0/24` |

---

**Project Status:** Initial virtual lab setup and NAT Network configuration documented. Remaining verification steps should be completed and supported with screenshots or command outputs before the task is submitted as fully verified.
