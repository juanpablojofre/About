---
title: about_Run_With_PowerShell
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9d9ca5f-eff9-4409-be9d-e43b5b4087eb
---
# about_Run_With_PowerShell
## TOPIC  
 about\_Run\_With\_PowerShell  
  
## SHORT DESCRIPTION  
 Explains how to use the "Run with PowerShell" feature to run a script from a file system drive.  
  
## LONG DESCRIPTION  
 Beginning in [!INCLUDE[wps_1]()] 3.0, you can use the "Run with PowerShell" feature to run scripts from File Explorer in Windows 8 and Windows Server 2012 and from Windows Explorer in earlier versions of Windows.  
  
 The "Run with PowerShell" feature is designed to run scripts that do not have required parameters and do not return output to the command prompt.  
  
 When you use the "Run with PowerShell" feature, the [!INCLUDE[wps_2]()] console window appears only briefly, if at all. You cannot interact with it.  
  
 To use the "Run with PowerShell" feature:  
  
 In File Explorer \(or Windows Explorer\), right\-click the script file name and then select "Run with PowerShell".  
  
 The "Run with PowerShell" feature starts a [!INCLUDE[wps_2]()] session that has an execution policy of Bypass, runs the script, and closes the session.  
  
 It runs a command that has the following format:  
  
```  
PowerShell.exe -File <FileName> -ExecutionPolicy Bypass  
```  
  
 "Run with PowerShell" sets the Bypass execution policy only for the session \(the current instance of the PowerShell process\) in which the script runs. This feature does not change the execution policy for the computer or the user.  
  
 The "Run with PowerShell" feature is affected only by the AllSigned execution policy. If the AllSigned execution policy is effective for the computer or the user, "Run with PowerShell" runs only signed scripts. "Run with PowerShell" is not affected by any other execution policy. For more information, see about\_Execution\_Policies.  
  
 Troubleshooting Note: Run with PowerShell command might prompt you to confirm the execution policy change.  
  
## SEE ALSO  
 about\_Execution\_Policies  
  
 about\_Group\_Policy\_Settings  
  
 about\_Scripts  
  
 "Running Scripts" \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=257680\)