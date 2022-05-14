+++
title = "PCNSA first time!"
weight = 61
+++

## Palo Alto
- Their policies focus on 3 principles
  - Securing the enterprise
    - Securing Operations response
      - Securing the cloud
      - Features that require licensing:
        - Logging
          - PAN-DB
          - Default IP address on the management of PaloAlto is 192.168.1.254
          - Three main concepts of Zero Trust are:
          - Access-control is on "need-to-know" basis and is strictly enforced
          - All resources are accessed in a secure manner, regardless of location
          - all traffic is logged and inspected
          - Application tags help content updates automate policy updates
          - configurations are saved as xml files
          - Palo Alto Networks operations platform is designed for three purposes
            1. Consume innovations quickly
            2. Prevent successful cyberattacks
            3. Focus on what matters

### PAN-DB 
          - Requires PAN-OS filtering license

### WildFire
##### This is malware protection suite
          - The minimum timeframe that can be set on a firewall to check for new WildFire signatures is:
            1. RealTime
            2. 1 Min
            3. 5 Min (publishing interval with wildfire license)
            4. 15 Min
    - Although is asked,  with a valid wildfire license the publishing interval is 5 minutes.
    - Wildfire can handle analysis of certain intrusions and some of the available verdicts are:
      - Malicious
      - phishing
      - grayware
      - benign
      - License with Wildfire allows you to get realtime updates vs Free tier you get update every 24hours and your limited to portable executable files (virus prevention is what gives you the 24hour updates)
  - There is a sandbox environment used to exploit and threats, dtonates the files and learns aboer to sent them.
  - In order for us to send files up to wioldfire first we need to enable sending decrypted information
      - under Servce > setup > then content ID, we see allow forwarding of decrypted content.
      - next we look at wildfire there

### Threat Prevention Subscriptions!
      - If you have a threat prevention subscription but no wildfire license then you must wit 24-48 hours for the wildfire signatures to be added
      - App-ID and Threat and application updates within as little as 30 minutes

      | Dynamic update | Time / Frequency |
      |---|---|
      | Antivirus | 24 hours, WildFire - Signatures updates every 5 minutes with subscription (requires threat prevention license) |
      | Applications (Ap-ID) | Only on the third Tuesday of each month, requries support contract|
      | Applications and Threats | Firewall can retrieve updates in as little time as 30 minutes of availability | 
      | GlobalProtect Data File | Containes vendor specific information for defining and evaluating (GlobalProtect Gateway subscription required) |
      | Global Protect Clientless VPN | Install latest updates and requires GlobalProtect Subscription | 
      | WildFire | Can be set to pull down updates as frequently as 1 minute, without subscription you must wait 24 hours |
      | WF-Private | Near Real-Time malware and antivirus signatures created as a result of analysis done by wildfire |

      - New and modified threat signatures and modified applications are published **weekly**



### Panorama 
##### This is the WebGUI included in Palo Firewalls

### Aperature 
##### This focuses on SaaS and interconnecting services
      - This protects cloud based applications such as dropbox and salesforce by administratering permissions and scanning file for sensitive information.


### DNS Inspection
      - To implement DNS securit inspections of traffic is to configure an anti-spyware security profile with dns remediations and to add an anti-spyware security pofile with DNS remediations to a security policy

### Prisma
##### Prisma™ Access protects your applications, remote networks and mobile users in a consistent manner, wherever they are. A cloud-delivered architecture connects all users to all applications, whether they’re at headquarters, branch offices or on the road.
      - Deployed Globally

### Cortex
#### Cortex Lake
      - Collect, transform and integrate your enterprise’s security data to enable Palo Alto Networks solutions.
#### Cortex XDR
      - AI:ML driven security fed by Cortex Lake

### GlobalProtect
##### VNP service for palo
      - provide work security for mobile endpoints by inspecting traffic deployed as internet gateways

### Auto Focus
      - Cloud Delivered security service which provides instant access to community-based threat data

