# Detection Lab

## Objective
[Brief Objective - Remove this afterwards]

The goal of this project is to build a hands-on detection lab that simulates real-world attack scenarios and defensive operations. By creating a controlled environment with logging, monitoring, and alerting, the lab aims to:

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

## Steps

1. Plot the architecture using any flowchart making website, I used [Draw.io](https://www.drawio.com/).<br>
   In the legend write down the network configs as it will be useful for referencing.

<img width="1406" height="792" alt="image" src="https://github.com/user-attachments/assets/518fc0be-d4a9-4998-b2ba-66b36d97aff4" />

2. Install a hypervisor on your host machine, I have use VMware Workstation Pro in this case. You can download it from [this link](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion).<br>
  You can refer to this YouTube video for complete installation steps [VMware Installation](https://www.youtube.com/watch?v=LWfaeLEhsXA).<br>
  It should look something like this after the installation is complete.

<img width="1912" height="1014" alt="image" src="https://github.com/user-attachments/assets/fd03df93-0efd-4dcf-8505-e673a2a95ad3" />

3. Now lets create our first Virtual Machine. I will be using Windows 10 as my target machine, Here is the download link for the Windos media creation tool file [Windows 10 Media creation tool](https://www.microsoft.com/en-ca/software-download/windows10).<br>
Media creation tool is the software we will be using to create a Windows 10 ISO image file for our Virtual Machine.<br>
After opening the setup, you will be presented with a window like this:

<img width="642" height="443" alt="image" src="https://github.com/user-attachments/assets/ee83dbf0-8d3f-4a39-82b4-7e78532a8148" />

4. Select **"Create Installation media"** and click **"Next"**<br>
   I would recommend leaving the settings as is for new users, however you can change your preferred language. Then click **"Next"**

<img width="642" height="443" alt="image" src="https://github.com/user-attachments/assets/9a0fb91a-f3d0-4ea5-b749-6726b128fe13" />

5. Select **""ISO File""** and click **"Next"**, it should start downloading now. It will also ask you to select a destination folder for the ISO file, In my case im keeping everything in **"Downloads"** folder.

<img width="642" height="446" alt="image" src="https://github.com/user-attachments/assets/1b900cfa-3964-4466-be56-0a392769d082" />

6. Now to create the Windows VM, head over to VMware window and click on **"Create new virtual machine"**

<img width="1872" height="993" alt="image" src="https://github.com/user-attachments/assets/d4440006-f6c5-445a-bff9-374f3d3ec9da" />

7. 

<img width="430" height="432" alt="image" src="https://github.com/user-attachments/assets/edc83b30-3f09-4689-95ba-7cbfbb863b23" />

<img width="430" height="431" alt="image" src="https://github.com/user-attachments/assets/ba73d404-3eac-4368-8bcb-0f04bcb2391b" />

<img width="425" height="428" alt="image" src="https://github.com/user-attachments/assets/a5f59e15-08d8-449e-8ce5-d1ea6801c1a4" />

<img width="428" height="433" alt="image" src="https://github.com/user-attachments/assets/30d6efe3-ccc7-4747-9d8e-00eff6422937" />

<img width="425" height="431" alt="image" src="https://github.com/user-attachments/assets/f769d9a9-7345-46ea-b884-3afd2dab25ad" />

<img width="621" height="464" alt="image" src="https://github.com/user-attachments/assets/8a6eeb0e-7279-4e81-9589-3c39135c3551" />

<img width="1890" height="965" alt="image" src="https://github.com/user-attachments/assets/8455f26b-a224-42bc-9011-d18f39db0d4f" />

<img width="620" height="455" alt="image" src="https://github.com/user-attachments/assets/e8035172-3bc0-4f4a-8fae-1fb64867df62" />

<img width="641" height="483" alt="image" src="https://github.com/user-attachments/assets/3d19da93-50a4-4a54-a23a-5f853d9ed669" />

<img width="639" height="478" alt="image" src="https://github.com/user-attachments/assets/191eb39d-17d8-4a3f-a9a7-2e38feae7ca1" />


<img width="642" height="483" alt="image" src="https://github.com/user-attachments/assets/556f2976-b71e-4a4b-8596-51657dbc9f1c" />

<img width="635" height="476" alt="image" src="https://github.com/user-attachments/assets/85b16626-d623-4bb5-8590-d32e54c7e571" />

<img width="643" height="481" alt="image" src="https://github.com/user-attachments/assets/ba12a543-06b4-49e2-8241-de603787966b" />

<img width="643" height="482" alt="image" src="https://github.com/user-attachments/assets/46955b03-84ed-4c60-b6a0-e68fe184c55f" />



















