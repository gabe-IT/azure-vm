# Virtual Machine Network in Microsoft Azure

This tutorial provides a comprehensive guide to setting up a Virtual Machine Network in Microsoft Azure and performing exercises to observe network traffic.

## Environments and Technologies Used

- **Microsoft Azure** (Virtual Machines/Compute)
- **Microsoft Remote Desktop**
- **Windows Command Prompt**
- **Wireshark**
- Network Protocols including DNS, ICMP, SSH, and RDP

## Operating Systems Used

- **Windows 10 (21H2)**
- **Linux (Ubuntu 20.04)**

## List of Prerequisites

1. **Microsoft Azure Account and Subscription**
2. **Access to Microsoft Remote Desktop Connection**
   - For MacOS users, a tutorial is available [here](https://www.youtube.com/watch?v=0lllpAhgAJs&ab_channel=TheHostingVideos).
3. (OPTIONAL) Notepad for noting Virtual Machine login details

## Installation Steps

### Creating our Resource Group and Virtual Machines

1. **Resource Group Creation**
   - Navigate to *Resource groups* in Azure Services.
   - Create a Resource Group named `RG-VM`.
   - Note the *Region* for later use.
   - Click *Review + Create* to finalize.

2. **Virtual Machine 1 using Windows 10**
   - Go to *Virtual Machines* in Azure Services.
   - Select `RG-VM` for the Resource Group.
   - Name the VM `VM-1`. Ensure the Region matches that of `RG-VM`.
   - Choose *Windows 10 Pro, Version 22H2, x64 Gen2* as the Operating System.
   - Select *Standard_E2s_V3* for Size (2 vCPUs, 16 GB RAM).
   - Set username and password for VM access.
   - Notice the *Virtual Network* automatically created.
   - Proceed to *Review + Create* and deploy the VM.

3. **Virtual Machine 2 using Ubuntu**
   - Repeat the process for VM-1.
   - Name this VM `VM-2` and choose *Ubuntu Server 20.04 LTS x64 Gen2* as the OS.
   - For authentication, select Password instead of SSH public key.

### Logging into a Virtual Machine using Remote Desktop Connection

1. **Access VM-1 via Remote Desktop**
   - In Azure Services, go to *Virtual Machines* and connect to VM-1.
   - Use the provided *Public IP Address* to log in via Remote Desktop Connection.

## Observing Traffic in Virtual Machines

### Download and Install Wireshark

- **Install Wireshark** on VM-1. Note that download speeds may vary based on VM specs.

### Observing ICMP Traffic

1. **Open Wireshark** and filter for ICMP packets.
2. **Ping the Ubuntu VM (VM-2)** from VM-1 using its private IP. Observe the packet exchange in Wireshark.
3. **Ping a public website** like google.com from VM-1. Monitor the traffic in Wireshark.
4. **Start a continuous ping** to VM-2 and note the traffic in Wireshark.
5. **Alter VM-2's Network Security Group** to block ICMP traffic. Observe the "Request timed out" message in VM-1.
6. **Re-enable ICMP traffic** and watch the resumption of ping responses in Wireshark.

### Observing SSH Traffic

1. **Filter for SSH traffic** in Wireshark.
2. **SSH into VM-2** from VM-1. Execute commands and monitor the SSH traffic in Wireshark.
3. **Terminate the SSH session** when done.

### Observing DHCP Traffic

1. **Filter Wireshark for DHCP traffic**.
2. **Renew the IP address** of VM-1 using `ipconfig /renew`. Track the DHCP traffic in Wireshark.

### Observing DNS Traffic

1. **Filter for DNS traffic** in Wireshark.
2. **Use nslookup** in VM-1 for domains like google.com. Observe the DNS queries in Wireshark.

### Observing RDP Traffic

1. **Filter for RDP traffic** in Wireshark (`tcp.port == 3389`).
2. **Note the continuous RDP traffic** and understand its nature as a live stream protocol.

## Lab Cleanup

1. **Close the Remote Desktop connection**.
2. **Delete the Resource Groups** created in this lab.
3. **Ensure the deletion** of the Resource Groups for cost management.
