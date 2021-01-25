# Current ConfigureDefender version: 3.0.0.1 - June 2020

## Overview
ConfigureDefender is a small utility for configuring Windows 10 built-in Defender Anti-Virus settings. ConfigureDefender utility is a part of Hard_Configurator project, but it can be used as a standalone application (portable).
In June 2020 the executables were additionally signed with new certificate valid until June 2021.

## Useful links
https://medium.com/palantir/microsoft-defender-attack-surface-reduction-recommendations-a5c7d41c3cf8
https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction

### ConfigureDefender version 1.1.1.1 and below notice
In the version 1.1.1.1, the option 'Real-time Monitoring' was removed, because of the new Microsoft criteria of malware detection.
With this option ConfigureDefender would be classified as a hack-tool.

## Installation
ConfigureDefender is a portable application, no installation is needed. Download and run the executable ConfigureDefender.exe - the application can be run both on Windows 32-bit and Windows 64-bit.
The ConfigureDefender.zip archive is not required for using ConfigureDefender, but it can be useful when one wants to remove the unnecessary ConfigureDefender entries in the taskbar notification area cache.

## Short program description
ConfigureDefender utility is a small GUI application to view and configure important Defender settings on Windows 10. It uses PowerShell cmdlets, with a few exceptions to change the Windows Defender settings. Furthermore, the user can apply one of three pre-defined protection levels: `DEFAULT`, `HIGH`, and `MAX`. Changing one of the protection levels requires a reboot in order to take effect.

### Using the Maximum Protection Level
The MAX Protection Level blocks anything suspicious via Attack Surface Reduction, Controlled Folder Access, SmartScreen (set to block) and cloud level (set to block) - Defender Security Center is hidden.  
 
### Advanced Users
Some important remarks on the possible ways used to configure Defender (for advanced users). 

Windows Defender settings are stored in the Windows Registry and most of them are not available form Windows Defender Security Center. They can be managed via:

* Group Policy Management Console (gpedit.msc is not available in Windows Home edition) 
* Direct via Registry editing (manually, via *.reg files or scripts) 
* PowerShell cmdlets (set-mppreference, add-mppreference, remove-mppreference, PowerShell 5.0).
 
### Windows Defender Registry Keys
Normally, Windows Defender stores most settings under the key (owned by SYSTEM):  
* `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender`

The registry keys can be changed while using Defender Security Center or PowerShell cmdlets.

### Overwriting settings via Group Policy Management Console (GPO)
Administrators can use Windows Group Policy Management Console (GPO) utility to override certain Windows Defender registry values. Group Policy settings are stored under another key (owned by ADMINISTRATORS):  
* `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender`

Keep in mind that GPOs do not delete the normal Defender settings!

### Manually changing WD setting via registry 
Registry editing is usually made, under the second key (see below), the first requires system admin-rights. 
Applying Defender settings by directly manipulating the registry under:
* `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender

is not recommended (!) on Windows 10 editions which officially supporting Group Policy Management Console e.g. PRO & Enterprise editions. 
* Those settings are not recognized by Group Policy Management Console.
* They can temporarily overwrite Group Policy Management Console setup in the Registry, because they share the same Registry keys. Those changes are not permanent, because Group Policy configuration is not overwritten. 
* After some hours, those settings are automatically and silently back-overwritten by Group Policy Refresh feature. 
* Those settings cannot be changed via Defender Security Center (or PowerShell cmdlets), even if they are visible (like folders and applications related for Controlled Folder Access).
 
### Windows 10 Home Editions
Under Windows 10 Home editions, someone can configure Defender settings (outside of the Defender Security Center), when using PowerShell cmdlets or via the manual Registry editing method. This may confuse some users, but ConfigureDefender utility can remove the settings made under the following path: 
* `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender` 

This is required, because those settings would override ConfigureDefender settings.

### ConfigureDefender utility and GPOs
ConfigureDefender utility can be used on Windows 10 Professional & Enterprise editions, if an Administrator did not apply Defender policies via Group Policy Management Console. Normally, all those policies are by default set to 'Not configured'. If an administrator applied or changed Defender policies manually, he must first ensure that they are changed back to 'Not configured' before using the ConfigureDefender utility. Those settings can be found in Group Policy Management Console:
* `Computer configuration` >> `Policies` >> `Administrative templates` >> `Windows components` >> `Windows Defender Antivirus`. 
 
The tabs: MAPS, MpEngine, Real-time Protection, Reporting, Scan, Spynet, and Windows Defender Exploit Guard, should be inspected before using the utility, if some settings are switched ensure they are set back to the defaults. 

## Available Windows Defender settings on different Windows 10 versions
The below list shows which ConfigureDefender settings are available in different Windows 10 versions:

### All Windows 10 versions
* Real-time Monitoring
* Behavior Monitoring
* Scan all downloaded files and attachments
* Reporting Level (MAPS membership level)
* Average CPU Load while scanning
* Automatic Sample Submission
* Potentially unwanted applications (short: PUA Protection)
* Cloud Protection Level (Default)
* Cloud Check Time Limit 

### Introduced since Build 1607 (Anniversary Update)
* Block At First Sight (BAFS).

### Introduced since Build 1703 (Creators Update)
* Cloud Protection Level (High level for Windows Pro and Enterprise)
* Cloud Check Time Limit (Extended to 60s)

### Introduced since Build 1709 (Fall Creators Update)
* Attack Surface Reduction
* Cloud Protection Level (extended Levels for Windows Pro and Enterprise)
* Controlled Folder Access
* Network Protection
