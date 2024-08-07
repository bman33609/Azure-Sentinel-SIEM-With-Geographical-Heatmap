<h1>Honeypot In Azure Sentinel With Geolocation Heatmap</h1>


<h2>Description</h2>
<p>In this project I created a honeypot with an Azure virtual machine. I then made the machine vulnerable to attacks by disabling firewalls and creating custom vm configuartions.
   After setting up the vm, I created a log analytics workspace within Azure and connected it to the vm in order to capture all security events from the vm. 
   I then ran a custom powershell script within the vm in order to parse out Windows Event Log information for failed RDP attempts and send them to the log analytics workspace in Azure. 
   Finally, I sent all the failed RDP events to a Sentinel workbook to generate a heatmap of live attacks from around the world.</p>


<h2>Languages and Utilities Used</h2>

- <b>Powershell ISE</b>
- <b>Command Line</b>
- <b>Windows Defender</b>
- <b>ipgeolocation.io</b>
- <b>Remote Desktop Connection</b>
  
<h2>Environments Used </h2>

- <b> Azure</b>
- <b> Windows</b>
- <b> Web Browser</b> 

<h2>Objectives:</h2>

- <b>Spin up virtual machine in Azure.</b> 
- <b>Make vm vulnerable to attacks by disabling firewalls.</b>
- <b>Ping vm from host to make sure machine is discoverable.</b>
- <b>Create log analytics workspace in Azure.</b> 
- <b>Connect vm to log analytics workspace.</b> 
- <b>Generate API key for powershell script via ipgeolocation.io.</b>
- <b>Run the powershell script</b>
- <b>Create Sentinel Workbook.</b>
- <b>Use Sentinel workbook to generate a geographical heatmap of live attacks.</b>


<h2>Program walk-through:</h2>

<p align="center">
Spin up virtual machine: <br/>
<img src="https://i.imgur.com/2vHExHT.png" height="80%" width="80%" alt="Vulnerability Scanning With Nessus"/>
<br />
  
<br />
 Let's make the vm vulnerable to attacks by disabling all firewalls via Windows Defender: <br/>
<img src="https://i.imgur.com/DTDOsMO.png" height="80%" width="80%" alt="Vulnerability Scanning With Nessus"/>
<br />

<br />
  Next, let's download Nessus: <br/>
<img src="https://i.imgur.com/TFmYmrI.png" height="80%" width="80%" alt="Vulnerability Scanning With Nessus"/>
<br />

<br />
   Now that Nessus has been installed, we need to locate the vm's IP: <br/>
<img src="https://i.imgur.com/3gRM2Qq.png" height="80%" width="80%" alt="Vulnerability Scanning With Nessus"/>
<br />

<br />
Run a basic uncredentialed network scan against the target IP address:  <br/>
<img src="https://i.imgur.com/TRzl709.png" height="80%" width="80%" alt="Vulnerability Scanning With Nessus"/>
<br />

<br />
View scan details:  <br/>
<img src="https://i.imgur.com/wHA1mLL.png" height="80%" width="80%" alt="Vulnerability Scanning With Nessus"/>
<br />

<br />
Now, run a credentialed scan:  <br/>
<img src="https://i.imgur.com/OPE30Ze.png" height="80%" width="80%" alt="Vulnerability Scanning With Nmap"/>
<br />
<br />
Let's view all the vulnerabilities that were found:  <br/>
<img src="https://i.imgur.com/AWfDkuI.png" height="80%" width="80%" alt="Vulnerability Scanning With Nmap"/>
<br />
<br />
Now, let's dive into one of the vulnerabilities that was found and see what we can learn about it:  <br/>
<img src="https://i.imgur.com/qakL1PA.png" height="80%" width="80%" alt="Vulnerability Scanning With Nmap"/>
<br />
<br />
Let's see what Nessus recommends us to do in order to mitigate these vulnerabilities:  <br/>
<img src="https://i.imgur.com/Ji9FTv0.png" height="80%" width="80%" alt="Vulnerability Scanning With Nessus"/>
<br />
<br />
Nessus suggests installing updates and re-enabling our firewalls so let's do that:  <br/>
<img src="https://i.imgur.com/Gdrao50.png" height="80%" width="45%" alt="Vulnerability Scanning With Nessus"/>
<br />

<br />
<img src="https://i.imgur.com/HGGz8nf.png" height="80%" width="45%" alt="Vulnerability Scanning With Nessus"/>
<br />

<br />
Now, let's scan again to see if the vulnerabilities have been removed:  <br/>
<img src="https://i.imgur.com/8Cb66dh.png" height="80%" width="80%" alt="Vulnerability Scanning With Nmap"/>
<br />

</p>

<h2>Findings:</h2>

- <b> Using Nessus can be instrumental in scanning a network device for various types of threats and vulnerablities.</b>
- <b> Nessus is very customizable and makes it easy to optimize your scans for specific purposes in a timely fashion.</b>
- <b> Credentialed scans are generally much more in depth and will help discover the majority of current vulnerabilities.</b>
- <b> Nessus gives us a categorical breakdown of vulnerabilties and offers steps to remediate each type of vulnerabilty.</b>
- <b> Upon diving into a particular vulnerability, Nessus will provide detailed information including port numbers, degree of severity, and many supportive reference links to assist in your investigations. In regards to the vulnerability shown above(SMB Signing Not 
      Required), Nessus told us that an unauthenticated, remote attacker could exploit this via man-in-the-middle attack. To mitigate this, Nessus recommends us to enforce message signing in the host's configuartion.</b>
- <b> In addition, Nessus recommended us to turn our firewalls back on and install all suggested updates on our virtual machine.
