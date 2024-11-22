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
![Screenshot 135925](https://github.com/user-attachments/assets/007d6224-93b7-4098-bfa2-26433e53b7da)

Install Wireshark in Virtual Machine 1 (VM-1)
![Screenshot 140113](https://github.com/user-attachments/assets/936175c9-476a-46f4-a08e-edb5ce88a559)
![Screenshot 140441](https://github.com/user-attachments/assets/b6d83dc1-3238-4856-b9b2-e7c364a724b5)

Open Wireshark, and click the blue fin to observe ICMP traffic.
![Screenshot 155429](https://github.com/user-attachments/assets/50a56728-a9c0-4bf5-bc5d-e10782e383c3)
![Screenshot 155539](https://github.com/user-attachments/assets/d334a70a-1495-457e-869d-3777a3984d91)

Observe ICMP Traffic 
Type ICMP in the filter bar to filter only for ICMP traffic 
![Screenshot 155629](https://github.com/user-attachments/assets/4f160c2a-a827-4061-a0d8-7dde211d5e65)

Ping Virtual Machine 2 (VM-2) using its private IP address from Azure.
![Screenshot 155721](https://github.com/user-attachments/assets/590dd7e6-2739-4609-b2fa-ad5decb01c63)
![Screenshot 155809](https://github.com/user-attachments/assets/4ccb11c1-1947-4bce-bd3f-e80ee01be7e0)



From Windows 11 virtual machine, open PowerShell and ping the website www.google.com and observe the traffic in Wireshark. 
![Screenshot 160739](https://github.com/user-attachments/assets/39fc3628-068f-4fd0-ae3f-a89cba130fc2)

Send a non-stop ping to VM-2 with the command "ping -t"
![Screenshot 075623](https://github.com/user-attachments/assets/1ef8ef1b-ef71-4158-a643-5fb49b6624a6)


In Azure, go into the VM-2 network security group and add an inbound rule to stop ICMP traffic.
![Screenshot 081521](https://github.com/user-attachments/assets/8302e313-dfba-4f5b-be0e-dc2904b1adba)
![Screenshot 081630](https://github.com/user-attachments/assets/6f901bc4-9d84-4c81-b985-3e391e1bbeb9)


Delete the inbound rule or simply allow the inbound rule to receive ICMP traffic (control+C to stop non-stop packets)
![Screenshot 081723](https://github.com/user-attachments/assets/0711104a-ec5c-4915-bb80-5843d9f9d2f1)

Observe SSH Traffic 
From the Windows 11 virtual machine, connect to VM-2 virtual machine using SSH via PowerShell. 
Using Powershell type SSH <username>@<VM-2 Private IP address> and hit Enter. Type in the login password [Note: password will not show]
![Screenshot 081815](https://github.com/user-attachments/assets/7d503855-40e9-450d-a933-b792afdedf6a)
![Screenshot 081849](https://github.com/user-attachments/assets/1fa40bdc-f353-4b46-8167-6846241ef213)

Observe DHCP Traffic 
Type the command "ipconfig /renew" the VM will receive a new IP address. Observe the traffic in WireShark [Note: The VM may restart to receive the IP address]
![Screenshot 2024-11-17 081938](https://github.com/user-attachments/assets/a9b85690-a3e9-4b55-93b6-5ed8bdd91923)

Observe DNS Traffic 
In Powershell, using the command "nslookup" type "nslookup www.google.com". Observe the IP address and DNS traffic in Wireshark.
![Screenshot 082030](https://github.com/user-attachments/assets/79d3fe19-ad44-442a-a030-3d1bc953fd86)

Observe RDP Traffic 
![Screenshot 082113](https://github.com/user-attachments/assets/e4e05239-455f-43b9-9dce-7ed35211905c)
