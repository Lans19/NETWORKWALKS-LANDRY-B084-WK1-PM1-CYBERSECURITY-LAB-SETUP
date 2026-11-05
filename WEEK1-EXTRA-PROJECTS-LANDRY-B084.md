# 🚀 Extra Projects for Week 1

⬅️ **Back to the main Week 1 project:**  
[README.md](./README.md)

**👤 Author:** Landry Kasapato Semilwo (Junior Cybersecurity Engineer)    
**🎓 Program:** Cybersecurity at NetworkWalks   
**🏷️ Batch:** B084   
**📅 Week:** 1  
**🛠️ Project:** Cybersecurity Lab Environment Setup — Extra Projects  
**✅ Status:** Completed  
**🗓️ Date:** 5 November 2026

This section documents the additional Week 1 projects completed alongside the eight Wireshark labs, the Wireshark quiz, and the Wireshark advanced quiz. I set up both an Android-x86 9.0 virtual machine and a Windows 10 virtual machine in Oracle VirtualBox, connected them to the same NAT Network as my Kali Linux VM, and completed the six extra SOC Wireshark browser labs.

---

## 1. 🤖 Week 1 Extra Project — Android-x86 in VirtualBox

### 🎯 Task

Set up an Android-x86 virtual machine inside VirtualBox, connect it to the same NAT Network as the Kali Linux VM, and confirm that both machines can reach each other and the internet.

### 📋 Requirements

- VirtualBox already installed, using the same installation used for Kali Linux.
- At least 10 GB of free disk space.
- At least 2 GB of RAM available for the Android VM.
- Kali Linux VM already configured on the NAT Network with IP address `10.0.0.2/24`.

### 🌐 Network Summary

| Setting | Value |
|---|---|
| Network type | VirtualBox NAT Network |
| Kali Linux IP address | `10.0.0.2 / 24` |
| Android 9.0 IP address | `10.0.0.9 / 24` |
| Gateway | `10.0.0.1` |
| DNS server | `8.8.8.8` |

### 🧩 Solution

#### Step 1: Download the Android-x86 9.0 ISO

1. Opened the official Android-x86 download page.
2. Selected the **Release 9.0** folder, which leads to the project’s official SourceForge release page.
3. Downloaded `android-x86_64-9.0-r2.iso` for a 64-bit virtual machine.
4. Noted the location where the ISO file was saved.

> **💡 Tip:** Always download Android-x86 from the official `android-x86.org` page or its linked SourceForge release folder. Avoid third-party mirror sites for security reasons.

#### Step 2: Create a New VM in VirtualBox

1. Opened VirtualBox and clicked **New**.
2. Named the virtual machine **Android9-Lab**.
3. Set **Type** to **Linux**.
4. Set **Version** to **Other Linux (64-bit)**.
5. Allocated **2048 MB (2 GB)** of RAM.
6. Created a new virtual hard disk using the **VDI** format.
7. Selected **Dynamically allocated** storage.
8. Set the disk size to at least **10 GB**.

VirtualBox does not have a dedicated Android guest type because Android-x86 is based on Linux.

#### Step 3: Attach the ISO and Start the Installation

1. Opened **Settings > Storage**.
2. Selected the empty optical disk under the storage controller.
3. Attached the Android-x86 9.0 ISO.
4. Opened **Settings > Display**.
5. Set Video Memory to at least **64 MB**.
6. Enabled **3D Acceleration** during the first installation attempt.
7. Started the VM.
8. From the Android-x86 boot menu, selected **Installation - Install Android-x86 to harddisk**.
9. Created/modified partitions and selected the virtual disk.
10. Selected the **ext4** filesystem.
11. Confirmed installation of **GRUB**.
12. Confirmed that the system should be made writable.
13. Allowed installation to complete and rebooted when prompted.

#### Step 4: Set the Network to NAT Network

1. Shut down the Android VM completely.
2. Opened **Settings > Network**.
3. Set **Attached to** to **NAT Network**.
4. Selected the same NAT Network used by the Kali Linux VM.
5. Started the VM again.

#### Step 5: Set a Static IP Address Inside Android

1. On the Android home screen, opened **Settings**.
2. Went to **Network & Internet > Ethernet**.
3. Disabled DHCP / selected **Static IP**.
4. Entered the following settings:

| Setting | Value |
|---|---|
| IP address | `10.0.0.9` |
| Subnet mask | `255.255.255.0` |
| Gateway | `10.0.0.1` |
| DNS 1 | `8.8.8.8` |

#### Step 6: Test Connectivity

From the Android terminal, I ran:

```bash
ping 10.0.0.2
```

This confirmed that Android could reach the Kali Linux VM.

```bash
ping 8.8.8.8
```

This confirmed that Android had internet access.

From Kali Linux, I ran:

```bash
ping 10.0.0.9
```

