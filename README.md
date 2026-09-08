  # 🔐 Cybersecurity Lab Setup

**NetworkWalks | Week 01 | Project Module 01**

A hands-on cybersecurity lab environment built with Oracle VirtualBox and Kali Linux. The setup provides an isolated and controlled workspace for cybersecurity, ethical hacking, networking, and security testing exercises.

---

## 📌 Project Overview

This project focused on designing and configuring a cybersecurity lab using **Oracle VirtualBox** as the virtualization platform and **Kali Linux** as the primary security-testing machine.

The lab uses a dedicated NAT Network based on the `10.0.0.0/24` subnet. This allows Kali Linux to access the Internet while remaining separate from the host machine’s primary network.

The completed environment provides a foundation for future exercises involving Linux administration, network analysis, vulnerability assessment, and authorized security testing.

---

## 🎯 Objectives

The main objectives were to:

* Install and configure Oracle VirtualBox.
* Install 7-Zip for extracting the Kali Linux archive.
* Create a custom NAT Network.
* Import and configure a Kali Linux virtual machine.
* Assign the required IP address.
* Confirm Internet connectivity.
* Enable clipboard sharing and drag-and-drop.
* Configure a shared folder for file exchange.
* Create a VM snapshot after completing the setup.

---

## 🛡️ Purpose of the Lab

This virtualized lab provides a safe environment for hands-on security learning and testing. It supports experimentation without affecting the host system and can be expanded with additional target machines or vulnerable systems.

* Test configurations and troubleshoot networking issues.
* Restore the system using snapshots.
* Perform network reconnaissance and port scanning.
* Conduct vulnerability assessments and packet analysis.
* Explore web security testing and exploitation.
* Practice using security tools in a controlled environment.

---

## 🏗️ Lab Architecture

```text
                         Host Machine
                              │
                       Oracle VirtualBox
                              │
                    ┌─────────▼─────────┐
                    │     NAT Network   │
                    │    10.0.0.0/24    │
                    └─────────┬─────────┘
                              │
                    ┌─────────▼─────────┐
                    │     Kali Linux    │
                    │     10.0.0.2/24   │
                    │ Security Testing VM│
                    └───────────────────┘
```

The host machine provides the virtualization layer, while VirtualBox manages the virtual network and Kali Linux guest. The NAT Network provides external connectivity while maintaining a clear lab boundary.

---

## ⚙️ Lab Configuration

| **Component**      | **Configuration**                      |
| ------------------ | -------------------------------------- |
| Hypervisor         | Oracle VirtualBox 7.2                  |
| Security VM        | Kali Linux 2026.2                      |
| Network Type       | NAT Network                            |
| Network Subnet     | `10.0.0.0/24`                          |
| Kali Linux Address | `10.0.0.2/24`                          |
| Internet Access    | Enabled                                |
| Shared Folder      | `/downloads`                           |
| Clipboard          | Enabled                                |
| Drag-and-Drop      | Enabled                                |
| Snapshot           | Created after successful configuration |

---

## 🪜 Lab Setup Procedure

### 1. Install 7-Zip

7-Zip was installed on the host machine to extract and manage compressed files, including the Kali Linux virtual machine archive.

### 2. Install Oracle VirtualBox

Oracle VirtualBox was installed as the virtualization platform for the lab. It provides the required controls for managing virtual machines, configuring networks, enabling guest integration features, and creating snapshots.

### 3. Create the NAT Network

A custom NAT Network was created in VirtualBox using the following subnet:

```text
10.0.0.0/24
```
<img width="1902" height="1068" alt="NAT Network" src="https://github.com/user-attachments/assets/3cd53976-6b8a-4992-8fcd-67408ebd74eb" />

This network provides a dedicated communication layer and allows the Kali Linux guest to access the Internet through VirtualBox’s NAT functionality.

### 4. Import and Configure Kali Linux

<img width="1920" height="1003" alt="kali" src="https://github.com/user-attachments/assets/1b75bc80-9bde-41ee-87ac-5c910041eceb" />

The Kali Linux archive was extracted using 7-Zip and imported into VirtualBox. The VM was then connected to the newly created NAT Network.

The network adapter settings were reviewed to ensure that the guest was attached to the intended NAT Network rather than a host-only or bridged interface.

### 5. Configure the Kali Linux Network

<img width="1920" height="1003" alt="ip manual" src="https://github.com/user-attachments/assets/6638b7bc-38f5-4469-bd72-77d673456546" />

<img width="1920" height="1003" alt="commands" src="https://github.com/user-attachments/assets/de9992d4-d6bb-4eba-b42a-b39f3c333d5f" />
Kali Linux was configured with the required IPv4 address:

```text
IP Address: 10.0.0.2/24
```

This places the guest within the lab subnet and provides a predictable address for future exercises.

### 6. Enable Guest Integration Features

The following VirtualBox features were enabled:

* Shared clipboard
* File drag-and-drop
* `/downloads` shared folder

These features support controlled file transfers and improve interaction between the host and guest systems.

