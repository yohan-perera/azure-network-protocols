<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Using resources in Azure, create environment consisting of a Windows 10 Virtual Machinee (VM), a Linux Ubuntu VM, and a Virtual Network and Subnet
- Use Remote Desktop Protocol (RDP) to connect to Windows 10 VM
- Install Wireshark on Windows 10 VM
- Set Wireshark to filter for ICMP packets and attempt to ping a public website, observing ping requests and replies
- Initiate perpetual ping to Ubuntu VM's private IP address
- Edit Azure Network Security Group for Ubuntu VM and disable incoming (inbound) ICMP traffic, observing Wireshark ICMP activity
- Re-enable ICMP traffic for Ubuntu VM and observe Wireshark ICMP activity, then terminate perpetual ping
- Set Wireshark to filter for SSH traffic and establish SSH connection to Ubuntu VM, observing Wireshark SSH traffic then exit connection
- Set Wireshark to filter for DHCP traffic and use command line to issue Windows 10 VM new IP address (ipconfig /renew), then observe Wireshark DHCP traffic
- Set Wireshark to filter for DNS traffic, then use nslookup to locate IP addresses for public websites, observing Wireeshark DNS traffic
- Set Wireshark to filter for RDP traffic and observe continuous traffic in Wireshark from live RDP connection to Windows 10 VM
- Close RDP connection and clean up Azure resources

<h2>Actions and Observations</h2>

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/23c537fe-f24f-4693-8ba0-b97996c06f14)"
<p>
Create Resource Group
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/885620c0-0420-487c-91ee-78a28d57af1c)
<p>
Create Virtual Machine 1 (Windows 10)
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/0b4fec17-f509-4ec7-ba13-015a43b4c814)
<p>
Create Virtual Network and Network Security Group (used for VM1 and VM2)
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/d59eadda-7412-40f3-bc2a-fa03b8e46465)
<p>
Network Overview found in auto-created NetworkWatcherRG Resource Group
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/1f0cfb12-7f80-49e9-9f8c-bcb1c9fa9efa)
<p>
Create Virtual Machine 2 (Linux – Ubuntu)</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/6f467afb-4044-475d-bfa6-9c66016c5cef)
<p>
Establish RDP (Remote Desktop Protocol) Connection to VM1
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/a7453233-aed0-47f3-ade9-8a4c2a4a3d9d)
<p>
Download and install Wireshark on VM1
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/804abe5a-53b3-490c-b81f-8e7016fae8c2)
<p>
Open Wireshark, filter to ICMP traffic, and ping VM2 (private IP) and public website (www.google.com)</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/6a97b4ee-ebc5-4c63-892c-f43b10b72271)
<p>
Initiate perpetual ping of VM2 in terminal
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/64139466-a2d8-4fb0-96f3-03d75e266d4f)
<p>
Access VM2 Network Security Group and add rule to block incoming ICMP traffic
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/4b7a7b14-15b8-4a9f-860f-33df065f208e)
<p>
All ICMP requests are denied, no response from ping
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/fb5f215f-a198-4368-a71e-c66d819937f7)
<p>
NSG inbound rule ammended to allow ICMP traffic</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/6502933a-e22e-4c1e-9eeb-4bdb5b6dec70)
<p>
ICMP traffic is allowed again, response from ping</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/d63eec8b-dd0f-4685-8230-5988066be20a)
<p>
Establish SSH connection to VM2 and observe packets in Wireshark</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/daffc98b-6aff-4143-aee9-75f98d064238)
<p>
Issue VM1 new IP  address and observe DHCP traffic in Wireshark
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/b1086fc7-ed6f-4a66-9345-e9ca697443fe)
<p>
Use nslookup command to obtain IP addresses and obsereve DNS traffic in Wireshark
</p>
<br />

![image](https://github.com/yohan-perera/azure-network-protocols/assets/156178441/8ffa492a-a8f0-44d7-b6a6-e3bc6939779c)
<p>
Observe RDP traffic in Wireshark (TCP port 3389). RDP traffic is constantly being transmitted due to live session connecting to VM1
</p>
<br />