This confirmed that Kali Linux could reach the Android VM.

#### Step 7: Submit Evidence

I took a screenshot showing successful pings in both directions:

- Android to Kali: `ping 10.0.0.2`
- Kali to Android: `ping 10.0.0.9`

The screenshot was submitted through the Week 1 submission page.

---

## 🛠️ Android-x86 Boot Issue and Solution

### ⚠️ Issue Encountered

When setting up the **Android9-Lab** virtual machine, Android-x86 could not boot properly. The VM took a very long time to start and experienced a black-screen / slow-boot issue.

### 🔍 Cause

The display configuration and boot options were not compatible with the Android-x86 guest. The virtual graphics controller, acceleration settings, EFI setting, and default GRUB boot parameters contributed to the problem.

### ✅ How I Solved It

I powered off the Android VM completely and applied the following VirtualBox settings.

#### Step 1: Correct the Display Settings

1. Powered off the Android VM completely.
2. Opened **Settings > Display**.
3. Set **Graphics Controller** to **VMSVGA**.
4. Set **Video Memory** to **128 MB**.
5. Disabled **3D Acceleration**.
6. Disabled **2D Video Acceleration**.

| Setting | Correct value |
|---|---|
| Graphics Controller | VMSVGA |
| Video Memory | 128 MB |
| 3D Acceleration | Off |
| 2D Video Acceleration | Off |

#### Step 2: Correct the System Boot Settings

1. Opened **Settings > System > Motherboard**.
2. Disabled **EFI**.
3. Set the boot order so that **Hard Disk** was first, followed by the optical drive.

| Setting | Correct value |
|---|---|
| EFI | Off |
| Boot order | Hard Disk first, then Optical |

#### Step 3: Add Display Compatibility Options in GRUB

1. Started the Android VM.
2. At the Android-x86 GRUB menu, pressed **E** to edit the selected boot entry.
3. Located the line containing `quiet`.
4. Replaced `quiet` with the following options:

```text
nomodeset xforcevesa
```

5. Pressed **ESC** or then selected **Android-x86 Debug (nomodeset)** to boot with the modified entry.

These options force basic display compatibility and fixed the black-screen and slow-boot issue with VMSVGA.

### 🎉 Result

After applying the VMSVGA settings, disabling EFI, correcting the boot order, and adding `nomodeset xforcevesa` to the GRUB boot entry, the Android-x86 VM booted successfully. I was then able to configure its static IP address and verify connectivity with Kali Linux and the internet.

---

## 2. 🪟 Week 1 Extra Project — Windows 10 in VirtualBox

### 🎯 Task

Set up a Windows 10 virtual machine inside VirtualBox, connect it to the same NAT Network as the Kali Linux VM, and confirm that both machines can reach each other and the internet.

### 📋 Requirements

- VirtualBox already installed, using the same installation used for Kali Linux.
- At least 40 GB of free disk space.
- At least 4 GB of RAM available for the Windows 10 VM.
- Kali Linux VM already configured on the NAT Network with IP address `10.0.0.2/24`.

### 🌐 Network Summary

| Setting | Value |
|---|---|
| Network type | VirtualBox NAT Network |
| Kali Linux IP address | `10.0.0.2 / 24` |
| Windows 10 IP address | `10.0.0.10 / 24` |
| Gateway | `10.0.0.1` |
| DNS server | `8.8.8.8` |

### 🧩 Solution

#### Step 1: Download the Windows 10 ISO

1. Opened Microsoft’s official Windows 10 download page.
2. Under **Create Windows 10 installation media**, selected **Download Now / Download tool now**.
3. Ran `MediaCreationTool.exe`.
4. Accepted the Microsoft licence terms.
5. Selected **Create installation media for another PC**.
6. Selected the required language, Windows 10 edition, and **64-bit (x64)** architecture.
7. Selected **ISO file**.
8. Chose a location to save the ISO.
9. Waited for the Media Creation Tool to download Windows and create the ISO file.

> **💡 Tip:** Microsoft’s page may show the Media Creation Tool instead of a direct ISO download. The tool can still create the ISO needed for VirtualBox.

**Backup method if a direct ISO option is not shown:**

1. Opened Microsoft’s Windows 10 ISO page in Chrome or Microsoft Edge.
2. Pressed **F12** to open Developer Tools.
3. Enabled the Device Toolbar / Responsive Design Mode.
4. Selected a mobile or tablet device profile.
5. Refreshed the page.
6. If Microsoft displayed edition and language selectors, selected **Windows 10** and downloaded the 64-bit ISO.
7. Used Microsoft’s official download source rather than unofficial ISO websites.

#### Step 2: Create a New VM in VirtualBox

