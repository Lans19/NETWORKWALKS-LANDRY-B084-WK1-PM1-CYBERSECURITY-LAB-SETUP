# NETWORKWALKS-LANDRY-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP
## NetworkWalks | Batch B084 | Week 1| Project1 (WK1-PM1)

An isolated virtual cybersecurity laboratory built with **Oracle VirtualBox** and **Kali Linux** for safe, authorised penetration-testing and ethical-hacking practice.

> **⚠️ Ethical use notice:** This lab is for education and authorized testing only. Do not scan, attack, or test systems you do not own or do not have explicit permission to test.

## 📌 Project Overview

This project sets up a controlled virtual environment for practising cybersecurity skills such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web application security testing
- Linux and security-tool practice

The lab uses a private NAT Network so that additional target virtual machines can be added later and communicate with the Kali Linux attacker machine.

## ✅ Task Requirements (WK1-PM1)

| Requirement | Status |
| ---| ---|
| Use Virtualbox as base (latest recommended version) | ✅ VirtualBox 7.2.22 |
| Setup Kali Linux as attacking/hacker machine | ✅ Kali 2026.2 |
| Setup the network in subnet 10.0.0.0/24 | ✅
| Use NATNetwork with 10.0.0.0/24 | ✅
| The clipboard & file drag/drop should be enabled in Virtual Machine settings | ✅ Bidirectional
| Shared folders should be enabled with /downloads folder shared from host machine | ✅
| Kali Linux IP Address should be 10.0.0.2/24 | ✅
| Kali Linux should have full Internet access | ✅

## 🎯 Objectives

- Install and configure Oracle VirtualBox 
- Install or import Kali Linux as a virtual machine
- Create a private NAT Network for the cybersecurity lab
- Enable clipboard sharing, file drag/drop, and a shared folder from host machine 
transfer.
- Configure network connectivity forKali Linux 
- Assign a consistent IP address to the Kali VM
- Verify connectivity, internet access, and DNS resolution
- Create a clean VM snapshot for recovery
- Document the setup process and troubleshooting steps
- Prepare the environment for future cybersecurity projects

## Lab Configuration

| 🧩 Component | ⚙️ Configuration |
|---|---|
| 🖥️ Host OS | Windows 11 Pro 26H2 |
| 💻 Host RAM | 16 GB |
| ⚡ Processor | AMD Ryzen 5 7520U with Radeon Graphics (2.80 GHz) |
| 🧰 Hypervisor | Oracle VirtualBox 7.2.22 |
| 🐉 Security OS | Kali Linux 2026.2 |
| 🧠 Kali RAM | 2048 MB |
| 📋 Clipboard | Bidirectional (enabled) |
| 📁 Drag & Drop | 2048 MB |
| 📂 Shared Folder | Host Downloads → Kali (Full access, Auto-mount) |
| 🌐 Virtual Network | NAT Network |
| 📡 Network address | `10.0.0.0/24` |
| 🐧 Kali Linux IP address | `10.0.0.2/24` |
| 🚪 Default gateway | `10.0.0.1` |
| 🌍 DNS server | `8.8.8.8` |
| 🔮 Future target VM IP range | `10.0.0.3` to `10.0.0.99` |

## Setup Procedure

### 1. Install 7-Zip

7-Zip can be used to extract files, the Kali Linux virtual-machine package may be distributed as a .7z archive. Download 7-Zip from the official website.

<img width="1917" height="1078" alt="Download and Install 7-Zip" src="https://github.com/user-attachments/assets/04053bcb-43d5-4d62-a72b-95cce76670c0" />


### 2. Install VirtualBox

Install Oracle VirtualBox on the host computer. VirtualBox is used to create and manage the virtual machines in the lab. VirtualBox can be downloaded from the official website.

<img width="1913" height="1078" alt="Download and Install VirtualBox" src="https://github.com/user-attachments/assets/cf25b79b-0c39-4913-9012-088b92b592d1" />

### 3. Download and Import Kali Linux

Download Kali Linux from the official website and import it into VirtualBox.

If the Kali VM is downloaded as a compressed archive, such as `.7z`, extract it using 7-Zip before importing it into VirtualBox.

Recommended VM settings:

- RAM: 2048 MB or more
- Processors: 2 or more virtual CPU cores
- Network Adapter 1: NAT Network
- Network name: `NatNetwork`
- Adapter type: Intel PRO/1000 MT Desktop

