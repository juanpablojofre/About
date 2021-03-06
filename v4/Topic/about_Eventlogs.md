---
title: about_Eventlogs
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b5279cd-daf1-4ed1-8575-2df4baf7042d
---
# about_Eventlogs
## TOPIC  
 about\_EventLogs  
  
## SHORT DESCRIPTION  
 [!INCLUDE[wps_1]()] creates a Windows event log that is named "[!INCLUDE[wps_2]()]" to record [!INCLUDE[wps_2]()] events. You can view this log in Event Viewer or by using cmdlets that get events, such as the Get\-EventLog cmdlet. By default, [!INCLUDE[wps_2]()] engine and provider events are recorded in the event log, but you can use the event log preference variables to customize the event log. For example, you can add events about [!INCLUDE[wps_2]()] commands.  
  
## LONG DESCRIPTION  
 The [!INCLUDE[wps_2]()] event log records details of [!INCLUDE[wps_2]()] operations, such as starting and stopping the program engine and starting and stopping the [!INCLUDE[wps_2]()] providers. You can also log details about [!INCLUDE[wps_2]()] commands.  
  
 The [!INCLUDE[wps_2]()] event log is in the Application and Services Logs group. The [!INCLUDE[wps_2]()] log is a classic event log that does not use the Windows Eventing technology. To view the log, use the cmdlets designed for classic event logs, such as Get\-EventLog.  
  
### VIEWING THE WINDOWS POWERSHELL EVENT LOG  
 You can view the [!INCLUDE[wps_2]()] event log in Event Viewer or by using the Get\-EventLog and Get\-WmiObject cmdlets. To view the contents of the [!INCLUDE[wps_2]()] log, type:  
  
```  
Get-EventLog -LogName "Windows PowerShell"  
```  
  
 To examine the events and their properties, use the Sort\-Object cmdlet, the Group\-Object cmdlet, and the cmdlets that contain the Format verb \(the Format cmdlets\).  
  
 For example, to view the events in the log grouped by the event ID, type:  
  
```  
Get-EventLog "Windows PowerShell" | Format-Table -GroupBy EventID  
```  
  
 Or, type:  
  
```  
Get-EventLog "Windows PowerShell" | Sort-Object EventID `  
          | Group-Object EventID  
  
```  
  
 To view all the classic event logs, type:  
  
```  
Get-EventLog -List  
  
```  
  
 You can also use the Get\-WmiObject cmdlet to use the event\-related Windows Management Instumentation \(WMI\) classes to examine the event log. For example, to view all the properties of the event log file, type:  
  
```  
Get-WmiObject Win32_NTEventLogFile | where `  
          {$_.LogFileName -eq "Windows PowerShell"} | Format-List -Property *  
  
```  
  
 To find the Win32 event\-related WMI classes, type:  
  
```  
Get-WmiObject -List | where {$_.Name -like "win32*event*"}  
```  
  
 For more information, type "Get\-Help Get\-EventLog" and "Get\-Help Get\-WmiObject".  
  
### SELECTING EVENTS FOR THE WINDOWS POWERSHELL EVENT LOG  
 You can use the event log preference variables to determine which events are recorded in the [!INCLUDE[wps_2]()] event log.  
  
 There are six event log preference variables; two variables for each of the three logging components: the engine \(the [!INCLUDE[wps_2]()] program\), the providers, and the commands. The LifeCycleEvent variables log normal starting and stopping events. The Health variables log error events.  
  
 The following table lists the event log preference variables.  
  
```  
        Variable                     Description  
        --------------------------   ----------------------------------------  
  
$LogEngineLifeCycleEvent     Logs starting and stopping of  
                                     Windows PowerShell.  
  
$LogEngineHealthEvent        Logs Windows PowerShell program errors.  
  
$LogProviderLifeCycleEvent   Logs starting and stopping of   
                                     Windows PowerShell providers.  
  
$LogProviderHealthEvent      Logs Windows PowerShell provider errors.  
  
$LogCommandLifeCycleEvent    Logs starting and completion of commands.  
  
$LogCommandHealthEvent       Logs command errors.  
  
```  
  
 \(For information about [!INCLUDE[wps_2]()] providers, type: "Get\-Help about\_providers".\)  
  
 By default, only the following event types are enabled:  
  