### Application Filters
      - Options for this include: 
        - Category
        - Subcategory
        - Technology
        - Risk
        - tags
        - Characteristic
        - It enbles an administrator to dynamicall categorize multiple applications
        - Application fulters can be dynamically updated when a new App-ID is created by Palo Alto

### Logging
        - **Shadowing**: This happens when you try to commit a rule when there is already  a similary matching rule, this results in a warnining. 

### App ID
                  - When you are dynamically updating App-ID, after you downoad the updates but before you perform the actual install you need to Review both the Apps and the Policies as well. 
                  - Characteristic of an application:
                    - excessive bandwidth sue
                      - evasive
                      - After downloading or after installing an APP-ID update can you determine if it will affect an existing policy rule
                      - to minimize the risk after installing new APP-ID updates you should disable new apps in content!
                      - In a Single-Pass Parallel Processing (SP3) there are two components:
                        - User-ID
                          - App-ID
                          - App-ID updates: existing security policy rules are not affected by application content updates and after an application content update, new applications are automatically identified and classified
                          - To minimize risk when installing new App-ID definitions you should disable new apps in content

### Security Policies
                          - pre-NAT IP, post-NAT zone is something helpfl to remember in configuring Security policies
                          - Default: **Intrazone**, **interzone**
                            - Common others: Universal zone
                            - To log on the default deny, you can use the overide button at the button and then add logging, once thats done there is a little gear next to the polixy icon. 
                            - Implicit dependancy does not require the dependant application to be added in the security policy
                            - explicit dependency does require the dependant application to ve added i th esecurity policy
#### Policy Optimizer
                            - Policy optimzer does not analyze the usage of existing App-IDs in Security Policy rules
                              - Rules without app control are policies that are not monitoring apps Although they are being monitored. 
                                  - Create Cloned Rule simply creates a rule with the application list specified. 
                                  - Security rules are inside of policies and Profile are inside of rules
                                  - Profiles are used in policies/ rules that set as allowed and the profile acts as a last check before it is finally allowed! 

#### Profile > Rule > Policy
                                  So Under Policies you find security, NAT, QOS etc. From here you can create a new rule, for example under security. In security you can pick the zone as wel las any particular IP addresses within the zone, and you can apply profiles to that traffic. The Profiles are those outlined below; Vulnerability protection, Anti-Spyware , URL Filtering, Wildfire, file Blocking, Data filtering, and antivirus. 

### Security Profiles
                                  - These are kept under objects, under security profiles.
                                  - Types include: 
                                    - URL Filtering
                                      - Antivirus
                                        - Anti-Spyware
                                          - Vulnerability

### URL Filtering
                                          - URL filtering actions include:
                                            - **Alert**: website allowed but logged
                                              - **Allow**: website is allowed and no logging
                                                - **Block**: The website is blocked and the user will see a response page and will not be able to conitnue to the site
                                                  - **Continue**: the user will be prompted with a response page indicating the company policy has blocked the site but they may continue if they want. typically used if a sight is beinign but could be categorized differently
                                                    - **Override**: requires a URL admin password for access
                                                      - **none**: custom url catgeory

### Vulnerability Profile
                                                      - This includes but not limited to:
                                                        1. SQL Injection
                                                          2. Protocol Anamolies
                                                            3. Buffer Overflow
                                                            - Avaialble actions include:
                                                              1. Default
                                                                2. Allow
                                                                  3. Alert
                                                                    4. Drop
                                                                      5. Reset Client
                                                                        6. Reset Server
                                                                          7. Reset Both
                                                                            8. Block IP 
                                                                            - Two benefits of vulnerability protection are:
                                                                              - Prevent unauthorized access to systems
                                                                                - prevent exploitation of systems flaws

### Anti-Spyware Profile
                                                                                - This includes but not limited to;
                                                                                  1. Unwarranted connection
                                                                                  - DNSSinkhole action enables the Anti-spywhere profile to forge a response to a DNS qiery for a known malicious domain or to a custom domain, so that you can identify hosts on your network that have been indected with malware. 2 Signtures available to identify these threats:
                                                                                    1. Local DNS Signatures (requires Threat Prevention license)
    2. DNS Security signatures (requires DNS Security) Check Palo Alto Cloud for up to date signatures 
    - This really comes down to protecting access to specific resources, usualy C2 (Command and control)
    - The way they do this is by sending radom acces requests to a sinkhole which is basically an empty site ,or false site

