## What is Logging?

Logs are detailed lists of application information, system performance statistics, or user activities. Logs can be useful for keeping track of computer use, network activity, security issues, and error reports. Every activity in your environment, from emails to logins to firewall updates, is considered a security event.

Let’s cover some examples:

- **Logging user events in Windows Active Directory domains.** This allows us to see when accounts are logged in, incorrect password attempts, administrative account usage, when new accounts are created or deleted, etc. This is a good way to detect activities such as brute-forcing attacks against login credentials or password spraying attacks.
- **Logging network connections from firewalls** can allow us to detect port scanning or vulnerability scanning activity, denial-of-service attacks, and network issues.

we will cover the following important log types:

- **Syslog**
- **Windows Event Logs**
- **Other Logs**

---

## Syslog

Actions on many devices generate events that are logged locally for analysis, such as shutdowns, start-ups, processes, and connections. When you have a large number of devices, it becomes impractical to review these locally. System Logging Protocol (Syslog) is a standard protocol used to convey event or system log notification messages to a designated server, known as a Syslog server. 

The Syslog server centralizes data collection from various devices for analysis, review, and intervention.

The protocol can be enabled on most network equipment such as switches, routers and firewalls, and even endpoint devices. Syslog is available on Unix and Linux-based systems and many web servers. Windows systems use their own by default as opposed to Syslog (Windows Event Manager) – these can also be forwarded to a central server, via third-party utilities or other configurations using the Syslog protocol. 

Custom applications can also be developed to use Syslog for log transport.

Syslog uses **UDP 514** by default; TCP **514** can be used for more reliability; however, certain stricter security standards require that logs are securely transferred, so **TCP 6514** is used as a de facto standard, although not official. Take note that Syslog does not offer authentication or encryption built-in, so it may be susceptible to attacks.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f0be9badb2b7bb3ab87f5ef469c14a1bc5c6a5097513b16ce0decf740840dec30c1d72cce29320b64589084e1646.png)
### Syslog Messages

A Syslog message is made of three components; a Priority Value (PRI), a Header, and a Message. We will explain these three parts below.

**Priority Value (PRI)**

The Priority Value is derived from both the **Facility Code** and the **Severity Level.** We can use the simple equation to calculate PRI:  
`(facility code * 8) + Severity value = PRI.`

Below are the Facility Code and Severity Level tables.
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1ba4083ccb2c9b7e376f5444e1d52cde971b40bc15d1cc72128845f3344e06837c1b53dcadc0f1600d0ffdf24021.png)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/09cedee50e8e71644fc87895a159eb1d76a92b522fa64d0d3185bffb96331934a48863e76430b6196278120bab3e.png)

**Header**

This contains identifying information, such as; Timestamp, Hostname, Application name, Message ID. This is useful for understanding where the system message has come from.

**Message**

This could be simple readable text or only machine-readable. The content of the message is not defined by the protocol only the format is. Each message sent to the Syslog server has two labels associated with it that make the message easier to handle. The first label describes the function (facility) of the application that generated it. For example, mail servers typically log using the **mail** facility. The second label specifies the severity level. After these two labels, the action is specified. The action is usually a filename in the **/var/log** directory tree, in which the messages will be stored.

---

## Windows Event Logs

“Windows Event logs” or “Event Logs” are files in binary format (with .evtx extension) stored locally in the Windows directory of a computer with that operating system:

- **Windows 2000 to WinXP/Windows Server 2003**:  
    `%WinDir%\system32\Config*.evt`
- **Windows Server 2008 to 2019, and Windows Vista to Win10**:  
    `%WinDir%\system32\WinEVT\Logs*.evtx`

These logs keep a detailed record of the vast majority of events that have occurred on the system (hardware events, user logins, program execution and installation, etc.), allowing system administrators to keep track of everything that happens within a system during its execution and being able to diagnose and foresee potential issues.

Categories of **registered events** include:

- **Application:** Events logged by an application (Execution, Deployment error, etc.)
- **System:** Events logged by the Operating System (Device loading, startup errors, etc.)
- **Security:** Events that are relevant to the security of the system (Logins and logouts, file deletion, granting of administration permissions, etc.)
- **Directory Service:** This is a record available only to Domain Controllers, it stores Active Directory (AD) events.
- **DNS Server:** It is a record available only to DNS servers; logs of DNS service are stored.
- **File Replication Service:** Is a record available only for Domain Controllers, it stores Domain Controller Replication events.

### Security Event Logs

Security Event Logs are events stored by the system that contain information related to the “Windows Security audit policies”, which are used to allow precise control over any possible incident present in the system.  

Some of these elements are:

