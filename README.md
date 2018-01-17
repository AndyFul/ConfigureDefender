# ConfigureDefender 

Utility for configuring Windows 10 built-in Defender antivirus settings. 
It is a portable utility. Simply, unzip the ConfigureDefender.zip (rigth-click on the file and select Extract All), next run ConfigureDefender_x32.exe (Windows 32-bit) or ConfigureDefender_x64 (Windows 64-bit) from the extracted folder. 
 
ConfigureDefender utility is a GUI application to view and configure important Defender settings on Windows 10. It mostly uses PowerShell cmdlets (with a few exceptions). Furthermore, the user can apply one of three predefined settings: default, high, and child protection. Some settings require restarting the computer. 
 
The child protection is mostly set to block anything suspicious via Attack Surface Reduction, Controlled Folder Access, SmartScreen (set to block) and 0-tolerance cloud level - also Defender Security Center is hidden. 

ConfigureDefender utility is a part of Hard_Configurator project, but it can be used as a standalone application.  

.
 
Some important remarks on the possible ways used to configure Defender (for advanced users). 
 
Windows Defender settings are stored in the Windows Registry and most of them are not available form Windows Defender Security Center. They can be managed via:

 a) Group Policy Management Console (gpedit.msc, not available in Windows Home edition), 

 b) Direct Registry editing (manual, *.reg files, scripts). 
 
 c) PowerShell cmdlets (set-mppreference, add-mppreference, remove-mppreference, only Windows 8.1+). 

. 

Normally, Windows Defender stores most settings under the key (owned by SYSTEM):  
 
HKLM\SOFTWARE\Microsoft\Windows Defender 

They can be changed when using Defender Security Center or PowerShell cmdlets.  

. 

Administrators can use Group Policy Management Console to override those settings. Group Policy settings are stored under another key (owned by ADMINISTRATORS):  
 
HKLM\SOFTWARE\Policies\Microsoft\Windows Defender 

Group Policy settings do not delete the normal Defender settings. 
 
. 

The Direct Registry editing is usually made, under the second key (the first requires System Rights). 

Applying Defender settings by Direct Registry editing under the key:  

HKLM\SOFTWARE\Policies\Microsoft\Windows Defender 

is not recommended, on Windows editions which support Group Policy Management Console (for example PRO and Enterprise editions), because of some cons: 

a) Those settings are not recognized by Group Policy Management Console. 
 
b) They can temporarily overwrite Group Policy Management Console setup in the Registry, because they share the same Registry keys. Those changes are not permanent, because Group Policy configuration is not overwritten. 

c) After some hours, those settings are automatically and silently back-overwritten by Group Policy Refresh feature. 

d) Those settings cannot be changed via Defender Security Center (or PowerShell cmdlets), even if they are visible there (like folders and applications related to Controlled Folder Access). 
 
. 

In Windows 8.1+ Home edition, one can configure Defender settings (outside of the Defender Security Center), when using PowerShell cmdlets or via the manual Registry editing. This may confuse some users, so ConfigureDefender utility can remove the settings made via Direct Registry editing under the key:  
 
HKLM\SOFTWARE\Policies\Microsoft\Windows Defender 
 
That is required, because those settings would override ConfigureDefender settings. 
 
. 

ConfigureDefender utility may be used also on Windows 10 Professional and Enterprise editions, if Administrator did not apply Defender policies via Group Policy Management Console. Normally all those policies are set to 'Not configured'. So, if Administrator applied Defender policies, then they must be set first to 'Not configured' before using ConfigureDefender. Those settings can be found in Group Policy Management Console:  
 
Computer configuration >> Policies >> Administrative templates >> Windows components >> Windows Defender Antivirus. 
 
The tabs: MAPS, MpEngine, Real-time Protection, Reporting, Scan, Spynet, and Windows Defender Exploit Guard, should be examined.  

. 

 
The below list shows which settings are available in different Windows versions: 

.
 
At least Windows 8.1: Real-time Monitoring, Behavior Monitoring, Scan all downloaded files and attachments, Reporting Level (MAPS membership level), Average CPU Load while scanning 

.
 
At least Windows 10: Automatic Sample Submission, PUA Protection, Cloud Protection Level (Default), Cloud Check Time Limit. 

.
 
At least Windows 10, version 1607 (Anniversary Update): Block At First Seen. 
 
.
 
At least Windows 10, version 1703 (Anniversary Update): Cloud Protection Level (High level for Windows Pro and Enterprise), Cloud Check Time Limit (Extended to 60s). 
 
.
 
At least Windows 10, version 1709 (Creators Fall Update): Attack Surface Reduction, Cloud Protection Level (extended Levels for Windows Pro and Enterprise), Controlled Folder Access, Network Protection. 