### File Blocking Profile

### Data Filtering Profile


### Antivirus Security Profile
    - Available actions include:
      - Allow
        - Alert
        - Threat Prevention License is required for this
         
### Zone Based Security
        - Zone Protection profiles can mitigate attacks based on packet count
        - Layer 3 Aggregate interface types are part of a layer 3 zone 
        - A Zone protection profile can be applied to an ingress zone

### External Zone
        - this refers to the zones in reference to virtual ssytems (or firewall virtual instances). A an external virtual system is in  an external zone. There are no interfaces in an external zone for this reason for this reason some protection profiles are not supported. 

### User Based Security
        - Two features can be used to tag a username to be included in a dynamic user
          - User-ID Windows-based agent
            - XML-API
            - Two pre-defined user roles are:
              - Device Administrator
                - SuperUsers

### URL Classification
                - URLs are processed in this order:
                  1. Block List
                    2. Allow List
                      3. Custom URL Categories
                        4. External Dynamics List
                          5. Download PAN-DB File
                            6. PAN-DB Cloud

### Best Practices
                            - Logging should be done at Session End but disables at session start

### Interface Types
                            General: 
                              Interface zone under advacned includes: Link Speed, link Duplex, and Link State
                              - ###### Layer 2 interfaces:
                                - Forwarding of spanning tree bpdu
                                  - traffic shaping via QOS
                                    - traffic examination
                                      - Still possible to implement layer 3 policies
                                        - VLAN interface
                                        - ##### Tap Inteface
                                          - these are used for SPAN or mirror port interfaces
                                          - ##### L3 Interface
                                            - They can have more than one IP address assigned to it
                                              - Three advanced settings available on layer 3 interfaces:
                                                  - link duplex configuration
                                                      - NDP configuration
                                                          - link speed configuration
                                                          - ##### Virtual Wire: 
                                                            - Just a passthrough interface, typically would require two interfaces to pass rtaffic
                                                              - the two actions which a virtual wire can take are NAT and Log traffic

### BPA - Best Practices Assesment Tool
                                                              - There are 3 primary categories
                                                                - DOS Protection
                                                                  - Security
                                                                    - Decryption
                                                                    - These two features normally do not achieve 100% adoption rate:
                                                                      - DNS Sinkhole
                                                                        - URL Filtering
                                                                        - This tool provides a percentage of adoption for  each assesment area
                                                                        - Heatmap provides adoption rate for:
                                                                          - WildFire
                                                                            - User-ID
                                                                              - File Blocking

### PPA - Prevention Posture Assesment
                                                                              - This provides a set of questionairs that help uncover security rrisk prevention gaps acrpss all areas of network and security architecture

### System Fucntions
                                                                              - DIPP (Dynamic IP and Port) Nat oversubscription is or can be either 1, 2, 4 or 8 depending on the mdoel
                                                                              - An authentication sequence must be configured for the firewall to acess multiple authentication profiles for external services to autenticatea non-local account
                                                                              - Starting in PAN 9.1 a new object type which is supported for use within the User Field of a Security policy rule is the Dynamic User Group
                                                                              - System named configuration snapshot that does not overwrite the default snapshot (.snapshot.xml)
  - The command "Load named configuration nsapshot" overwrites the current candidate configuration with: 
    1. A custom-named candidate configuration snapshot (instead of the default)
    2. current running configuration (running-config.xml)
    3. custom-named running confiugration that you imported
    - Service routes must be enables to allow a data plane interface to submit DNS quieres on behalf of the control plane.
      - A service route is a path from the interface to the service on the server, they can configure this globally for the firewall. 