- **Account logon** events (valid and invalid sign-ons and sign-offs)
- **Account management** (creation, modification, interaction and deletion of user accounts)
- **Privilege use**.
- **Resource usage** (file creation, modification, interaction and deletion)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a34ca71740c218d02befb4906b42948e53184f53b0f387d5c9b13fdda11eca0580f7a7137f77ec4ab5cd305cc5de.png)

### Event Viewer

On Windows 10 we can view Windows Events using the Event Viewer. 

**Event Viewer** allows us to create custom search profiles, called “Custom Views”. We can easily use these to retrieve the event IDs we want from a system, removing all of the extra noise that we’re not interested in. Below we will walk you through creating a Custom View to look only for logon and logoff activity. Firstly, open Event Viewer and click on Custom Views on the left-hand side.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8c8be5b8581ce8674577184c8b1fe79bc965c9c5fed5430f81325465d0bafedbcfbb71a125d9110951977279877c.png)

We can see in the above screenshot that by default there is already one Custom View, named “Administrative Events”. On the right-hand side we can click “Create Custom View” to make our own filter. The below window will popup, allowing us to create the View. Below we will cover all of the properties we can set.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/86c9164eb9f0b9ebb53bc2eb3f43593ad94d251c5f25ad7db25a39209976c9cdc2c8457fd5126c5c6c7646b18296.png)

- **Logged:** Allows us to set a date range to retrieve logs from. We can set a custom range, or use the presets including “Any Time”, “Last Hour”, “Last 12 Hours”, “Last 24 Hours”, and “Last 7 Days”. This can be useful if a system is not connected to a SIEM, allowing us to retrieve specific event logs after a malware infection or security incident.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/cbb953a59101485834518c721915353b4ceb6aa5123169124b26910fd2621f54d5169ea1c5aa9396f682425d3148.png)

- **Event Level:** Allows us to select which event levels we want to filter on, which will provide us with different events based on the selected levels.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e22d405154166390f45b0bfff95461bdd149c5590f2433e38a709e6a03fd8964b83ef1d4ef103441a69af6ba9ebe.png)

- **By Log:** We can choose what logs we want to filter on. The below screenshot shows a hierarchy structure, where we can select logs at any level. In the below screenshot example, we’re only looking for Security and Systems event logs from Windows.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/59d8ec9d907ae18791e9512de0d01d00aaddf88802890ba4056f8acf73a9fa7c3f8e794db1f088e8305156923a2e.png)

- By Source: If we don’t want to select log groups, we can instead choose sources. These are specific areas of the operating system and applications. See the below screenshot for some examples of the source we can choose from.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3ae54e7fbdf856bdcd8014105698852c7d09ed7f8c3511bbc26290fd2116cd7b58a2f5dde4126eae2b7877983a70.png)  
 

- **Includes/Excludes Event IDs:** This section allows us to define exactly what event IDs we want to capture. We can enter in any Event IDs we want to retrieve by listing them, using a comma as a separator, for example: `56,991,4101,3314`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/13f6571442501090d0d05bbd6cf0b3987ce023f224d737b3c758036870f69cc249222c40cf57c9a3ce10d27a9cde.png)

- **Keywords:** We can look for specific keywords within Events. See the below screenshot for the options we can choose.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5ac11b7de15676c7a5e43808eff6d4cb748781e61e2f71d6b5d6bb8bbc20a8c1adf8c3130d0617b277b8f6adcaf4.png)

- User and Computers: This section lets us focus on specific users or systems, if other Windows systems are pushing their event logs to the system we’re viewing Event Viewer on. If there was a user named “KellyP” and we only wanted to investigate events related to them, we would use their user account name in the User field.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/02427364b3d37bc4f8877ee057210d423ebbeb7ee62ad6257c553c0f87c7d1d63f9141b2a334c25e44b5b0b5a5c7.png)

**Custom Views Example: Login Monitoring**

Just so that you fully understand how Custom Views can be used, let’s go through an example where we want to monitor employee login and logoff times. The following are events we need to consider for our View:

- **User Logon Successful –** 4624
- **Special Logon –** 4672
- **User Initiated Logoff –** 4647
- **User Logoff –** 4634

In the below screenshot you can see the settings we have set. We want to view all events associated with users logging in and out, over the past 24 hours.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/73c25d8717f1645071b7e1cf7a48e2361031b41d8e716b3c9be1dba69c2993825bf178ef827effbd3cf2c498dc31.png)

Next we’ll be prompted to provide a name, description, and where we want to save the View.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4fffaa5be1d6d8e6dbf8127e26e99a5b42d9d144caa604d165328dd1a938941bcbdd3770286734bd0ed9881e72f5.png)

