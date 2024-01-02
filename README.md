<p align="center">
  <img width="600" height="300" src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/945ededb-aa45-40b7-a2d7-c44243483fc8">
</p>
<h1 align = "center">Virtual Machine Network in Microsoft Azure</h1>
This tutorial demonstrates how to set up a Virtual Machine Network, as well as how to observe internet traffic between two virtual machines on the same network

<br />

<h2>Environments and Technologies Used</h2>

<ul>
  <li>Microsoft Azure</li>
  <li>Microsoft Remote Desktop </li>
  <li>Windows Command Prompt</li>
  <li>Wireshark</li>
  <li>Network Protocols</li>
  <ul>
    <li>DNS - Domain Name System</li>
    <li>ICMP - Internet Control Message Protocol</li>
    <li>SSH - Secure Shell</li>
    <li>RDP - Remote Desktop Protocol</li>
  </ul>
</ul>

</br>

<h2>Operating Systems Used </h2>
<ul>
  <li>Windows 10 (21H2)</li>
  <li>Linux (Ubuntu 20.04)</li>
</ul>

</br>

<h2>List of Prerequisites</h2>
<ol>
  <li>Microsoft Azure Account and Subscription</li>
  <li>Access to Microsoft Remote Desktop Connection (installed on Windows OS by default)</li>
  <li>(OPTIONAL): Notepad- We will be noting several specific IP addresses during this tutorial </li>
</ol>

<h2>Installation Steps</h2>

<h3>Creating our Virtual Machines</h3>

<p>
  <ul>
    <li><b>Resource Group</b></li>
      <ul>
       <li>To create a virtual machine we will first need to create a resource group. You can check out my <a href = "https://github.com/joshuafinchCC/azure-portal/tree/main">Resource Group Guide</a>. For the purposes of this tutorial, lets name it VMRG.  </li>

![image](https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/89ae91dc-4d6b-4157-af4c-185d7c7a0cd5)
    
        
   </ul>
    <li><b>Virtual Machine 1 using Windows 10</b></li>
    <ul>
      <li>On the <b>Azure Services Portal</b> go to <b>Virtual Machines</b> and click create, followed by "Azure virtual machine". Select the Resource group we've created (VMRG) and name the virtual machine <b>VM1</b>. The <b>Region</b> SHOULD default to the same as the resource group, but if not, set it to the same region. Set the <b>Availability Options</b> set to <i>No infrastructure</i> and <b>Security Type</b> to <i>Standard</i> for this tutorial</li>
      <li>Set the <b>Image</b> (our Operating System) to <i>Windows 10 Pro, Version 22H2, x64 Gen2</i></li>
      <li>The <b>Size</b> selected dicates the general processing power and RAM of our VM, for this tutorial we'll set it to <i>Standard_E2s_V3</i> which provides 2 virtual CPUs and 16 GBs of RAM</li>
      <ul>
       <p align="center">
        <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/48302ec2-049c-4a76-a01e-62981e38a57e" height="80%" width="80%"/>
       </p>
      <li>Set the username and password of your VM for logging in (you will need to remember this login for Remote Desktop Connection) and check the box at the bottom for licensing agreement</li>
      <ul>
        <p align="center">
        <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/d57dcad0-6d78-46cd-a5ec-c13da5f83e90" height="80%" width="80%" />
        </p>
      </ul>
      <li>On the <b>Network</b> tab, you'll notice a <b>Virtual Network</b> was created by the Virtual Machine automatically. You can keep all these settings on default</li>
      <ul>
        <p align="center">
        <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/a8f1579d-d744-45e4-9a1b-4815bbf523f9" height="80%" width="80%">
        </p>   
      </ul>
      <li>Next, head to the <b>Review + Create</b> tab and wait for your settings to fully validate. Then click on <b>Create</b> to deploy your Virtual Machine. It may take a moment to fully deploy. You'll notice the setup and deployment of your virtual machine automatically created several resources: An IP, Network Security Group, Virtual Network, Network Interface and Disk!</li>

 <p align="center">
 <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/348b687c-ef53-4505-abf6-91f81437fffa" height="80%" width="80%">
 </p>  
    </ul>
    <li><b>Virtual Machine 2 using Ubuntu</b></li>
    <ul>
      <li>This is the same process as Virtual Machine 1 but we'll name the VM <b>VM2</b> and set the Image to <i>Ubuntu Server 20.04 LTS x64 Gen2</i> (this will be our linux operating system!) Make Sure this VM is under the same resource group, region, and virtual network as VM1 (NOTE: you may have to wait for the full deployment of VM1 for its virtual network to be selectable while creating VM2)</li>
      <li>Ubuntu by default has their Administrator Account authentication as SSH public key, so we must set it as Password for logging in through Remote Desktop</li>
      <ul>
        <p align="center">
        <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/a62f621e-7aa6-4526-a934-fff178b3aece" height="80%" width="80%"/>
        </p> 
      </ul>
    </ul>
  </ul>
