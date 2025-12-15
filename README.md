# azure-sentinel-honeypot-lab
My home lab using Azure Sentinel and Ubuntu VM as a honeypot

I created a Home SOC Lab in the cloud using Microsoft Azure. I start of by creating a free Azure subscription. Then I headed to [azure.portal.com](http://azure.portal.com) to create the resource group(folder) for the entire project to be in. Next, I create the Virtual Network, Virtual Machine(Honeypot) using Ubuntu, configure the NSG(Network Security Group), Log Analytics Workspace(to log failed attack attempts), and SIEM(Microsoft Sentinel) and align them in the correct Resource Group folder. Downloaded the geolocation file provided by Josh Madakor’s Azure SOC Lab YouTube Tutorial (https://www.youtube.com/watch?v=g5JL2RIbThM), to set up a map in Sentinel and reveal where hackers that are trying to attack my Virtual Machine are located. Be sure to turn your running machines off to avoid unwanted charges from Azure

## Create Azure Subscription(Free)

- Create Account

## Create a Resource Group

- After creating the account head to azure.portal.com
- Create a Resource Group
    - Resource Group - A folder for my cloud materials
    - First create Resource Group. Type *Resource Group* in the search bar
    
    <img width="951" height="906" alt="image(1)" src="https://github.com/user-attachments/assets/0a278112-18b0-42ad-8e7e-f506d87bf87e" />

- Created Resource Group. Click create, which is at the bottom of this screen
<img width="595" height="474" alt="Screenshot 2025-12-10 012208" src="https://github.com/user-attachments/assets/fea2c059-e158-43b6-97b8-f8a847634442" />
<img width="566" height="231" alt="Screenshot 2025-12-10 012307" src="https://github.com/user-attachments/assets/c1d234df-eec1-4191-bc55-dbf039ea6390" />

*Resource Group creation confirmation*

- Type resource groups in the search bar and click the first search
<img width="708" height="498" alt="Screenshot 2025-12-10 012843" src="https://github.com/user-attachments/assets/083b3275-2eb0-453b-ba61-68e2e6f6bf08" />

*Click the one at the top to reveal resource groups*
<img width="1657" height="546" alt="Screenshot 2025-12-10 013012" src="https://github.com/user-attachments/assets/5869a168-e5b9-4a3a-89dc-57a09c2e9bab" />

*Currently Nothing inside the Resource Group*
<img width="1880" height="713" alt="Screenshot 2025-12-10 013149" src="https://github.com/user-attachments/assets/44f190b0-2c98-418e-b6b5-c2b29b1373e7" />

- Now create virtual network by typing virtual network in the search bar

*Searching for Virtual Network*
<img width="728" height="204" alt="Screenshot 2025-12-10 013133" src="https://github.com/user-attachments/assets/5adac18b-7d15-4b67-8493-4f971153273c" />

- Click create

<img width="993" height="776" alt="Screenshot 2025-12-10 013608" src="https://github.com/user-attachments/assets/ff0e0ec8-cf39-4ba3-a568-f59b4e347c73" />
    
- Be sure to use the correct Resource Group to place the Virtual Network in
- I pressed next and seen that there was already a subnet created for me and an IP address range, then pressed review + create and wait
- By now I created a resource group, a virtual network, and a subnet inside of that virtual network

<img width="712" height="862" alt="Screenshot 2025-12-10 013947(2)" src="https://github.com/user-attachments/assets/a452a1c2-a025-4c6a-afdd-0c4711d53bf8" />

*Click create*

<img width="1347" height="618" alt="Screenshot 2025-12-10 014104(1)" src="https://github.com/user-attachments/assets/c296cb61-6184-4029-9bee-0d512e431f01" />

*Virtual Network is created*

- Now I can see that the Virtual Network I created is inside the resource group

<img width="1684" height="530" alt="Screenshot 2025-12-10 014220" src="https://github.com/user-attachments/assets/ce996f33-f60e-4e5d-b6bf-e78a8b4a3d4d" />

## Create a Virtual Machine

- This actual honeypot exposed to the internet for hackers to attack
- Type virtual machines in the search bar

<img width="1254" height="793" alt="Screenshot 2025-12-10 014452" src="https://github.com/user-attachments/assets/1f688811-4f75-41da-ae3b-da9a5731eab7" />

*Searched for Virtual Machines and clicked the first result*

- Click the Virtual Machine for low traffic at the top

<img width="732" height="550" alt="Screenshot 2025-12-10 014611" src="https://github.com/user-attachments/assets/7327ac77-3c4d-4189-8b9a-9998fea2a044" />

<img width="1261" height="723" alt="Screenshot 2025-12-10 020137" src="https://github.com/user-attachments/assets/c5cb77a0-1eef-4a4d-b7ea-8fbda046e1ce" />

<img width="991" height="527" alt="Screenshot 2025-12-10 020226(1)" src="https://github.com/user-attachments/assets/2c0834c0-b6f0-48df-9be3-3b375697cd34" />

*I used the Ubuntu OS for the Virtual Machine because it is for free tier users. Be sure to turn off Virtual Machine when done to avoid charges*

<img width="1017" height="464" alt="Screenshot 2025-12-10 020356(1)" src="https://github.com/user-attachments/assets/123c49dd-7dbe-40ba-8255-6ff2be972f1e" />

*Create a password for ssh in the key pair name section below the SSH Key Type section*

- Then press next for Disks and leave everything as is. The disk type can be changed, but I refrained from doing so to avoid extra charges as this lab is only being used for testing purposes
- Click next for Networking

<img width="1048" height="659" alt="Screenshot 2025-12-10 020821(1)" src="https://github.com/user-attachments/assets/893e95c9-926b-4aac-bdcb-f04658ce494f" />

*Networking tab, I name the Virtual Machine and I can view the subnet for my Virtual Machine* 

- I scrolled down to check the checkbox to delete IP and NIC(Mac Address) when IP is done and I shut my Virtual Machine off
- Click next to Management, then next to monitoring. We click to disable boot diagnostics

<img width="1048" height="659" alt="Screenshot 2025-12-10 020821(1)" src="https://github.com/user-attachments/assets/c785628a-ec14-40a8-a0d0-0d6ca93c8e9c" />

*Disable Boot Diagnostics*

- Then next, then click review + create and wait until it validates

<img width="826" height="632" alt="Screenshot 2025-12-10 021308(3)" src="https://github.com/user-attachments/assets/f7325f31-fcd8-4fe9-9b27-fbaa5209ae68" />

*Reviewing Virtual Machine information*

- Then click create
    - A pop-up will tell you about downloading your private ssh key for Ubuntu. I downloaded it and clicked return to create virtual machine

<img width="1066" height="457" alt="Screenshot 2025-12-10 021559(1)" src="https://github.com/user-attachments/assets/6f45dc20-cbf9-4185-a4be-bfccd1f6d19a" />

<img width="1765" height="705" alt="Screenshot 2025-12-10 021705(1)" src="https://github.com/user-attachments/assets/cb0808fd-ed7a-451c-9770-2e78fb3d4521" />


*The Virtual Machine, Virtual Network, Public IP Address, Network Interface, Disk type, and NSG are all in our RG-SOC-LAB Resource folder*

- In the resource group I have:
    - Virtual Machine: CORP-NET-EAST-2
    - Public IP Address: CORP-NET-EAST-2-ip
    - NSG: CORP-NET-EAST-2-nsg
        - NSG(Network Security Group) - Cloud firewall
    - Network Interface: corp-net-east-2826_z1
    - Disk: CORP-NET-EAST-2_OnDisk_1_fa308dcab
- Edit the NSG to open the firewall up to the internet, click NSG link in the resource group

<img width="1881" height="893" alt="Screenshot 2025-12-10 022254" src="https://github.com/user-attachments/assets/a6e58574-de20-47c1-9dd2-2759dadd9b19" />

*Delete the SSH rule* 

- Go to right hand corner and delete the SSH rule by clicking the trashcan
- Go to settings and click inbound security rules

<img width="332" height="96" alt="Screenshot 2025-12-10 022602" src="https://github.com/user-attachments/assets/f6ba0e1f-922e-4d7a-a0f5-910690777bbe" />

*Inbound Security rules in the Settings drop down menu*

- Click add, then allow any type of inbound traffic

<img width="1551" height="744" alt="Screenshot 2025-12-10 022845" src="https://github.com/user-attachments/assets/d75b744e-1889-4d40-8cba-5e3db5611f62" />

*Scrolling down, change destination port ranges to * to allow all port ranges*

- Now log into the Virtual Machine and disable firewall
- Since I have the Ubuntu OS(Free tier) selected, I go to the connect tab and click the check access button which provides me with a code to connect with ssh from the Windows commnd prompt. Also, I use the path to the ssh key password file that I downloaded to access the ssh, the file should be a ***.pem*** file
    - ssh -i [private-key-file-path] [azureuser@20.161.184.9](mailto:azureuser@20.161.184.9)

<img width="1686" height="772" alt="Screenshot 2025-12-10 024238" src="https://github.com/user-attachments/assets/fa6309d1-f204-4139-8ea2-7ecb83d839b0" />

<img width="719" height="237" alt="Screenshot 2025-12-14 193455" src="https://github.com/user-attachments/assets/ff0f683d-338b-417b-918c-38501e25cecf" />

<img width="721" height="182" alt="Screenshot 2025-12-14 193525" src="https://github.com/user-attachments/assets/3455255f-32d4-495f-87b5-5baa7567c82b" />

<img width="860" height="738" alt="Screenshot 2025-12-10 024439" src="https://github.com/user-attachments/assets/98193045-d154-44d1-a465-90dd1c84277d" />

- Using Ubuntu, we will disable the firewalls on the machine. UFW(Uncomplicated Firewall) is usually disabled with this Azure VM. We can check using:
    - sudo ufw status verbose - Checks the current status
    - sudo ufw disable - Disable UFW
    - sudo systemctl disable ufw - Make sure disabled even after reboot
        
    <img width="554" height="114" alt="Screenshot 2025-12-10 025052" src="https://github.com/user-attachments/assets/8fef4ced-a5aa-4d02-a9ae-1db131995c6b" />
        
        *ufw is already disabled on Azure Ubuntu VM*
        
- Now ping the Virtual Machine using the Machine’s public IP address
    
<img width="745" height="494" alt="Screenshot 2025-12-10 025438" src="https://github.com/user-attachments/assets/6fa4a46c-6e80-4c77-bb41-7ddb4c2ab083" />
    

## View Raw Logs on the Virtual Machine

- Close the ssh and then fail to log in about 4 times, intentionally
    
    <img width="721" height="338" alt="Screenshot 2025-12-14 193545" src="https://github.com/user-attachments/assets/133a7e2a-97df-4a8e-bff5-89762b46c05b" />
    
    *Shows failed log in attempts*
    
    - sudo tail -f /var/log/auth.log shows all of the logs for the machine, like event viewer in Windows
        
        <img width="1822" height="362" alt="Screenshot 2025-12-10 031427" src="https://github.com/user-attachments/assets/b95d2bf3-fb36-4d55-a880-39f586b68957" />
        
        *The first 3 logs are of the failed log in attempts*
        

## Configure a Log Repository and Forward our VM logs into it

- Type log analytics workspaces in the search bar
    
<img width="651" height="275" alt="Screenshot 2025-12-10 031916(1)" src="https://github.com/user-attachments/assets/60932f9e-1dc2-4564-8c21-37a806cd748e" />
    
- Click Create
    
    <img width="949" height="881" alt="Screenshot 2025-12-10 032051" src="https://github.com/user-attachments/assets/b4ee3215-fe0a-426c-90f1-44218a96dad1" />
    
    *Make sure to choose the right Resource Group to put the Log Analytics workspace in*
    
- Then click Review+Create, then wait, then click create
    
    <img width="1117" height="419" alt="Screenshot 2025-12-10 032313" src="https://github.com/user-attachments/assets/392316d3-3aac-4782-a257-ddeed04dd695" />
    
- Now create a Sentinel instance
    
  <img width="708" height="255" alt="Screenshot 2025-12-10 032350" src="https://github.com/user-attachments/assets/2ef8beab-b73c-466c-9f3a-51f8e43594b8" />
    
- Click Create
- Click the workspace, then click add
    
<img width="566" height="580" alt="Screenshot 2025-12-10 032514" src="https://github.com/user-attachments/assets/24b15a6d-fcf7-4f14-8494-2975e249f4ed" />
    

- Now we have a connection from our Log workspace to the SIEM(Microsoft Sentinel). Now we have to connect the VM to the Log workspace

<img width="1721" height="752" alt="Screenshot 2025-12-10 033846" src="https://github.com/user-attachments/assets/c5b69992-1d15-483a-b12e-9a001b379c97" />

*Successfully added Log Workspace to Sentinel*

## Connecting your VM to Log Analytics Workspace

- Go to content management tab, then content hub
    
    <img width="435" height="464" alt="Screenshot 2025-12-10 034208" src="https://github.com/user-attachments/assets/d81e1ab1-f893-40bf-82ab-25b95bc0e828" />
    
- Type in Syslog and click the Syslog and install
    
    <img width="1881" height="757" alt="Screenshot 2025-12-10 041116" src="https://github.com/user-attachments/assets/0cb9d14a-2c0d-4c31-b9a0-d54cd2647ef5" />
    
- Click Syslog via AMA(Azure Monitoring Agent)
    
    <img width="668" height="322" alt="Screenshot 2025-12-10 041505" src="https://github.com/user-attachments/assets/6938b1fa-2bcf-4ba4-b92f-c2132f471c4c" />
    
    - Click Open Connector Page
        
        <img width="1631" height="946" alt="Screenshot 2025-12-10 041605" src="https://github.com/user-attachments/assets/319f53fc-0de3-4a45-ab60-162dd9bca8ec" />
        
- The click create data collection rule
    
    <img width="897" height="267" alt="Screenshot 2025-12-10 041642" src="https://github.com/user-attachments/assets/bf7ad2fb-9834-4346-a441-c4b79a69de7b" />


<img width="718" height="823" alt="Screenshot 2025-12-10 041810" src="https://github.com/user-attachments/assets/621c9928-ae94-43e8-8245-bb54cd4044b3" />

*Created the rule name and selected the correct resource group*

- Press next and select our Virtual Machine
    
    <img width="727" height="681" alt="Screenshot 2025-12-10 041912" src="https://github.com/user-attachments/assets/4510b3e3-e9cb-4a58-b0b0-308491ae9f40" />

- Click next and collect all events
- Click review+create

<img width="739" height="567" alt="Screenshot 2025-12-10 042138" src="https://github.com/user-attachments/assets/901251e7-5d66-4001-a895-06302a2284d9" />

- Then click create
- Navigate to Azure to see the Agent was created in the Virtual Machine
    
    <img width="1892" height="838" alt="Screenshot 2025-12-10 042351(1)" src="https://github.com/user-attachments/assets/0ca20af9-90e5-4b78-8e73-82ede3b3884a" />
    
- After this, we go to Sentinel and then click logs after clicking on the workstation
- Then switch to KQL mode and type Syslogs in the text space
- The honeypot didn’t work until I edited the rules of the SIEM. Type Sentinel in the search bar. Then click on the log workshop. Click on content hub and go to the defender portal:
    
    <img width="1586" height="782" alt="Screenshot 2025-12-14 121407" src="https://github.com/user-attachments/assets/a8b20cce-577e-4ce8-aec1-6edbf4b38293" />

    
- Type in Syslog then enter to edit the logging rule
    
    <img width="1283" height="887" alt="Screenshot 2025-12-14 121542" src="https://github.com/user-attachments/assets/9f5816a8-dc4d-4014-87d8-b4a6891e74f4" />

- Click on the rule and click manage:
    
    <img width="729" height="394" alt="Screenshot 2025-12-14 121714" src="https://github.com/user-attachments/assets/bd822c0a-7eb7-4b93-8a5d-309b2f5fcfc2" />

    
- Click Syslog via AMA:
    
    <img width="784" height="319" alt="Screenshot 2025-12-14 121852" src="https://github.com/user-attachments/assets/028b19ee-456b-4f2a-a705-21c20a5063b3" />

- Click open connector page
- Scroll down and edit this rule:
    
    <img width="797" height="528" alt="Screenshot 2025-12-14 122037(1)" src="https://github.com/user-attachments/assets/547214a5-54d8-478e-af66-b7116a4b5ecd" />

- Under “collect” change LOG_AUTH and LOG_AUTHPRIV to LOG_INFO, a higher log alert so that it won’t be considered a nominal request and drop it. It was previously only set to LOG_NOTICE
    
    <img width="768" height="688" alt="Screenshot 2025-12-14 122133" src="https://github.com/user-attachments/assets/303830f8-e81f-47de-9e1b-5cea4aeaa754" />
    
- Back to the log workshop

## Querying Our Log Repository with KQL

- The Azure Monitoring Agent(AMA) is forwarding every log into our central log repository, our Log Workshop aka a Log Analytics workspace
- It’s important to wait a couple of minutes to a couple of hours for attackers to appear in logs
- Use KQL to filter our everything you want to see in this workspace:
    
    <img width="1325" height="685" alt="Screenshot 2025-12-14 123128" src="https://github.com/user-attachments/assets/1776398d-e997-4de8-b752-4189e28b859d" />

    *Using KQL to filter out only ProcessNames including CRON* 
    
    <img width="1131" height="649" alt="Screenshot 2025-12-14 123641" src="https://github.com/user-attachments/assets/466ff220-d8a6-48fe-a69b-e2f79e4a4d50" />

    
    *Using KQL to show where Preccessname includes CRON. Also use project to only show the ProcessName, Host IP, ProcessID, TimeGenerated, SourceSystem, and SeverityLevel columns*
    
    <img width="1497" height="710" alt="Screenshot 2025-12-14 124540" src="https://github.com/user-attachments/assets/e1fab150-c199-4ef8-b3e6-312894dc1b03" />
    
    *Shows where hackers failed to log on to my HoneyPot within the last 5 min*
    
    <img width="1373" height="533" alt="Screenshot 2025-12-14 130214" src="https://github.com/user-attachments/assets/4267c153-0454-4d74-84e4-0ba746b3282c" />
    *Using KQL query to show logs where ProecessID includes 218580*
    
    <img width="1357" height="705" alt="Screenshot 2025-12-14 131052" src="https://github.com/user-attachments/assets/3326fbbf-0bc3-41d0-b360-e8e4d879d2a5" />
    *Used KQL and created a column named SourceIP to show IP Addresses of attackers. The IP Addresses are derived from the SyslogMessage column and stored in the SourceIP column*
    
    <img width="1320" height="671" alt="Screenshot 2025-12-14 131334" src="https://github.com/user-attachments/assets/0a88ceee-2ee4-4b9e-8cc1-2c28b76cd19e" />
    *Used KQL to show SourceIP and the number of attempts to log into my Virtual Machine*
    

## Uploading your Geolocation Data to the SIEM

- Download [geoip-summarized.csv](https://drive.google.com/file/d/13EfjM_4BohrmaxqXZLB5VUBIz2sv9Siz/view?usp=sharing) that shows random IP Addresses and their locations and save it to your system
    
    <img width="818" height="517" alt="Screenshot 2025-12-14 131915" src="https://github.com/user-attachments/assets/84fa8e0d-b00f-409d-a368-1a58ea680c8e" />
    *Save this file to your system*
    
- Go to Sentinel and click on the Log Analytics Workshop:
    
    <img width="796" height="464" alt="Screenshot 2025-12-14 132209" src="https://github.com/user-attachments/assets/242f626e-3aab-4b88-8ef6-78b0d3456678" />

    
- Go to Watchlist
    
    <img width="481" height="379" alt="Screenshot 2025-12-14 132319" src="https://github.com/user-attachments/assets/ae5da3cc-3550-4179-a1ec-b525680e9239" />

    
- Click create a new Watchlist
    
    <img width="1056" height="509" alt="Screenshot 2025-12-14 132423" src="https://github.com/user-attachments/assets/c98d3fa7-5e62-4902-8ad1-eff85badaa01" />

    
- Type geoip for name and source
    
    <img width="1381" height="834" alt="Screenshot 2025-12-14 132543" src="https://github.com/user-attachments/assets/1903b681-7d29-4f85-ac3b-b9aa76c8bd43" />

    
- Fill in source information and use downloaded csv
    
    <img width="1230" height="663" alt="Screenshot 2025-12-14 132739" src="https://github.com/user-attachments/assets/1cc091a7-ad58-4a04-85b1-dc6c378a8989" />

    
    <img width="1648" height="800" alt="Screenshot 2025-12-14 132756" src="https://github.com/user-attachments/assets/83d0877f-25bd-4906-8683-6f55eccf8523" />

    
- Click review and create
    
    <img width="742" height="193" alt="Screenshot 2025-12-14 132942" src="https://github.com/user-attachments/assets/e80b095b-9ef0-444e-a5fb-cf25bb0f1e74" />

    
- Search for Watchlists under the Microsoft Sentinel tab to see the newly created Watchlist
- Let the Watchlist upload
    
    <img width="1206" height="537" alt="Screenshot 2025-12-14 133231" src="https://github.com/user-attachments/assets/0bcf0991-a669-4479-9637-a4fc9316a863" />

    

## Inspecting our Enriched Logs

- The watchlist created another table inside Log Analytics
    
    <img width="1627" height="759" alt="Screenshot 2025-12-14 134538" src="https://github.com/user-attachments/assets/ed523bcd-7548-4ba3-a306-4a5b24f39148" />

    
    *The Watchlist got put into Sentinel, specifically into our Log Analytics workspace*
    
- Get random IP address from a Hacker
    
    <img width="1264" height="560" alt="Screenshot 2025-12-14 134920" src="https://github.com/user-attachments/assets/dcd3096e-1c7b-4447-b03c-c78f61ea89a1" />

    
- This KQL Query reveals where the IP Address is located
    
    <img width="1499" height="681" alt="Screenshot 2025-12-14 142021" src="https://github.com/user-attachments/assets/8712bc9b-e2d9-40e2-9f2a-d0b1886fa8ca" />

    <img width="1460" height="652" alt="Screenshot 2025-12-14 142054" src="https://github.com/user-attachments/assets/6bbff83d-5e70-42b4-b3ee-797c86d11e36" />

    
- Add project to the query to show only the columns needed
    
    <img width="1546" height="707" alt="Screenshot 2025-12-14 142826" src="https://github.com/user-attachments/assets/f851f15c-8992-4e57-9a84-07075f6cf287" />


## Creating our Attack Map

- Head to Sentinel, then click on the Log Analytics instance, then click workbook under threat management
    
    <img width="799" height="711" alt="Screenshot 2025-12-14 143240" src="https://github.com/user-attachments/assets/ad6fd773-b770-43f5-b5c8-23af01f59944" />

    
- Click add a workbook
    
    <img width="802" height="347" alt="Screenshot 2025-12-14 143431" src="https://github.com/user-attachments/assets/2d5e9606-fb65-4862-9258-0710c3436aef" />

    
- Click Edit
- Open https://www.google.com/url?q=https://drive.google.com/file/d/1ErlVEK5cQjpGyOcu4T02xYy7F31dWuir/view?usp%3Ddrive_link&sa=D&source=editors&ust=1765764403357369&usg=AOvVaw3QsESjJOJldE6fcSStdqhZ and copy the data
    
    <img width="1696" height="907" alt="Screenshot 2025-12-14 144105" src="https://github.com/user-attachments/assets/e3f2f2c2-e6ac-4631-9a39-df903d6bdf2d" />

    
- Go back to Sentinel and click add a query
    
    <img width="580" height="598" alt="Screenshot 2025-12-14 144337" src="https://github.com/user-attachments/assets/1b5a26db-22ba-481c-935d-b7499a226727" />

    *Click Add data source + visualization*
    
- Go to advanced editor tab and delete the code already in there and paste the text from the  json file then click “apply”
    
    <img width="1279" height="617" alt="Screenshot 2025-12-14 144559" src="https://github.com/user-attachments/assets/245d60a5-21a3-47a6-ad0b-23a5c8e90ee5" />

- Go back to the Query Settings tab and press run query
    
    <img width="1001" height="514" alt="Screenshot 2025-12-14 144925" src="https://github.com/user-attachments/assets/96820b94-0331-4390-8f83-9eeb7c546d00" />

    
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
    
    <img width="1469" height="809" alt="Screenshot 2025-12-14 151041" src="https://github.com/user-attachments/assets/0bf513f8-8018-48f8-b9e1-020682de4a33" />

    
- Click done editing in the top and click save to save the workbook
    
    <img width="1531" height="722" alt="Screenshot 2025-12-14 151234" src="https://github.com/user-attachments/assets/5027628b-5ee8-4da6-a182-99ba55516790" />

    
- Fill in the Workbook name and save
    
    <img width="1253" height="638" alt="Screenshot 2025-12-14 151411" src="https://github.com/user-attachments/assets/e7c5e398-fbc6-4294-ab35-0e715fcfb412" />

    
- Can see the IP addresses of the failed attackers
    
    <img width="1540" height="789" alt="Screenshot 2025-12-14 151643" src="https://github.com/user-attachments/assets/931526a2-ad4b-4e40-a305-c914f83fe431" />

    
- The attack map is live! So the longer you leave the Virtual Machine on the more populated your map will be