1. Opened VirtualBox and clicked **New**.
2. Named the virtual machine **Windows10-Lab**.
3. Set **Type** to **Microsoft Windows**.
4. Set **Version** to **Windows 10 (64-bit)**.
5. Allocated **4096 MB (4 GB)** of RAM.
6. Created a new virtual hard disk using the **VDI** format.
7. Selected **Dynamically allocated** storage.
8. Set the disk size to at least **40 GB**.

#### Step 3: Attach the ISO and Start the Installation

1. Opened **Settings > Storage**.
2. Selected the empty optical disk under the storage controller.
3. Attached the Windows 10 ISO.
4. Started the VM.
5. Windows Setup booted from the ISO.
6. Followed the on-screen steps:
   - Selected language and keyboard preferences.
   - Clicked **Install Now**.
   - Skipped the product key when asked.
   - Selected **Custom install**.
   - Selected the virtual disk.
   - Allowed Windows to complete installation.

#### Step 4: Set the Network to NAT Network

1. Shut down the Windows 10 VM completely.
2. Opened **Settings > Network**.
3. Set **Attached to** to **NAT Network**.
4. Selected the same NAT Network used by the Kali Linux VM.
5. Started the VM again.

#### Step 5: Set a Static IP Address Inside Windows

1. Opened **Control Panel > Network and Sharing Center > Change adapter settings**.
2. Right-clicked the network adapter and selected **Properties**.
3. Selected **Internet Protocol Version 4 (TCP/IPv4)**.
4. Clicked **Properties**.
5. Selected **Use the following IP address**.
6. Entered the following settings:

| Setting | Value |
|---|---|
| IP address | `10.0.0.10` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `10.0.0.1` |
| Preferred DNS server | `8.8.8.8` |

#### Step 6: Test Connectivity

From Windows Command Prompt, I ran:

```cmd
ping 10.0.0.2
```

This confirmed that Windows could reach the Kali Linux VM.

```cmd
ping 8.8.8.8
```

This confirmed that Windows had internet access.

From Kali Linux, I ran:

```bash
ping 10.0.0.10
```

This confirmed that Kali Linux could reach the Windows 10 VM.

---

## 3. 🕵️ SOC Project Module — Wireshark (Extra)

### 🎯 Mission

I acted as a SOC analyst and investigated six live Wireshark labs in the browser. Each lab provided a network capture and 10 tasks. I used Wireshark skills to identify attackers, hidden data, clear-text passwords, brute-force activity, and a scam call.

### 🧠 What I Practised

- Finding an attacker’s IP address.
- Using **Follow TCP Stream** to rebuild conversations.
- Identifying hidden data inside network captures.
- Finding usernames and passwords sent in clear text over HTTP.
- Detecting brute-force login attempts.
- Investigating VoIP calls and identifying a call scammer.

### 📜 Practice Rules

- Work was performed only inside the provided labs.
- No traffic was captured or tested on a network that I do not own or do not have written permission to test.
- Each task was attempted independently before using hints.
- Hints were used only when I got stuck.

### 🧪 The 6 SOC Wireshark Labs Completed

| SOC Lab | Focus | Link | Status |
|---|---|---|---|
| Identify the Attacker’s IP | Find the attacker’s IP address in the traffic. | `networkwalks.com/wireshark-lab3/` | Completed — all 10 tasks |
| Follow TCP Stream 1 | Rebuild a conversation and read what was sent. | `networkwalks.com/wireshark-lab4/` | Completed — all 10 tasks |
| Follow TCP Stream, Part 2 | Practise Follow TCP Stream on a new capture and find hidden data. | `networkwalks.com/wireshark-lab5/` | Completed — all 10 tasks |
| HTTP Plain Text Credentials | Find usernames and passwords sent in clear text over HTTP. | `networkwalks.com/wireshark-lab6/` | Completed — all 10 tasks |
| Catch the Brute Force Attacker | Spot repeated login attempts and identify who is guessing passwords. | `networkwalks.com/wireshark-lab7/` | Completed — all 10 tasks |
| Catch the Call Scammer | Investigate the capture, play the call, and identify the scammer. | `networkwalks.com/wireshark-lab8/` | Completed — all 10 tasks |




### ✅ Completion Record

- Completed all 8 Wireshark labs.
- Completed the Wireshark quiz.
- Completed the Wireshark advanced quiz.
- Completed all 6 extra SOC Wireshark labs, with all 10 tasks in each lab.
- Set up and verified the Android-x86 9.0 VM at IP address `10.0.0.9`.
- Set up and verified the Windows 10 VM at IP address `10.0.0.10`.
- Confirmed Kali-to-VM and VM-to-Kali connectivity.
- Confirmed internet access from Kali Linux, Android-x86, and Windows 10.

---

## 4. ⚠️ Issues Encountered and Solutions

### Issue 1: 🤖 Android-x86 VM Could Not Boot Properly