#### Control Plane vs Data Plane
      - Control plane provides two management features of a firewall:
        - Reporting
          - Logging
            - Firewall Configuration   
            - When dealing with the Dataplane you are using the tabs across the top such as Network Tab
            - SP3: Single Pass Parallele Processing - Check everything only once
            - If there is an automatic commit feature, be sure to disable auto commit and prioritize content database installationsbefore committing
            - On a management plane is where the firewall provides configuration logging and reporting functions on a seperate processor !

### Firewall
            - Default administrative distance for static routes: 10
            - Traps can:
              - Stops malware, exploits, and ransomware before they can compromise endpoints  
                - Provides protection while endpoints are online and offline, on network and off  
                  - Coordinates enforcement with network and cloud security to prevent successful attacks  
                    - Detects threats and automates containment to minimize impact  
                      - Includes WildFire cloud‐based threat analysis service with your Trapssubscription  
                        - Integrates with the Palo Alto Networks Security Operating Platform

### User ID settings
                        - With NO Active-Directory, users should use a Captive Portal
                        - syslog can be used for IP-to-user mappings
                        - Dynamic Roles Include;
                          - Device Administrator
                            - Superuser
                            - Authentication Sequence allows you to configure multiple authentication profiles
                            - Dynamic Users allow you to create a policy that provides auto-remidation for anomalous user behavior and malicious activity
                            - Two features which can be used to tag a user name to be included ina dynamic user group are: 
                              - XML API
                                - User-ID Windows-based agent
                                - SAML users cannot be used to authenticate user traffic flowing throuh the firewalls data plane
                                - three methods od mapping usernames to IP addresses are:
                                  - Server monitoring
                                    - syslog
                                      - port mapping
                                      - Two features that can be used to tag a username so that it is included in a dynamic user group include XML API, and user-ID windows based agent
                                        - In cases where its difficult to tag a user either because of private VPN usage or 802.1x enabled devices you can use PAN-OS XML-API to capture login events and send them to PAN-OS

### IPSec site-to-site
                                        ![](https://www.nwexam.com/files/nwexam/download/PCNSA_FC_2019-06-12_15.png)

                                        Server Log Monitoring (2 seconds) and Enable session (  ) are incorrect default times
                                        ![[Pasted image 20220310103952.png]]


### HA setup
                                        - Failover events
                                          1. Internal Failure
                                            2. Monitored Path (setting up a health check)
    3. HeartBeat - used as amonitoring tool
      4. Health Monitoring
      - Priority in this HA settup up is the lower the score the better in terms of priority (default priority is 100)
  - There is an option for pre-empt to establish who is active and passive
  - HA links used to join those sites together. I dont know much about their setup
  - There are two links relevant to the HA pair:
    1. Control Link (HA-1)
    2. Data Link (HA-2)
  - The control link is usd to transport /sync the config, the heartbeat, and hellos
  - The Datalink is used to sync live sessions
  - In order for two devices to be in a HA link they must match:
    - Model
      - Version
        - Interfaces
          - Licensing
          - HA States:
            - Active
              - Passive
                - Tentative
                  - suspended
                  - Any changes made on the active firewall are replicated over the Control Link or the HA1 link because this is where configurations are synced.

### Cyber Attack Lifecycle

                  - Blockage of just one stage in the cyberattack lifecycle will protect a companys network from attack
                  1. **Reconnaissance**: 
                    - This is when research is done, attackers will identify their targets through publicily available means such as social media. This is mostly through human systems perspective.
                    2. **Weaponization and Delivery**
                      - Attackers will then determine which merethods to use in order to deliver malicious payloads. This includes exploit klts, speak phisihing, malicious links, or attachmentts and malvertising
                      3. **Exploitation**
                        - Attackers deploy and exploit against a vulnerable application or system, typically using an exploit kit or weaponized document. Thus giving them a foothold.
                        4. **Installation**
                          - After the foothold, attackers will install malware in order to conduct firther operations such as maintaining access, persistence and escalating privileges
                          5. **Command and Control**
                            - With malware installed, now attackers own both sides of the connection. This is where they control the system.
                            6. **Actions on the objective**
                              - This is where they exfil data, destroy things, deface web property etc. 
