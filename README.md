<h1>Failed Rdp Logins Azure Sentinel (SIEM)</h1>

<h2>Description</h2>
This walkthrough shows the process of creating a virtual machine (VM), monitoring and collecting data for creating custom logs of failed login attempts, organizing the data so its readable, and displaying the data based on where the attackers lauched their attacks on my VM. Over 3000 events were accounted for in the final report.
<br />


<h2>Resources Used</h2>

- <b>Virtual Machine (VM)</b> 
- <b>Resource Group</b>
- <b>Log Analytics Workspace</b>
- <b>Microsoft Defender for Cloud</b>
- <b>Azure Sentinel (Siem)</b>
- <b>PowerShell</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2) (VM)
- <b>Microsoft Azure</b> 

<h2>Walk-through:</h2>

<p align="center">
Create new VM:<br/>
<a href="https://imgur.com/JV1FFVq"><img src="https://i.imgur.com/JV1FFVq.png" title="Create New Virtual Machine" /></a>
<a href="https://imgur.com/gPKUO2q"><img src="https://i.imgur.com/gPKUO2q.png" title="VM Instance Details" /></a>
<br />
<br />
Create New Resource Group:  <br/>
<a href="https://imgur.com/rdpXk2l"><img src="https://i.imgur.com/rdpXk2l.png" title="Create New Resource Group" /></a>
<br />
<br />
Create Log Analytics Workspace: <br/>
This will be used to ingest and store windows event logs from the virtual machine. Custom logs will be created with this data.
<a href="https://imgur.com/KcCYkPk"><img src="https://i.imgur.com/KcCYkPk.png" title="Create New Log Analytics Workspace" /></a>
<a href="https://imgur.com/I0eNvRF"><img src="https://i.imgur.com/I0eNvRF.png" title="Info To Set Up Log Analytics Workspace" /></a>
<a href="https://imgur.com/XikgzJB"><img src="https://i.imgur.com/XikgzJB.png" title="Deployment Completed" /></a>
<br />
<br />
Go to winddows defender for cloud to enable gathering logs for the VM to the Log Analytics Workspace:  <br/>
<a href="https://imgur.com/rEuRSA7"><img src="https://i.imgur.com/rEuRSA7.png" title="Windows Defender For Cloud" /></a>
Click on environment settings, click your azure subscription, and click on log analytics: <br/>
<a href="https://imgur.com/r166DmE"><img src="https://i.imgur.com/r166DmE.png" title="source: imgur.com" /></a>
<br />
<br />
Turn servers on. Turn SQL servers on machines off:  <br/>
<a href="https://imgur.com/ppOFQHd"><img src="https://i.imgur.com/ppOFQHd.png" title="Turn servers On" /></a>
Click on Data collection on the left side of the screen: <br/>
Select all data
Click save
<a href="https://imgur.com/ZyrSw57"><img src="https://i.imgur.com/ZyrSw57.png" title="All Data" /></a>
<br />
<br />
Go back to log analytics workspace to connect the workspace to the VM:  <br/>
<a href="https://imgur.com/E2hTSLS"><img src="https://i.imgur.com/E2hTSLS.png" title="Reconnect Log Analytics Workspace" /></a>
<br />
Connect:  <br/>
<a href="https://imgur.com/rbLzrm4"><img src="https://i.imgur.com/rbLzrm4.png" title="Connect VM" /></a>
</p>