Now the filter will show us only the event IDs we have defined. It’s worked! We can now see events related to user accounts logging in and out!

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/bde7b3cdbec0d4e79ac9e1db069b07123ace74a4290f6d425948006da13cef3bdd9e994ac80f0f57514ab4a4f492.png)

---

# Sysmon

Sysmon is a Windows system service and device driver that, once installed on a system, remains resident across system reboots to monitor and log system activity to the Windows event log. It provides detailed information about process creations, network connections, and changes to file creation time.
## Benefits and Capabilities

- Logs process creation with full command line for both current and parent processes.
- Include a session GUID in each event to allow correlation of events on the same logon session.
- Logs loading of drivers or DLLs with their signatures and hashes.
- Optionally logs network connections, including each connection’s source process, IP addresses, port numbers, hostnames, and port names.
- Detects changes in file creation time to understand when a file was really created. Modification of file create timestamps is a technique commonly used by malware to cover its tracks.
- Rule filtering to include or exclude certain events dynamically.

## Windows Event Logs vs Sysmon Logs

Some security professionals believe that Windows event logs are.. well.. terrible, and that Sysmon is a **much** better way to log information on Windows endpoints. Why? Because the formatting is nicer, and there’s just a ton more useful information compared to Windows event logs. Black Hills Information Security made a great YouTube video covering the use of Sysmon, and we recommend all students watch it at the following link: [https://youtu.be/9qsP5h033Qk?t=491.](https://youtu.be/9qsP5h033Qk?t=491.)

## Installing Sysmon

If you want to try out Sysmon on your Windows host or virtual machine, below is a quick guide on how to set it up! First, download Sysmon from the Sysinternals website [here](https://download.sysinternals.com/files/Sysmon.zip). Once you’ve extracted the folder within the Zip file, open a command prompt as administrator (Windows search bar > CMD > Right-click > Run as Administrator) and move to the location of the executable files. Use the command `**sysmon -i**` to begin the install, and click Agree when the EULA pops up.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0f4c9d435a157a14c08002ce804ce2cca2a7e35ecf74f54d64b49043db9775a8e4005aee9fd33e353ec4893d43c8.png)

Now Sysmon is installed! Easy right? Now we want to look at Sysmon logs alongside Windows Event Logs in the tool Event Viewer. Press the Windows start button, search for “Event Viewer” and open the application.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5ad642c342006dfbcbfdf1042adb95078f9de5aa41823c67f2954006a4ae6e5e8bf028c2eb3e8214954dfc7f6dd1.png)

To actually see Sysmon logs, we need to create a Custom View – something we covered in the previous lesson. Click “Create Custom View” on the right-hand side, and copy what we’ve done in the below screenshot.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4b947ae91efa4548d01414e0575707f1906a5452920339c0725587bd88d0bc6ca03b022980f5f7a8b14b366b08cf.png)

We also want to tick all of the Event Level options to ensure we can see all Sysmon logs.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8c076f39514cf15e5bc106ca85c653a6aec460cbff050435125283a871dcb657a8726fc6aeaa9c8886bceee96506.png)

Name the View whatever you want – we’ve decided to go for the simple name “Sysmon View”, and click OK. We can now see Syslog logs, and boy do they contain a lot of information!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ab9e49e31cbc2ffa01e0baa2fddfc20b8524317f1de206d39175729fda0be54707a890f75c031253ae249d16b2ec.png)

In an organization, we could then feed this into our SIEM to provide additional detailed logs from Windows endpoints, working alongside Windows Event Logs! The problem with Sysmon is that it’s very broad, and can generate a lot of noise, something we don’t want to fill our SIEM up with. To combat this, we can use Sysmon configuration files, that work to reduce logs that aren’t really necessary, allowing us to focus on the logs that we really need to monitor.

