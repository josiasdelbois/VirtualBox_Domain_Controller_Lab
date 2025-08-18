
# VirtualBox Domain Controller Lab Setup

![Antenna Project cover photo](https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/Blank%20diagram.jpeg)

## 📘 Introduction
This project documents the setup of a VirtualBox home lab consisting of Windows Server 2022 and a Windows 11 client machine. The server hosts key network services including Active Directory (AD), Domain Name System (DNS), and Dynamic Host Configuration Protocol (DHCP). The client machine is domain-joined to simulate a small business IT environment.

This lab environment is designed to help practice system administration, domain management, and client/server networking in a safe, isolated environment..

## 🎯 Objectives 

- Deploy Windows Server 2022 as a Domain Controller with AD, DNS, and DHCP
- Configure a Windows 11 client machine to join the domain
- Practice managing user accounts, DNS resolution, and automated IP address assignment 
- Simulate a small-scale enterprise IT infrastructure in VirtualBox

## 🚀 Skills Learned

- Virtualization & Networking (VirtualBox networking modes, internal networks)
- Active Directory Setup (domain creation, OU structure, user management)
- DNS Configuration (zone creation, name resolution for clients)
- DHCP Setup (IP scope creation, lease management)
- Client Domain Join (Windows 11 integration with domain services)
- IT Documentation (step-by-step technical writing, screenshots, testing validation)

## 🔧 Tools Used

- VirtualBox (virtualization platform) 
- Windows Server 2022
- Windows 11 
- Networking: VirtualBox Internal Network & NAT Adapter
- Documentation: Markdown, screenshots, diagrams <img src="https://github.com/josiasdelbois/Wireless-Signal-Infrastructure-Implementation/blob/main/Assets/Lucidchart_logo_(September_2021).svg.png" width="124" style="vertical-align:middle;">

## 🧪 Project Walkthrough

✅ Step 1: VirtualBox Setup

- Download ISOs for Windows Server 2022 and Windows 11.
- Create two VMs in VirtualBox: one for the server, one for the client.
- Configure networking:
    - Server → 2 NICs (NAT for internet access + Internal Network for LAN).
    - Client → 1 NIC (Internal Network).

📸 Image placement: Screenshot of VirtualBox network adapter settings for both VMs.

✅ Step 2: Windows Server 2022 Installation
- Install Windows Server 2022.
- Assign static IP (e.g., 192.168.10.10).
- Rename the server (e.g., LAB-DC01).
📸 Image placement: Screenshot of static IP configuration in Server Manager.

✅ Step 3: Active Directory Domain Services (AD DS)
- Install AD DS role via Server Manager.
- Promote the server to a Domain Controller.
- Create new forest/domain (e.g., lab.local).

📸 Image placement: Screenshot of Server Manager role installation wizard.
📸 Image placement: Screenshot of “Promote to Domain Controller” wizard.

✅ Step 4: DNS Setup
- DNS is automatically installed with AD DS.
- Verify Forward Lookup Zone for lab.local is created.
- Test DNS resolution with nslookup.
📸 Image placement: Screenshot of DNS Manager showing Forward Lookup Zone.

✅ Step 5: DHCP Setup
- Install DHCP role via Server Manager.
- Create new scope:

    - Range: 192.168.10.100 – 192.168.10.200
    - Subnet Mask: 255.255.255.0
    - Gateway: 192.168.10.1
    - Authorize DHCP server in AD.

📸 Image placement: Screenshot of DHCP scope configuration.

✅ Step 6: Windows 11 Client Setup
- Install Windows 11 VM.
- Configure network adapter to Internal Network.
- Set to obtain IP automatically → verify it gets DHCP lease.
- Join domain: lab.local using domain admin credentials.

📸 Image placement: Screenshot of client machine showing DHCP IP lease.
📸 Image placement: Screenshot of domain join confirmation.

✅ Step 7: Testing
- Log in to Windows 11 using a domain account.
- Ping server by hostname and FQDN.
- Verify DNS name resolution works.
- Confirm client receives DHCP IP dynamically.

📸 Image placement: Screenshot of successful login with domain account.
📸 Image placement: Screenshot of ping and nslookup test results.

## 📸 Project Images

- VirtualBox VM settings (network adapter setup)
- Windows Server 2022 installation (static IP, role installations)
- AD DS promotion wizard
- DNS Manager with forward lookup zone
- DHCP scope settings
- Windows 11 client domain join process
- Testing validation screenshots

## 🔑 Key Takeaways

- Successfully deployed a functional AD/DNS/DHCP lab inside VirtualBox.
- Learned to configure networking for isolated lab environments.
- Practiced core system administration tasks like creating a domain, setting up DHCP, and managing DNS.
- Demonstrated how a client-server architecture works in practice.

## 📎 References 

[FCC Guidelines on Cellular Boosters](https://www.fcc.gov/wireless/bureau-divisions/mobility-division/signal-boosters/consumer-signal-boosters) 

[weBoost Specs](https://github.com/josiasdelbois/Wireless-Signal-Infrastructure-Implementation/blob/main/Assets/weBoost%20Technical%20Specs.pdf)

[weBoost installation Guide](https://github.com/josiasdelbois/Wireless-Signal-Infrastructure-Implementation/blob/main/Assets/weBoost%20installation%20Guide.pdf)