```  
$LogEngineLifeCycleEvent  
$LogEngineHealthEvent  
$LogProviderLifeCycleEvent  
$LogProviderHealthEvent  
  
```  
  
 To enable an event type, set the preference variable for that event type to $true. For example, to enable command life\-cycle events, type:  
  
```  
$LogCommandLifeCycleEvent  
  
```  
  
 Or, type:  
  
```  
$LogCommandLifeCycleEvent = $true  
```  
  
 To disable an event type, set the preference variable for that event type to $false. For example, to disable command life\-cycle events, type:  
  
```  
$LogProviderLifeCycleEvent = $false  
```  
  
 You can disable any event, except for the events that indicate that the [!INCLUDE[wps_2]()]engine and the core providers are started. These events are generated before the [!INCLUDE[wps_2]()]profiles are run and before the host program is ready to accept commands.  
  
 The variable settings apply only for the current [!INCLUDE[wps_2]()] session. To apply them to all [!INCLUDE[wps_2]()] sessions, add them to your [!INCLUDE[wps_2]()] profile.  
  
### LOGGING MODULE EVENTS  
 Beginning in [!INCLUDE[wps_2]()] 3.0, you can record execution events for the cmdlets and functions in [!INCLUDE[wps_2]()] modules and snap\-ins by setting the LogPipelineExecutionDetails property of modules and snap\-ins to TRUE. In [!INCLUDE[wps_2]()] 2.0, this feature is available only for snap\-ins.  
  
 When the LogPipelineExecutionDetails property value is TRUE \($True\), [!INCLUDE[wps_2]()] writes cmdlet and function execution events in the session to the [!INCLUDE[wps_2]()] log in Event Viewer. The setting is effective only in the current session.  
  
 To enable logging of execution events of cmdlets and functions in a module, use the following command sequence.  
  
```  
Import-Module <ModuleName>  
$m = Get-Module <ModuleName>  
$m.LogPipelineExecutionDetails = $True  
  
```  
  
 To enable logging of execution events of cmdlets in a snap\-in, use the following command sequence.  
  
```  
$m = Get-PSSnapin <SnapInName> [-Registered]  
$m.LogPipelineExecutionDetails = $True  
  
```  
  
 To disable logging, use the same command sequence to set the property value to FALSE \($False\).  
  
 You can also use the "Turn on Module Logging" Group Policy setting to enable and disable module and snap\-in logging. The policy value includes a list of module and snap\-in names. Wildcards are supported.  
  
 When "Turn on Module Logging" is set for a module, the value of the LogPipelineExecutionDetails property of the module is TRUE in all sessions and it cannot be changed.  
  
 The Turn On Module Logging group policy setting is located in the following Group Policy paths:  
  
```  
Computer Configuration\Administrative Templates\Windows Components\Windows PowerShell  
User Configuration\Administrative Templates\Windows Components\Windows PowerShell  
  
```  
  
 The User Configuration policy takes precedence over the Computer Configuration policy, and both policies take preference over the value of the LogPipelineExecutionDetails property of modules and snap\-ins.  
  
 For more information about this Group Policy setting, see about\_Group\_Policy\_Settings \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=251696\).  
  
### SECURITY AND AUDITING  
 The [!INCLUDE[wps_2]()] event log is designed to indicate activity and to provide operational details for troubleshooting.  
  
 However, like most Windows\-based application event logs, the [!INCLUDE[wps_2]()] event log is not designed to be secure. It should not be used to audit security or to record confidential or proprietary information.  
  
 Event logs are designed to be read and understood by users. Users can read from and write to the log. A malicious user could read an event log on a local or remote computer, record false data, and then prevent the logging of their activities.  
  
## NOTES  
 Authors of module authors can add logging features to their modules. For more information, see "Writing a [!INCLUDE[wps_2]()] Module" in MSDN at http:\/\/go.microsoft.com\/fwlink\/?LinkID\=144916.  
  
## SEE ALSO  
 Get\-EventLog  
  
 Get\-WmiObject  
  
 about\_Group\_Policy\_Settings  
  
 about\_Preference\_Variables