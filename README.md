# HOME SOC Setup With Windows-Linux(Pardus) -Splunk Enterprice -Universal Forwarder-Trend Micro

 "This project demonstrates the setup of a home Security Operations Center (SOC) using virtual machines running Windows 10, Pardus, and Kali Linux. The aim is to integrate security tools such as Sysmon, Splunk Forwarder, Splunk Enterprise, and Trend Micro Agent for real-time security monitoring and threat detection."
 
 ##  Technologies and Requirements
- VirtualBox (Installed )
    
- Windows 10: Hosts Sysmon, Splunk Forwarder, and Trend Micro Agent to monitor and forward security logs.

- Splunk Forwarder: Collects log data from Windows 10 and sends it to Splunk Enterprise for analysis.

- Pardus: Hosts Splunk Enterprise to centralize log collection and analysis.

- System Requirements: Specify the minimum system requirements for running these virtual machines, such as 4 GB of RAM and 50 GB of disk space.

## Windows 10 Server Virtual Machine Installation 

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

   ## Installing Sysmon and  Configuration on Windows Server
   
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
   8.**Install Sysmon with the config file**
    
      - Run the command via CMD as Administrator
   
      - C:\Path of yor files\Downloads\Sysmon>Sysmon64.exe -h
   
      - C:\Path of yor files\Downloads\Sysmon>Sysmon64.exe -c Florian_config.xml
         - To see log on Splunk run whoami command
   
      - C:\Path of yor files\Downloads\Sysmon\Sysmon64.exe -c Olaf_harton_config.xml
   
         - To see log on Splunk run whoami command
        
      ## Splunk Forwarder On Windows Server
    1.**Download Splunk Universal Forwarder**

    -   Go to Splunk’s official website:Splunk Downloads page for Universal Forwarder.
    
    2.**Install Splunk Universal Forwarder**
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
   - Configure and Enable the agent from Trend Micro Agent consol

## Trend Micro Vision One Integration with Splunk XDR

## Prerequisites

Before you begin, ensure you have:
- A running instance of **Splunk Enterprise**.
- Access to **Trend Micro Vision One** with administrative rights.
- The necessary credentials for both Splunk and Trend Micro.

---

### Step 1: Install Trend Micro Vision One for Splunk XDR

1. Navigate to the **Splunkbase Marketplace**.
2. Search for the app by entering "Trend Micro Vision One" in the search bar.
3. Find the **Trend Micro Vision One for Splunk XDR** integration and click **Install**.
4. Enter your **Splunk.com** username and password when prompted.
5. Agree to the terms and proceed with the installation.

### Restarting Splunk
Once the installation is complete, restart your Splunk instance to apply the changes:
- Go to **Settings > Server Controls** and select **Restart Splunk**.

After the restart, the app should be available in your Splunk dashboard.

---

### Step 2: Configure the Integration

### Obtaining Credentials from Trend Micro Vision One

1. Log in to your **Trend Micro Vision One Console**.
2. Navigate to **Administration > Third-Party Integration**.
3. Select **Trend Micro Vision One for Splunk XDR** and click on the **Copy** icons to obtain the **Endpoint URL** and **Authentication Token**.

### Configuring the App in Splunk

1. Go back to the **Splunk console**.
2. Open the **Trend Micro Vision One for Splunk XDR** app.
3. Paste the **Endpoint URL** and **Authentication Token** you copied from the Trend Micro console.
4. If your environment requires a proxy, configure the custom proxy settings.
5. Click **Save**.

You should see a confirmation message, indicating that the application settings have been updated and the connection to Trend Micro Vision One is successful.

---

### Step 3: Start Pulling XDR Data

After configuring the app, **Splunk will begin pulling new XDR data** from Trend Micro Vision One. Please note that **pre-existing XDR data will not be pulled** into Splunk. Allow some time for new data to appear.

### Modifying Data Input Settings

You can adjust various settings for data inputs:
- **Polling Interval**: Define how often Splunk pulls data from Trend Micro.
- **Index**: Choose where the XDR data will be indexed within Splunk.
- **Risk Level**: Set the minimum risk level for data collection. For example, setting it to "Low" ensures all events, regardless of risk, are pulled.

---

### Step 4: Analyzing Data in Splunk

You can run searches using the **Search tab** to view the raw logs that Splunk has collected. Additionally, the app supports the **Splunk Common Information Model (CIM)**, which allows you to normalize the data at search time.

