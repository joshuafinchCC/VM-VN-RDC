<p align="center">
<img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/2cb238ff-4e46-4a75-8967-7ef5d124ab74" height="15%" width="15%" alt="Microsoft Azure logo"/>
</p>

<h1 align = "center">Virtual Machine Network in Microsoft Azure</h1>
This tutorial outlines how to set up an Virtual Machine Network in Microsoft Azure and doing some exercises observing traffic.

<br />

<h2>Environments and Technologies Used</h2>

<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Microsoft Remote Desktop</li>
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
  <li>Access to Microsoft Remote Desktop Connection</li>
  <ul>
    <li>For MacOS users, follow <a href = "https://www.youtube.com/watch?v=0lllpAhgAJs&ab_channel=TheHostingVideos">this video</a> to use Remote Desktop on Mac</li>
  </ul>
  <li>(OPTIONAL): Notepad for typing down log in information for our Virtual Machines</li>
</ol>

<h2>Installation Steps</h2>

<h3>Creating our Resource Group and Virtual Machines</h3>

<p>
  <ul>
    <li><b>Resource Group</b></li>
      <ul>
       <li>Through <b>Azure Services</b>, go to <b>Resource groups</b> to create a Resource Group and name your Resource Group <b>RG-VM</b>. Take note of the <b>Region</b> of your Resouce Group as it'll come in play when setting up our VMs. Once done, then click on <b>Review + Create</b></li>
        <ul>
          <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/89c6d771-64e6-495f-959c-640e482cc8a2" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
        </ul>
      </ul>
    <li><b>Virtual Machine 1 using Windows 10</b></li>
    <ul>
      <li>Through <b>Azure Services</b>, go to <b>Virtual Machines</b> to create an Azure Virtual Machine. Select the Resource group we've created (RG-VM) and name the virtual machine <b>VM-1</b>. Make sure the <b>Region</b> is the same as your Resource Group and we'll set our <b>Availability Options</b> set to <i>No infrastructure</i> and <b>Security Type</b> to <i>Standard</i> for this tutorial</li>
      <li>Set the <b>Image</b> (our Operating System) to <i>Windows 10 Pro, Version 22H2, x64 Gen2</i></li>
      <li>The <b>Size</b> selected dicates the general processing power and RAM of our VM, for this tutorial we'll set it to <i>Standard_E2s_V3</i> which provides 2 virtual CPUs and 16 GBs of RAM</li>
      <ul>
        <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/be86a82d-db6c-4d45-9961-9acc61c2aadb" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
      </ul>
      <li>Set the username and password of your VM for logging in and make sure to check the box for licensing agreement</li>
      <ul>
        <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/f4aedc00-a714-438b-bd34-5ca68694795e" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
      </ul>
      <li>Go to the <b>Network</b> tab and notice the <b>Virtual Network</b> created by the Virtual Machine as it should've been made by the Resource Group. It will be made automatically by the Virtual Machine</li>
      <ul>
        <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/3d2688ab-110e-41cd-b60d-7c5772ccd480" height="80%" width="80%"></li>
      </ul>
      <li>Then head to the <b>Review + Create</b> and click on <b>Create</b> to deploy your Virtual Machine. Give it some time to fully deploy before moving on.</li>
    </ul>
    <li><b>Virtual Machine 2 using Ubuntu</b></li>
    <ul>
      <li>Same process as Virtual Machine 1 but we'll name the VM <b>VM-2</b> and set the Image to <i>Ubuntu Server 20.04 LTS x64 Gen2</i></li>
      <li>Ubuntu by default has their Administrator Account authentication as SSH public key, so we must set it as Password for logging in through Remote Desktop</li>
      <ul>
        <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/70b6006b-a0f2-4b59-9eff-cf73e7174c70" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
      </ul>
    </ul>
  </ul>
</p>

<br />

<h3>Logging into a Virtual Machine using Remote Desktop Connection</h3>

<p>
  <ul>
   <li>Through <b>Azure Services</b>, go to <b>Virtual Machines</b> and select VM-1 we've created and click on <b>Connect</b> to connect to the VM, from this page you can obtain the <b>Public IP Address</b> which we will use to connect to it via Remote Desktop Connection</li>
    <ul>
      <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/f38f8254-73c7-42a4-8b31-2bd3d328cff1" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>Copy the address and paste it into Remote Desktop Connection and click on <b>Connect</b> and log in using the username and password you set up for VM-1 (a pop up may show up for verification, just click on "Yes" if it does)</li>
    <ul>
      <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/8ebbf47a-ec01-414e-8757-3eb272491e35" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>You are now successfully logged into your VM!</li>
    <ul>
      <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/a42e65d9-f9e3-4059-a04e-de51bb335d85" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
  </ul>
</p>

<br />

<h2>Observing Traffic in Virtual Machines</h2>

<h3>Download and Install Wireshark</h3>

<p>
  <ul>
    <li>First, download <a href="https://www.wireshark.org/download.html">Wireshark</a> in your VM. Downloads may be slow depending on your VM's CPU</li>
  </ul>
