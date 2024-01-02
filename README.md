<h1>Basic Home Lab Running Active Directory</h1>

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
<h3><b>Sections: </b></h3><br/>
<h4><b>1. Set up Azure account</b></h4>
<h4><b>2. Create a Virtual machine</b></h4>
    <h5><i>Steps to create VM:</i></h5>
<h4><b>3. Log Analytics Workspace</b></h4>
    <h5><i>Steps to create log analytics workspace</i></h5>
<h4><b>4. Microsoft Sentinel</b></h4>
    <h5><i>Connect Virtual Machine</i></h5>
<h4><b>5. Open virtual machine</b></h4>
    <h5><i>wf.msc</i></h5>
<h4><b>6. Log Analytics</b></h4>
    <h5><i>Create the Custom Logs</i></h5>
<h4><b>7. Logs Query</b></h4>
<h4><b>8. Maps in Azure</b></h4>
    <h5><i>Create Workbook</i></h5>

<br/><br/><br/>
 
1: Set up Azure account
<br/>
Link : <a href="https://azure.microsoft.com/en-us/free/">Azure Trial</a><br />
Every new user is given $200 worth of free credits which is to be used to complete this project. After project completion, the resources must be removed to ensure no unnecessary charges are incurred.
<br />
<img src="https://i.postimg.cc/0ydBMXfK/1.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />
In the subsequent step, a virtual machine will be generated; navigate to the search bar and input "virtual machine." It is imperative to note that this machine will intentionally be kept vulnerable and be accessible on the internet, rendering it susceptible to external attacks from individuals.
<br />

















Step 2: Now click on "Change adapter options"<br/>
<img src="https://i.postimg.cc/zG1KxqPx/7.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 3: Change the names of the below adapters to _INTERNET and X_INTERNAL_X to differentiate between the Main controller and client<br/>
<img src="https://i.postimg.cc/prhz6rH6/8.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 4: Click on the Internal network properties, and go to Internet protocol version 4 to change the IP address and add loopback address as shown below:<br/>
<img src="https://i.postimg.cc/h4697L8W/9.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/1tTNwSqc/10.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br/>
<br/>
Step 5: Rename the PC to DC for convenience. Click on System<br/>
<img src="https://i.postimg.cc/cH6nvCrL/11.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/ZndvLQPk/12.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h3><b>Installing AD/DS</b></h3><br/><br/><br/>
 
Step 1: Open "Server Manager"
<br/>
<img src="https://i.postimg.cc/K4hkp5Q1/13.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 2: Click "Add roles and features"<br/>
<img src="https://i.postimg.cc/h4fw9RwJ/14.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 3: This is the first screen, and you must click Next to proceed<br/>
<img src="https://i.postimg.cc/VsphgHQK/15.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 4: Click Next until this window where you must install the AD comes up<br/>
Now, Add features > next > next > next > install <br />
<img src="https://i.postimg.cc/13Zjhnz6/17.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/N0sCF3mj/18.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/YSdnWdzf/19.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br/><br />
Done, close
<br/>
<br/>
Step 5: Click on the exclamation mark at the top and then "Promote this server to a domain controller" <br/>
<img src="https://i.postimg.cc/wjcb6qtr/20.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/sX1n95nF/21.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/pT7s0y7m/22.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/x8ztBnDt/23.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Next > Next > Install<br/>
<img src="https://i.postimg.cc/Df9CLJLD/24.png" height="60%" width="80%" alt="Disk Sanitization Steps"/><br/><br/>
At the end of the installation, you will automatically be signed out
<img src="https://i.postimg.cc/2jbc1Fbh/25.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br />
Now, mydomain/admin is visible when attempting to login
<img src="https://i.postimg.cc/R0pdFNvg/26.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br/>
<br/>
<br/>
<h3><b>Creating own Admin account instead of dedicated admin account</b></h3>
<br/>
<br/>
<br/>
Step 1: Click on "Active Directory Users and Computers" as in picture"
<img src="https://i.postimg.cc/JzqKfpvV/27.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br /><br />
Step 2: Next you will find yourself on this screen where you can see the AD domain that was created. <br /> Create a new organizational unit as in picture.
<img src="https://i.postimg.cc/g2dNtCMH/28.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/Fs0TZrxK/29.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Step 3: We are creating a new user now, which will be an administrator.
<img src="https://i.postimg.cc/43xwszRK/30.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/jd4QRD0x/31.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br /><br />
Next <br/>
<img src="https://i.postimg.cc/rwh1t7w7/32.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/>
Next > Finish <br/><br/>
Step 4: Now, after this user was created, we are going to make it an administrator.
<img src="https://i.postimg.cc/g0nvy4wj/33.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br /><br />
Ok > Apply > Ok <br />
<img src="https://i.postimg.cc/rsLxkkfR/34.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/W3ZgC3wP/35.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br/><br/>
After this is done, Sign out of the account and sign in as the user just created.<br />
<img src="https://i.postimg.cc/VvBMsVhG/36.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
<h3><b>Installing RAS/NAT</b></h3><br/><br/><br/>
Step 1: Open Server Manager and click on "Add Roles and Features"<br/>
<img src="https://i.postimg.cc/tg9JXGq4/37.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Next > next > Remote access<br/>
<img src="https://i.postimg.cc/CdyMXWrY/38.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Next > next > next > Routing > Addfeatures<br/>
<img src="https://i.postimg.cc/g04Jjtjq/39.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Next> next > next > Install<br/>
<img src="https://i.postimg.cc/PxR5zLmC/40.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Step 2: Click on the exclamation mark at the top and then "Routing and Remote Access"<br />
<img src="https://i.postimg.cc/bNb1r8hx/41.png" height="40%" width="40%" alt="Disk Sanitization Steps"/><br/><br/>
Right-click on the server named DC (local) and Select "Configure and Enable ROuting and Remote Access"<br/>
<img src="https://i.postimg.cc/C11KqCfy/42.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/c1PQdCV1/43.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Select "Network Address Translation (NAT) and then click Next"<br/>
<img src="https://i.postimg.cc/zDyCmK2P/44.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/>
<img src="https://i.postimg.cc/qq6MmkLj/45.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Next > Finish<br/><br/></br/> 