### 7. Create a Recovery Snapshot

After confirming the network, integration features, and Internet access, a VM snapshot was created.

This provides a recovery point that can be used to restore the completed baseline after future experiments.

---

## 💻 Commands Used

The following commands were used to inspect the network configuration, assign a static IPv4 address, and verify connectivity.

### Network Inspection

```bash
ip a
```

```bash
ip route
```

### Static Network Configuration

```bash
sudo nmcli con mod "Wired connection 1" ipv4.addresses 10.0.0.2/24
```

```bash
sudo nmcli con mod "Wired connection 1" ipv4.gateway 10.0.0.1
```

```bash
sudo nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8"
```

```bash
sudo nmcli con mod "Wired connection 1" ipv4.method manual
```

The updated connection profile was activated with:

```bash
sudo nmcli con up "Wired connection 1"
```

### Connectivity Test

```bash
ping -c 4 google.com
```

This confirmed DNS resolution and external connectivity from the Kali Linux virtual machine.

---

## 🔎 Lab Verification

| **Test**                           | **Command / Method**               | **Result**                                                               |
| ---------------------------------- | ---------------------------------- | ------------------------------------------------------------------------ |
| Verify IPv4 address                | `ip a`                             | Interface shows `10.0.0.2/24`.                                           |
| Verify routing                     | `ip route`                         | Default route shows `via 10.0.0.1`; connected route shows `10.0.0.0/24`. |
| Verify Internet and DNS            | `ping -c 4 google.com`             | Domain resolves and replies are received with no packet loss.            |
| Verify NAT Network                 | VirtualBox VM Settings → Network   | Adapter is enabled and attached to the custom NAT Network.               |
| Verify clipboard and drag-and-drop | Copy text and transfer a test file | Text and file transfer complete successfully.                            |
| Verify shared folder               | `ls -la /downloads`                | `/downloads` is accessible.                                              |
| Verify snapshot                    | VirtualBox → Snapshots             | Completed-configuration snapshot is listed and available.                |

---

## 🐞 Problems Encountered & Solutions

### 1. IP Address Conflict

Kali Linux initially received `10.0.0.3`+ with the gateway `10.0.0.1`, while the lab required `10.0.0.2/24`.

Assigning `10.0.0.2` manually caused an IP conflict with the existing NAT Network configuration.

**Solution:**
The connection was configured with the required network parameters:

```text
IP Address : 10.0.0.2/24
Gateway    : 10.0.0.1
DNS        : 8.8.8.8
```

The settings were applied using:

```bash
sudo nmcli con mod "Wired connection 1" ipv4.addresses 10.0.0.2/24
sudo nmcli con mod "Wired connection 1" ipv4.gateway 10.0.0.1
sudo nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8"
sudo nmcli con mod "Wired connection 1" ipv4.method manual
sudo nmcli con up "Wired connection 1"
```

---

### 2. Network Disconnect / Reconnect Loop

After the static address was assigned, the interface repeatedly connected and disconnected.

The cause was **DHCP remaining enabled on the VirtualBox NAT Network while Kali Linux used a static IP**. These settings conflicted with each other.

**Solution:**
DHCP was disabled in the VirtualBox NAT Network settings. The connection was then activated again:

```bash
sudo nmcli con up "Wired connection 1"
```

The result was checked with:

```bash
ip a
ip route
```

Connectivity was verified with:

```bash
ping -c 4 google.com
```

---

## 💡 What I Learned

Through this project, I learned how to create and configure a virtual environment for cybersecurity practice. The most important lessons were:

* A NAT Network allows multiple virtual machines to communicate while providing external connectivity.
* VirtualBox network adapter settings determine how virtual machines communicate.
* Static IP configuration requires correctly setting the address, subnet, gateway, and DNS.
* Snapshots provide a reliable recovery point before testing or making risky changes.
* Clear documentation of commands, problems, solutions, and verification steps is essential in cybersecurity projects.

Overall, I learned that a reliable virtual lab requires proper network design, configuration, testing, recovery planning, and documentation.

---

## 🔐 Security & Ethical Use

This laboratory is intended strictly for **educational and authorized cybersecurity practice**.

Any scanning, exploitation, password testing, vulnerability assessment, or other security activity must only be performed against:

* Systems personally owned by me.
* Intentionally vulnerable machines created for practice.
* Authorized CTF or training environments.
* Systems covered by clear written permission.

The tools must never be used against public or third-party systems without authorization.

---

## 🧰 Tools & Resources

* [Oracle VirtualBox](https://www.virtualbox.org/)
* [Kali Linux](https://www.kali.org/)
* [7-Zip](https://7-zip.org/)
* NetworkWalks — Week 01, Project Module 01
---

## 👤 Author

**Debashree Sinha**

LinkedIn : www.linkedin.com/in/debashrees
---

### 📌 Project Information

**Program:** NetworkWalks Cybersecurity Internship
**Week:** 01
**Project:** Cybersecurity Lab Setup
**Focus:** Virtualization, Networking & Kali Linux
