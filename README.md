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
Click on Data collections on the left side of the screen: <br/>
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

<h2>Set Up Azure Sentinel (SIEM)>
- <b>Open Azure Portan in a 2nd tab portal.aszure.com</b> 
- <b>Search for Azure Sentinel</b>
- <b>Click create Microsoft Sentinel</b>
<a href="https://imgur.com/oW8iNwV"><img src="https://i.imgur.com/oW8iNwV.png" title="Create Microsoft Sentinel" /></a>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
