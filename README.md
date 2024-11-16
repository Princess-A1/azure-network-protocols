<p align="center">

  ![Screenshot  124912](https://github.com/user-attachments/assets/bb64eb49-0e3b-4212-94a6-96115b2825fd)

</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we will observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 11
- Ubuntu Server 22.04

<h2>High-Level Steps</h2>

- Create Resource Groups and Virtual Machines
- Install & Run Wireshark
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

Create your Resource Groups and Virtual Machines [Note: If you need help with this step, check out this [repository](https://github.com/Princess-A1/virtual-machine).]

![Screenshot 133214](https://github.com/user-attachments/assets/aad6e4f5-5377-4f06-9d06-d1cbf72fcd6c)



Install Wireshark in Virtual Machine 1 (VM-1)

<img 
<img 

Open Wireshark, and click the blue fin to observe ICMP traffic.

<img 
<img 

Observe ICMP Traffic 
Type ICMP in the filter bar to filter only for ICMP traffic 

<img 

Ping Virtual Machine 2 (VM-2) using its private IP address from Azure.

<img 
<img 

From Windows 11 virtual machine, open PowerShell and ping the website www.google.com and observe the traffic in Wireshark. 
<img 

Send a nonstop ping to VM-2 with the command "ping -t"
<img 

In Azure, go into the VM-2 network security group and add an inbound rule to stop ICMP traffic.
<img 
<img 

Delete the inbound rule or simply allow the inbound rule to receive ICMP traffic (control+C to stop non-stop packets)
<img 

Observe SSH Traffic 
From the Windows 11 virtual machine, connect to VM-2 virtual machine using SSH via PowerShell. 
Using Powershell type SSH <username>@<VM-2 Private IP address> and hit Enter. Type in the login password [Note: password will not show]
<img 
<img 

Observe DHCP Traffic 
Type the command "ipconfig /renew" the VM will receive a new IP address. Observe the traffic in WireShark [Note: The VM may restart to receive the IP address]

<img 

Observe DNS Traffic 
In Powershell, using the command "nslookup" type "nslookup www.google.com". Observe the IP address and DNS traffic in Wireshark.
<img 

Observe RDP Traffic 
