# ConfigureDefender ver. 2.0.1.1 August 2019

Utility for configuring Windows 10 built-in Defender antivirus settings. It is a portable utility. 

Warning!
Setting SmartScreen to Block via ConfigureDefender may prevent updating ConfigureDefender to the new version. This can happen, for
example, when using MAX Protection Level. It is recommended to change SmartScreen settings to 'Warn' before making an update, or change
the Protection Level to HIGH. 
It is also possible to unblock the executable and force SmartScreen to ignore it. Just do a right-click on ConfigureDefender executable
and choose Properties. Look at the Security entry in the bottom of the window and tick Unblock.

.

In the version 1.1.1.1, the option 'Real-time Monitoring' was removed, because of the new Microsoft criteria of malware detection.
With this option ConfigureDefender would be classified as a hack-tool.

.

Installation.

ConfigureDefender is a portable application. Download and next run ConfigureDefender_x86.exe (for Windows 32-bit) or ConfigureDefender_x64 (for Windows 64-bit). 

.

Short program description

ConfigureDefender utility is a GUI application to view and configure important Defender settings on Windows 10. It mostly uses PowerShell cmdlets (with a few exceptions). Furthermore, the user can apply one of three predefined Protection Levels: Default, High, and Max. After changing the settings the computer has to be rebooted. 


The Max Protection Level blocks anything suspicious via Attack Surface Reduction, Controlled Folder Access, SmartScreen (set to block) and cloud level (set to block) - also Defender Security Center is hidden. 


ConfigureDefender utility is a part of Hard_Configurator project, but it can be used as a standalone application.  

.
 
Some important remarks on the possible ways used to configure Defender (for advanced users). 
 
Windows Defender settings are stored in the Windows Registry and most of them are not available form Windows Defender Security Center. They can be managed via:

 a) Group Policy Management Console (gpedit.msc, not available in Windows Home edition), 

 b) Direct Registry editing (manual, *.reg files, scripts). 
 
 c) PowerShell cmdlets (set-mppreference, add-mppreference, remove-mppreference, PowerShell 5.0). 

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

In Windows 10 Home edition, one can configure Defender settings (outside of the Defender Security Center), when using PowerShell cmdlets or via the manual Registry editing. This may confuse some users, so ConfigureDefender utility can remove the settings made via Direct Registry editing under the key:  
 
HKLM\SOFTWARE\Policies\Microsoft\Windows Defender 
 
That is required, because those settings would override ConfigureDefender settings. 
 
. 

ConfigureDefender utility may be used also on Windows 10 Professional and Enterprise editions, if Administrator did not apply Defender policies via Group Policy Management Console. Normally all those policies are set to 'Not configured'. So, if Administrator applied Defender policies, then they must be set first to 'Not configured' before using ConfigureDefender. Those settings can be found in Group Policy Management Console:  
 
Computer configuration >> Policies >> Administrative templates >> Windows components >> Windows Defender Antivirus. 
 
The tabs: MAPS, MpEngine, Real-time Protection, Reporting, Scan, Spynet, and Windows Defender Exploit Guard, should be examined.  

. 

 
The below list shows which ConfigureDefender settings are available in different Windows 10 versions: 

.
 

At least Windows 10: Real-time Monitoring, Behavior Monitoring, Scan all downloaded files and attachments, Reporting Level (MAPS membership level), Average CPU Load while scanning, Automatic Sample Submission, PUA Protection, Cloud Protection Level (Default), Cloud Check Time Limit. 

.
 
At least Windows 10, version 1607 (Anniversary Update): Block At First Seen. 
 
.
 
At least Windows 10, version 1703 (Anniversary Update): Cloud Protection Level (High level for Windows Pro and Enterprise), Cloud Check Time Limit (Extended to 60s). 
 
.
 
At least Windows 10, version 1709 (Creators Fall Update): Attack Surface Reduction, Cloud Protection Level (extended Levels for Windows Pro and Enterprise), Controlled Folder Access, Network Protection. 