<h3><b>Setting up DHCP Server on Domain Controller</b></h3><br/><br/><br/>

Step 1: Open Server Manager and click on "AddRoles and Features"<br/>
<img src="https://i.postimg.cc/ht3vX8kk/46.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Click on DHCP Server > Add Features > Next > Next > Next > Install<br/>
<img src="https://i.postimg.cc/k505cJXw/47.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/>
<img src="https://i.postimg.cc/fyZTG8d9/48.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br /><br />
Step 2: After installation, Click on the exclamation mark at the top and then "DHCP"<br />
<img src="https://i.postimg.cc/CMHKGVyH/49.png" height="40%" width="40%" alt="Disk Sanitization Steps"/><br /><br />
Step 3: Now, as in image below, create a new scope by clicking on "IPv4"<br />
<img src="https://i.postimg.cc/sX5gHkMz/50.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br /><br />
Step 4: Follow the image and make the changes exactly as described in them<br/>
<img src="https://i.postimg.cc/25b6hbmV/51.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.postimg.cc/4y5NspvF/52.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Explanation for 8 days as in picture: If you are in a starbucks and want to connect to the internet, an IP address is automatically leased  to you for a specified amount of time. Now the IP address cannot be leased to you for multiple days, as you will be leaving the restaurant in about an hour and will not use the internet there. If the IP is leased to you for 8 days, even if you leave the restaurant in 15 minutes, the IP address is blocked for 8 days which means no one else can be assigned that IP when you disconnect. So, usually the limit in public networks is set to a lower time period which does not cause IP addresses not being enough.<br/>
Since we are using a test environment which only we are accessing, we will set the time to 8 days.<br/>
<img src="https://i.postimg.cc/02kyZHPg/53.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/>
<img src="https://i.postimg.cc/ZKwKQF5W/54.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Here, do not forget to Add the IP address after you've entered it. <br/>
<img src="https://i.postimg.cc/P5NrnpC2/55.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Next > Next > Next > Finish<br />
<img src="https://i.postimg.cc/K8dzZwgj/56.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Step 5: Right click DHCP Server > Authorize
<img src="https://i.postimg.cc/MK0NZr35/58.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Step 6: Now, do the same and then refresh<br/><br/><br/> 

<h3><b>Runing PowerShell script to create 1000 users in Active Directory.</b></h3><br/><br/><br/>

Step 1: Open Powershell(ICE) and run it as administrator<br/><br/>
Step 2: Download the <a href="https://github.com/gparakh102/Active-Directory/blob/main/AD_PS-master.zip"> Script </a>on to the virtual machine. <br/><br/>Before running the script, run the following command:<br/>
Set-ExecutionPolicy Unrestricted<br/>
<img src="https://i.postimg.cc/jjL6DLcc/57.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
O/p after ececution of script<br/>
<img src="https://i.postimg.cc/JhNXDZJb/59.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/><br/>

<h3><b>Create a new virtual machine, name it "CLIENT1", and install Windows 10 on it.</b></h3><br/><br/><br/>

Make sure that the network it uses is "Internal Network"<br/>
<img src="https://i.postimg.cc/HsRDjPQ7/61.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/>
<img src="https://i.postimg.cc/PfVjZqmc/60.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/><br/>

<h3><b>Connecting the client machine to the private network and joining it to the domain</b></h3><br/><br/><br/>
Step 1: After setting up "CLIENT1", open command prompt in the machine and enter the command,<br/>
ipconfig<br/>
If eberything has been setup properly, the output is similar to the image below:<br/>
Also, run the ping command to confirm the machine has internat access.<br/>
<img src="https://i.postimg.cc/JnxgcpSm/62.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
The picture below explains how CLIENT1 connects to the internet.<br/>
<img src="https://i.postimg.cc/QM25YsGJ/63.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Step 2: Rename the CLIENT1 machine as in the image.<br/>
Don't just rename the computer description directly, click on "change" to rename it as well as add it to "mydomain"<br/>
The system will ask for the admin account credentials, so enter them to change the name.<br/>
<img src="https://i.postimg.cc/QxYqg2t0/64.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
Step3: After all this, the system will automatically restart. After tis, login with any one of the 1000 users created previously.<br/>
<img src="https://i.postimg.cc/7Zpd9G6s/65.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br/><br/>
To confirm if you have logged in with the correct user, open command prompt and run the command<br/>
whoami<br/>
<img src="https://i.postimg.cc/26HxHMGk/66.png" height="40%" width="40%" alt="Disk Sanitization Steps"/><br/><br/>


<h1>VOILA!!! You're done!!!!<h1>
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
