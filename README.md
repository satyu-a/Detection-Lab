# Basic Detection Lab

## Objective

The goal of this project is to build a hands-on basic detection lab that simulates real-world attack scenarios and defensive operations. By creating a controlled environment with logging, monitoring, and alerting, the lab aims to:

- Practice identifying and analyzing malicious activity.
- Develop and test detection rules using SIEM tools (e.g., Splunk).
- Strengthen threat hunting and incident response skills.
- Gain practical, job-ready experience in SOC workflows.

This lab is not just about setting up tools—it’s about learning how attackers operate and how defenders can spot and stop them.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis (Splunk Enterprise).
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Host system specifications
- 4 Core Intel i5 8th gen, 16GB ram, 2TB SSD
- Windows 10 64bit
- All softwares and tools used are 64bit versions so you need to check your windows version before the installation. Other than 64bit is the 32bit version.
- To find out your architecture type go to **"Settings > System > About"**, there under **"Device Specification"** you will see your **"System type"**.

## Process

1. Designing an architecture of the detection lab for referencing and ease of organisation,
2. Setting up a Hypervisior, where all our virtual machines will be installed.
3. Installing Windows 10 Pro as our target machine
4. Installing Kali Linux as our attacking machine
5. Installing and setup SPLUNK Enterprise on Windows 10 Pro
6. Setting up the Network configurations
7. Generating some logs to check connectivity


## Step 1: Designing Setup Architecture

