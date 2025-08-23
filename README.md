
# VirtualBox Domain Controller Lab Setup

![Antenna Project cover photo](https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/VirtualBox%20Domain%20Controller%20Lab%20Diagram.png)

## 📘 Introduction
This project documents the setup of a VirtualBox home lab consisting of Windows Server 2022 and a Windows 10 client machine. The server hosts key network services including Active Directory (AD), Remote Access Service / Remote Access Service (RAS / NAS), Domain Name System (DNS), and Dynamic Host Configuration Protocol (DHCP). The client machine is domain-joined to simulate a small business IT environment.

This lab environment is designed to help practice system administration, domain management, and client/server networking in a safe, isolated environment..

## 🎯 Objectives 

- Deploy Windows Server 2022 as a Domain Controller with AD, DNS, and DHCP
- Configure a Windows 10 client machine to join the domain
- Practice managing user accounts, DNS resolution, and automated IP address assignment 
- Simulate a small-scale enterprise IT infrastructure in VirtualBox

## 🚀 Skills Learned

- Virtualization & Networking (VirtualBox networking modes, internal networks)
- Active Directory Setup (domain creation, OU structure, user management)
- DNS Configuration (zone creation, name resolution for clients)
- DHCP Setup (IP scope creation, lease management)
- Client Domain Join (Windows 10 integration with domain services)
- IT Documentation (step-by-step technical writing, screenshots, testing validation)

## 🔧 Tools Used

- <img src="https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/VirtualBox%20Logo.png" width="124" style="vertical-align:middle;">
- <img src="https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/Windows%20Server%202022%20Logo.png" width="195" style="vertical-align:middle;">
- <img src="https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/Windows%2010%20Logo.png" width="114" style="vertical-align:middle;">
- <img src="https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/Lucidchart_logo_(September_2021).svg.png" width="124" style="vertical-align:middle;">

## 🧪 Project Walkthrough

✅ Step 1: VirtualBox Setup

- Download ISOs for Windows Server 2022 and Windows 10.
- Create two VMs in VirtualBox: one for the server, one for the client.
- Configure networking:
    - Server → 2 NICs (NAT for internet access + Internal Network for LAN).
    - Client → 1 NIC (Internal Network)(We will do this later).

![VM creation](https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/Screenshots/1%20VM%20Creation%201.png)
![CD Settings](https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/Screenshots/2%20Click%20to%20highlight%20the%20DC%20VM.png)
![VM creation](https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/Screenshots/3%20Memory%20and%20Processor%20Allocation.png)
![VM creation](https://github.com/josiasdelbois/VirtualBox_Domain_Controller_Lab/blob/main/Asset/Screenshots/4%20Network%20Adapters%20Configuration.png)

✅ Step 2: Windows Server 2022 Installation
- Install Windows Server 2022.
- Assign static IP (e.g., 192.168.10.10).
- Rename the server (DC).
📸 Image placement: Screenshot of static IP configuration in Server Manager.

✅ Step 3: Active Directory Domain Services (AD DS)
- Install AD DS role via Server Manager.
- Promote the server to a Domain Controller.
- Create new forest/domain (mydomain.com).

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

✅ Step 6: Windows 10 Client Setup
- Install Windows 10 VM.
- Configure network adapter to Internal Network.
- Set to obtain IP automatically → verify it gets DHCP lease.
- Join domain: lab.local using domain admin credentials.

📸 Image placement: Screenshot of client machine showing DHCP IP lease.
📸 Image placement: Screenshot of domain join confirmation.

✅ Step 7: Testing
- Log in to Windows 10 using a domain account.
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
- Windows 10 client domain join process
- Testing validation screenshots

## 🔑 Key Takeaways

- Successfully deployed a functional AD DS, DNS, DHCP, RAS, and NAT lab environment inside VirtualBox..
- Learned to configure networking for isolated lab environments.
- Practiced core system administration tasks including creating a domain controller with AD DS, configuring DHCP and DNS, and setting up RAS and NAT for remote access and network connectivity.
- Demonstrated how a client-server architecture works in practice.

## 📎 References 

[FCC Guidelines on Cellular Boosters](https://www.fcc.gov/wireless/bureau-divisions/mobility-division/signal-boosters/consumer-signal-boosters) 

[weBoost Specs](https://github.com/josiasdelbois/Wireless-Signal-Infrastructure-Implementation/blob/main/Assets/weBoost%20Technical%20Specs.pdf)

[weBoost installation Guide](https://github.com/josiasdelbois/Wireless-Signal-Infrastructure-Implementation/blob/main/Assets/weBoost%20installation%20Guide.pdf)
