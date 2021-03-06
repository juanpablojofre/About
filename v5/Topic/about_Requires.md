---
title: about_Requires
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 391781e3-b11e-40b6-aeb7-af98302e19b9
---
# about_Requires
## TOPIC  
 about\_Requires  
  
## SHORT DESCRIPTION  
 Prevents a script from running without the required elements.  
  
## LONG DESCRIPTION  
 The \#Requires statement prevents a script from running unless the [!INCLUDE[wps_1](../Token/wps_1_md.md)] version, modules, snap\-ins, and module and snap\-in version prerequisites are met. If the prerequisites are not met, [!INCLUDE[wps_2](../Token/wps_2_md.md)] does not run the script.  
  
 You can use \#Requires statements in any script. You cannot use them in functions, cmdlets, or snap\-ins.  
  
### SYNTAX  
  
```  
#Requires -Version <N>[.<n>]   
#Requires –PSSnapin <PSSnapin-Name> [-Version <N>[.<n>]]  
#Requires -Modules { <Module-Name> | <Hashtable> }   
#Requires –ShellId <ShellId>  
#Requires -RunAsAdministrator  
```  
  
### RULES FOR USE  
 \- The \#Requires statement must be the first item on a line in a script.  
  
 \- A script can include more than one \#Requires statement.  
  
 \- The \#Requires statements can appear on any line in a script.  
  
### PARAMETERS  
 \-Version \<N\>\[.\<n\>\]  
  
 Specifies the minimum version of [!INCLUDE[wps_2](../Token/wps_2_md.md)] that the script requires. Enter a major version number and optional minor version number.  
  
 For example:  
  
```  
#Requires -Version 3.0  
```  
  
 \-PSSnapin \<PSSnapin\-Name\> \[\-Version \<N\>\[.\<n\>\]\]  
  
 Specifies a [!INCLUDE[wps_2](../Token/wps_2_md.md)] snap\-in that the script requires. Enter the snap\-in name and an optional version number.  
  
 For example:  
  
```  
#Requires –PSSnapin DiskSnapin -Version 1.2  
  
```  
  
 \-Modules \<Module\-Name\> &#124; \<Hashtable\>  
  
 Specifies [!INCLUDE[wps_2](../Token/wps_2_md.md)] modules that the script requires. Enter the module name and an optional version number. The Modules parameter is introduced in [!INCLUDE[wps_2](../Token/wps_2_md.md)] 3.0.  
  
 If the required modules are not in the current session, [!INCLUDE[wps_2](../Token/wps_2_md.md)] imports them. If the modules cannot be imported, [!INCLUDE[wps_2](../Token/wps_2_md.md)] throws a terminating error.  
  
 For each module, type the module name \(\<String\>\) or a hash table with the following keys. The value can be a combination of strings and hash tables.  
  
```  
-- ModuleName. This key is required.  
-- ModuleVersion. This key is required.  
-- GUID. This key is optional.  
```  
  
 For example,  
  
```  
#Requires -Modules PSWorkflow, @{ModuleName="PSScheduledJob";ModuleVersion=1.0.0.0}  
```  
  
 \-ShellId  
  
 Specifies the shell that the script requires. Enter the shell ID.  
  
 For example,  
  
```  
#Requires –ShellId MyLocalShell  
```  
  
 \-RunAsAdministrator  
  
 When this switch parameter is added to your requires statement, it specifies that the [!INCLUDE[wps_2](../Token/wps_2_md.md)] session in which you are running the script must be started with elevated user rights \(Run as Administrator\).  
  
 For example,  
  
```  
#Requires -RunAsAdministrator  
```  
  
### EXAMPLES  
 The following script has two \#Requires statements. If the requirements specified in both statements are not met, the script does not run. Each \#Requires statement must be the first item on a line:  
  
```  
 #Requires –Modules PSWorkflow  
 #Requires –Version 3  
 Param  
(  
    [parameter(Mandatory=$true)]  
    [String[]]  
    $Path  
)  
...  
  
```  
  
### NOTES  
 In [!INCLUDE[wps_2](../Token/wps_2_md.md)] 3.0, the [!INCLUDE[wps_2](../Token/wps_2_md.md)] Core packages appear as modules in sessions started by using the InitialSessionState.CreateDefault2 method, such as sessions started in the [!INCLUDE[wps_2](../Token/wps_2_md.md)] console. Otherwise, they appear as snap\-ins. The exception is Microsoft.PowerShell.Core, which is always a snap\-in.  
  
## SEE ALSO  
 about\_Automatic\_Variables  
  
 about\_Language\_Keywords  
  
 about\_PSSnapins  
  
 get\-PSSnapin