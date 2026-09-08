                    # 🔐 Cybersecurity Lab Setup

A hands-on cybersecurity lab environment built using Oracle VirtualBox and Kali Linux designed to provide an isolated and controlled setup for future cybersecurity, ethical hacking, networking, and security testing exercises.

---

## 📌 Project Overview

This project focused on designing and configuring a functional cybersecurity lab using **Oracle VirtualBox** as the virtualization platform and **Kali Linux** as the primary security-testing machine.

The lab is connected through a dedicated NAT Network based on the `10.0.0.0/24` subnet. This provides Kali Linux with a controlled environment that supports Internet access while remaining separate from the host machine’s primary network configuration.

The completed setup serves as the foundation for future practicals involving Linux administration, network analysis, vulnerability assessment, and authorized security testing.

---

## 🎯 Objectives

The main objectives of this project were to:

* Install and configure Oracle VirtualBox.
* Create a custom NAT Network.
* Import and configure a Kali Linux virtual machine.
* Assign an IP address to Kali VM
* Confirm Internet connectivity from the VM.
* Enable clipboard sharing and drag-and-drop functionality.
* Configure a shared folder for file exchange
* Create a VM snapshot to preserve the completed working state.

---

## 🛡️ Purpose of the Lab

This virtualized cybersecurity lab provides a safe, isolated environment for hands‑on security learning and testing. It allows experimentation without affecting the host system and can be expanded with additional target machines or vulnerable setups.

* Test configurations and troubleshoot networking issues
* Restore systems to a known‑good state using snapshots
* Perform network reconnaissance and port scanning
* Conduct vulnerability assessments and packet analysis
* Explore web security testing and exploitation practice
* Experiment with security tools in a controlled setup
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

The host machine provides the virtualization layer, while VirtualBox manages the isolated network and Kali Linux guest system. The NAT Network allows the guest to communicate externally while maintaining a clear and manageable lab boundary.

---

## ⚙️ Lab Configuration

| Component          | Configuration                          |
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

### 1. Install Oracle VirtualBox

Oracle VirtualBox was installed and prepared as the virtualization platform for the cybersecurity laboratory.

The platform was selected because it provides the required controls for managing virtual machines, configuring virtual networking, enabling guest integration features, and creating snapshots.

### 2. Create the NAT Network

A custom NAT Network was created in VirtualBox using the following subnet:

```text
10.0.0.0/24
```

This network provides a dedicated communication layer for the virtual machines used in the lab. The configuration also allows the Kali Linux guest to access the Internet through VirtualBox’s NAT functionality.

### 3. Import and Configure Kali Linux

The Kali Linux virtual machine was imported into VirtualBox and connected to the newly created NAT Network.

The VM settings were reviewed to confirm that the correct network adapter was enabled and that the guest was attached to the intended virtual network rather than the host-only or bridged interface.

### 4. Configure the Kali Linux Network

Kali Linux was configured with the required IPv4 address:

```text
IP Address: 10.0.0.2/24
```

This address places the guest within the configured lab subnet and provides a predictable identity for future exercises.

### 5. Enable Guest Integration Features

The following VirtualBox integration features were enabled:

* Shared clipboard
* File drag-and-drop
* `/downloads` shared folder

These features improve the usability of the lab by allowing controlled movement of notes, tools, and downloaded resources between the host system and the virtual machine.

### 6. Create a Recovery Snapshot

Once the network, integration features, and Internet access had been confirmed, a VM snapshot was created.

The snapshot provides a recovery point that can be used to restore the laboratory to its completed baseline if a future experiment causes an unwanted configuration change.

---

## 💻 Commands Used

The following NetworkManager commands were used while troubleshooting the Kali Linux network connection:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0

sudo nmcli connection down "Wired connection 1"

sudo nmcli connection up "Wired connection 1"
```

The connection was brought down and back up after modifying the connection profile so that the updated settings could take effect.

### Network Inspection

The following commands were used to inspect the local interface and routing configuration:

```bash
ip addr
```

```bash
ip route
```

### Connectivity Test

External connectivity was tested with:

```bash
ping -c 4 8.8.8.8
```

This test helped confirm that the virtual machine could reach an external network address after the connection was restarted.

---

## 🔎 Lab Verification

The completed environment was verified through the following checks:

* Confirmed that Kali Linux received the expected IPv4 configuration.
* Reviewed the active routing information.
* Tested external network connectivity.
* Checked that the VM was attached to the correct NAT Network.
* Confirmed clipboard and drag-and-drop functionality.
* Verified the availability of the `/downloads` shared folder.
* Confirmed that a recovery snapshot had been created.

These checks established that the lab was ready for future practical work.

---

## 🐞 Problems Encountered & Solutions

### Internet Connectivity Issue

During the setup process, Kali Linux experienced an Internet connectivity issue.

The problem was investigated by reviewing both the VirtualBox NAT Network configuration and the active Kali Linux connection profile. After confirming that the virtual machine was attached to the intended network, the NetworkManager connection was modified and restarted:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

The connection was then tested again using the network inspection and connectivity commands listed above. Internet access was successfully restored and verified.

This troubleshooting step reinforced the importance of checking both sides of a virtual network: the hypervisor configuration and the guest operating system’s network profile.

---

## 💡 What I Learned

This project provided practical experience with:

* Building a cybersecurity lab using virtualization.
* Configuring a custom NAT Network in VirtualBox.
* Applying IPv4 addressing within a defined subnet.
* Connecting a Kali Linux guest to a virtual network.
* Using `nmcli` to modify and restart NetworkManager connections.
* Inspecting interfaces and routes with standard Linux commands.
* Verifying external connectivity from a guest operating system.
* Using shared folders and guest integration features responsibly.
* Creating snapshots as recovery points before future experimentation.
* Maintaining a controlled environment for ethical cybersecurity practice.

The most valuable lesson was that a working virtual lab depends on more than simply importing a virtual machine. Network design, guest configuration, verification, and recovery planning are all important parts of a reliable cybersecurity workspace.

---

## 🔐 Security & Ethical Use

This laboratory is intended strictly for **educational and authorized cybersecurity practice**.

Any scanning, exploitation, password testing, vulnerability assessment, or other security activity must only be performed against:

* Systems personally owned by me.
* Intentionally vulnerable machines created for practice.
* Authorized CTF or training environments.
* Systems covered by clear written permission.

The lab should be treated as a controlled learning environment, and its tools must never be used against public or third-party systems without authorization.

---

## 🧰 Tools & Resources

* [Oracle VirtualBox](https://www.virtualbox.org/)
* [Kali Linux](https://www.kali.org/)
* [7-Zip](https://7-zip.org/)

---

## 👤 Author

**Debashree Sinha**

BCA Graduate | Aspiring Cybersecurity Analyst
