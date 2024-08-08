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
<img src="https://i.imgur.com/RSP1GTQ.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />
  
<br />
 Let's make the vm vulnerable to attacks by disabling all firewalls via Windows Defender: <br/>
<img src="https://i.imgur.com/hNnhlGQ.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />

<br />
  Next, let's ping our vm from our host machine to make sure it's discoverable: <br/>
<img src="https://i.imgur.com/2mc9g9t.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />

<br />
   Now let's create the log analytics workspace: <br/>
<img src="https://i.imgur.com/DIfXdkF.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />

<br />
At this point we need to connect our log workspace to our vm:  <br/>
<img src="https://i.imgur.com/v2MGvke.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />

<br />
Now we need to setup defender to collect all events:  <br/>
<img src="https://i.imgur.com/vUwQMWs.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />

<br />
Next, let's get a custom API key from ipgeolocation.io to feed into our powershell script:  <br/>
<img src="https://i.imgur.com/QVTr23d.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />
<br />
Now let's run the powershell script on our vm to automatically parse out our events to Azure. Look!, we can already see several failed RDP attacks!:  <br/>
<img src="https://i.imgur.com/MTD5AFt.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<img src="https://i.imgur.com/hPj4mAv.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />
<br />
Finally, we can create a sentinel workbook and use the data coming from our vm to create a heatmap of live attacks!:  <br/>
<img src="https://i.imgur.com/iO6h10s.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />
<br />
Here is the heatmap after only a few hours!:  <br/>
<img src="https://i.imgur.com/g9Twdzu.png" height="80%" width="80%" alt="Honeypot In Azure Sentinel With Geolocation Heatmap"/>
<br />



</p>

<h2>Findings:</h2>

- <b> A honeypot is a tool that can help detect, deflect, and counteract unauthorized access to computer systems and networks. By pretending to be a legitimate target, a honeypot can lure hackers into a controlled environment where their activities and behaviors can be 
      monitored.</b>
- <b> Honeypots can waste attackers' time and resources by providing false information or creating misleading environments. This can make it harder for attackers to succeed and may deter them from future attacks.</b>
- <b> A honeypot or honeynet can divert attackers' attention away from valuable assets, giving security teams more time to respond to attacks.</b>
- <b> Also, honeypots can help organizations identify vulnerabilities in their security systems by analyzing how attackers access the honeypot's data. This information can help organizations update their systems to block these attack methods.</b>
- <b> Upon analyzing the event logs I discovered that the majority of the failed RDPs from Thailand came from a single user attempting to brute force the machine.</b>
- <b> To mitigate these attacks from our vm we can turn all of our firewalls back on making the machine less discoverable. We could also reconfigure the vm to limit the amount of ports allowed.</b> 
- <b> Finally, a honeypot is a fantastic tool to better understand the mind of a hacker, to develop a deeper understanding of their behaviors and can ultimately be extremely benficial to protect organizations along with their assets.</b> 