**Problem:**  
The Android9-Lab VM could not boot normally. It took a long time to boot and showed a black-screen issue.

**Cause:**  
The VM’s display configuration, EFI setting, boot order, and default GRUB boot parameters were not compatible with Android-x86.

**Solution:**  
I powered off the Android VM completely and made the following changes:

1. Opened **Settings > Display**.
2. Set **Graphics Controller** to **VMSVGA**.
3. Increased **Video Memory** to **128 MB**.
4. Turned **3D Acceleration** off.
5. Turned **2D Video Acceleration** off.
6. Opened **Settings > System > Motherboard**.
7. Turned **EFI** off.
8. Set the boot order to **Hard Disk first**, then optical drive.
9. Started the VM and pressed **E** at the Android-x86 GRUB menu.
10. Replaced `quiet` with:

```text
nomodeset xforcevesa
```

11. Pressed **ESC** then selected **Android-x86 Debug (nomodeset)** to boot.

**Result:**  
The Android-x86 VM booted successfully. The display compatibility options resolved the black-screen and slow-boot problem.

### Issue 2: 🪟 Kali Linux Could Not Reach Windows 10

**Problem:**  
After assigning the static IP address `10.0.0.10` to the Windows 10 VM, Kali Linux could not successfully ping Windows 10 using:

```bash
ping 10.0.0.10
```

The IP addressing and NAT Network configuration appeared correct, but connectivity from Kali to Windows was still failing.

**Cause:**  
The Windows 10 Ethernet network profile was set to **Private**. The Private network profile applied stricter network discovery and firewall behaviour, which prevented Kali Linux from reaching the Windows VM.

**Solution:**  
I changed the Windows 10 Ethernet network profile from **Private** to **Public**.

#### 🔧 How I Fixed It for Ethernet

1. On the Windows 10 VM, opened **Settings**.
2. Went to **Network & Internet**.
3. Selected **Ethernet**.
4. Clicked the active Ethernet connection.
5. Under **Network profile**, changed the setting from **Private** to **Public**.
6. Returned to Kali Linux and tested the connection again:

```bash
ping 10.0.0.10
```

**Result:**  
After changing the Ethernet network profile to **Public**, Kali Linux was able to successfully ping the Windows 10 VM. Two-way connectivity between Kali Linux and Windows 10 was confirmed.

| Test | Command | Result |
|---|---|---|
| Windows to Kali | `ping 10.0.0.2` | Successful |
| Kali to Windows | `ping 10.0.0.10` | Successful after changing network profile to Public |
| Internet access | `ping 8.8.8.8` | Successful |

---

## 5. 📚 Lessons Learned

### 🖥️ Virtualisation and Lab Design

- I learned how to create additional target virtual machines in the same VirtualBox lab environment.
- I learned how to allocate appropriate RAM, disk space, and display settings for different operating systems.
- I learned that VM settings such as graphics controller, video memory, EFI, and boot order can directly affect whether a guest operating system boots correctly.
- I learned the importance of using an isolated NAT Network for safe cybersecurity practice.

### 🌐 Virtual Networking

- I learned how to place multiple virtual machines on the same NAT Network.
- I learned how to assign static IP addresses to Android-x86 and Windows 10.
- I learned how to verify connectivity between Kali Linux and other virtual machines.
- I learned how to test gateway access, internet access, and DNS resolution.

### 🔧 Troubleshooting

- I learned that troubleshooting should be done step by step rather than assuming that a VM or network setting is correct.
- I learned how to identify and resolve a VM boot/display issue by adjusting VirtualBox graphics and system settings.
- I learned how GRUB boot parameters such as `nomodeset` and `xforcevesa` can force basic display compatibility.
- I learned that changing one setting at a time and testing afterwards makes problems easier to isolate.
- I learned that Windows network profiles and firewall behaviour can block connectivity even when IP addressing and the VirtualBox NAT Network are configured correctly.
- I learned how to change the Windows 10 Ethernet network profile from Private to Public to allow Kali Linux to communicate with the Windows VM.

### 🕵️ Wireshark and SOC Analysis

- I improved my ability to analyse packet captures in Wireshark.
- I learned how to follow TCP streams to reconstruct network conversations.
- I learned how attackers can expose sensitive information through insecure protocols such as HTTP.
- I learned how to recognise brute-force behaviour through repeated login attempts.
- I learned how VoIP traffic can be analysed to investigate suspicious or scam calls.
- I strengthened my understanding of safe, authorised security testing.

### 🏆 Overall Skills Gained

This extra project strengthened my practical skills in:

- VirtualBox virtual machine setup.
- Android-x86 and Windows 10 installation.
- NAT Network configuration.
- Static IP addressing.
- Network troubleshooting.
- Wireshark packet analysis.
- SOC investigation workflows.
- Technical documentation.
- Safe and ethical cybersecurity practice.
