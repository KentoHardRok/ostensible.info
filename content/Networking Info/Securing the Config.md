

# Run down the file
First off I'm running down the Cisco suggested hardening guide and as I go through this I'll make not of the changes that need to occur as well as the steps necessary to get there.

### Centralize Log Collection and Monitoring 
First topic is that of logging and monitoring, centralize these two things. Enable authentication through a tacacs+ server... definitely on the to do list  but as of today, thats a problem for tomorrow.
Logging best practices dictate logging to a central service. to do that:
```cisco
logging-plane host
	management-interface
```
You also have configuration options to log to ATA flash that is peristent on reboot which is definitely useful but not the better options. To be fair you can also use this in conjunction with a central logging server.
Now for some logging things to avoid. No logging to console or monitor
```cisco
no logging console  
no logging monitor
```
As an alternative to logging to either console or monitor its suggested, if you must, to log to buffer to troubleshooting purposes. 
```cisco
logging buffered 16384 6
```
When logging its also importnant to controll what interfaces are sending logs and be sure to monitor that traffic. To that end set the logging source manually, preferably to the loopback interface which you should be using for management traffic.
```cisco
logging source-interface Loopback 0
```
a few other helpful commands to ensure your logs are accurate include.
```cisco
clock timezone PST -8  
service timestamps log datetime msec localtime show-timezone
```

### Use Secure Protocols when possible
Use the more secure protocols when given the option. i.e. SSH over telnet or SCP in stead of FTP or TFTP. These commands facilitate ssh and scp:
This configuration example enable ssh services:
```cisco
hostname router
ip domain-name example.com  
crypto key generate rsa modulus 2048  
ip ssh time-out 60  
ip ssh authentication-retries 3  
ip ssh source-interface GigabitEthernet 0/1  
ip ssh version 2
!  
line vty 0 4  
 transport input ssh  
````
This configuration example enables SCP services:
```cisco
ip scp server enable  
```
This is a configuration example for HTTPS services:
```cisco
crypto key generate rsa modulus 2048  
ip http secure-server
```

### Gain Traffic Visibility with netflow
Originially intended to export traffic to a management application, it can be used to monitor traffic real time.

### Configuration Management
So Cisco IOS has built into it a feature to locally hold backup configurations so that you can roll back when necessary. This is different than simply copying a configuration file as the rollback completely replaces the running configuration as opposed to adding on the additional commands. 
```cisco
archive  
 path disk0:archived-config  
 maximum 14  
 time-period 1440  
 write-memory
```
 This configuration example above adds an archive with a maximum amount of 14 backups completed daily (1440 min) as well as a backup each time write mem is completed
 Also important in config management is to ensure only one person can write to a device at any one time.
 ```cisco
 configuration mode exclusive auto
 ```
 least we forget to secure our boot image and config
 ```cisco
 secure boot-img
 secure boot-config
```
So one other config management consideration which is pretty helpful is to enable config change notifications.
```cisco
archive  
 log config  
  logging enable  
  logging size 200  
  hidekeys  
  notify syslog