### Creating Reports and Dashboards

Leverage Splunk’s **Data Model** to create compelling reports and dashboards based on your XDR data. T

### Step 5: Investigating Alerts

When viewing XDR data on the **Splunk dashboard**, you can view details such as:
- **Severity Score**: How critical the event is.
- **Model Name**: The security model or tool that flagged the event.

Click on any alert to be redirected to the **Trend Micro Vision One Workbench**, where you can initiate an investigation immediately.

---

### Conclusion

Integrating **Trend Micro Vision One** with **Splunk XDR** provides a powerful way to manage and investigate security incidents. 

### Additional Notes
- **Pre-existing Data**: The app does not pull historical XDR data, only new events.
- **Custom Dashboards**: After integrating, consider setting up custom dashboards for better visualization of critical events.
- **Proxy Configurations**: Ensure proxy settings are correctly configured if your environment requires it.

# Installing Splunk on Pardus (Linux)

In this guide, we'll walk through installing **Splunk Enterprise** on **Pardus**, a Linux distribution similar to Kali. This tutorial can also be applied to other Linux flavors such as **Ubuntu**.

---

## Prerequisites

Before we begin, ensure you have:
- **Pardus** or any other Linux flavor installed.
- Sufficient system resources (at least 2GB RAM recommended for testing purposes).
- An account on [Splunk.com](https://www.splunk.com) to download Splunk.

---

## Step 1: Download Splunk

1. Go to [Splunk.com](https://www.splunk.com) and log in or create an account.
2. Navigate to the **Downloads** section.
3. Download the **Linux** version of Splunk Enterprise (you'll get a 90-day free trial for testing purposes).
4. After the download, you should have a `.deb` package for Debian-based distributions like Pardus.

---

## Step 2: Install Splunk

Once the package is downloaded, follow these steps to install it:

1. **Open a terminal** and navigate to your **Downloads** directory:
    ```bash
    cd ~/Downloads
    ```
2. **List the files** to ensure the Splunk package is there:
    ```bash
    ls -l
    ```
    You should see the downloaded `.deb` file.

3. **Install Splunk** using `dpkg` (Debian Package Manager):
    ```bash
    sudo dpkg -i splunk_package_name.deb
    ```
   Replace `splunk_package_name.deb` with the actual filename of your downloaded package.

4. **Wait for the installation** to complete. It may take a few moments.

---

## Step 3: Start and Configure Splunk

Now that Splunk is installed, let's start the service and configure it:

1. **Navigate to the Splunk bin directory**:
    ```bash
    cd /opt/splunk/bin
    ```
2. **Start Splunk**:
    ```bash
    sudo ./splunk start
    ```

3. **Agree to the license** by pressing `Enter` to scroll through the terms, and type `yes` when prompted to accept.

4. **Set up admin credentials**:
    - **Username**: Choose a username (default is `admin`).
    - **Password**: Set a secure password.

---

## Step 4: Accessing Splunk Web Interface

Once Splunk starts, it will be available on **port 8000** of your local machine. To access it:

1. **Open your web browser**.
2. Navigate to:
    ```bash
    http://localhost:8000
    ```
3. **Log in** with the username and password you set earlier.

---

## Step 5: Enable SSL for Secure Communication (Optional)

By default, Splunk doesn’t use SSL for its web interface. Here's how you can enable SSL:

1. **Go to Settings** > **Server Settings** > **General Settings** in the Splunk web interface.
2. Enable **SSL** and save your changes.
3. **Restart Splunk** to apply the changes:
    ```bash
    sudo ./splunk restart
    ```
4. After the restart, access the web interface using:
    ```bash
    https://localhost:8000
    ```
5. You’ll receive a **self-signed certificate warning**. This is normal for local environments. Proceed by accepting the risk.

---

## Step 6: Verify Installation

To verify that Splunk is working correctly:
1. Go to the **Search** tab in the web interface.
2. Perform a basic search to ensure Splunk is collecting data.

---

## Conclusion

You've successfully installed and set up **Splunk Enterprise** on **Pardus (Linux)**. You can now start configuring Splunk to collect, index, and visualize your logs.


---

**Note**: The installation process for other Linux distributions like **Ubuntu**, **Debian**, and **Kali Linux** is nearly identical. Simply follow the steps outlined above.

Happy Splunking!

      
        

   

   

   

   

  
