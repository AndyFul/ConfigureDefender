

# ConfigureDefender stable version 4.0.0.1 - July 2024
https://github.com/AndyFul/ConfigureDefender/raw/master/ConfigureDefender.exe

## Overview
ConfigureDefender is a small utility for configuring Windows 10/11 (and Windows Server) built-in Defender Anti-Virus settings. It is a part of the Hard_Configurator project (including source files), but it can be used as a standalone application (portable).

#### ConfigureDefender sources
https://github.com/AndyFul/Hard_Configurator/tree/master/src/


## Useful links
https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/attack-surface-reduction-rules-reference?view=o365-worldwide

https://medium.com/palantir/microsoft-defender-attack-surface-reduction-recommendations-a5c7d41c3cf8

https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction

https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/bg-p/MicrosoftDefenderATPBlog/label-name/Demystifying%20ASR%20rules


## Installation
ConfigureDefender is a portable application, no installation is needed. Download and run the executable ConfigureDefender.exe - the application can run both on Windows 32-bit and Windows 64-bit.

## Short program description
ConfigureDefender utility is a small GUI application to view and configure important Defender settings on Windows 10/11 and Windows Server 2019+. It uses PowerShell cmdlets (with a few exceptions) to change the Windows Defender settings. Furthermore, the user can apply one of three pre-defined protection levels: DEFAULT, HIGH, INTERACTIVE, and MAX. Changing one of the protection levels requires a reboot to take effect.

### Using the Maximum Protection Level
The MAX Protection Level blocks anything suspicious via Attack Surface Reduction, Controlled Folder Access, SmartScreen (set to block), and Cloud Level (set to block). These settings are very restrictive and using them can produce many false positives even in the home environment. Such a setup is not recommended in the business environment.
 
### Advanced Users
Some important remarks on the possible ways used to configure Defender (for advanced users). 

Windows Defender settings are stored in the Windows Registry and most of them are not available from Windows Defender Security Center. They can be managed by using:

* Group Policy Management Console (gpedit.msc is not available in Windows Home edition) 
* Direct Registry editing (manually, via *.reg files or scripts) 
* PowerShell cmdlets (set-mppreference, add-mppreference, remove-mppreference, PowerShell 5.0).
 
### Windows Defender Registry Keys
Normally, Windows Defender stores most settings under the key (owned by SYSTEM):  
* `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender`

The registry keys can be changed when using Defender Security Center or PowerShell cmdlets.

### Overwriting settings via Group Policy Management Console (GPO)
Administrators can use the Windows Group Policy Management Console (GPO) utility to override certain Windows Defender registry values. Group Policy settings are stored under another key (owned by ADMINISTRATORS):  
* `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender`

Keep in mind that GPOs do not delete the normal Defender settings!

### Manually changing WD settings via registry 
Registry editing is usually made, under the second key (see below), the first requires system privileges. 
Applying Defender settings by directly manipulating the registry under:
* `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender

is not recommended (!) on Windows editions that officially support Group Policy Management Console e.g. PRO & Enterprise editions. 
* Those settings are not recognized by the Group Policy Management Console.
* They can temporarily overwrite the GPO setup in the Registry because they share the same Registry keys. Those changes are not permanent, because Group Policy configuration is not overwritten. 
* After some hours, those settings are automatically and silently back-overwritten by the Group Policy Refresh feature. 
* Those settings cannot be changed via Defender Security Center (or PowerShell cmdlets), even if they are visible (like folders and applications related to Controlled Folder Access).
 
### Windows Home Editions
Under Windows Home editions, someone can configure Defender settings (outside of the Defender Security Center), when using PowerShell cmdlets or via the manual Registry editing method. This may confuse some users, but the ConfigureDefender utility can remove the settings made under the policy path: 
* `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender` 

This is required, because those settings would override ConfigureDefender settings.

### ConfigureDefender utility and GPOs
ConfigureDefender utility can be used on Windows Professional & Enterprise editions if an Administrator did not apply Defender policies via the Group Policy Management Console. Normally, all those policies are by default set to 'Not configured'. They can be found in the Group Policy Management Console:
* Computer configuration >> Policies >> Administrative templates >> Windows components >> Windows Defender Antivirus. 
 
The tabs: MAPS, MpEngine, Real-time Protection, Reporting, Scan, Spynet, and Windows Defender Exploit Guard, should be inspected before using ConfigureDefender. The corresponding policies have to be set to 'Not configured'. If not, then the GPO Refresh feature will override the settings applied via ConfigureDefender.

## Available Windows Defender settings on different Windows versions
Configuredefender requires Windows ver. 1809 or later.

The ASR rule "Block persistence through WMI event subscription" requires Windows ver. 1903 or later.

See also:
https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/attack-surface-reduction-rules-reference?view=o365-worldwide
