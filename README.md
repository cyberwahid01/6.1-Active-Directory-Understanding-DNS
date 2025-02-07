<p align="center">
<img src="https://i.imgur.com/9JmwJSF.png" alt="osTicket logo"/>
</p>

<h1>Active Directory: Understanding DNS 🪟</h1>
In this lab we attempt to understand DNS a bit deeper by executing some of its functions. We attempt to Ping the mainframe of the Domain Controller, Create DNS Records for the Mainframe, Change the IP Address of the Mainframe, Assess Old IP Information Left Over in the Cache, Perform a DNS Flush and Assess the New IP Information. We then use the ipconfig, ping and nslookup commands in Windows Powershell to demonstrate how we can see DNS information for different websites and what we can find out from IP Addresses.

(Link Back to Main Project Contents Page is at the Bottom of this Repo)
<h2>Environments and Technologies Used</h2>

- Lenovo Ideapad 5 Pro 16gb AMD Ryzen 7
- Microsoft Azure Resource Group
- Microsoft Azure Windows 10 Pro version 22H2 - x64 Gen2 Virtual Machine
- Microsoft Azure Windows Server 22 Datacenter: Azure Edition - x64 Gen2 Virtual Machine
- Windows Powershell

<h2>Operating Systems Used </h2>

- Local Windows 11 Home Version 21H2</b>
- Windows 10 Pro Version 22H2 Virtual Machine
- Windows Server 22 Datacenter: Azure Edition - x64 Gen2 Virtual Machine
  
<h2>List of Prerequisites</h2>

- Microsoft Azure Subscription
- Microsoft Azure Subscription Credit

<h2>Installation, Setup, Resource Setup, Executing Functions</h2>
1. To start off we will attempt to Ping the mainframe. The host mainframe can not be found. Later we will create a new Host (A) record named mainframe and assign it the Private IP address of the Domain Controller Server.
</p>
<br />
<p>
<img src="https://i.imgur.com/wvtNIa5.png" alt="1"/>
</p>
<p>
2. Here we are showing the order in the areas which the Ping request will search for DNS information. It shows which is faster and where the command will look if one level is failed. From this we can see that there is no record of the mainframe on the local cache or a local host file.
</p>
<br />
<p>
<img src="https://i.imgur.com/hoWVJIU.png" alt="2"/>
</p>
<p>
3. Now we are starting the process of creating a DNS Host (A) record for the mainframe. To do this we need to access the DNS Manager from within out Domain Controller Server.
</p>
<br />
<p>
<img src="https://i.imgur.com/afTiEMM.png" alt="3"/>
</p>
<p>
4. Within our Domain, we are creating a new Host with name mainframe, pointing to the IP Address 10.0.0.4.
</p>
<br />
<p>
<img src="https://i.imgur.com/d8V2WSc.png" alt="4"/>
</p>
<p>
5. Here we see confirmation of the Host record created within the DNS Manager.
</p>
<br />
<p>
<img src="https://i.imgur.com/N8ckIrX.png" alt="5"/>
</p>
<p>
6. If we Ping the mainframe now we can see the IP Address information being returned. Since this is the first time this information has been pulled after the record was created, it has been pulled from the DNS Server and not a local cache or host file.
</p>
<br />
<img src="https://i.imgur.com/5TDhnPj.png" alt="6"/>
</p>
<p>
7. We are now going into the DNS Manager and changing the IP Address to 8.8.8.8. This will be to demonstrate how DNS IP information is saved on our Client machine Cache.
</p>
<br />
<p>
<img src="https://i.imgur.com/sg6a8hJ.png" alt="7"/>
</p>
<p>
8. Here we can now see that if we Ping the mainframe again, it can not find the host because we have changed the IP Address from 10.0.0.4. However if we use the nslookup command we can see the old IP Address information as it is saved on the local cache of the Client machine.
</p>
<br />
<p>
<img src="https://i.imgur.com/u7aRKgC.png" alt="8"/>
</p>
<p>
9. This can be further reiterated if we use the ipconfig command and display dns information. The old A (Host) Record still shows up.
</p>
<br />
<p>
<img src="https://i.imgur.com/tCUQ0bV.png" alt="9"/>
</p>
<p>
10. We will now use the flushdns command to wipe all data from the DNS Resolver Cache.
</p>
<br />
<img src="https://i.imgur.com/gYnBXPP.png" alt="10"/>
</p>
<p>
11. If we now use the displaydns function we can see the old A (Host) Record information that has been flushed.
</p>
<br />
<p>
<img src="https://i.imgur.com/OhfXhlm.png" alt="11"/>
</p>
<p>
12. If we now Ping the mainframe after flushing the local Cache, the Ping request will search the DNS Server instead of the local cache since the cache has been flushed. As we can see the IP Address that is now showing is 8.8.8.8.
</p>
<br />
<p>
<img src="https://i.imgur.com/OnQ70sg.png" alt="12"/>
</p>
<p>
13. Since 8.8.8.8 is the public DNS Server for Google, when we perform the nslookup command for 8.8.8.8 we are shown the internal Private IP address for our Domain Server but also the dns.google domain.
</p>
<br />
<p>
<img src="https://i.imgur.com/NFpgA2Z.png" alt="13"/>
</p>
<p>
14. We will now create a CNAME record within our DNS Manager named Search and name the target host domain www.google.com
</p>
<br />
<p>
<img src="https://i.imgur.com/c5kFvml.png" alt="14"/>
</p>
<p>
15. We will now ping this CNAME record named "search" and analyse the results. From the reply we can see the IP Address 216.58.212.228. If we type this IP Address into our web browser search bar we are taken to the Google homepage.
</p>
<br />
<p>
<img src="https://i.imgur.com/Z1AvSD0.png" alt="15"/>
</p>
<p>
16. If we perform an nslookup command for our "search" record we can see the www.google.com domain showing up.
</p>
<br />
<p>
<img src="https://i.imgur.com/FQcOAp8.png" alt="16"/>
</p>
<p>
LINK BACK TO THE MAIN PROJECT CONTENTS PAGE - https://github.com/cyberwahid01/Azure-Compute-and-Networking
