# egwin
This repository compiles some commands, options, tools, and sys admin related topics on Windows. Without doubt, Windows remains a dominant Operating System on Home and Business desktops and laptops since Windows 1998 and Windows XP followed by Windows 7 and Windows 10/11. 

* [egwin](#egwin)
  * [File System](#file-system)
  * [Services](#services)
  * [System Information](#system-information)
  * [Windows Permissions](#windows-permissions)
  * [Utilities](#utilities)
  * [Security](#security)
 


## File System 

**FAT**: Earlier Microsoft Windows operating systems, removable disks, and floppy disks (3.5 inch, 5.4 inch) supported only the FAT file system. FAT means File Allocation Table. FAT16 and FAT32 volumes were limited to 4 GB and 32 GB, respectively; yes! You heard right. So, people must use NTFS (New Technology File System) to create volumes in sizes larger than 32 GB.   

**NTFS**: For magnetic disks, NTFS can help to ensure metadata integrity and reliability (using journaling, checkpoints), security (by setting access permissions), and support larger volumes up to Terabytes in sizes. [How does NTFS work?](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc781134(v=ws.10))     

[Alternate Data Streams (ADS)](https://www.malwarebytes.com/blog/news/2015/07/introduction-to-alternate-data-streams) are a file attribute on NTFS to write hidden data or hide data on the Windows system.     

---- 

## Services   

Type Services.msc in the search box or use computer Management to view Service and Applications.    

----

## System Information 

Getting windows system information is important like OSINT and for troubleshooting the problems.    

Type `msconfig` in the search box to open System Information app or widget. Check the Services and Tools tabs.   

Like msconfig, one can use many other commands and features.    
* System Information: msinfo32 - look for computer hardware-related information.     
* Command Prompt: cmd.exe - CLI to execute commands    
* Task Manager: taskmgr    
* Control Panel: control.exe     
* Computer Management: compmgmt.msc    
* Event Viewer: eventvwr - to view event logs of systems, applications, etc.    
* Performance Monitor: perfmon   
* Resource Monitor: resmon - shows CPU, Disk, Network and Memory usage information    
* Windows Registry: regedit or regedt32 -  a hierarchical database to store information necessary to configure the system for users, applications, and hardware devices.    

To See environment variables:    
1. msinfo32 => Software Environment => Environment Variables   
2. Control Panel => System and Security => System => Advanced system settings => Environment Variables
3. Settings => System => About => system info => Advanced system settings => Environment Variables

To get help on command use /? on cmd.exe    

```
C:\Users\Administrator>ipconfig  /?

USAGE:
    ipconfig [/allcompartments] [/? | /all |
                                 /renew [adapter] | /release [adapter] |
                                 /renew6 [adapter] | /release6 [adapter] |
                                 /flushdns | /displaydns | /registerdns |
                                 /showclassid adapter |
                                 /setclassid adapter [classid] |
                                 /showclassid6 adapter |
                                 /setclassid6 adapter [classid] ]
where
    adapter             Connection name
                       (wildcard characters * and ? allowed, see examples)
    Options:
       /?               Display this help message
       /all             Display full configuration information.
       /release         Release the IPv4 address for the specified adapter.
       /release6        Release the IPv6 address for the specified adapter.
       /renew           Renew the IPv4 address for the specified adapter.
       /renew6          Renew the IPv6 address for the specified adapter.
       /flushdns        Purges the DNS Resolver cache.
       /registerdns     Refreshes all DHCP leases and re-registers DNS names
       /displaydns      Display the contents of the DNS Resolver Cache.
       /showclassid     Displays all the dhcp class IDs allowed for adapter.
       /setclassid      Modifies the dhcp class id.
       /showclassid6    Displays all the IPv6 DHCP class IDs allowed for adapter.
       /setclassid6     Modifies the IPv6 DHCP class id.

The default is to display only the IP address, subnet mask and
default gateway for each adapter bound to TCP/IP.

For Release and Renew, if no adapter name is specified, then the IP address
leases for all adapters bound to TCP/IP will be released or renewed.

For Setclassid and Setclassid6, if no ClassId is specified, then the ClassId is removed.

Examples:
    > ipconfig                       ... Show information
    > ipconfig /all                  ... Show detailed information
    > ipconfig /renew                ... renew all adapters
    > ipconfig /renew EL*            ... renew any connection that has its
                                         name starting with EL
    > ipconfig /release *Con*        ... release all matching connections,
                                         eg. "Wired Ethernet Connection 1" or
                                             "Wired Ethernet Connection 2"
    > ipconfig /allcompartments      ... Show information about all
                                         compartments
    > ipconfig /allcompartments /all ... Show detailed information about all
                                         compartments
```

----

## Windows Permissions  

### File System Permissions 

On NTFS, a file or folder can be given Full Access, Write Access, Read or execute access to users created on the system.     


### Windows App Permissions    

[Windows 11/10 App Permissions](https://support.microsoft.com/en-us/windows/app-permissions-aea98a7c-b61a-1930-6ed0-47f0ed2ee15c)    
- What comes as a surprise to us is why and when it became normal to give permissions like "Allow elevation" and "App diagnostics"!     
- While tech companies, collect and share data, are they alone going to control and dictate terms of privacy and security?     
- Data exfiltration at the cost of using the so-called free apps and implicit consent to "Terms and Conditions" users do not read or are not shown prominently!    

----

## Utilities 

### Disk Fragmenter 
Disk Defragmenter analyzes local volumes and consolidates fragmented files and folders into a contiguous space on the volume. As a result, a system can access files and folders and save new ones more efficiently. By consolidating files and folders, Disk Defragmenter also consolidates a volume’s free space, making it less likely that new files will be fragmented. Not all files can be moved, like system files.    

### Volume Shadow Copy Service (VSS)  
Volume Shadow Copy Service (VSS) can be used to create a consistent shadow copy (System Disk backup), or a snapshot, or a point-in-time copy of the disk or a LUN (Logical Unit Number).   

Volume Shadow Copies are stored in the System Volume Information folder on each drive with protection enabled.   

### Powershell 


----

## Security   

Navigate Settings => Windows Security   

You can check a few Protection areas:    
* Virus & threat protection - live protection from Virus and ransomware using Windows Defender, current threats and scan options (Full, Quick, Custom)    
* Firewall & network protection - Windows Firewall settings for domain (domain controlled systems), public (external WiFi) and private networks (home) 
* App & browser control - under Exploit Protection, check [CFG, DEP, ASLR, SEHOP, Heap Integrity](https://github.com/rks101/egwin/blob/main/windows-exploit-protection.png) settings. 
* Device security - Core isolation, TPM related settings 
* Device performance and health

BLDE = [BitLocker](https://learn.microsoft.com/en-us/windows/security/operating-system-security/data-protection/bitlocker/) Drive Encryption is a data protection feature against theft and can provide Full Disk Encryption (FDE) with credentials. You can dual-boot a Windows 10/11 machine and check a 48-digit key required to access the BLDE-protected drive.    

[Recent Windows Security features](https://www.csoonline.com/article/564531/the-best-new-windows-10-security-features.html)     

[LOLBAS](https://lolbas-project.github.io/) - Living off the Land binaries, scripts, and libraries.    

---- 