```

### Management Plane 
Functions that achieve the managemnt goals of the network.

### Password Management
Required Commands:
```cisco
enable secret
service password-encryption
```

### Enhanced Password Security 
This feature was introduced in Cisco IOS 12.2(8) and it allows the passwords to be conigured with MD5 hashing, The requied commands are:
```cisco
username <name> secret <password>
```

### Login Password Retry Lockout 
This allows you to lock out a local user account after a configured number of unsuccesful login attempts. Once locked out, their account is locked until you unlock it. An authorized user with privelege level 15 cannot be locked out with this feature. Keep priv 15 users to a minimum. The required commands are:
```cisco
aaa new-model  
aaa local authentication attempts max-fail <max-attempts>
aaa authentication login default local
```
#### Important to estalished admin priv level with some limitations below 15

### No Service Password-Recovery
This does not allow anyone with console acess to insecurely access the device config and clear the password. It also does not allow malicious users to change the config registry value and access NVRAM. Required Commands are:
```cisco
no service password-recovery
```
this prevents the use of rommon on recovery and instead a backup of the config is suggested in case of emergencies. 

### Disable unused services
Turn off unused services... The TCP and UDP small services must be disabled. These services include:
* echo (port number 7)
* discard (port number 9)
* daytime (port number 13)
* chargen (port number 19)	
Fortunately these are turned off by default but instead there are a few other features that can be turned off. Rememeber that these are only suggestions on alternative services that are enabled and should be disabled only if they are not needed.
* `no ip finger` global configuration command in order to diable finger service
* `no ip bootp server` global config, disable bootstrap protocol (BOOTP)
* `ip dhcp bootp ignore` global config, to disable BOOTP although this leaves DHCP serves enables
* `no service dhcp` global config, to disable DHC relay services if they are not needed.
* `no mop enabled` interface config, to disable maintenance operation protocol
* `no ip domain-lookup` global config, to disable DNS services
* `no service pad` global config, to disable Packet Assembler/Disassembler (PAD), used for x.25 networks
* `no ip http server | no ip http secure-server` global config, to disable http ad https servers respectively.
* `no service config` global config, unless the device pulls its config from the network during startup, this command *MUST* be used. This prevents the IOS device from an attempt to locate a configuration file on the network.
* `no cdp enable` interface config, CDP must be diabled on all interfaces touching untrusted networks. `no cdp run` global config, can also be used to disable cdp globally. 
* `no lldp transmit & no lldp receive` interface config, this is the same threat and rationale as cdp usage. also `no lldp run` isused to disable it globally if not used at all.

### EXEC Timeout
this is used to set the interval the exec command waits for user input before it terminates the session. 
```cisco
line con 0  
exec-timeout <minutes> [seconds]  
line vty 0 4  
exec-timeout <minutes> [seconds]
```

### Keepalive for TCP sessions
Enabling TCP keepalives both in and out of the device ensure the tcp connections remain active and half-opened or orphaned TCP connections are removed. The commands required are:
```cisco
service tcp-keepalives-in  
service tcp-keepalives-out
```

### Management Interface Use
Its important to use a configured loopback address for either in-bound or Out-of-bound management access. Physical interfaces ay go down but loopbacks are always up. Required commands are:
```cisco
interface Loopback0
	ip address 192.168.1.1 255.255.255.0
```


### Memory Threshold Notification
In order to mitigate low memory conditions on your cisco IOS device you should deploy:
```cisco
memory free low-watermark processor <threshold>
memory free low-watermark io <threshold> 
```
Memory Threshold Notification generates a log message in order to indicate that free memory on a device has fallen lower than the configured threshold. 
There is also a command used to be sure there is sufficient memory for delieverying critical notifications. 
```cisco
memory reserve critical <value>
```
These commands are concerned with your devices being overwhelmed by anyone of several attacks that could increase the memory usage of your IOS device.

### CPU Threshold Notification
Same idea as above, except for CPU threshold:
```cisco
snmp-server enable traps cpu threshold  
snmp-server host <host-address> <community-string> cpu   
!  
process cpu threshold type <type> rising <percentage> interval <seconds>   
     [falling <percentage> interval <seconds>]  
process cpu statistics limit entry-percentage <number> [size <seconds>]  
```

### Reserve memory for Consol Access
This reserves memory to assure you can access device via console in case of an emergency.
```cisco
memory reserve console 4096
```

### Enhanced Crashinfo File Collection
reclaims memory for crash info
```cisco
exception crashinfo maximum files <number-of-files>
```

### Network Time Protocol
Although not enherintly dangerous, it needs to be secured. Its important for IPSec as well as logging. All devices should agree on time information otherwise its difficult to correlate events with eachother. Suggested to use NTP authenti  here's how. 
Client:
```cisco
(config)#**ntp authenticate**  
(config)#**ntp authentication-key 5 md5 ciscotime**  
(config)#**ntp trusted-key 5**  
(config)#**ntp server 172.16.1.5 key 5**
```
Server:
```
(config)#**ntp authenticate**  
(config)#**ntp authentication-key 5 md5 ciscotime**  
(config)#**ntp trusted-key 5**
```

#### Here I will just remind you that ACLs exist and you should use them. There are examples of things to filter but ultimately this is something you have to decide on in your environment. 

### Aux Port access
line AUX has a lot of privleges that make it dangeous and it should be secured in most cases, and by secured I mean disabled. This is of course you dont intend to use it for things like password recovery. Here is how you do that:
```cisco
line aux 0  
 transport input none  
 transport output none  
 no exec  
 exec-timeout 0 1  
 no password
