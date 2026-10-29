# NETWORKWALKS-B804-WK1-PM1-CYBERSECURITY-LAB-SETUP
Set up a cybersecurity testing lab environment on your Laptop/PC   
---  

## 📌 Project Overview

This project focuses on setting up a **virtual cybersecurity and penetration-testing laboratory** using Virtual machine (UTM), Kali Linux, and **OPNsense** as a virtual firewall/router.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

Rather than relying on Virtualmachine's built-in NAT Network, this lab uses **OPNsense** to route and firewall an isolated **Internal Network**, more closely mirroring how a real enterprise network segments and controls traffic between machines.    
--

## 🎯 Objectives

The main objectives of this project are to:

- Install and configure UTM.
- Install/import Kali Linux as a virtual machine.
- Create a private **NAT Network** for the cybersecurity lab.
- Configure network connectivity for Kali Linux.
- Assign a consistent IP address to the Kali VM.
- Verify network connectivity and DNS resolution.
- Take a clean VM snapshot for recovery.
- Document the complete setup process.
- Prepare the environment for future cybersecurity projects.


  ----
  
  ## 🛡️ Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

----    
## 🏗️ Lab Architecture      
<div align="center">  
<img width="1440" height="900" alt="Screenshot 2026-10-29 at 4 45 03 pm" src="https://github.com/user-attachments/assets/4c8ca530-7131-4f41-a8eb-ebf90f516b27" />  
additional target machine can be added to the same virtual network in future attacks .  
</div>    

---  

## ⚙️ Lab Configuration

| 🧩 Component       | ⚙️ Configuration   |
| ------------------ | ------------------  |
| 🖥️ Host OS         | Mac OS         |
| 🧠 Host RAM        | 8 GB               |
| ⚡ Processor       | M1 silicon      |
| 🧰 Hypervisor      | VirtualBox 7.2  |
| 🐉 Security OS     | Kali Linux 2026.2  |
| 🧠 Kali RAM        | 2048 MB            |
| 🌐 Virtual Network | NAT Network        |
| 📡 Network Address | 10.0.0.0/24        |
| 🐧 Kali IP Address | 10.0.0.11/24        |
| 🚪 Default Gateway | 10.0.0.10           |
| 🌍 DNS Server      | 8.8.8.8            |
| 🔮 Future VM Range | 10.0.0.10–10.0.0.100 |    

----    
## Lab Walkthrough      

# Step 1  

Download and install kali Linus from safari    

# Step 2    

UTM was installed as the hypervisor     

---      

## Step 3. Create the NAT Network

A dedicated NAT Network was created in VirtualBox.

Configuration:
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled    

<div align="center">  
<img width="1440" height="900" alt="Screenshot 2026-10-27 at 8 06 06 pm" src="https://github.com/user-attachments/assets/aa445c16-96d7-48a0-9700-4529c8420dbd" />    
NAT configuration   
</div>  

----

A **NAT Network** was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.    

<img width="1440" height="900" alt="Screenshot 2026-10-29 at 4 21 35 pm" src="https://github.com/user-attachments/assets/64580521-7ef5-437a-bf20-a93d41370a3e" />        
A shared folder was also configured for transferring required files between the host operating system and the Kali VM.    

----

## Step 5. Configure the Kali Linux Network

The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

```text
IP Address: 10.0.0.11
Subnet Mask: 255.255.255.0
Gateway: 10.0.0.10
DNS: 8.8.8.8
```

A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.    
<img width="1440" height="900" alt="Screenshot 2026-10-27 at 8 10 24 pm" src="https://github.com/user-attachments/assets/2c1291fb-181a-4492-ba12-fd83edfa05f9" />    

   
<img width="1440" height="900" alt="Screenshot 2026-10-29 at 5 17 34 pm" src="https://github.com/user-attachments/assets/bbe78a5f-f03e-42ac-a122-203726ee09a9" />      

----    

# 🔎 Lab Verification

| ✅ Test                        | 🧾 Command                      | 🎯 Expected Result              |
| ----------------------------- | ------------------------------- | ------------------------------- |
| 🌐 Check IP address           | `ip 10.0.0.11`                          | Correct Kali IP displayed       |
| 📡 Test gateway               | `ping 10.0.0.10`                 | Successful replies              |
| 🌍 Test Internet connectivity | `ping 8.8.8.8`                  | Successful replies              |
| 🔎 Test DNS resolution        | `nslookup networkwalks.com`     | Domain resolves                 |  



### Example Results

```text
IP Address:
10.0.0.11/24

Gateway:
10.0.0.1

DNS:
8.8.8.8
```

---      

# 🐞 Problems Encountered & Solutions

Documenting problems is an important part of the project.

## Problem 1. Internet Connectivity After Static IP Configuration

After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali/NetworkManager configuration.

One workaround used during this lab was:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

The network connection was then restarted/rebooted and connectivity was tested again.

> **Important:** Network interface and connection names may differ between systems. Students should first identify their actual connection name before running an `nmcli` command.

---

# 💡 What I Learned

Through this project, I learned how to create and configure a virtual environment for cybersecurity practice.

The most important concepts I learned include:

### 1. NAT vs NAT Network

A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.

This makes it useful for building a multi-machine cybersecurity laboratory.    


-------      

### 2. Virtual Machine Networking

I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configuration affects communication between machines.

### 3. Static IP Configuration

I learned how to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings in Kali Linux.

### 4. VM Snapshots

I learned that a clean snapshot should be created **before performing risky or experimental activities**.

This provides a known-good recovery point for future cybersecurity exercises.

### 5. Documentation

I learned that documenting commands, configuration, screenshots, problems, and solutions is an important part of a professional cybersecurity project.

---

# 🔐 Security & Ethical Use

This laboratory is intended strictly for education purposes only.

---

# 🔗 Tools    

- **UTM:**
- **Kali Linux:**

---

# 👤 Author

**Alatishe idris**\
Cybersecurity Intend B084    

-----

## 📌 Project Information

**Program Name:** Cybersecurity at Networkwalks | **Week:** 01 | **Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub.


