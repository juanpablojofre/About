---
title: Registry Provider
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3c8013c-8caa-48d7-9feb-bfef0d95926e
---
# Registry Provider
## PROVIDER NAME  
 Registry  
  
## DRIVES  
 HKLM:, HKCU:  
  
## SHORT DESCRIPTION  
 Provides access to the registry keys, entries, and values in Windows PowerShell.  
  
## DETAILED DESCRIPTION  
 The Windows PowerShell Registry provider lets you get, add, change, clear, and delete registry keys, entries, and values in Windows PowerShell.  
  
 Registry keys are represented as instances of the Microsoft.Win32.RegistryKey class. Registry entries are represented as instances of the PSCustomObject class.  
  
 The Registry provider lets you access a hierarchical namespace that consists of registry keys and subkeys. Registry entries and values are not components of that hierarchy. Instead, they are properties of each of the keys.  
  
 The Registry provider supports all the cmdlets that contain the Item noun \(the Item cmdlets\), such as [Get\-Item](assetId:///0650f666-6d85-4b5f-ab57-34fd9b3d6f19), [Copy\-Item](assetId:///2c819aec-96c0-49e9-ae3e-9a57559ec99a), and [Rename\-Item](assetId:///cf036d63-7739-4f1c-ba54-d1049fbcf21d), except for the [Invoke\-Item](assetId:///38a9887b-ce1a-4bde-be4e-98012efae204) cmdlet. Use the Item cmdlets when you work with registry keys and subkeys.  
  
 The Registry provider also supports the cmdlets that contain the ItemProperty noun \(the ItemProperty cmdlets\). Use the ItemProperty cmdlets when you work with registry entries. You cannot use the cmdlets that contain the Content noun \(the Content cmdlets\) with the Registry provider.  
  
 Each registry key is protected by a security descriptor. You can use [Get\-Acl](assetId:///2a7eb90d-0ece-4fbe-bb33-f452d1af621d) to view the security descriptor of a key.  
  
## CAPABILITIES  
 ShouldProcess, UseTransactions  
  
## EXAMPLES  
  
### Navigating the Registry  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command sets the current location to the HKEY\_LOCAL\_MACHINE\\Software registry key:  
  
```  
set-location hklm:\software  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command gets an object that represents the current location:  
  
```  
get-location  
  
```  
  
### Managing Registry Keys  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command gets each immediate subkeys of the HKEY\_LOCAL\_MACHINE\\Software registry key:  
  
```  
get-childitem -path hklm:\software  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command creates the TestNew subkey under the HKCU:\\Environment subkey:  
  
```  
new-item -path hkcu:\Environment\TestNew  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 3 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command deletes the TestNew subkey of the HKEY\_CURRENT\_USER\\Environment key:  
  
```  
remove-item -path hkcu:\Environment\TestNew  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 4 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command copies the TestNew key to the TestCopy subkey:  
  
```  
copy-item -path  hkcu:\Environment\TestNew  hkcu:\Environment\TestNew\TestCopy  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 5 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command gets all the subkeys of the HKEY\_LOCAL\_MACHINE\\Software registry key:  
  
```  
get-childitem -path hklm:\Software -recurse  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 6 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command moves the HKEY\_CURRENT\_USER\\Environment\\testnewcopy registry key, its subkeys and their registry entries to the HKEY\_CURRENT\_USER\\Environment\\testnew key:  
  
```  
move-item -path hkcu:\environment\testnewcopy -destination hkcu:\environment\testnew  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 7 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command renames the HKEY\_CURRENT\_USER\\Environment\\testnew registry key to HKEY\_CURRENT\_USER\\Environment\\test:  
  
```  
rename-item -path hkcu:\environment\testnew\ -newname test  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 8 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command gets the security descriptor of the specified registry key:  
  
```  
get-acl -path hkcu:\environment\testnew | format-list -property *  
  
```  
  
### Managing Registry Entries  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command gets the registry entries in the HKEY\_CURRENT\_USER\\Environment registry key:  
  
```  
get-itemproperty -path hkcu:\Environment  
  
```  
  
 This command gets the Default registry entry only when it contains data.  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command gets the Temp registry entry in the HKEY\_CURRENT\_USER\\Environment key:  
  
```  
get-itemproperty -path hkcu:\Environment -name Temp  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 3 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command creates a PSTest registry entry in the HKEY\_CURRENT\_USER\\Environment key and sets its value to 1:  
  
```  
new-itemproperty -path hkcu:\environment -name PSTest -value 1 -propertyType dword  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 4 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command changes the value of the PSTest registry entry  in the HKEY\_CURRENT\_USER\\Environment key to "Start" and changes its data type to REG\_SZ \(string\):  
  
```  
set-itemproperty -path hkcu:\environment -name PSTest -value Start -type string  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 5 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command renames the PSTest registry entry in the HKEY\_CURRENT\_USER\\Environment key to PSTestNew:  
  
```  
rename-itemproperty -path hkcu:\environment -name PSTest  
-newname PSTestNew  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 6 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command copies the PSTestNew registry entry from the HKEY\_CURRENT\_USER\\Environment key to the HKEY\_CURRENT\_USER\\Environment\\testnewcopy key:  
  
```  
copy-itemproperty -path hkcu:\environment -destination hkcu:\environment\testnewcopy -name pstestnew  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 7 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 The command moves the pstestnew registry entry from the HKEY\_CURRENT\_USER\\environment\\testnewcopy key to the HKEY\_CURRENT\_USER\\environment\\testnew key:  
  
```  
move-itemproperty -path hkcu:\environment\testnewcopy -destination hkcu:\environment\testnew -name pstestnew  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 8 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command clears the value of the pstestnew registry entry in the HKEY\_CURRENT\_USER\\Environment\\testnew key:  
  
```  
clear-itemproperty -path hkcu:\environment\testnew -name pstestnew  
  
```  
  
 You can use the Clear\-Item cmdlet to clear the value of the default registry entry for a subkey. For example, the following command clears the value of the default entry of the HKEY\_CURRENT\_USER\\Environment\\testnew registry key:  
clear\-item \-path hkcu:\\environment\\testnew  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 9 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command deletes the pstestnew registry entry from the HKEY\_CURRENT\_USER\\Environment\\testnew registry key:  
  
```  
remove-itemproperty -path hkcu:\environment\testnew -name pstestnew  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 10 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command changes the value of the default registry entry in the HKEY\_CURRENT\_USER\\Environment\\testnew key to "default value":  
  
```  
set-itemproperty -path hkcu:\environment\testnew -name "(default)" -value "default value"  
  
```  
  
 You can also change the default value of a registry key by using the Set\-Item cmdlet. For example, the following command updates the default value of the testnew key:  
set\-item \-path hkcu:\\environment\\testnew \-value "another default value"  
  
## DYNAMIC PARAMETERS  
 Dynamic parameters are cmdlet parameters that are added by a Windows PowerShell provider and are available only when the cmdlet is being used in the provider\-enabled drive.  
  
### Type \<Microsoft.Win32.RegistryValueKind\>  
 Establishes or changes the data type of a registry value. The default is String \(REG\_SZ\).  
  
 This parameter works as designed on the [Set\-ItemProperty](assetId:///e8b394a3-e87c-42e5-ad9e-5a1576da6701) cmdlet. It is also available on the [Set\-Item](assetId:///2ae0f9bc-105b-4363-8410-7f94a3c12fa3) cmdlet in the registry drives, but it has no effect.  
  
|Value|Description|  
|-----------|-----------------|  
|String|Specifies a null\-terminated string. Equivalent to REG\_SZ.|  
|ExpandString|Specifies a null\-terminated string that contains unexpanded references to environment variables that are expanded when the value is retrieved. Equivalent to REG\_EXPAND\_SZ.|  
|Binary|Specifies binary data in any form. Equivalent to REG\_BINARY.|  
|DWord|Specifies a 32\-bit binary number. Equivalent to REG\_DWORD.|  
|MultiString|Specifies an array of null\-terminated strings terminated by two null characters. Equivalent to REG\_MULTI\_SZ.|  
|QWord|Specifies a 64\-bit binary number. Equivalent to REG\_QWORD.|  
|Unknown|Indicates an unsupported registry data type, such as REG\_RESOURCE\_LIST.|  
  
#### Cmdlets supported:  
  
-   [Set\-Item](assetId:///2ae0f9bc-105b-4363-8410-7f94a3c12fa3)  
  
-   [Set\-ItemProperty](assetId:///e8b394a3-e87c-42e5-ad9e-5a1576da6701)  
  
## See Also  
 [about\_Providers](assetId:///55e2974f-3314-48d2-8b1b-abdea6b303cb)