<h2>Set Up Azure Sentinel (SIEM)</h2>
<p align="center">
Open Azure Portan in a 2nd browser tab at portal.aszure.com 
Search for Azure Sentinel
Click create Microsoft Sentinel
<a href="https://imgur.com/oW8iNwV"><img src="https://i.imgur.com/oW8iNwV.png" title="Create Microsoft Sentinel" /></a>
Choose workspace you want to add Azure Sentinel to > Click add
<a href="https://imgur.com/Jo7HLOu"><img src="https://i.imgur.com/Jo7HLOu.png" title="Add Sentinel To Workspace" /></a>
<br />
<br />
<h2>Connect To VM Using RDP</h2>
<br />
<p align="center">
Download Microsoft Remote Desktop from the app store (Mac users)<br /> 
Go back over to the VM you created and get the public IP adddress associated with the vm:
<a href="https://imgur.com/DmcbKJr"><img src="https://i.imgur.com/DmcbKJr.png"VM ip address " /></a>
Click connect > RDP to get the RDP session (this is for Mac users.<br /> Windows users click start and type RDP.:<br/> 
<a href="https://imgur.com/2zgDC0h"><img src="https://i.imgur.com/2zgDC0h.png" title="Get RDP Session" /></a>
Enter the ip address of the VM you desire to access via RDP > Download RPD File
<a href="https://imgur.com/pqAfjQR"><img src="https://i.imgur.com/pqAfjQR.png" title="RDP Information" /></a>
<p align="center">
Double click RDP file<br />
<a href="https://imgur.com/k08WJ4G"><img src="https://i.imgur.com/k08WJ4G.png" title="RDP" /></a> 
<br> <br> 
Enter user credentials (Usernam and password you chose when you created the VM)
<a href="https://imgur.com/0vDRpv4"><img src="https://i.imgur.com/0vDRpv4.png" title="Creds" /></a>
<br>
<h2>Get Powershell Script</h2>
<p align="center">
<br>Powershell script is in the files section for download, or you can click on it and manually copy the script. Remember to save the file. Open powershell ISE (on the vm) and paste the script > Click File > New > Save As *file name* *Next, get your own API code and change it in the powershell script.<br />
<h2>Get API Code For Geolocation</h2>
<p align="center"> 
Go to ipgeolocation.io > Click get free API Access. This will take you to an account set up screen
<a href="https://imgur.com/wNY87FG"><img src="https://i.imgur.com/wNY87FG.png" title="Site For Geolocation API" /></a>
<br>After you have set up your free account, copy your API code and paste it into the powershell script. $API_KEY ="put you key here" and save the file.
<br>
<h2>Create Custom Log File For Geolocation Data</h2>
<p align="center">
<br>Minimize VM and go back to Azure on your device. Search for log analytics > Click of the workspace that is already set up > Go to custom logs > Add custom log.
<a href="https://imgur.com/ptDRZ5F"><img src="https://i.imgur.com/ptDRZ5F.png" title="Custom Logs" /></a>
<br>Go back to the VM > Open the log file > Copy log file data and paste it into notepad on your host machine, NOT THE VM > Save file as failed_rdp.log. This data will be used to teach log analytics what to look for. ** Log file can be found at C:\ProgramData. **
<a href="https://imgur.com/XNF7Q1B"><img src="https://i.imgur.com/XNF7Q1B.png" title="failed RDP Logs" /></a>
<br>Add the path to the custom log file you just saved on your host machine.
<a href="https://imgur.com/qKjixNW"><img src="https://i.imgur.com/qKjixNW.png" title="Path For Custom Log" /></a>
<br>Raw data for logs collected.
<a href="https://imgur.com/rGXrwQJ"><img src="https://i.imgur.com/rGXrwQJ.png" title="Raw data Logs" /></a>
<br>Extract Raw data fields by expanding a data filed and click extract fields from...
<a href="https://imgur.com/KA90BIW"><img src="https://i.imgur.com/KA90BIW.png" title="Extract Raw Data" /></a>
<br>Highlight desired data. For example, if you want latitude, highlight that data and save extraction. **This needs to be repeated for every piece of daata you want ta extract from the raw data.
<a href="https://imgur.com/ngoPKTy"><img src="https://i.imgur.com/ngoPKTy.png" title="Extract Data" /></a>
<br>Logs with headings for the extracted data.
<a href="https://imgur.com/c8uWELa"><img src="https://i.imgur.com/c8uWELa.png" title="Logs With Extracted Data" /></a>
 <br>
 <br>
 <h2>Azure Sentinel Workbook (Map)</h2>
 <br><p align="center">
 <br>Azure Sentinel dashboard diskplaying all data. 
<a href="https://imgur.com/GyxGUKe"><img src="https://i.imgur.com/GyxGUKe.png" title="Azure Sentinel Dashboard" /></a>
<br>Click workbook > Add new workbook > Edit > Remove all widgets that are there >Add a query > Change visualization to "Map"<br>
<a href="https://imgur.com/H6RHF2G"><img src="https://i.imgur.com/H6RHF2G.png" title="Query For Workbook" /></a>
<br>Map Visualization of failed login attempts (brute force attack). Over 3,000 attacks are shown in this map by country and ip address:<br>
<a href="https://imgur.com/PL08KXf"><img src="https://i.imgur.com/PL08KXf.png" title="Map Showing Attacks" /></a>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
