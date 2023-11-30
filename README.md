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
![tAFcGdO](https://github.com/gabe-IT/azure-vm/assets/148400020/b3a15de4-a90f-44eb-ac61-1c25f75ee499)

2. **Virtual Machine 1 using Windows 10**
   - Go to *Virtual Machines* in Azure Services.
   - Select `RG-VM` for the Resource Group.
   - Name the VM `VM-1`. Ensure the Region matches that of `RG-VM`.
   - Choose *Windows 10 Pro, Version 22H2, x64 Gen2* as the Operating System.
   - Select *Standard_E2s_V3* for Size (2 vCPUs, 16 GB RAM).
     ![1g6BE7q](https://github.com/gabe-IT/azure-vm/assets/148400020/4f6ed5a1-42ee-4ad2-9fe1-be56154855a2)

   - Set username and password for VM access.
     ![hDnUuTG](https://github.com/gabe-IT/azure-vm/assets/148400020/940e434d-bb0d-40bd-9650-d3d5f4fba78a)

   - Notice the *Virtual Network* automatically created.
     ![8jSSyTT](https://github.com/gabe-IT/azure-vm/assets/148400020/3c48d908-8f06-466b-a540-2636353a94ac)

   - Proceed to *Review + Create* and deploy the VM.

3. **Virtual Machine 2 using Ubuntu**
   - Repeat the process for VM-1.
   - Name this VM `VM-2` and choose *Ubuntu Server 20.04 LTS x64 Gen2* as the OS.
   - For authentication, select Password instead of SSH public key.
     ![JbinPaA](https://github.com/gabe-IT/azure-vm/assets/148400020/e6a9809b-80c5-4ff6-b411-c67253864bc4)


### Logging into a Virtual Machine using Remote Desktop Connection

1. **Access VM-1 via Remote Desktop**
   - In Azure Services, go to *Virtual Machines* and connect to VM-1.
     ![0PPYsXC](https://github.com/gabe-IT/azure-vm/assets/148400020/da24175c-2b93-42c1-8d43-d538016a65b0)
   - Use the provided *Public IP Address* to log in via Remote Desktop Connection.
     ![BClhAJR](https://github.com/gabe-IT/azure-vm/assets/148400020/08710299-285b-4cee-b03a-e5a9a063a4f1)
   - You have now logged into your VM.
     ![R8Ma1Ea](https://github.com/gabe-IT/azure-vm/assets/148400020/120e3e52-8b45-49c8-9415-9a87dbfd63eb)




## Observing Traffic in Virtual Machines

### Download and Install Wireshark

- **Install Wireshark** on VM-1. Note that download speeds may vary based on VM specs.

### Observing ICMP Traffic

1. **Open Wireshark** and filter for ICMP packets
2. **Ping the Ubuntu VM (VM-2)** from VM-1 using its private IP. Observe the packet exchange in Wireshark.
   ![276381560-08260fcb-734a-48fd-b202-c863b9306ab6](https://github.com/gabe-IT/azure-vm/assets/148400020/7eb3cea5-7ac6-4033-87b5-73bd2091a2a8)
3. We will now start a perpetual between the Virtual Machines by entering ping then the private IP of VM-2 followed by -t causing nonstop ICMP packets displaying in Wireshark
![276385531-474bfaac-5695-43dc-9f55-63d2ded0ccba](https://github.com/gabe-IT/azure-vm/assets/148400020/059efc9e-2b83-4e27-85ef-6ea93cc63ab2)
4. Heading back to the Microsoft Azure Account, we'll go to the VM-2's Network Security Group (NSG) in order to stop the traffic. In VM-2-nsg, we'll go to inbound security rules and create a security rule that denies ICMPs. Click on Add to open a right side pop up to set the rule and dot in Deny under action and ICMP under Protocol. Set the Priority higher than 300 (lower numbers have higher priority) and name the rule DENY_ICMP_PING then click Add to finish
   ![276388246-1d628322-94f9-479f-ad6d-cb2d2e3b6dba](https://github.com/gabe-IT/azure-vm/assets/148400020/072ba408-e679-42c2-a2cf-cfc8a9c0884d)
5. Once completed, you'll notice the message "Request timed out" will start displaying in Powershell in VM-1, meaning ICMP packets can no longer be transferred due to our security rule.
   ![lQBOBiz](https://github.com/gabe-IT/azure-vm/assets/148400020/38bdc96c-8f14-4413-99f1-0d84a8d0f770)

6. **Ping a public website** like google.com from VM-1. Monitor the traffic in Wireshark.
7. **Start a continuous ping** to VM-2 and note the traffic in Wireshark.
8. **Alter VM-2's Network Security Group** to block ICMP traffic. Observe the "Request timed out" message in VM-1.
9. **Re-enable ICMP traffic** and watch the resumption of ping responses in Wireshark.

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
