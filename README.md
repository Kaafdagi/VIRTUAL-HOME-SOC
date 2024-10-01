# HOME SOC Setup With Windows,Linux(Pardus) Splunk Enterprice ,Forvarder,Trend Micro

 "This project demonstrates the setup of a home Security Operations Center (SOC) using virtual machines running Windows 10, Pardus, and Kali Linux. The aim is to integrate security tools such as Sysmon, Splunk Forwarder, Splunk Enterprise, and Trend Micro Agent for real-time security monitoring and threat detection."
 
 ##  Technologies and Requirements
- VirtualBox (Installed )
    
- Windows 10: Hosts Sysmon, Splunk Forwarder, and Trend Micro Agent to monitor and forward security logs.

- Splunk Forwarder: Collects log data from Windows 10 and sends it to Splunk Enterprise for analysis.

- Pardus: Hosts Splunk Enterprise to centralize log collection and analysis.

- System Requirements: Specify the minimum system requirements for running these virtual machines, such as 4 GB of RAM and 50 GB of disk space.

## Windows 10 Virtual Machine Installation 

1.**Create a new Virtual Machine (VM):**
- Open VirtualBox and click on “New” to create a virtual machine. 
   - Name: Windows Server
   - Type: Microsoft Windows
   -Version: Windows 10 (64-bit)

2.**Allocate resources:**

   - Memory: 4096 MB (4 GB)
   -Hard Disk: Create a virtual hard disk (at least 50 GB)



3.**Mount the Windows Server ISO:**

   - Go to the VM settings -> Storage -> Load the Windows Server ISO file.

4.**Start the VM and follow the installation steps:**

   - Select language, time, and keyboard preferences.
 
  -  Click "Install Now".
 
 - Select the appropriate edition (e.g., Standard with GUI).
   
 - Accept the license terms.
 
 - Choose "Custom: Install Windows only (advanced)".

 - Select the unallocated space and click "Next" to install.

   ## Installing Sysmon and  Configuration on Windows
   
 1.**Download Sysmon:**

 - Download Sysmon from the Microsoft Sysinternals website.
 2.**Install Sysmon**

   - Extract  the Sysmon.zip file  to a folder on your computer.

  3.**Open Command Prompt as Administrator**

  4.**Run Sysmon.exe:**

 - Sysmon is a command-line tool, so you’ll need to run it via the Command Prompt. To install Sysmon with a configuration file, use the following command:
```
   sysmon -accepteula -i sysmonconfig.xml
```
5.**Create or download a configuration file:**

- The configuration file defines which events Sysmon will monitor.
   
 - You can download a recommended configuration file from SwiftOnSecurity’s GitHub page.

  - Save the sysmonconfig.xml file to the same folder where you extracted Sysmon.
   
6.**Verify Sysmon Installation and Operation**
 - To check if Sysmon is running correctly, use this command:

  ```
  sysmon -s
```
- This will show the status of Sysmon.

 - To view the event logs generated by Sysmon:

    - Open Event Viewer by searching for it in the Start menu, and navigate to Applications and Services Logs > Microsoft > Windows > Sysmon/Operational.

   7.**Configuration Sysmon**
   
 - Create or download configurations files:

     -  Configuration file from https://github.com/SwiftOnSecurity/sysmon-config

     -  Copy to file   sysmonconfig-export.xml to the Notepad ++
   
     -  Save the file type of  xml file name florian_config.xml

     -  Configuration file from https://github.com/olaf_harton/sysmon-modular

     - Copy to file sysmonconfig-research.xml To the Notepad++
      
     -  Save the file type of  xml file name Olaf_harton_config.xml
  - Install Sysmon with the config file
    
      - Run the command via CMD as Administrator
   
      - C:\Path of yor files\Downloads\Sysmon>Sysmon64.exe -h
   
      - C:\Path of yor files\Downloads\Sysmon>Sysmon64.exe -c Florian_config.xml
         - To see log on Splunk run whoami command
   
      - C:\Path of yor files\Downloads\Sysmon\Sysmon64.exe -c Olaf_harton_config.xml
   
         - To see log on Splunk run whoami command
        
      ## Splunk Forwarder On Windows
    1.**Download Splunk Universal Forwarder**

    -   Go to Splunk’s official website:Splunk Downloads page for Universal Forwarder.
    
    7.**Install Splunk Universal Forwarder**
     -  After downloading, double-click the .msi file to start the installation
   
     -  Follow the installation steps:
     -  Accept the license agreement and click "Next".
     - Choose the installation path (the default is usually fine) and click "Next".

     - When prompted, provide the administrator username and password (this will be used to manage the forwarder).
     - Choose Local system

     - select all Windows Event logs files
     - Receiving Indexer ip =Your Splunk enterprice Ip  and port 9997
     - Finish the installation

    3.**Configuration port**

     - Open Windows Defender Firewall
     -    Configure the outbound Rule
     -    Click on **"New Rule..."** in the right pane.

     -   Select **"Port"** and click **"Next"**.
     -    Choose **"TCP"** and enter `9997` in the **"Specific local ports"** field. Click **"Next"**.
     -   select **"Allow the connection"** and click **"Next"**.
     -   Choose when the rule applies (Domain, Private, Public) and click **"Next"**.
     -  Name the rule **"Splunk Forwarder Inbound Rule"** and click **"Finish"**.
     -  Configuration for the inbound Rule follow the same step
     
     - Launch the Splunk Enterprice
   
     - Click the Forwarder and Receving
     - click  the Configure Receving
     - Write port number :9997 .Save and enable the status
     
    4.**Verify the Rule**
    
      - Ensure that the new rule appears in the Inbound Rules and outbound rule list are  enabled.
      - Select "Launch Splunk Enterprise Services" to ensure it runs after installation
   
        ##  Installing and Configuring Trend Micro Vision One

        Before you begin, ensure you have the following:
- A valid Trend Micro Vision One subscription.
- Administrative access to the device where you will install the agent.
- Compatible operating system (Windows, Mac, or Linux).

  1.**Download the Agent**

 - Access the Trend Micro Vision One Console
   - Log in to your Trend Micro Vision One account.

  2. **Download the Agent:**
      -   Navigate to the **"Endpoints"** section.
      -   Select **"Add Endpoint"** and choose the appropriate agent for your operating system.
      -   Download the installation file.
 
  3. **Run the Installer:**
      - Double-click the downloaded `.exe` file to start the installation.
    
      -  Follow the Installation Wizard:
    
      -  Accept the License Agreement.
    
      -  Choose the installation folder or use the default location.
    
      -  Click **"Install"** to begin the installation process.

4. **Complete Installation:**
   - Once the installation is complete, click **"Finish"** to exit the wizard.
        



      
        

   

   

   

   

  