An example of a Sysmon configuration file can be found here – [https://github.com/SwiftOnSecurity/sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config)  
Take a look! The file has lots of comments and explanations, meaning it can also act as a tutorial on the important logs for monitoring.

---

# Other Logs

Cloud providers such as Microsoft Azure and Amazon Web Services use their own methods for logging and monitoring, called an Application Programming Interface, or API. We will also cover OSQuery for endpoints, and Moloch for network traffic capture and indexing.
## Microsoft Azure

Microsoft Azure is one of the most commonly used cloud services in the world. Because of the large adoption of Azure, it is important to have general knowledge on how to navigate logging and monitoring in Azure. Logs in Azure, are primarily monitored through [Azure Monitor](https://azure.microsoft.com/en-us/services/monitor/#features) and [Log Analytic Workspaces](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/manage-access).

Azure Monitor is able to pick up logs from a multitude of different Azure services such as, virtual machines, virtual networks, Azure Active Directory, and Azure Security Center, as well as on-premises services. Azure has three primary categories of logs: Control/Management logs, Data Plane logs, and Processed Events. These logs are fed to Azure through the Azure REST API, the Microsoft Graph API, JSON, and various other sources. Azure logs can also be connected to different kinds of SIEMs such as Splunk or even Microsoft’s own Azure Sentinel.

When investigating logs in Azure, you will need to use the [Kusto Query Language (KQL)](https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/query-language) to query logs. While the details of KQL are out of scope for this exam, it is something to be aware of, if you are tasked with monitoring logs inside of an Azure environment. The below screenshot is an example of a KQL query.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3b398bb0de107853ba98615fe0caf9fc7857dee44b8e64925eedf85bc239ea8297416447a576dd3cf3ebe29ec0b0.png)
## Amazon Web Services

AWS is huge. Like, seriously, freaking massive. While the GUI offers an easy way to access and manage resources, Amazon uses their own API for AWS, which is extremely extensive.

AWS provides monitoring capabilities, and this call instructs AWS to enable this monitoring. The AUTHPARAMS part is a stand-in for the information that AWS uses to implement security in its API. Know that this call has the appropriate security mechanisms in place to ensure its execution.
## OSQuery

Osquery is a universal endpoint agent that was developed by Facebook in 2014. It is an active and growing open source [project on GitHub](https://github.com/facebook/osquery), with 230 contributors and over 90 releases to date.

According to the official osquery docs, osquery (os=operating system) is an operating system instrumentation framework that exposes an operating system as a high-performance relational database. Using SQL, you can write a single query to explore any given data, regardless of the operating system.

This is a unique approach in the security landscape, creating one agent for many operating systems, leveraging a standard query language instead of creating a proprietary one, and collecting rich data sets which have broad applications. 

With that said, osquery is just an agent – “an instrumentation framework” for data collection. Security teams looking to put osquery into production and leverage the data for security protocols will need to consider:  

1. How you’ll configure, deploy, and manage the agent
2. How you’ll manage query packs (more on these below) and schedules as the community adds more
3. Where you’ll store osquery data (and how much it will cost)
4. How you’ll analyze the data – i.e., what problems are you looking to solve? What questions do you need to ask?
5. How you’ll handle suspicious activity that requires further investigation or remediation
6. Whether you need any integrations with existing tooling
7. How you’ll troubleshoot production issues and develop any custom functionality you may need
# Moloch (Arkime)

Moloch, renamed to Arkime, augments your current security infrastructure to store and index network traffic in standard PCAP format, providing fast, indexed access. An intuitive and simple web interface is provided for PCAP browsing, searching, and exporting. Moloch exposes APIs which allow for PCAP data and JSON formatted session data to be downloaded and consumed directly. Moloch stores and exports all packets in standard PCAP format, allowing you to also use your favorite PCAP ingesting tools, such as Wireshark, during your analysis workflow.

Moloch is built to be deployed across many systems and can scale to handle tens of gigabits/sec of traffic. PCAP retention is based on available sensor disk space. Metadata retention is based on the Elasticsearch cluster scale. Both can be increased at any time and are under your complete control.

---

# Log Aggregation Explained

Log aggregation is the process of collecting logs from multiple computing systems, parsing them, extracting structured data, and putting them together in a format that is easily searchable and explorable by modern data tools.

**There are four common ways to aggregate logs, and many log aggregation systems combine multiple methods. These include:**
## Syslog

- A standard logging protocol. Network administrators can set up a Syslog server that receives logs from multiple systems, storing them in an efficient, condensed format that is easily queryable. Log aggregators can directly read and process Syslog data.
## Event Streaming

- Protocols like SNMP, Netflow, and IPFIX allow network devices to provide standard information about their operations, which can be intercepted by the log aggregator, parsed, and added to central log storage.
## Log Collectors

- Software agents that run on network devices, capture log information, parse it and send it to a centralized aggregator component for storage and analysis.
## Direct Access

- Log aggregators can directly access network devices or computing systems, using an API or network protocol to directly receive logs. This approach requires custom integration for each data source.

# Data Types

When considering the data that is being pulled into a SIEM platform, there are two categories; structured data, and unstructured data.

- **Structured data:** These are usually logs for Apache, IIS, Windows events, Cisco logs, and some other manufacturers. They have clearly-defined fields (such as “`src_ip`“) and are similar to other structured logs, making them relatively easy to parse and normalize.
- **Unstructured data:** This type of logging typically comes from a custom-built application where each message can be printed differently in different operations and the event itself can span multiple lines with no defined event start point, event endpoint, or both. This is likely to be the majority of the data being sent to the SIEM.

In order to get all logs to follow a similar format to make it easier to perform searches across a large set of different logs, where possible, we can use normalization techniques, which we will cover in the next section of this domain.

---