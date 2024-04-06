<h1>Azure Sentinel map with live cyber attacks</h1>

<h2>Description</h2>
The focal point of this project was the deployment of Azure Sentinel to monitor unsuccessful remote desktop login attempts. The approach involved the use of a PowerShell script, designed to interface with an API for fetching location data associated with the respective IP addresses linked to these failed login attempts. Subsequently, this location data was meticulously mapped to provide an insightful visual representation of the attempted security breaches. <br/><br/>
The primary objective was to extract valuable insights into the origins of these security threats, ultimately enhancing the organization's overall security posture. The culmination of this effort is a comprehensive visual depiction that significantly improves our understanding of potential vulnerabilities. A special acknowledgment goes to Josh Madakor for his invaluable insight into the success of this project.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Virtal Box</b>
- <b>Microsoft Azure</b>

<h2>Practical lab walk-through:</h2>

<p>
<h2><b>Sections:- </b></h2>
<h3><b>1. Set up Azure account</b></h3>
<h3><b>2. Create a Virtual machine</b></h3>
    <h4><i>Steps to create VM:</i></h4>
<h3><b>3. Log Analytics Workspace</b></h3>
    <h4><i>Steps to create log analytics workspace</i></h4>
<h3><b>4. Microsoft Sentinel</b></h3>
<h3><b>5. Connect Virtual Machine</b></h3>
<h3><b>6. Open virtual machine</b></h3>
    <h4><i>wf.msc</i></h4>
<h3><b>7. Log Analytics</b></h3>
    <h4><i>Create Custom Logs</i></h4>
<h3><b>8. Maps in Azure</b></h3>
    <h4><i>Create Workbook</i></h4>

<br/><br/><br/>
 
<h3><b>1: Set up Azure account</b></h3>
<br/>
Link : <a href="https://azure.microsoft.com/en-us/free/">Azure Trial</a><br />
Every new user is given $200 worth of free credits which is to be used to complete this project. After project completion, the resources must be removed to ensure no unnecessary charges are incurred.
<br />
<img src="https://i.postimg.cc/0ydBMXfK/1.png" height="50%" width="50%" alt="Steps"/>
<br />
<br />
In the subsequent step, a virtual machine will be generated; navigate to the search bar and input "virtual machine." It is imperative to note that this machine will intentionally be kept vulnerable and be accessible on the internet, rendering it susceptible to external attacks from individuals.
<br /><br />
<h3><b>2: Create a Virtual machine</b></h3><br/>
<h4>Steps to create VM:</h4><br />
(i)	Resource Group: Create a new resource and give it a name (Honeypot_lab in this case)
<img src="https://i.postimg.cc/W46HQWKw/2.png" height="50%" width="50%" alt="Steps"/>
<br />
(ii)	Virtual machine name: Honeypot <br />
(iii)	Region: (US) West US 3<br />
(iv)	Image: Select the Windows 10 Pro version<br />
<img src="https://i.postimg.cc/tTqMydGQ/3.png" height="50%" width="50%" alt="Steps"/><br />
(v)     Administrator Account<br />
These are credentials of the virtual machine when attempting to login (You can set them up as anything)<br />
Username: g-admin<br />
Password: *************<br />
Select inbound port: RDP (3389)<br /><br />
(vi) Click on <b><i>Next : Disks > </i></b><br />
<img src="https://i.postimg.cc/T1hN5RPt/4.png" height="50%" width="50%" alt="Steps"/>
<br />
<img src="https://i.postimg.cc/50sktHfH/5.png" height="50%" width="50%" alt="Steps"/>
<br/>
<br/>
(vii) Leave everything as default and go to <br />
<b><i>Next : Networking > NIC network security group > Advanced > Configure network security group > Create new</i></b>
<img src="https://i.postimg.cc/nrxWX1fb/6.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(viii) Remove the existing inbound rules and Create default Allow Rule as per the image, for all traffic from any source, allowing anyone access to it as it is a honeypot.<br/>
<img src="https://i.postimg.cc/MZ04hg1W/7.png" height="40%" width="40%" alt="Steps"/>
<br />
(ix) <b><i>Add > Review + Create > Create</i></b>
<br/>
<br />
<h3><b>3: Log Analytics Workspaces</b></h3><br/>
<h4>Steps to create a log Analytics Workspace:</h4><br />
- Search log analytics workspaces in the search bar.<br/>
    -	This is used to link the virtual machine logs in windows event viewer to azure logs.<br/> 
    -	This will also be used to create custom logs and map their geo location data.<br /><br/>
 (i) Create log analytics workspace by clicking on <b><i>Create</i></b><br />
