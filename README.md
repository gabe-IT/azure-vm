# Virtual Machine Network in Microsoft Azure

This tutorial outlines how to set up a Virtual Machine Network in Microsoft Azure and conduct exercises to observe network traffic.

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop
- Windows Command Prompt
- Wireshark
- Network Protocols: DNS, ICMP, SSH, RDP

## Operating Systems Used

- Windows 10 (21H2)
- Linux (Ubuntu 20.04)

## Prerequisites

1. Microsoft Azure Account and Subscription
2. Access to Microsoft Remote Desktop Connection
3. (Optional) Notepad for logging Virtual Machine information

## Lab Steps

### Part 1: Creating Resources

1. **Create a Resource Group** in Azure Services. Name it `RG-VM` and note its region.
2. **Create a Windows 10 VM** (`VM-1`). Select `RG-VM` and allow it to create a new Virtual Network and Subnet.
3. **Create a Linux (Ubuntu) VM** (`VM-2`). Use `RG-VM` and the same Virtual Network.
4. **Observe the Virtual Network** within Network Watcher.

### Part 2: Observing Traffic

#### Observing ICMP Traffic
1. **Connect to VM-1** using Remote Desktop.
2. **Install Wireshark** on VM-1.
3. **Open Wireshark**, filter for ICMP traffic.
4. **Ping the Ubuntu VM** from VM-1 and observe in Wireshark.
5. **Ping a public website** (e.g., google.com) from VM-1 and observe.
6. **Start a perpetual ping** to VM-2 from VM-1.
7. **Modify inbound rules** in VM-2's Network Security Group to deny ICMP traffic. Observe the effect in Wireshark.
8. **Re-enable ICMP traffic** and observe the resumed ping activity.

#### Observing SSH Traffic
1. **Filter Wireshark for SSH traffic**.
2. **SSH into VM-2** from VM-1 and execute commands. Observe traffic in Wireshark.
3. **Exit the SSH session**.

#### Observing DHCP Traffic
1. **Filter Wireshark for DHCP traffic**.
2. **Issue a new IP address** to VM-1 (`ipconfig /renew`). Observe in Wireshark.

#### Observing DNS Traffic
1. **Filter Wireshark for DNS traffic**.
2. **Use nslookup** in VM-1 for domains like google.com. Observe in Wireshark.

#### Observing RDP Traffic
1. **Filter Wireshark for RDP traffic** (`tcp.port == 3389`).
2. **Observe the continuous RDP traffic**. Understand its nature as a live stream protocol.

### Lab Cleanup

1. **Close the Remote Desktop connection**.
2. **Delete the Resource Groups** created during the lab.
3. **Verify the deletion** of the Resource Groups.