Plot the architecture using any flowchart making website, I used [Draw.io](https://www.drawio.com/).<br>
In the legend write down the network configs as it will be useful for referencing.

   <img width="1406" height="792" alt="image" src="https://github.com/user-attachments/assets/518fc0be-d4a9-4998-b2ba-66b36d97aff4" />

## Step 2: Setting up a hypervisor VMware Workstation Pro

Install a hypervisor on your host machine, I have use VMware Workstation Pro in this case. You can download it from [this link](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion).<br>
  You can refer to this YouTube video for complete installation steps [VMware Installation](https://www.youtube.com/watch?v=LWfaeLEhsXA).<br>
  It should look something like this after the installation is complete.

   <img width="1912" height="1014" alt="image" src="https://github.com/user-attachments/assets/fd03df93-0efd-4dcf-8505-e673a2a95ad3" />

## Step 3: Installing Windows 10 (Target machine)

1. Now lets create our first Virtual Machine. I will be using Windows 10 as my target machine, Here is the download link for the Windos media creation tool file [Windows 10 Media creation tool](https://www.microsoft.com/en-ca/software-download/windows10).<br>
Media creation tool is the software we will be using to create a Windows 10 ISO image file for our Virtual Machine.<br>
After opening the setup, you will be presented with a window like this:

   <img width="642" height="443" alt="image" src="https://github.com/user-attachments/assets/ee83dbf0-8d3f-4a39-82b4-7e78532a8148" />

2. Select **"Create Installation media"** and click **"Next"**<br>
   I would recommend leaving the settings as is for new users, however you can change your preferred language. Then click **"Next"**

   <img width="642" height="443" alt="image" src="https://github.com/user-attachments/assets/9a0fb91a-f3d0-4ea5-b749-6726b128fe13" />

3. Select **""ISO File""** and click **"Next"**, it should start downloading now. It will also ask you to select a destination folder for the ISO file, In my case im keeping everything in **"Downloads"** folder.

   <img width="642" height="446" alt="image" src="https://github.com/user-attachments/assets/1b900cfa-3964-4466-be56-0a392769d082" />

4. Now to create the Windows VM, head over to VMware window and click on **"Create new virtual machine"**

   <img width="1872" height="993" alt="image" src="https://github.com/user-attachments/assets/d4440006-f6c5-445a-bff9-374f3d3ec9da" />

5. Select **"Typical"** and click **"Next"**

   <img width="430" height="432" alt="image" src="https://github.com/user-attachments/assets/edc83b30-3f09-4689-95ba-7cbfbb863b23" />

6. Select **"Installer disc image file"** and click **"Browse"**. Enter the path where the ISO file is saved. Click **"Next"**,

   <img width="430" height="431" alt="image" src="https://github.com/user-attachments/assets/ba73d404-3eac-4368-8bcb-0f04bcb2391b" />

7. Enter your virtual machine name and where you want to store it. Then click **"Next"**.

   <img width="425" height="428" alt="image" src="https://github.com/user-attachments/assets/a5f59e15-08d8-449e-8ce5-d1ea6801c1a4" />

8. Allocate the disk size. I would recommend atleast 30GB because it would give you a lot of headroom to download and install tools if you wish to, Also splunk SIEM requirs a minimum space free for logs ingestion. Click **"Next"**.

   <img width="428" height="433" alt="image" src="https://github.com/user-attachments/assets/30d6efe3-ccc7-4747-9d8e-00eff6422937" />

9. You can leave it as is but if you have 16 GB ram, i would recommend allocating atleast 4GB. Click on **"Customize Hardware"** and then select **"Memory"** and adjust the slider as needed and click **"OK"**.<br>
   Make use the **"Power on this virtual machine after creation"** is checked as it will automatically turn on the VM.<br>

   **NOTE:** The moment you click **"Finish"** it may display **"Press any key"** message so immidiately click on a key to boot to setup. If u miss this and it says **"Time out"** just restart the Virtual machine from the toolbar: **VM > Power > Restart Guest**
    

      <img width="425" height="431" alt="image" src="https://github.com/user-attachments/assets/f769d9a9-7345-46ea-b884-3afd2dab25ad" /><br>
   
      <img width="953" height="649" alt="image" src="https://github.com/user-attachments/assets/9abe49a4-2bb9-44dc-9576-47024c236823" /><br>
   
      <img width="1890" height="965" alt="image" src="https://github.com/user-attachments/assets/8455f26b-a224-42bc-9011-d18f39db0d4f" />


10. Now You should see the Windows Setup screen like this and click on **"Next"** after selecting your preferences: 

      <img width="621" height="464" alt="image" src="https://github.com/user-attachments/assets/8a6eeb0e-7279-4e81-9589-3c39135c3551" />

11. Click **"Install Now"**

      <img width="620" height="455" alt="image" src="https://github.com/user-attachments/assets/e8035172-3bc0-4f4a-8fae-1fb64867df62" />

12. If you are like me and don't have a license (T^T) then click on **"I don't have a product key"**.

      <img width="641" height="483" alt="image" src="https://github.com/user-attachments/assets/3d19da93-50a4-4a54-a23a-5f853d9ed669" />

13. Select **"Windows 10 Pro"** as this is the one we would be using, and click **"Next"**.

      <img width="639" height="478" alt="image" src="https://github.com/user-attachments/assets/191eb39d-17d8-4a3f-a9a7-2e38feae7ca1" />

14. Accept the terms and click **"Next"**.

      <img width="642" height="483" alt="image" src="https://github.com/user-attachments/assets/556f2976-b71e-4a4b-8596-51657dbc9f1c" />

15. Select **"Custom"**.

      <img width="635" height="476" alt="image" src="https://github.com/user-attachments/assets/85b16626-d623-4bb5-8590-d32e54c7e571" />

16. Click **"Next"**.

      <img width="643" height="481" alt="image" src="https://github.com/user-attachments/assets/ba12a543-06b4-49e2-8241-de603787966b" />

17. And now your windows should begin installing.
    
      <img width="643" height="482" alt="image" src="https://github.com/user-attachments/assets/46955b03-84ed-4c60-b6a0-e68fe184c55f" />

18. Now setup windows as you would. After the setup is complete and you boot to the desktop, make sure to take a **"snapshot"**. A snapshot is like a config backup that saves the machines state at the time of creating the snapshot.
    It will allow you to restore the     machine to the current **"Fresh Install"** state if you break something. Name the snapshot and write a any credientials or info you want in the discription and click **"Take Snapshot"**.
    To revert to a snapshot, in the toolbar: **VM > Snapshot > Revert to a snapshot**

      <img width="762" height="377" alt="image" src="https://github.com/user-attachments/assets/feeb1fbe-0df8-46b9-90a9-027b004cfc35" /><br>

      <img width="461" height="298" alt="image" src="https://github.com/user-attachments/assets/376b00dc-1b9e-4576-89b7-f9f65be030f0" />


## Step 4: Installing Kali Linux (Attacking machine)

1. Kali Linux distro is the one most used to perform tests as it has the necessary tools. Now lets begin the installation. First we need to download the ISO file from Kali's website.<br>
   Go to the website using this link: [Kali VM](https://www.kali.org/get-kali/#kali-virtual-machines) Select the **VMware** option and it will prompt you to save the file in a folder of your choice.<br>
   The download will begin now,

   <img width="1816" height="923" alt="image" src="https://github.com/user-attachments/assets/37f0eb7a-a05b-4e89-8a9f-939661255428" />

2. The downloaded file will be a compressed or a Zip file so we need an "Unzipping" tool. We will be using **"7Zip"**. Download it from this link: [7Zip download](https://www.7-zip.org/),
   Click on **"Download"**. After the download is complete, run the file and it will be installed.

   <img width="685" height="209" alt="image" src="https://github.com/user-attachments/assets/36aa7f5b-fd73-4a1b-a5ad-ff4401d5ea05" />

3. After Kali is downloaded, extract it using 7Zip by right clicking on the file > 7Zip > Extract.

    <img width="1051" height="587" alt="image" src="https://github.com/user-attachments/assets/ae9c3d74-de32-45f1-b37d-5c884b229568" />

4. Open the extracted folder

   <img width="544" height="157" alt="image" src="https://github.com/user-attachments/assets/41fe3f43-093e-4524-a4ff-c6de4f2a8fd8" />

6. Open the folder further and you should see lots of files. Select the file with the extension **".vmx"** and double click it.

   <img width="991" height="431" alt="image" src="https://github.com/user-attachments/assets/21b5b22f-509f-4228-8c9d-7a943c8597c9" />

7. If you are unable to see file extensions, enable it from the toolbar: **"View > File name extensions (Checkbox)"**

   <img width="1008" height="142" alt="image" src="https://github.com/user-attachments/assets/226a3910-80b4-4b2e-89be-ff90eb9c9d93" />

9. After double clicking the file, system will prompt you to select an app to open the file with, if it doesn't open using VMware automatically. Select the VMware Workstation

   <img width="1035" height="567" alt="image" src="https://github.com/user-attachments/assets/a762e83b-4479-4626-a384-e1f08d5ef63c" />

10. Kali will automatically load into the VMware, ready to use. 

    <img width="1881" height="1008" alt="image" src="https://github.com/user-attachments/assets/18529eaa-a653-486a-ad98-4a75c35a5ea7" />

11. Now power on the machine and use the credentials: **username: root, password: toor** to login for the first time.
    Always change the credentials after logging in for security reasons.<br>
Just like the windows system, take a Snapshot of the fresh install.


## Step 5: Installing SPLUNK Enterprise and configuring it on Windows 10 Pro (VM-target)
1. Power on the Windows 10 Pro VM and update the drivers to their latest versions by going to: **"Settings > Windows Update"**

   <img width="1023" height="798" alt="image" src="https://github.com/user-attachments/assets/13829e30-e0cf-47c5-9b59-a89f1b6dc15e" />

2. After the windows is up to date, open Microsoft Edge and navigate to splunk's website using this link [Splunk Signup](https://www.splunk.com/en_us/form/sign-up.html?redirecturl=https://www.splunk.com/).

   <img width="1637" height="901" alt="image" src="https://github.com/user-attachments/assets/499ed969-92b0-433c-bb8f-90dc30ce9a50" />

3. Create a splunk enterprise account and login, then Click on **"Trials and Downloads"** on the top right corner. Then click on **"Get my free Trial"** button below the **"Splunk Enterprise"** section.

   <img width="1561" height="925" alt="image" src="https://github.com/user-attachments/assets/60fe043f-d1e9-4d31-8d5b-a77299f9285b" />

4. I will take you to a downloads page with several splunk versions. Click on **"Previous Releases"** to see all the options. Make sure you select the **"Windows"** tab.

   <img width="1184" height="605" alt="image" src="https://github.com/user-attachments/assets/3390c30a-967b-4495-8166-1336f96c455b" />

5. At the time of drafting this document, the latest version was **"9.4.4"**, to make sure we have a stable release we will be downloading N-1, i.e, 9.4.3. Also make sure the operating system is mentioned, like for us Windows 10 should be mentioned there.

    <img width="1197" height="727" alt="image" src="https://github.com/user-attachments/assets/53caec89-af38-405f-aa18-ebbeb05b1c74" />

6. Click on **"Download now"** and the download will begin.

      <img width="1258" height="554" alt="image" src="https://github.com/user-attachments/assets/66c27b49-8009-4b3c-803a-1c7dc597c5b7" />

7. After the download is complete, go to downloads and run the splunk file.

      <img width="660" height="262" alt="image" src="https://github.com/user-attachments/assets/844b76b4-262f-4a19-8cf5-2ad2d1aee672" />

8. Agree the license and click **"Customize"**.

     <img width="360" height="284" alt="image" src="https://github.com/user-attachments/assets/68a60bbc-3eb6-47fe-a826-26105f8d72b6" />

9. Here we can set a custom installation path, however I'am going to leave it as default and click **"Next"**

      <img width="363" height="282" alt="image" src="https://github.com/user-attachments/assets/4ecfac1c-603c-4107-a158-9359eb7eaf77" />

10. Since we are on a local account, select **"Local System"** and click **"Next"**

       <img width="362" height="283" alt="image" src="https://github.com/user-attachments/assets/6681c9e4-e10e-4003-91d2-50dec17c7783" />

11. Enter a username and password. We will be using these credentials to loging to the splunk instance.
    **NOTE:** These credentials and the SPLUNK.COM credentials have nothing to do with each other and can be different.

      <img width="365" height="287" alt="image" src="https://github.com/user-attachments/assets/9f22b28e-e958-4667-97ce-27c0757c157e" />

12. Click **"Install"**

      <img width="362" height="281" alt="image" src="https://github.com/user-attachments/assets/14643b17-f592-4f48-93d3-f7af583d3c76" />

13. After the install is complete, and you click **"Finish"**, you should be redirected to splunk web login portal. Alternatively, you can go to your browser of choice and enter: http://localhost:8000 or http://127.0.0.1:8000 to go to the console as splunk web runs on port 8000 by default.

      <img width="1204" height="624" alt="image" src="https://github.com/user-attachments/assets/1cbb2edb-77bf-46be-bb92-cd6908404c88" />

14. Use the credentials created during installation to login and you should be greeted with window like this.

      <img width="1242" height="549" alt="image" src="https://github.com/user-attachments/assets/e26d3ad6-639a-4de0-950a-d9f69faf20c9" />

15. Click on **"Add data"** to add data sources for log ingestion. If you want to take the tour, go ahead.

       <img width="1247" height="591" alt="image" src="https://github.com/user-attachments/assets/df001b09-e983-40c3-b25c-24bf537f950d" />

16. Then click on **"Monitor"**

       <img width="1237" height="594" alt="image" src="https://github.com/user-attachments/assets/5cfc703f-34ff-474a-883a-a5050f54e3e0" />

17. Then click on **"Local Event logs"**

       <img width="1240" height="589" alt="image" src="https://github.com/user-attachments/assets/7e8690e7-b2b8-4f28-838c-a01fea60af91" />

18. Now on the right side select **"System"**, **"Application"** and **"Security"** as these are the logs we want to monitor for now.

       <img width="1224" height="579" alt="image" src="https://github.com/user-attachments/assets/3fbdc179-9b63-4149-a3ae-3b24baf537d7" />

19. Leave it as is for now. Default index is the **"Main"** index so its fine. Then click on **"Review"**.

       <img width="1227" height="572" alt="image" src="https://github.com/user-attachments/assets/b475f6ff-0d40-4691-a93a-62b9a39c28b4" />

20. Now click on **"Submit"** and we should be ready to search the logs!!

       <img width="1229" height="603" alt="image" src="https://github.com/user-attachments/assets/20a04316-8612-408a-a2fc-c64fbad13e4f" /> <br>

       <img width="1238" height="572" alt="image" src="https://github.com/user-attachments/assets/f5eff1c5-024b-4fb8-806d-8c48c9d70b3b" />

21. This is the search window

       <img width="1253" height="581" alt="image" src="https://github.com/user-attachments/assets/87567ea8-2c38-49ca-8483-fdbf09bf7b39" />

-Now we have some logs but there is a better way! For that we will be using **"Sysmon"** to get more logs. Now begins the Sysmon setup:







## Step 6: Setting up Network configurations

Before setting up a network configuration, I will quickly tell you about the different network options available to us

- NAT: This is the default configuration of the VMware, in this config, each vm is assigned a network within the host, all of them have access to the internet.
  
  <img width="913" height="644" alt="image" src="https://github.com/user-attachments/assets/8c3727fb-65fa-424c-a824-ba7ba317ebea" />

-NAT Network: In this network, all VMs have access to the internet but are meshed into a single network.

   <img width="913" height="644" alt="image" src="https://github.com/user-attachments/assets/179ff2b2-e4de-49d3-a0d0-b3c2f03f9a42" />

-Bridged: In this network, the VMs will act as physical machines and will be on the same network as the host machine.
   
   <img width="998" height="644" alt="image" src="https://github.com/user-attachments/assets/829d30b4-247d-4a56-a49a-d1f23cd1fca8" />

-Host only network: These VMs are only accessible to the host machine, they do not have internet access.

   <img width="933" height="645" alt="image" src="https://github.com/user-attachments/assets/7e3be929-2052-4685-9409-573b08a48de5" />

-Lan Segment/Internal Network: The VMs will be in their own network, IP are assigned statically and no communication outside.

   <img width="939" height="648" alt="image" src="https://github.com/user-attachments/assets/e07f799f-fba6-4420-a4ce-3a07ccbb83f9" />

-Not attached: Here the network adapter is simply not attached, i.e, isolated device config, no communication at all.

   <img width="909" height="640" alt="image" src="https://github.com/user-attachments/assets/13d217be-56d5-4ed5-bd11-7568b8b69801" />













