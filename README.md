
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

✅ Step 2: Installing Windows Server 2022 (with Desktop Experience)
1. Boot from the **Windows Server 2022 ISO** in your VM or physical machine.
2. When prompted, select:

   * **Windows Server 2022 Standard (Desktop Experience)** or
   * **Windows Server 2022 Datacenter (Desktop Experience)**

   ⚠️ Be sure to choose **Desktop Experience**, otherwise you’ll only get a command-line interface.
3. Continue through the setup wizard:

   * Accept the license terms
   * Choose **Custom installation**
   * Select your disk and install
4. After installation, set the **Administrator password**.
5. Log in for the first time using `Administrator` and the password you created.

✅ Step 3: Checking Network Adapters
1. Click the **Network icon** in the bottom-right corner of the taskbar.
2. Select **Network & Internet settings**.
3. Go to **Change adapter options**.

Now we need to properly name the adapters (important later for routing).

4. Right-click the first adapter → **Status**.
5. Click **Details**. Look for the adapter with the IP `10.0.2.15` — this shows it’s getting its IP from your home network.

Once you’ve identified the main adapter, rename it:

6. Right-click the adapter → **Rename** → set it to **INTERNET**.
7. Rename the other adapter to **Internal**.

📸 Image placement: Screenshot of Server Manager role installation wizard.
📸 Image placement: Screenshot of “Promote to Domain Controller” wizard.

✅ Step 3.2: Assigning a Static IP to the Internal Adapter

1. Open **Change adapter options** again.

2. Right-click **Internal** → **Properties**.

3. Double-click **Internet Protocol Version 4 (TCP/IPv4)**.

4. Select **Use the following IP address** and configure:

   * **IP address**: `172.16.0.1`
   * **Subnet mask**: `255.255.255.0`
   * **Default gateway**: *leave blank*
   * **Preferred DNS server**: `127.0.0.1` (loopback, since this server will run its own DNS)

5. Click **OK**.

✅ Step 4: Renaming the Server
1. Right-click the **Start menu** → **System**.
2. Select **Rename this PC**.
3. Name it **DC** (*Domain Controller*).
4. Click **Next**, then **Restart now**.
📸 Image placement: Screenshot of DNS Manager showing Forward Lookup Zone.

✅ Step 5: Creating a Domain
1. Open **Server Manager** → **Add roles and features**.
2. Click **Next** until you reach **Installation type**.
3. Choose **Role-based or feature-based installation**, then **Next**.
4. Select the target server, then **Next**.
5. Choose **Active Directory Domain Services**.

   * In the pop-up, click **Add features**, then **Next**.
6. Continue → **Next** → **Install**.

After installation:

7. In Server Manager, click the **yellow notification flag** (top-right).
8. Select **Promote this server to a domain controller**.
9. Choose **Add a new forest**.
10. Enter a **Root domain name** (e.g., `MyDomain.com`).
11. Enter a password when prompted.
12. Continue → **Install**.
13. The server will restart.

📸 Image placement: Screenshot of DHCP scope configuration

✅ Step 6: Windows 10 Client Setup
- Install Windows 10 VM.
- Configure network adapter to Internal Network.
- Set to obtain IP automatically → verify it gets DHCP lease.
- Join domain: lab.local using domain admin credentials.

📸 Image placement: Screenshot of client machine showing DHCP IP lease.
📸 Image placement: Screenshot of domain join confirmation.

✅ Step 7: Installing RAS/NAT on the Domain Controller
1. Open **Add roles and features**.
2. Continue → select your server.
3. On **Server roles**, select **Remote Access**, then **Next**.
4. Choose **Routing**, click **Add features**, then **Next**.
5. Continue → **Install**.

After installation:

6. Open **Tools → Routing and Remote Access**.
7. Right-click the server (`DC (Local)`) → **Configure and Enable Routing**.
8. Select **NAT (Network Address Translation)**.
9. Choose the **public interface** (`INTERNET`).
10. Click **Next → Finish**.

The icon should turn **green** (from red), confirming it’s active.

📸 Image placement: Screenshot of successful login with domain account.
📸 Image placement: Screenshot of ping and nslookup test results.

✅ Step 8: Setting Up DHCP on the Domain Controller
1. Open **Add roles and features**.
2. Click **Next**.
3. Select your server → **Next**.
4. Choose **DHCP Server**, then **Add features**.
5. Continue → **Install**.

After installation:

6. Open **Tools → DHCP**.

7. Right-click **IPv4** → **New Scope**.

8. Enter a **name** (e.g., `LabScope`) → **Next**.

9. Configure the IP range:

   * **Start IP**: `172.16.0.100`
   * **End IP**: `172.16.0.200`
   * **Length**: 24
   * **Subnet mask**: `255.255.255.0`

10. Continue → set **lease duration** → **Next**.

11. Add the **Default Gateway**: `172.16.0.1` → **Add → Next**.

12. Finish the wizard.

Finally, authorize DHCP:

13. Right-click the DHCP server → **Authorize**.
14. Refresh — the icon should change from **red** to **green**.

✅ Step 7:

## 📸 Project Images

- VirtualBox VM settings (network adapter setup)
- Windows Server 2022 installation (static IP, role installations)
- AD DS promotion wizard
- DNS Manager with forward lookup zone
- DHCP scope settings
- Windows 10 client domain join process
- Testing validation screenshots

## 🔑 Key Takeaways

- Successfully deployed a functional AD DS, DHC, RAS, and NAT lab environment inside VirtualBox..
- Learned to configure networking for isolated lab environments.
- Practiced core system administration tasks including creating a domain controller with AD DS, configuring DHCP and DNS, and setting up RAS and NAT for remote access and network connectivity.
- Demonstrated how a client-server architecture works in practice.

## 📎 References 

[FCC Guidelines on Cellular Boosters](https://www.fcc.gov/wireless/bureau-divisions/mobility-division/signal-boosters/consumer-signal-boosters) 

[weBoost Specs](https://github.com/josiasdelbois/Wireless-Signal-Infrastructure-Implementation/blob/main/Assets/weBoost%20Technical%20Specs.pdf)

[weBoost installation Guide](https://github.com/josiasdelbois/Wireless-Signal-Infrastructure-Implementation/blob/main/Assets/weBoost%20installation%20Guide.pdf)