```

### Use TACACS+
Just use it already, it can be free. There are tutorials, use it for user/admin authentication on your network devices. Radius is also an option but it only encryps the password where as TACACS+ encrypts the whole TCP payload. Here are the commands needed to enable TACACS+ on a cisco device:
```cisco
aaa new-model  
aaa authentication login default group tacacs+ enable
!  
tacacs-server host <ip-address-of-tacacs-server>  
tacacs-server key <key>
```
the above configuration also allows for a secondary authentication method, enable is used but you can also fallback to local which would use your local username and password. 
##### Command Authorization
Gives you the ability to permit or deny commands entered by an administrator based on their priv level:
```cisco
aaa authorization exec default group tacacs none  
aaa authorization commands 0 default group tacacs none  
aaa authorization commands 1 default group tacacs none   
aaa authorization commands 15 default group tacacs none
```
##### Command Accounting
Sends information about each EXEC command that is entered: 
```cisco
aaa accounting exec default start-stop group tacacs   
aaa accounting commands 0 default start-stop group tacacs  
aaa accounting commands 1 default start-stop group tacacs  
aaa accounting commands 15 default start-stop group tacacs
```
##### also redundant servers ...
### SNMP services
Just use SNMPv3. Not 2 if you want to use it at all. SNMPv3 consists of three primary configuration options:

* **no auth** - This mode does not require any authentication nor any encryption of SNMP packets
* **auth** - This mode requires authentication of the SNMP packet without encryption
* **priv** - This mode requires both authentication and encryption (privacy) of each SNMP packet

This command configures a Cisco IOS device for SNMPv3 with an SNMP server group AUTHGROUP and enables only authentication for this group with the 
**auth** keyword:
```cisco
snmp-server group AUTHGROUP v3 auth
```
This command configures a Cisco IOS device for SNMPv3 with an SNMP server group PRIVGROUP and enables both authentication and encryption for this group with the **priv** keyword:
```cisco
snmp-server group PRIVGROUP v3 priv
```
This command configures an SNMPv3 user snmpv3user with an MD5 authentication password of **authpassword** and a 3DES encryption password of **privpassword**:
```cisco
snmp-server user snmpv3user PRIVGROUP v3 auth md5 authpassword priv 3des privpassword
````

### Management Plane Protection
Also an important part to this SNMP puzzle is the management plane protection.  Once MPP is enabled, only the interfaces identified as management may accpt management traffic. The command to do so is :
```cisco  
control-plane host  
 management-interface FastEthernet0/0 allow ssh snmp   
```

### Control Plane Hardening
Here are just a few commands to help do just that. Harden the control plane. Usually has to do with the way rouge packets and random pings are handled... or not.
#### IP ICMP Redirects
Filtering with an interface access list elicits the transmission of ICMP unreachable messages back to the source of the filtered traffic. The generation of these messages can increase CPU utilization on the device. In Cisco IOS software, ICMP unreachable generation is limited to one packet every 500 milliseconds by default
dont do it. 
```cisco
no ip icmp redirects
```
#### IP proxy arp
Proxy ARP is the technique in which one device, usually a router, answers ARP requests that are intended for another device. By "faking" its identity, the router accepts responsibility for routing packets to the real destination. Proxy ARP can help machines on a subnet reach remote subnets without configuring routing or a default gateway
dont do it
```cisco
no ip proxy-arp
```
This is an interface problem but i think that it can be done in both global and interface level. 

## Etcetera
So at this point this is all of the general OS hardening, There is a lot more than can and should be done with access lists but that really is something that should be tailored to your environment. The idea there is that you allow only what you need and block everything else. To be fair it does get much more complex than that.