</p>

<br />

<h3>Logging into a Virtual Machine using Remote Desktop Connection</h3>

<p>
  <ul>
   <li>Once again use the <b>Azure Portal</b>, go to <b>Virtual Machines</b> and select VM1. From here we can obtain the <b>Public IP Address</b> which we will use to connect to it via Remote Desktop Connection</li>
    <ul>
       <p align="center">
      <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/83903cce-5359-4920-9882-c42ebbb0ffd3" height="80%" width="80%" />
       </p> 
    </ul>
    <li> Open your start menu and search "Remote Desktop Connection". Copy VM1's PUBLIC IP address and click <b>Connect</b>. You may have your personal computers log in username appear, hit "more choices" and enter in the Username and Password you set for VM1 (a pop up may show up for verification, just click on "Yes")</li>
    <ul>
      <p align="center">
      <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/7e183bd9-bf28-4ff5-acde-e319d236bfc2" height="80%" width="80%"/>
      </p> 
    </ul>
    <li>You have now successfully logged into your virtual machine via Remote Desktop Connection!</li>
    <ul>
      <p align="center">
      <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/30b2c143-6646-49cc-a80d-9ec726b4c818" height="80%" width="80%"/>
      </p> 
    </ul>
  </ul>
</p>

<br />

<h2>Observing Traffic in Virtual Machines</h2>

<h3>Download and Install Wireshark</h3>

<p>
  <ul>
    <li>First, download <a href="https://www.wireshark.org/download.html">Wireshark</a> (windows x64 installer) on VM1. Through wireshark we can filter and observe ICMP, SSH, DHCP, DNS and RDP traffic </li>
  </ul>
</p>

<br />

<h3>Observing ICMP (Internet Control Message Protocol) Traffic</h3>

<p>
  <ul>
    <li>Once installed, open Wireshark and click the blue fin icon in the top left to begin capturing traffic. In the filter bar, type <b>icmp</b> to filter incoming ICMP packets. Think of this traffic as a sort of "network diagnostic" traffic. When we ping VM2, we will see it here</li>
    <ul>
    <p align="center">
      <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/6f2b622a-c549-4272-a555-6534e5424498" height="80%" width="80%"/>
    </p> 
    </ul>
    <li>On your physical desktop, head to the Azure Portal and select VM2 to obtain the <b>Private IP Address</b> and copy it (NOTE: Your VM's private IP's may be different, in this instance VM1's IP is 10.0.0.4, while VM2's is 10.0.0.5) </li>
    <ul>
    <p align="center">
      <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/b492ceaf-f5de-4801-aeaf-baf643d25263" height="50%" width="50%"/>
    </p> 
    </ul>
    <li>Open <b>Windows Powershell</b> on VM1 and in the command line enter <b>ping</b> and the private IP of VM2. ICMP packets should now display in Wireshark. Our virtual machines are now talking to each other!</li>
    <ul>
      <p align="center">
    <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/0cba0bee-1618-438d-af2a-bb647aeb139b" height="80%" width="80%"/>
      </p> 
    </ul>
    <li>We can now set up a non-stop ping between the two Virtual Machines by entering <b>ping</b> then the private IP of VM-2 followed by <b>-t</b> causing a consistent stream of ICMP packets displaying in Wireshark. Afterwards we can set up some inbound security rules to block this traffic</li>
    <ul>
    <p align="center">
      <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/1e4056b0-2fad-42e0-8ac3-fb58eecc5804" height="80%" width="80%"/>
      </p> 
    </ul>
    <li>Heading back to the Azure Portal and selecting your resource group (VMRG) we can find VM2's <b>Network Security Group </b> (which should be named <i>VM2-nsg</i>) in order to halt the traffic</li>
     <p align="center">
