<p align="center">

  ![Screenshot  124912](https://github.com/user-attachments/assets/bb64eb49-0e3b-4212-94a6-96115b2825fd)

</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we will observe various network traffic to and from Azure Virtual Machines with Wireshark. We will also experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro
- Ubuntu Server 22.04

<h2>High-Level Steps</h2>

- Create Resource Group and Virtual Machines
- Install & Run Wireshark
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

Create your Resource Groups and Virtual Machines [Note: If you need help with this step, check out this [repository](https://github.com/Princess-A1/virtual-machine).]
- In the following steps, I’ll be using virtual machines named Client-1 and Client-2
- Client-1: Windows 10 Pro
- Client-2: Ubuntu 22.04

![Screenshot 140757](https://github.com/user-attachments/assets/e0a0f451-e48d-4592-9c61-9bb5f2192aa4)


Install Wireshark on your virtual machine
- Log in to Client-1
- Open web browser, and download Wireshark
- Once downloaded, open the file and follow the installation prompt
![Screenshot 140113](https://github.com/user-attachments/assets/628842f9-f891-4663-9fad-2f110a142644)
![Screenshot 140441](https://github.com/user-attachments/assets/562d787e-b553-49f5-9dc7-a30f414504ef)


Open Wireshark, and click the blue fin to start observing the packet captures.
![Screenshot 142831](https://github.com/user-attachments/assets/c6251901-f87d-4ec2-80a3-aff22b78f0a4)
![Screenshot 143000](https://github.com/user-attachments/assets/8be0e8f2-f08d-48da-98f6-2c961a92c9a3)


<h3>Observe ICMP Traffic</h3>

**ICMP**, or Internet Control Message Protocol, is used to diagnose network communication issues. One common tool that uses this protocol is the “ping” command.
- In the filter bar, you can type “icmp” to filter only for ICMP traffic 

![Screenshot 155629](https://github.com/user-attachments/assets/4f160c2a-a827-4061-a0d8-7dde211d5e65)

- Open PowerShell
- Ping Client-2 using its private IP address
  - "ping 10.0.0.6"
- View the ICMP packet request and replies in Wireshark
![Screenshot 143703](https://github.com/user-attachments/assets/f877f2ab-c6e3-45be-a369-74db75f30832)
![Screenshot 143931](https://github.com/user-attachments/assets/b2f432f0-32fc-4d11-a49b-ec5473edf802)



- Send a non-stop ping to Client-2 use the "-t" option.
  - "ping -t 10.0.0.6"
 ![Screenshot 144242](https://github.com/user-attachments/assets/eb6d126f-7e11-4592-98c5-59a13edce6a3)



- In the Azure portal, go into the Client-2’s network security group and add an inbound rule to stop ICMP traffic.
![Screenshot 144341](https://github.com/user-attachments/assets/ab3c8052-cff5-44c9-a955-b44d01374527)
![Screenshot 144416](https://github.com/user-attachments/assets/a731ac3e-4df4-43fd-a91d-277819185160)
![Screenshot 144557](https://github.com/user-attachments/assets/65c9f9b4-e558-45d6-abfc-572333f44f5a)
![Screenshot  144648](https://github.com/user-attachments/assets/430f38a6-7249-4a97-963d-fa7fd88913b6)


- Delete the inbound rule or simply allow the inbound rule to receive ICMP traffic
  - Use [control+C] to end the non-stop packets 
![Screenshot  144752](https://github.com/user-attachments/assets/f8419d19-1045-4f13-b659-ce17dcdf4606)



<h3>Observe SSH Traffic</h3>

**SSH**, or SecureShell, is a protocol that allows users to securely access and manage remote computers over an unsecure network.
- From Client-1, connect to Client-2  using SSH via PowerShell. 
- Using PowerShell, type “ssh <username>@<IP-address>” and hit Enter. 
  - Ex. “ssh labuser@10.0.0.5”
- Type in the login password [Note: password will not show] 
- View the packet captures in Wireshark by filtering for “ssh”

![Screenshot 161657](https://github.com/user-attachments/assets/efbf4b40-f87b-4378-98b8-f394eea05535)


<h3>Observe DHCP Traffic</h3>

**DHCP**, or Dynamic Host Configuration Protocol, is a protocol that automatically assigns IP addresses and other network configurations to a device.
- On Client-1, type the command "ipconfig /renew" in PowerShell.
  - The VM will receive a new IP address. 
- Observe the DHCP traffic in WireShark by filtering for "dhcp" [Note: The VM may restart to receive the IP address]

![Screenshot 162116](https://github.com/user-attachments/assets/03ccc0c6-e57f-4d29-8f2e-cfd8c17d4955)


<h3>Observe DNS Traffic</h3>

**DNS**, or Domain Name System, is a protocol used to translate domain names to IP addresses.
- In Powershell, use the "nslookup" command to observe the DNS traffic in Wireshark. 
- Type “nslookup www.google.com”
- Filter for "dns" within Wireshark
  
![Screenshot 162312](https://github.com/user-attachments/assets/df6127db-6947-4a1b-bdbf-e9a246767a37)


<h3>Observe RDP Traffic</h3>

**RDP**, or Remote Desktop Protocol, is a secure network communication protocol that is used to remotely access and control other computers.
- To view RDP traffic, type “rdp” in the filter bar.
  - We used RDP to connect to our VM’s in Azure using their Public IP address.
 
![Screenshot 162522](https://github.com/user-attachments/assets/b4d25733-412a-4c7d-ab3a-0e650e825068)