</p>

<br />

<h3>Observing ICMP (Internet Control Message Protocol) Traffic</h3>

<p>
  <ul>
    <li>Once installed, open Wireshark and start capturing packets (the blue fin icon). In the filter bar, type <b>icmp</b> to filter incoming ICMP packets</li>
    <ul>
      <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/08260fcb-734a-48fd-b202-c863b9306ab6" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>Back to your physical desktop, head to your Microsoft Azure Account obtain the <b>Private IP Address</b> of VM-2 and copy it</li>
    <ul>
    <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/14f48437-5d89-417a-b4b5-218fd845fa54" height="50%" width="50%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>Open up <b>Windows Powershell</b> in VM-1 and in the command line enter <b>ping</b> and the private IP of VM-2. Once done, ICMP packets should now display in Wireshark</li>
    <ul>
    <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/a5bd2c40-4a1f-490d-90a0-3155ff281c89" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>We will now start a perpetual / non-stop ping between the Virtual Machines by entering <b>ping</b> then the private IP of VM-2 followed by <b>-t</b> causing nonstop ICMP packets displaying in Wireshark</li>
    <ul>
    <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/474bfaac-5695-43dc-9f55-63d2ded0ccba" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>Heading back to the Microsoft Azure Account, we'll go to the VM-2's <b>Network Security Group (NSG)</b> (which should be named <i>VM-2-nsg</i>) in order to halt the traffic</li>
    <li>In VM-2-nsg, we'll go to <b>inbound security rules</b> and create a security rule that denies ICMPs. Click on <b>Add</b> to open a right side pop up to set the rule and dot in <b>Deny</b> under action and <b>ICMP</b> under Protocol. Set the Priority higher than 300 (priorities are inversely proportional meaning lower numbers have higher priority) and name the rule <b>DENY_ICMP_PING</b> then click <b>Add</b> to finish</li>
    <ul>
    <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/1d628322-94f9-479f-ad6d-cb2d2e3b6dba" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>Once completed, you'll notice the message "Request timed out" will start displaying in Powershell in VM-1, meaning ICMP ping has been halted from our security rule</li>
    <ul>
    <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/e7f22595-3c67-40e5-83a2-6344027b80a5" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>To reinstate the traffic, simply head back to your Microsoft Azure Account and set the DENY_ICMP_PING inbound rule's action to <b>Allow</b> and save</li>
  </ul>
</p>

<br />

<h3>Observing SSH (Secure Shell) Traffic</h3>

<p>
<ul>
  <li>In Windows Powershell inside VM-1, type in <b>ssh VM-2@[VM-2's Private IP]</b> then hit Enter, enter in "yes" and it will ask for the password for VM-2</li>
  <li>Since we are accessing the Terminal of VM-2 (essentially Linux's version of a command prompt) it doesn't diplay input/dots when typing a password but do know it is registering input when typing</li>
  <li>Once logged in, you will be connected to the Terminal of VM-2. You can exit by entering the command <b>exit</b></li>
  <ul>
  <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/c8c7f09d-79e0-4426-a47c-c937947b3eba" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
  </ul>
  <li>Typing in commands such as <i>username, pwd, or sudo apt</i> will display traffic on Wireshark, you can filter ssh traffic in Wireshark by typing in <b>ssh</b> in the filter bar</li>
</ul>
</p>

<br />

<h3>Observer DHCP (Dynamic Host Configuration Protocol) Traffic</h3>

<p>
  <ul>Filter DHCP Traffic in Wireshark by entering <b>dhcp</b> in the filter bar</ul>
  <ul>DHCP assigns IP Addresses to devices new to the network the moment said device joins the network. We can reassign an IP Address in the VM by going to Powershell an enterning the command <b>ipconfig /renew</b></ul>
</p>

<br/>

<h3>Observing DNS (Domain Name System) Traffic</h3>

<p>
  <ul>
    <li>Filter DNS traffic in Wireshark by entering <b>dns</b> in the filter bar</li>
    <li>In Powershell, type in <b>nslookup</b> and a website such as google.com</li>
  </ul>
</p>

<br/>

<h3>Observing RDP (Remote Desktop Protocol) Traffic</h3>

<p>
  <ul>
    <li>Filter RDP traffic in Wireshark by entering <b>tcp.port == 3389</b> in the filter bar and you'll notice non-stop traffic</li>
    <li>This is because the RDP is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted</li>
  </ul>
</p>

<br/>

<h2>Clean Up</h2>
<ul>
  <li>Log off Remote Desktop Connection</li>
  <li>It is advise to delete your Resource Group and VMs after finishing tinkering with them to prevent future costs, deletion of assets on Azure require verification by entering the name of the asset. Also to note, the Resource Group <b>NetworkWatcherRG</b> is created when creating NSGs for Virutal Machines and requires its own deletion</li>
  <ul>
  <li><img src="https://github.com/ColtonTrauCC/vm-network/assets/147654000/0f329b9c-4f52-4d9e-96ff-7aa33445cab6" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
  </ul>
</ul>