<img width="1917" height="1078" alt="Download and Import Kali Linux" src="https://github.com/user-attachments/assets/1e4873db-168d-4fed-b9c1-a534a0e85c6b" />


### 4. Create the NAT Network

In VirtualBox, create a dedicated NAT Network.

| Setting | Value |
|---|---|
| Network name | `NatNetwork` |
| IPv4 prefix | `10.0.0.0/24` |
| DHCP | Enabled |
| IPv6 | Disabled |

A NAT Network is used instead of a standard NAT adapter because it allows multiple virtual machines on the same network to communicate with each other while still providing outbound internet access.

<img width="1917" height="1078" alt="Creating NAT Network" src="https://github.com/user-attachments/assets/4c73efeb-ac41-4258-800b-8dca637f358b" />

<img width="1917" height="1078" alt="Selecting NAT Network " src="https://github.com/user-attachments/assets/99bf5b75-e9e9-4f7a-97b3-717464f7c3f9" />

### 5. Enable Shared Clipboard and Drag & Drop

Shared Clipboard and Drag & Drop were enabled in VirtualBox to make it easier to transfer text and files between the Windows host computer and the Kali Linux virtual machine.

With these settings enabled, text copied on the host can be pasted into Kali Linux, and text copied in Kali Linux can be pasted on the host. Files and folders can also be dragged between the host and the virtual.

<img width="1917" height="1078" alt="Enabling Shared Clipboard and Drag   Drop" src="https://github.com/user-attachments/assets/2f04aecf-1885-4a73-9462-efd84e83bd80" />

### 6. Add and Enable a Shared Folder

A shared folder named `Kali-VBOX-NW` in the host's downloads folder was created in order to transfer files between the Windows host computer and the Kali Linux virtual machine.

After the VM starts, the shared folder can be accessed from the Kali Linux file manager. This makes it easier to move screenshots, documents, tools, and other files between the host computer and the Kali VM.

<img width="1917" height="1078" alt="Adding and Enabling Shared Folders" src="https://github.com/user-attachments/assets/83c92aeb-5ff2-4441-a7c5-0540c6f6a1ab" />


### 7. Configure Kali Linux Networking

The Kali Linux network settings were configured through the Kali Linux graphical network settings rather than using terminal commands.

1. Open the network settings in Kali Linux.
2. Select the wired network connection.
3. Open the IPv4 settings.
4. Change the configuration method from automatic DHCP to manual.
5. Enter the following network details:

| Network setting | Value |
|---|---|
| IP address | `10.0.0.2` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `10.0.0.1` |
| DNS server | `8.8.8.8` |

6. Save the settings and reconnect the network.
7. Test internet by using browser


<img width="1920" height="923" alt="Configuring Kali Linux Netwotk Settings" src="https://github.com/user-attachments/assets/7389f445-a57d-4e74-8d5d-3d1d5cdac27d" />

<img width="1920" height="923" alt="Tested network and internet is working" src="https://github.com/user-attachments/assets/ee3184ad-d6cb-4006-8da1-1437875ac955" />


### 8. Create a Clean Snapshot

After completing the initial setup, create a VirtualBox snapshot.

**Snapshot name:** `Fresh Install of Kali Linux`

This snapshot provides a known-good recovery point. If a future exercise changes or damages the VM configuration, the lab can be restored to this clean baseline.

<img width="1917" height="1078" alt="Clean Snapshot" src="https://github.com/user-attachments/assets/d7656319-a75d-42c3-a5b2-dede683c72d9" />


## Verification

| Test | Command | Expected result |
|---|---|---|
| Check IP address | `ip a` | Kali IP address `10.0.0.2/24` is displayed |
| Test gateway | `ping 10.0.0.1` | Successful replies |
| Test internet access | `ping 8.8.8.8` | Successful replies |
| Test DNS resolution | `nslookup kali.org` | Domain resolves successfully |
| Verify Nmap | `nmap --version` | Nmap version information is displayed |
| Verify snapshot recovery | Restore snapshot, then run `ip a` | Baseline configuration is restored |

<img width="1920" height="922" alt="Verification Tests" src="https://github.com/user-attachments/assets/057c4244-9609-4109-988f-a422cb8b3ad8" />


## Problems Encountered and Solutions

