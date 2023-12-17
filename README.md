<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Deployed Cloud-Based On-Premises Active Directory (Azure)</h1>
This tutorial illustrates the process of installing Active Directory through Azure. This forms the basis for upcoming labs. Utilizing two Azure VMs on the same virtual network, this lab centers on configuring one VM as the domain controller. The second VM will serve as a client, joining in a subsequent lab.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Advanced Deployment and Configuration Steps</h2>

- Create a virtual network in Azure
- Deploy two virtual machines within the same virtual network
- Focus on one VM for installing Active Directory
- Configure the selected VM to function as the domain controller
- Designate the second VM as a client to join the domain in a future lab

<h2>Deployment and Configuration Steps</h2>

![image](https://github.com/Skizfly/configuring-AD/assets/153954157/9afdacc9-95dd-470e-8a82-f554aa772d73)

<p>
</p>
<p>
Before utilizing the VMs, it's crucial to configure the domain controller VM's IP address as static. By default, if both VMs have dynamic IPs on the same virtual network, communication is hindered. Failing to make this adjustment may impede the client from joining the domain later. In the Azure portal, navigate to the Networking tab of the domain controller VM. Access the Network Interface, open the IP configurations tab, switch the Assignment to Static, and save changes. This ensures the domain controller has a static IP, serving as a reference for future configurations.
</p>
<br />

![image](https://github.com/Skizfly/configuring-AD/assets/153954157/11f0fef5-5a22-4c5a-a150-1a85917af136)
![image](https://github.com/Skizfly/configuring-AD/assets/153954157/92abd55f-e056-4294-aa20-4ec755f6cf96)
![image](https://github.com/Skizfly/configuring-AD/assets/153954157/32d96c7f-93d2-4372-a9d4-90a2ff360f6b)

<p>
</p>
<p>
Following the static IP configuration, proceed to log in to the client VM and check connectivity to the domain controller. When using "ping -t" with the domain controller's private IP address, it might show a connection timeout. To resolve this, on the domain controller VM, enable ICMPv4 in the local Windows Firewall. Open Windows Defender Firewall using "wf.msc" in the search bar. In the Inbound Rules section, enable the Core Networking Diagnostics - ICMP Echo Request rules. Returning to the client VM should now demonstrate successful pinging without errors.
</p>
<br />

![Capture](https://github.com/Skizfly/configuring-AD/assets/153954157/d31420cd-66d0-4348-83b8-8a7f8cb92525)

<p>
</p>
<p>
Now, proceed with installing Active Directory on the domain controller VM. In Server Manager, select "Add Roles and Features" and proceed. Verify the private IP address of the domain controller VM. In the Server Roles tab, choose "Active Directory Domain Services," add features, then click "Next" and "Install." Subsequently, promote the server to a domain controller. In Server Manager, address the warning sign in the top right corner, select "Promote this server to a domain controller." Opt for "Add a new forest" and define a domain name (e.g., lyanceytest.com). Set a domain password and click "Next" on each screen before selecting "Install."
</p>
<br />

<h2>A crucial point to consider</h2>
Upon relogging into the domain controller VM via Remote Desktop Connection, ensure logging in within the context of the domain. Input the domain path followed by the username, like mydomain.com\labuser. For instance, in my scenario, it is lyanceytest.com\labuser. With Active Directory installed, future configurations can be applied in subsequent labs, and the client VM will seamlessly join the created domain.