<img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/f6ab07ac-d401-40d1-b6f9-3862e9ae26b2" height="80%" width="80%"/>
    </p> 
    <li>In VM2-nsg, we'll go to <b>inbound security rules</b> and create a security rule that denies ICMPs. Click on <b>Add</b> and select <b>ICMP</b> as the protocol to <b>Deny</b> under action. Set the Priority higher than 300 (priorities are inversely proportional meaning lower numbers have higher priority) and name the rule <b>DENYICMP</b> then click <b>Add</b> to finish</li>
    <ul>
    <p align="center">
      <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/97ad35fa-a791-4bbb-88f5-7120bd6ec7fd" height="80%" width="80%"/>
    </p> 
    </ul>
    <li>Once completed, you'll notice the message "Request timed out" will start displaying in Powershell in VM-1, meaning ICMP ping has been halted from our security rule</li>
    <ul>
      <p align="center">
    <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/20fbafdf-b89c-4b89-b1b4-5801d411c195" height="80%" width="80%"/>
      </p> 
    </ul>
    <li>To reinstate the traffic, simply head back to VM2's NSG and set the DENYICMP inbound rule's action to <b>Allow</b> and save</li>
  </ul>
</p>

<br />

<h3>Observing SSH (Secure Shell) Traffic</h3>

<p>
<ul>
  <li>In Windows Powershell inside VM1, type in <b>ssh VM2@[VM2's Private IP]</b> then hit Enter, enter in "yes" and it will ask for the password for VM2 (ex. "ssh vm2@10.0.0.5")</li>
  <li>Since we are accessing the Terminal of VM2 (essentially Linux's version of a command prompt) it doesn't diplay input/dots when typing a password, but it is definately registering input when typing</li>
  <li>Once logged in, you will be connected to the Terminal of VM2. You can exit by entering the command <b>exit</b></li>
  <li>Typing in commands such as <i>username, pwd, or sudo apt</i> will display traffic on Wireshark, you can filter ssh traffic in Wireshark by typing in <b>ssh</b> in the filter bar</li>
</ul>
</p>

<br />

<h3>Observing DHCP (Dynamic Host Configuration Protocol) Traffic</h3>

<p>
  <ul>Filter DHCP Traffic in Wireshark by entering <b>dhcp</b> in the filter bar</ul>
  <ul>DHCP assigns IP Addresses to new devices on the network. We can re-assign an IP Address to VM1 by going to Powershell an enterning the command <b>ipconfig /renew</b></ul>
<p align="center">
    <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/25a43434-a0fe-4c3c-916e-1021c7d08441" height="80%" width="80%"/> </p> 


<br/>

<h3>Observing DNS (Domain Name System) Traffic</h3>

<p>
  <ul>
    <li>Filter DNS traffic in Wireshark by entering <b>dns</b> in the filter bar</li>
    <li>In Powershell, you can type <b>nslookup</b> and a website such as "www.google.com" and observe the DNS traffic in wireshark</li>
  </ul>
<p align="center">
    <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/367e237c-5fae-4a8d-b9b7-6fd19c66297b" height="80%" width="80%"/> </p> 

<br/>

<h3>Observing RDP (Remote Desktop Protocol) Traffic</h3>

<p>
  <ul>
    <li>Filter RDP traffic in Wireshark by entering <b>tcp.port == 3389</b> in the filter bar and you'll see a stream of traffic already, can you guess why?</li>
    <li>Since we are filtering by RDP traffic, and we are currently remotely logged into VM1, we observe the constant stream of traffic on wireshark!</li>
  </ul>
 </p> 
<br/>

<h2>Clean Up</h2>
<ul>
  <li>Log off Remote Desktop Connection</li>
  <li>As with the resource group tutorial, it is advised to delete all your Resource Groups and VMs after you are finished experimenting. Note that when we create virtual machines, a second resource group is automatically created. </li>
  <ul>
  <img src="https://github.com/joshuafinchCC/VM-VN-RDC/assets/155266044/b382e382-8ce6-42ea-98c3-0442c1cdb0e8" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </ul>
</ul>