### Problem 1: No internet after static IP configuration

After setting a static IP address and restarting Kali VM, internet connectivity failed because of NetworkManager configuration.

The solution was to disable duplicate address detection for the connection:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

Then restart the connection and test connectivity again:

```bash
ping 8.8.8.8
nslookup kali.org
```

<img width="1917" height="1078" alt="Restarted VM and Network Issues" src="https://github.com/user-attachments/assets/75efed08-6cdd-4f9d-bf2e-65ca248dd58b" />

<img width="1917" height="1078" alt="Network working after fix" src="https://github.com/user-attachments/assets/b3247ddb-f1e9-487c-ae7a-331c5d35bc19" />


## 💡 What I Learned

Through this project, I learned how to build a safe and isolated cybersecurity laboratory using Oracle VirtualBox and Kali Linux. I now understand that virtualisation allows security tools and vulnerable target systems to be tested without affecting the host computer or unauthorised networks.

### 1. Virtualization and Lab Setup
- I learned how to install and configure Oracle VirtualBox as a hypervisor for creating and managing virtual machines.

- I learned how to download, extract, and import a Kali Linux virtual machine into VirtualBox.

- I learned how to allocate appropriate VM resources, including RAM, virtual processors, and network adapter settings.

- I learned the importance of creating a clean VirtualBox snapshot after completing the initial setup, so the lab can be restored to a known-working baseline if future exercises cause problems.

### 2. Virtual Networking
- I learned the difference between a standard NAT adapter and a VirtualBox NAT Network.

- I learned that a NAT Network allows multiple virtual machines, such as a Kali attacker machine and future target machines, to communicate on the same private network while still accessing the internet.

- I learned how to create a private network using the 10.0.0.0/24 subnet.

- I learned how to assign a static IP address to Kali Linux, including the IP address, subnet mask, default gateway, and DNS server.

- I learned how to verify network connectivity using commands such as ip a, ping, and nslookup.

### 3. Kali Linux and Host Integration
- I learned how to enable bidirectional Shared Clipboard and Drag & Drop between the Windows host and the Kali Linux virtual machine.

- I learned how to configure a shared folder so files such as screenshots, documents, and tools can be transferred easily between the host and the VM.

- I learned how to configure Kali Linux network settings through the graphical Network Settings interface rather than relying only on terminal commands.

- I became more comfortable navigating Kali Linux and using basic Linux networking commands.

### 4. Troubleshooting and Verification
- I learned how to test whether a virtual machine has correct IP configuration, gateway access, internet access, and DNS resolution.

- I learned how to troubleshoot a loss of internet connectivity after applying a static IP configuration.

- I learned that NetworkManager settings can affect connectivity and that network issues should be verified step by step rather than assumed.

- I learned how to confirm that security tools such as Nmap are installed and working using nmap --version.

### 5. Cybersecurity Practice and Ethics
- I learned the importance of using an isolated lab for cybersecurity practice.

- I learned that scanning, testing, or attacking systems without ownership or explicit permission is unethical and potentially illegal.

- I now understand how a properly configured lab prepares the environment for future authorised practice in network reconnaissance, port scanning, vulnerability assessment, packet analysis, and web application security testing.

### Overall Skills Gained
This project strengthened my practical skills in virtualisation, Linux networking, IP addressing, DNS, troubleshooting, documentation, and safe cybersecurity lab design. It also improved my ability to follow technical requirements, test configurations, document problems and solutions, and prepare a reusable environment for future cybersecurity projects.

## 🔗 Tools & Resources

- [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Kali Linux](https://www.kali.org/get-kali/)
- [7-Zip](https://www.7-zip.org/download.html) — used to extract compressed VM files if required
- [Nmap](https://nmap.org/) — installed with Kali Linux for network scanning practice

## 👤 Author

**Landry Kasapato Semilwo**  
Junior Cybersecurity Engineer — Internship - Batch B084 NetworkWalks

- LinkedIn: https://www.linkedin.com/in/landry-semilwo-756904258

## 📌 Project Information

| Field | Details |
|---|---|
| Project title | Cybersecurity Lab Environment Setup |
| Focus area | Virtualisation, networking, Linux, and ethical hacking practice |
| Tools used | VirtualBox, Kali Linux, 7-Zip|
| Status | Completed |
| Date | 27 October 2026 |