<img src="https://i.postimg.cc/VL9FsbRM/8.png" height="50%" width="50%" alt="Steps"/>
(ii) Resource Group: Same as created earlier during virtual machine creation (Honeypot_lab) <br/>
(iii) Name: LAW-Honeypot_lab<br/>
(iv) Region: West US 3<br/>
<img src="https://i.postimg.cc/VLzBL50r/9.png" height="50%" width="50%" alt="Steps"/> <br /><br />
(v)	<b><i>Review + Create > Create</i></b><br /> <br />
<h3><b>4: Microsoft Sentinel</b></h3><br />
-	Navigate to search bar, search for <b><i>Microsoft Sentinel</i></b> and click <b><i>Create</i></b> <br/>
<img src="https://i.postimg.cc/tgnFmnwf/10.png" height="50%" width="50%" alt="Steps"/> <br /><br />
(i) <b><i>LAW-Honeypot1 > Add</i></b><br />
<img src="https://i.postimg.cc/ncTKsJqd/11.png" height="20%" width="30%" alt="Steps"/> <br /><br />
<h3><b>5: Connect Virtual Machine</b></h3><br />
(i) Search for <b><i>log analytics workspaces</i></b> in the search bar<br />
(ii) <b><i>LAW-Honeypot1 > Virtual machines > Honeypot</i></b><br />
<img src="https://i.postimg.cc/j2tN5g20/12.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(iii) <b><i>Connect</i></b><br />
<img src="https://i.postimg.cc/SxvWrfTC/13.png" height="30%" width="30%" alt="Steps"/><br/<br/>
<h3><b>6: Open virtual machine</b></h3><br />
(i)	On the local machine, search for <b><i>Remote Desktop Connection</i></b> to connect to the virtual machine created.<br />
(ii) Paste the Public IP Address of the VM and use the same username - password combination to login to the machine, which was created during the VM setup.<br />
<img src="https://i.postimg.cc/7YB7HNyd/14.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(iii) Open Terminal on Local machine and ping VM to check if there is a connection. <br />
There will be no response as windows firewall on the VM is blocking ICMP packets<br />
<img src="https://i.postimg.cc/wjvXLGV9/15.png" height="50%" width="50%" alt="Steps"/><br/<br/>
<h4><i>wf.msc</i></h4><br /><br />
(i) Search for <b><i>wf.msc</i></b> in the VM, turn off the firewall as in picture, and recheck the command line on the local system. <br />
<img src="https://i.postimg.cc/ncVBfPNq/16.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(ii) It is working now, as the ping request from local machine to VM is being replied to now.
<img src="https://i.postimg.cc/G2kGbwcx/17.png" height="50%" width="50%" alt="Steps"/><br/<br/>
-	Subsequently, locate the Event Viewer within the VM. Within the Event Viewer, navigate to Custom logs, Windows logs, and Application and Services logs, specifically focusing on the Windows Log categories such as Application, Security, Setup, System, and Forwarded Events.<br />
-	Within the Security event logs, examine login attempt logs, including failed and successful logins, among other logs. The primary emphasis should be on Event ID 4625, denoting a failed login attempt. Filter the logs to scrutinize and identify failed attempts. Given that the machine is now exposed to the external environment, it is expected that individuals will attempt to perform unauthorized logins.<br />
-	To simulate a failed login attempt, initiate an attempt to log in via RDP from the main computer, deliberately entering incorrect username and password credentials. Subsequently, access the Event Viewer, specifically the Security log, and filter the log using Event ID.<br />
-	The displayed information will include Event ID 4625 (Failed Logon) along with details such as the attempted account username. Notably, the location is not explicitly mentioned; only the IP address is known at this stage. Subsequent steps will involve exploring methods to map the IP address to a geolocation for further analysis.<br /><br />
<b>Steps:</b><br />
(i) On the VM and search Windows Powershell ISE as administrator<br />
(ii) Copy the <a href="https://github.com/gparakh102/Azure-Sentinel/blob/main/Sentinel%20Powershell%20script.txt">script</a> and paste in powershell ISE<br />
<img src="https://i.postimg.cc/hvsm7LQJ/18.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(iii) The API key is going to be different for each person, and to get it, sign up at <a href="https://ipgeolocation.io/">ipgeolocation</a> and you immediately get API key<br />
The image below is my custom API key.
<img src="https://i.postimg.cc/858L8PVC/19.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(iv)Once the custom API Key is obtained, replace API key in script as in image.
<img src="https://i.postimg.cc/DfPLDTp2/20.png" height="20%" width="30%" alt="Steps"/><br/<br/>
(v) Save script on desktop and run it<br />
Output. (Text in purple indicates failed login attempts to the VM)<br />
<img src="https://i.postimg.cc/y8tZ9YxT/21.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(vi) The location where logs are stored from script is hidden, so have to go manually through Run (choose 1st option in image)<br />
<img src="https://i.postimg.cc/Nj5X5rsM/22.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(vii) “failed_rdp” is name of the file where the logs are stored<br />
<img src="https://i.postimg.cc/bvn2Rc2f/23.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(viii) Copy logs from VM to notepad in local machine and save<br />
<img src="https://i.postimg.cc/rmLRnnS0/24.png" height="50%" width="50%" alt="Steps"/><br/<br/>
<h3><b>7: Log Analytics</b></h3><br />
<h4>Create Custom Logs</h4><br />
(i) Search <b><i>log analytics workspace</i></b> on local machine in Azure<br />
(ii) Select LAW-Honeypot_lab, and search <b><i>tables</i></b><br />
(iii) There, Create > New custom log (MMA-based)<br />
<img src="https://i.postimg.cc/kMZs9Tjp/25.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(iv) Create custom logs by selecting the log file saved on local machine<br />
<img src="https://i.postimg.cc/9F7pfyKF/26.png" height="40%" width="40%" alt="Steps"/><br/<br/>
(v) Continue until <b><i>Collection Paths</i></b>. Here, paste the location where the logs are stored on VM. <br /><br />
<h3><b>8: Maps in Azure</b></h3>
<h4><i>Create Workbook</i></h4><br />
(i) Now in Sentinel, we are going to plot a map. <b><i>Add Workbook</i></b><br />
<img src="https://i.postimg.cc/mrbNVJDt/27.png" height="40%" width="40%" alt="Steps"/><br/<br/>
(ii) <b><i>Edit</i></b><br />
<img src="https://i.postimg.cc/1tX01FDS/28.png" height="40%" width="40%" alt="Steps"/><br/<br/>
(iii) <b><i>Add query</i></b><br />
<img src="https://i.postimg.cc/rw29RK2G/29.png" height="25%" width="25%" alt="Steps"/><br/<br/>
(iv) Paste the <a href="https://github.com/gparakh102/Azure-Sentinel/blob/main/Sentinel%20Query.txt">query</a> here, and filter Visualization by map
<img src="https://i.postimg.cc/sXLYj2Jh/30.png" height="50%" width="50%" alt="Steps"/><br/<br/>
(v) Filter <b><i>metric label</i></b> by label<br />
<img src="https://i.postimg.cc/Z5Px84JG/31.png" height="35%" width="35%" alt="Steps"/><br/<br/>
<b>Result:</b>
<img src="https://i.postimg.cc/Pq2b7ypK/32.png" height="50%" width="50%" alt="Steps"/><br/<br/>
<h1>VOILA!!! You're done!!!!</h1>
<b>Note:</b> If you leave the map and machine for a day or two, attacks will come from all over the world and will be plotted in the map.
</p>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
