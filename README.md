# azure-sentinel-honeypot-lab
My home lab using Azure Sentinel and Ubuntu VM as a honeypot

I created a Home SOC Lab in the cloud using Microsoft Azure. I start of by creating a free Azure subscription. Then I headed to [azure.portal.com](http://azure.portal.com) to create the resource group(folder) for the entire project to be in. Next, I create the Virtual Network, Virtual Machine(Honeypot) using Ubuntu, configure the NSG(Network Security Group), Log Analytics Workspace(to log failed attack attempts), and SIEM(Microsoft Sentinel) and align them in the correct Resource Group folder. Downloaded the geolocation file provided by Josh Madakor’s Azure SOC Lab YouTube Tutorial (https://www.youtube.com/watch?v=g5JL2RIbThM), to set up a map in Sentinel and reveal where hackers that are trying to attack my Virtual Machine are located. Be sure to turn your running machines off to avoid unwanted charges from Azure

### Create Azure Subscription(Free)

- Create Account

### Create a Resource Group

- After creating the account head to azure.portal.com
- Create a Resource Group
    - Resource Group - A folder for my cloud materials
    - First create Resource Group. Type *Resource Group* in the search bar
    
    <img width="951" height="906" alt="image(1)" src="https://github.com/user-attachments/assets/0a278112-18b0-42ad-8e7e-f506d87bf87e" />

    

![*Created Resource Group. Click create, which is at the bottom of this screen*](attachment:4bdfc46f-0159-4c1c-974e-e11a96187d73:Screenshot_2025-12-10_012208.png)

*Created Resource Group. Click create, which is at the bottom of this screen*

![*Resource Group creation confirmation*](attachment:76125902-6d15-46b7-8b90-8d644762f5dd:Screenshot_2025-12-10_012307.png)

*Resource Group creation confirmation*

- Type resource groups in the search bar and click the first search

![*I originally clicked the one under Marketplace to create the resource group. Click the one at the top to reveal resource groups*](attachment:9599525a-c7a9-416d-889d-b623b28f8f68:Screenshot_2025-12-10_012843.png)

*I originally clicked the one under Marketplace to create the resource group. Click the one at the top to reveal resource groups*

![Screenshot 2025-12-10 013012.png](attachment:823b356e-3452-40c0-b460-88daac99dc11:Screenshot_2025-12-10_013012.png)

![*Currently Nothing inside the Resource Group*](attachment:b88b5d6d-033f-4cc2-ac6d-aa5102927381:Screenshot_2025-12-10_013149.png)

*Currently Nothing inside the Resource Group*

- Now create virtual network by typing virtual network in the search bar

![*Searching for Virtual Network*](attachment:1c45828f-0ca7-4079-851e-49345ea679b8:Screenshot_2025-12-10_013133.png)

*Searching for Virtual Network*

- Click create

![*Be sure to use the correct Resource Group to place the Virtual Network in*](attachment:14e0ca41-69cb-4e2e-95c0-7684325d7a73:Screenshot_2025-12-10_013608.png)

*Be sure to use the correct Resource Group to place the Virtual Network in*

- I pressed next and seen that there was already a subnet created for me and an IP address range, then pressed review + create and wait
- By now I created a resource group, a virtual network, and a subnet inside of that virtual network

![*Click create*](attachment:bfbedd6f-9108-4156-93a4-2302ef444e17:Screenshot_2025-12-10_013947.png)

*Click create*

![*Virtual Network is created*](attachment:64bcdf6a-5def-412a-962d-e8dfca23361e:Screenshot_2025-12-10_014104.png)

*Virtual Network is created*

- Now I can see that the Virtual Network I created is inside the resource group

![Screenshot 2025-12-10 014220.png](attachment:b9ee66cb-71c3-41fa-becf-5a225a39813e:Screenshot_2025-12-10_014220.png)

### Create a Virtual Machine

- This actual honeypot exposed to the internet for hackers to attack
- Type virtual machines in the search bar

![*Searched for Virtual Machines and clicked the first result*](attachment:bfac1073-4bd4-4bb3-bdd9-476e858514fb:Screenshot_2025-12-10_014452.png)

*Searched for Virtual Machines and clicked the first result*

- Click the Virtual Machine for low traffic at the top

![Screenshot 2025-12-10 014611.png](attachment:8d8b8564-17f6-4c33-9dfe-57333248391f:Screenshot_2025-12-10_014611.png)

![Screenshot 2025-12-10 020137.png](attachment:19f9e721-d824-400e-a4d2-5930c8d08ef4:Screenshot_2025-12-10_020137.png)

![*I used the Ubuntu OS for the Virtual Machine because it is for free tier users. Be sure to turn off Virtual Machine when done to avoid charges*](attachment:6f268cd2-80ed-4c28-833c-26855c7fa735:Screenshot_2025-12-10_020226.png)

*I used the Ubuntu OS for the Virtual Machine because it is for free tier users. Be sure to turn off Virtual Machine when done to avoid charges*

![*Create a password for ssh in the key pair name section below the SSH Key Type section*](attachment:c49c760c-6fa1-4d4a-a286-5af07927e888:f9deb4c9-5ad5-4c5d-84f6-d2924e5f7112.png)

*Create a password for ssh in the key pair name section below the SSH Key Type section*

- Then press next for Disks and leave everything as is. The disk type can be changed, but I refrained from doing so to avoid extra charges as this lab is only being used for testing purposes
- Click next for Networking

![*Networking tab, I name the Virtual Machine and I can view the subnet for my Virtual Machine* ](attachment:74b999d2-9433-4684-a5a2-b2bd096500d0:Screenshot_2025-12-10_020821.png)

*Networking tab, I name the Virtual Machine and I can view the subnet for my Virtual Machine* 

- I scrolled down to check the checkbox to delete IP and NIC(Mac Address) when IP is done and I shut my Virtual Machine off
- Click next to Management, then next to monitoring. We click to disable boot diagnostics

![*Disable Boot Diagnostics*](attachment:7fd9dfef-a2de-4edb-a1c2-f0de8239ff42:Screenshot_2025-12-10_021140.png)

*Disable Boot Diagnostics*

- Then next, then click review + create and wait until it validates

![*Reviewing Virtual Machine information*](attachment:940779a0-24aa-4833-a99e-3570c2b49386:Screenshot_2025-12-10_021308.png)

*Reviewing Virtual Machine information*

- Then click create
    - A pop-up will tell you about downloading your private ssh key for Ubuntu. I downloaded it and clicked return to create virtual machine

![Screenshot 2025-12-10 021559.png](attachment:85baea4e-db6a-467f-8963-75ef1cd026aa:Screenshot_2025-12-10_021559.png)

![*The Virtual Machine, Virtual Network, Public IP Address, Network Interface, Disk type, and NSG are all in our RG-SOC-LAB Resource folder*](attachment:70ff0ec6-5f6d-4181-928e-655574f731f0:Screenshot_2025-12-10_021705.png)

*The Virtual Machine, Virtual Network, Public IP Address, Network Interface, Disk type, and NSG are all in our RG-SOC-LAB Resource folder*

- In the resource group I have:
    - Virtual Machine: CORP-NET-EAST-2
    - Public IP Address: CORP-NET-EAST-2-ip
    - NSG: CORP-NET-EAST-2-nsg
        - NSG(Network Security Group) - Cloud firewall
    - Network Interface: corp-net-east-2826_z1
    - Disk: CORP-NET-EAST-2_OnDisk_1_fa308dcab
- Edit the NSG to open the firewall up to the internet, click NSG link in the resource group

![*Delete the SSH rule* ](attachment:0a60da11-1ea9-4fb5-a8ea-70fea169c040:Screenshot_2025-12-10_022254.png)

*Delete the SSH rule* 

- Go to right hand corner and delete the SSH rule by clicking the trashcan
- Go to settings and click inbound security rules

![*Inbound Security rules in the Settings drop down menu*](attachment:064492b1-6011-473b-8f05-49e570b5cb76:Screenshot_2025-12-10_022602.png)

*Inbound Security rules in the Settings drop down menu*

- Click add, then allow any type of inbound traffic

![*Scrolling down, change destination port ranges to * to allow all port ranges*](attachment:b808290b-5b0d-4ba1-bfea-4e68a553e733:Screenshot_2025-12-10_022845.png)

*Scrolling down, change destination port ranges to * to allow all port ranges*

- Now log into the Virtual Machine and disable firewall
- Since I have the Ubuntu OS(Free tier) selected, I go to the connect tab and click the check access button which provides me with a code to connect with ssh from the Windows commnd prompt. Also, I use the path to the ssh key password file that I downloaded to access the ssh, the file should be a ***.pem*** file
    - ssh -i <private-key-file-path> [azureuser@20.161.184.9](mailto:azureuser@20.161.184.9)

![Screenshot 2025-12-10 024238.png](attachment:ea9d66f3-ec95-4fc9-ac57-6a7d460c0416:Screenshot_2025-12-10_024238.png)

![Screenshot 2025-12-14 193455.png](attachment:752c6497-0201-466e-8207-a8ebc72402ec:Screenshot_2025-12-14_193455.png)

![Screenshot 2025-12-14 193525.png](attachment:952513cb-9449-4063-8444-765a022ec321:Screenshot_2025-12-14_193525.png)

![Screenshot 2025-12-10 024439.png](attachment:1aece51d-2ea4-4655-962c-0fe48e25bc80:Screenshot_2025-12-10_024439.png)

- Using Ubuntu, we will disable the firewalls on the machine. UFW(Uncomplicated Firewall) is usually disabled with this Azure VM. We can check using:
    - sudo ufw status verbose - Checks the current status
    - sudo ufw disable - Disable UFW
    - sudo systemctl disable ufw - Make sure disabled even after reboot
        
        ![*ufw is already disabled on Azure Ubuntu VM*](attachment:b1e544e1-1f0f-4c50-8331-94663a7b817b:Screenshot_2025-12-10_025052.png)
        
        *ufw is already disabled on Azure Ubuntu VM*
        
- Now ping the Virtual Machine using the Machine’s public IP address
    
    ![Screenshot 2025-12-10 025438.png](attachment:2f9361cb-d8f8-4bb8-9d91-4b95b99e2613:Screenshot_2025-12-10_025438.png)
    

### View Raw Logs on the Virtual Machine

- Close the ssh and then fail to log in about 4 times, intentionally
    
    ![*Shows failed log in attempts*](attachment:b37dbb3d-ef45-43bd-b91a-a1f53e1ea858:Screenshot_2025-12-14_193545.png)
    
    *Shows failed log in attempts*
    
    - sudo tail -f /var/log/auth.log shows all of the logs for the machine, like event viewer in Windows
        
        ![*The first 3 logs are of the failed log in attempts*](attachment:32c62b85-2be3-4af5-b99a-d92a8f20670e:Screenshot_2025-12-10_031427.png)
        
        *The first 3 logs are of the failed log in attempts*
        

### Configure a Log Repository and Forward our VM logs into it

- Type log analytics workspaces in the search bar
    
    ![Screenshot 2025-12-10 031916.png](attachment:8583d499-5e74-4d7c-8238-09a8a4da5d78:Screenshot_2025-12-10_031916.png)
    
- Click Create
    
    ![*Make sure to choose the right Resource Group to put the Log Analytics workspace in*](attachment:f3e17634-1052-409f-9f06-94b942aa9871:Screenshot_2025-12-10_032051.png)
    
    *Make sure to choose the right Resource Group to put the Log Analytics workspace in*
    
- Then click Review+Create, then wait, then click create
    
    ![Screenshot 2025-12-10 032313.png](attachment:20b4e057-f60e-48cf-beae-a806a9d68baa:Screenshot_2025-12-10_032313.png)
    
- Now create a Sentinel instance
    
    ![Screenshot 2025-12-10 032350.png](attachment:843d6aca-072d-484b-b09e-be55e8c36c35:Screenshot_2025-12-10_032350.png)
    
- Click Create
- Click the workspace, then click add
    
    ![Screenshot 2025-12-10 032514.png](attachment:2d8cfdab-0478-4045-a8de-4678c19be03e:Screenshot_2025-12-10_032514.png)
    

- Now we have a connection from our Log workspace to the SIEM(Microsoft Sentinel). Now we have to connect the VM to the Log workspace

![*Successfully added Log Workspace to Sentinel*](attachment:a7a74bbc-f56c-4919-9afb-1a50d961cff1:Screenshot_2025-12-10_033846.png)

*Successfully added Log Workspace to Sentinel*

### Connecting your VM to Log Analytics Workspace

- Go to content management tab, then content hub
    
    ![Screenshot 2025-12-10 034208.png](attachment:8aa5c18d-f7ba-4308-83ba-9613156ea134:Screenshot_2025-12-10_034208.png)
    
- Type in Syslog and click the Syslog and install
    
    ![Screenshot 2025-12-10 041116.png](attachment:45d4f03a-600e-49b6-9598-72c309e2a966:Screenshot_2025-12-10_041116.png)
    
- Click Syslog via AMA(Azure Monitoring Agent)
    
    ![Screenshot 2025-12-10 041505.png](attachment:c5d7ba76-8fb7-46e9-b2b8-2ef891696d7a:Screenshot_2025-12-10_041505.png)
    
    - Click Open Connector Page
        
        ![Screenshot 2025-12-10 041605.png](attachment:65ab7033-96ec-42d3-9ca6-438eed509897:Screenshot_2025-12-10_041605.png)
        
- The click create data collection rule
    
    ![Screenshot 2025-12-10 041642.png](attachment:f675ea74-45e1-4e67-9f7e-389f16d648df:Screenshot_2025-12-10_041642.png)
    

![*Created the rule name and selected the correct resource group*](attachment:30cfd5ec-560b-4dbd-9e9f-12b1e846592e:Screenshot_2025-12-10_041810.png)

*Created the rule name and selected the correct resource group*

- Press next and select our Virtual Machine
    
    ![Screenshot 2025-12-10 041912.png](attachment:42d1b0e9-73ce-458b-8347-8d32d1740cc6:Screenshot_2025-12-10_041912.png)
    
- Click next and collect all events
- Click review+create

![Screenshot 2025-12-10 042138.png](attachment:5e4a3978-04b9-4ebd-8ba3-6fa6c04ed4b2:Screenshot_2025-12-10_042138.png)

- Then click create
- Navigate to Azure to see the Agent was created in the Virtual Machine
    
    ![Screenshot 2025-12-10 042351.png](attachment:b4025408-bfd7-46b8-810b-386b3cfadd95:Screenshot_2025-12-10_042351.png)
    
- After this, we go to Sentinel and then click logs after clicking on the workstation
- Then switch to KQL mode and type Syslogs in the text space
- The honeypot didn’t work until I edited the rules of the SIEM. Type Sentinel in the search bar. Then click on the log workshop. Click on content hub and go to the defender portal:
    
    ![Screenshot 2025-12-14 121407.png](attachment:d8da8f56-b4ab-4959-b268-52cd7bdc3246:Screenshot_2025-12-14_121407.png)
    
- Type in Syslog then enter to edit the logging rule
    
    ![Screenshot 2025-12-14 121542.png](attachment:4af92a17-fcfe-4d1e-8142-96f36276a9eb:Screenshot_2025-12-14_121542.png)
    
- Click on the rule and click manage:
    
    ![Screenshot 2025-12-14 121714.png](attachment:7351c263-5329-4744-a936-d78104764f51:Screenshot_2025-12-14_121714.png)
    
- Click Syslog via AMA:
    
    ![Screenshot 2025-12-14 121852.png](attachment:28e86f7e-e3a8-4979-80a4-0f33d7e59fff:Screenshot_2025-12-14_121852.png)
    
- Click open connector page
- Scroll down and edit this rule:
    
    ![Screenshot 2025-12-14 122037.png](attachment:74bba90c-f7c9-4857-b4dd-7edaad9c13ce:Screenshot_2025-12-14_122037.png)
    
- Under “collect” change LOG_AUTH and LOG_AUTHPRIV to LOG_INFO, a higher log alert so that it won’t be considered a nominal request and drop it. It was previously only set to LOG_NOTICE
    
    ![Screenshot 2025-12-14 122133.png](attachment:462caa7c-231d-42bd-9c7a-7e5e9902411d:Screenshot_2025-12-14_122133.png)
    
- Back to the log workshop

### Querying Our Log Repository with KQL

- The Azure Monitoring Agent(AMA) is forwarding every log into our central log repository, our Log Workshop aka a Log Analytics workspace
- It’s important to wait a couple of minutes to a couple of hours for attackers to appear in logs
- Use KQL to filter our everything you want to see in this workspace:
    
    ![*Using KQL to filter out only ProcessNames including CRON* ](attachment:8bc94b88-f2dc-48e6-9c11-a00cc33570cf:Screenshot_2025-12-14_123128.png)
    
    *Using KQL to filter out only ProcessNames including CRON* 
    
    ![*Using KQL to show where Preccessname includes CRON. Also use project to only show the ProcessName, Host IP, ProcessID, TimeGenerated, SourceSystem, and SeverityLevel columns*](attachment:3afd3276-758e-474a-9884-74ad2e4a688d:Screenshot_2025-12-14_123641.png)
    
    *Using KQL to show where Preccessname includes CRON. Also use project to only show the ProcessName, Host IP, ProcessID, TimeGenerated, SourceSystem, and SeverityLevel columns*
    
    ![*Shows where hackers failed to log on to my HoneyPot within the last 5 min*](attachment:369396e7-2fb8-48be-95e8-559159998e18:Screenshot_2025-12-14_124540.png)
    
    *Shows where hackers failed to log on to my HoneyPot within the last 5 min*
    
    ![*Using KQL query to show logs where ProecessID includes 218580*](attachment:48341a59-5732-43b0-ad6e-5785f7a3d003:Screenshot_2025-12-14_130214.png)
    
    *Using KQL query to show logs where ProecessID includes 218580*
    
    ![*Used KQL and created a column named SourceIP to show IP Addresses of attackers. The IP Addresses are derived from the SyslogMessage column and stored in the SourceIP column*](attachment:97c3c487-e267-45b2-9bc8-757f6295547d:Screenshot_2025-12-14_131052.png)
    
    *Used KQL and created a column named SourceIP to show IP Addresses of attackers. The IP Addresses are derived from the SyslogMessage column and stored in the SourceIP column*
    
    ![*Used KQL to show SourceIP and the number of attempts to log into my Virtual Machine*](attachment:7e7f304e-e680-40d0-9a73-bb8b24077b35:Screenshot_2025-12-14_131334.png)
    
    *Used KQL to show SourceIP and the number of attempts to log into my Virtual Machine*
    

### Uploading your Geolocation Data to the SIEM

- Download [geoip-summarized.csv](https://drive.google.com/file/d/13EfjM_4BohrmaxqXZLB5VUBIz2sv9Siz/view?usp=sharing) that shows random IP Addresses and their locations and save it to your system
    
    ![*Save this file to your system*](attachment:66f68ef7-c256-4e17-ba93-4709c81ae3d5:Screenshot_2025-12-14_131915.png)
    
    *Save this file to your system*
    
- Go to Sentinel and click on the Log Analytics Workshop:
    
    ![Screenshot 2025-12-14 132209.png](attachment:d871fc6e-318b-4707-90eb-960b53a9f3f3:Screenshot_2025-12-14_132209.png)
    
- Go to Watchlist
    
    ![Screenshot 2025-12-14 132319.png](attachment:a969f9f4-1d35-4e25-bbdf-5be7d8865b01:Screenshot_2025-12-14_132319.png)
    
- Click create a new Watchlist
    
    ![Screenshot 2025-12-14 132423.png](attachment:23269720-d2fe-4af8-b5b4-814f57acff4b:Screenshot_2025-12-14_132423.png)
    
- Type geoip for name and source
    
    ![Screenshot 2025-12-14 132543.png](attachment:8085ba38-3c5d-4682-a1e7-d21a8a456339:Screenshot_2025-12-14_132543.png)
    
- Fill in source information and use downloaded csv
    
    ![Screenshot 2025-12-14 132739.png](attachment:d0178a36-a236-4dc9-9469-88bcc727123a:Screenshot_2025-12-14_132739.png)
    
    ![Screenshot 2025-12-14 132756.png](attachment:3ccc1cf2-4926-4c41-9559-db1a29b922bf:Screenshot_2025-12-14_132756.png)
    
- Click review and create
    
    ![Screenshot 2025-12-14 132942.png](attachment:9e324449-574b-4234-848d-77c910d4da47:Screenshot_2025-12-14_132942.png)
    
- Search for Watchlists under the Microsoft Sentinel tab to see the newly created Watchlist
- Let the Watchlist upload
    
    ![Screenshot 2025-12-14 133231.png](attachment:77b0ed78-d16c-4b6d-b906-66bafa9ba130:Screenshot_2025-12-14_133231.png)
    

### Inspecting our Enriched Logs

- The watchlist created another table inside Log Analytics
    
    ![*The Watchlist got put into Sentinel, specifically into our Log Analytics workspace*](attachment:140f3974-d3d3-4f27-8860-91b4235f83ce:Screenshot_2025-12-14_134538.png)
    
    *The Watchlist got put into Sentinel, specifically into our Log Analytics workspace*
    
- Get random IP address from a Hacker
    
    ![Screenshot 2025-12-14 134920.png](attachment:7efb82c2-c32d-4c64-84eb-03d954e1891e:Screenshot_2025-12-14_134920.png)
    
- This KQL Query reveals where the IP Address is located
    
    ![Screenshot 2025-12-14 142021.png](attachment:a13c5d26-75eb-4f4c-8935-da499d4a0dbe:Screenshot_2025-12-14_142021.png)
    
    ![Screenshot 2025-12-14 142054.png](attachment:2b928cdc-466f-44ed-a4a3-04e209928c2f:Screenshot_2025-12-14_142054.png)
    
- Add project to the query to show only the columns needed
    
    ![Screenshot 2025-12-14 142826.png](attachment:0bfc7790-cb34-4435-900d-f0b99efa5396:Screenshot_2025-12-14_142826.png)
    

### Creating our Attack Map

- Head to Sentinel, then click on the Log Analytics instance, then click workbook under threat management
    
    ![Screenshot 2025-12-14 143240.png](attachment:4bcdf3f7-6a06-4cb1-9e61-bc2aa1e475a3:Screenshot_2025-12-14_143240.png)
    
- Click add a workbook
    
    ![Screenshot 2025-12-14 143431.png](attachment:cb45785a-4023-4a1b-8da3-43b5a199cdee:Screenshot_2025-12-14_143431.png)
    
- Click Edit
- Open https://www.google.com/url?q=https://drive.google.com/file/d/1ErlVEK5cQjpGyOcu4T02xYy7F31dWuir/view?usp%3Ddrive_link&sa=D&source=editors&ust=1765764403357369&usg=AOvVaw3QsESjJOJldE6fcSStdqhZ and copy the data
    
    ![Screenshot 2025-12-14 144105.png](attachment:9ecc35fb-eb47-44eb-acf9-bd66e4d65f0f:Screenshot_2025-12-14_144105.png)
    
- Go back to Sentinel and click add a query
    
    ![*Click Add data source + visualization*](attachment:f4673ec6-0049-4111-a29f-ebd4c3adeade:Screenshot_2025-12-14_144337.png)
    
    *Click Add data source + visualization*
    
- Go to advanced editor tab and delete the code already in there and paste the text from the  json file then click “apply”
    
    ![Screenshot 2025-12-14 144559.png](attachment:2ec873dd-b4ae-4458-bbb5-9e238d3efaf2:Screenshot_2025-12-14_144559.png)
    
- Go back to the Query Settings tab and press run query
    
    ![*This particular query failed because it’s for Windows. For Linux, use the KQL query below*](attachment:a983f1ba-4d48-495b-8d22-e3b3bd451244:Screenshot_2025-12-14_144925.png)
    
    *This particular query failed because it’s for Windows. For Linux, use the KQL query below*
    
- Run this KQL query to see attackers location in the HoneyPot
    
    ```
    let GeoIPDB = _GetWatchlist("geoip");
    Syslog
    | where Facility in ("auth", "authpriv")
    | where SyslogMessage contains "Invalid user" or SyslogMessage contains "Failed password" or SyslogMessage contains "from"
    | extend SourceIP = extract(@"from ((?:\d{1,3}\.){3}\d{1,3})", 1, SyslogMessage)
    | where isnotempty(SourceIP)
    | order by TimeGenerated desc
    | evaluate ipv4_lookup(GeoIPDB, SourceIP, network)
    | summarize FailureCount = count() by SourceIP, latitude, longitude, cityname, countryname
    | project FailureCount, AttackerIP = SourceIP, city = cityname, country = countryname, 
    latitude, longitude, friendly_location = strcat(cityname, " (", countryname, ")");
    ```
    
    ![Screenshot 2025-12-14 151041.png](attachment:33c250cf-e913-49f2-9312-fd39d7643cc7:Screenshot_2025-12-14_151041.png)
    
- Click done editing in the top and click save to save the workbook
    
    ![Screenshot 2025-12-14 151234.png](attachment:dd09d059-0387-4c65-997e-cb5feb4b07ad:Screenshot_2025-12-14_151234.png)
    
- Fill in the Workbook name and save
    
    ![Screenshot 2025-12-14 151411.png](attachment:f48705f3-7faa-4bf7-ac29-a0f658a54939:Screenshot_2025-12-14_151411.png)
    
- Can see the IP addresses of the failed attackers
    
    ![Screenshot 2025-12-14 151643.png](attachment:029f7d2c-fb19-45cb-afa3-6a54e7f289a7:Screenshot_2025-12-14_151643.png)
    
- The attack map is live! So the longer you leave the Virtual Machine on the more populated your map will be
