---
title: Certificate Provider
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f743541-d0c6-4670-809a-b16fb01f7c4d
---
# Certificate Provider
## PROVIDER NAME  
 Certificate  
  
## DRIVES  
 Cert:  
  
## SHORT DESCRIPTION  
 Provides access to X.509 certificate stores and certificates in Windows PowerShell.  
  
## DETAILED DESCRIPTION  
 The Windows PowerShell Certificate provider lets you navigate the certificate namespace and view the certificate stores and certificates. It also lets you open the Certificates snap\-in for the Microsoft Management Console \(MMC\).  
  
 NOTE: Beginning in Windows PowerShell 3.0, the Microsoft.PowerShell.Security module that contains the [Certificate Provider](../Topic/Certificate-Provider.md) is not imported automatically into every session. To use the Cert: drive, use the [Import\-Module&#91;PSITPro4\_Core&#93;](assetId:///af616c24-e122-4098-930e-1e3ea2080ade) cmdlet to import the module, or run a command that uses the Cert: drive, such as a "[Set\-Location&#91;PSITPro4\_Management&#93;](assetId:///d7f353cd-ebd7-462a-bd57-1498dc8b88a6) Cert:" command.  
  
 Beginning in [!INCLUDE[wps_2]()] 3.0, the Certificate provider enhances its support for managing Secure Socket Layer \(SSL\) certificates for web hosting by adding support for cmdlets and new dynamic parameters that create and delete certificate stores in the LocalMachine certificate store location, and find, move, and delete certificates.  
  
 New dynamic parameters, DnsName, EKU, SSLServerAuthentication, and ExpiringInDays have been added to the [Get\-ChildItem&#91;PSITPro4\_Management&#93;](assetId:///75cf79bb-4db6-4a67-8c36-3d20754e2190) cmdlet in the Cert: drive. Also, a DeleteKey dynamic parameter has been added to [Remove\-Item&#91;PSITPro4\_Management&#93;](assetId:///0fe3ff11-a1f7-43b9-8c85-f92d52641395) in the Cert: drive. The new dynamic parameters are available in the [!INCLUDE[wps_2]()] 3.0 and newer [!INCLUDE[wps_2]()] releases, and work with IIS 8.0, available on [!INCLUDE[win8_server_2]()] and later releases of the Windows Server operating system.  
  
 New script properties, DnsNameList, EnhancedKeyUsageList, and SendAsTrustedIssuer, have been added to the x509Certificate2 object that represents the certificates to make it easy to search and manage the certificates.  
  
 These new features let you search for certificates based on their DNS names and expiration dates, and distinguish client and server authentication certificates by the value of their Enhanced Key Usage \(EKU\) properties.  
  
 These enhancements are designed to support the WebHosting certificate store created by IIS. This certificate store is optimized to scale for efficient, automated management of the thousands of certificates that are required for dynamic shared hosting. The WebHosting certificate store is available starting in IIS 8.0, available with Web Server \(IIS\) on [!INCLUDE[win8_server_2]()] and later releases of the Windows Server operating system.  
  
 To populate the DnsNameList property, the Certificate provider copies the content from the DNSName entry in the SubjectAlternativeName \(SAN\) extension. If the SAN extension is empty, the property is populated with content from the Subject field of the certificate.  
  
 To populate the EnhancedKeyUsageList property, the Certificate provider copies the OID properties of the EnhancedKeyUsage \(EKU\) field in the certificate and creates a friendly name for it..  
  
 The Certificate provider exposes the certificate namespace as the Cert: drive in Windows PowerShell. The Cert: drive has the following three levels:  
  
 \-\-  Store locations \(Microsoft.PowerShell.Commands.X509StoreLocation\), which are high\-level containers that group the certificates for the current user and for all users. Each system has a CurrentUser and LocalMachine \(all users\) store location.  
  
 \-\- Certificates stores \(System.Security.Cryptography.X509Certificates.X509Store\), which are physical stores in which certificates are saved and managed.  
  
 \-\- X.509 certificates \(System.Security.Cryptography.X509Certificates.X509Certificate2\), each of which represent an X.509 certificate on the computer. Certificates are identified by their thumbprints.  
  
 In Windows PowerShell 3.0, the Certificate provider supports the [Get\-Location&#91;PSITPro4\_Management&#93;](assetId:///b4c8d674-ba23-4bdf-8322-1f08acdc0ca9), [Set\-Location&#91;PSITPro4\_Management&#93;](assetId:///d7f353cd-ebd7-462a-bd57-1498dc8b88a6), [Get\-Item&#91;PSITPro4\_Management&#93;](assetId:///4ed2b1e1-fde4-4425-90a0-87774477fefa), [Get\-ChildItem&#91;PSITPro4\_Management&#93;](assetId:///75cf79bb-4db6-4a67-8c36-3d20754e2190), [Invoke\-Item&#91;PSITPro4\_Management&#93;](assetId:///61bc0652-39d8-44fe-9ff4-476ae75c38c8), [Move\-Item&#91;PSITPro4\_Management&#93;](assetId:///de1b4217-de99-45cd-a12c-35e87b0c8466), [New\-Item&#91;PSITPro4\_Management&#93;](assetId:///67038d02-6598-49c6-b5bd-77b59d445abe), and [Remove\-Item&#91;PSITPro4\_Management&#93;](assetId:///0fe3ff11-a1f7-43b9-8c85-f92d52641395) cmdlets.  
  
 In Windows PowerShell 2.0, the Certificate provider supports the [Get\-Location&#91;PSITPro4\_Management&#93;](assetId:///b4c8d674-ba23-4bdf-8322-1f08acdc0ca9), [Set\-Location&#91;PSITPro4\_Management&#93;](assetId:///d7f353cd-ebd7-462a-bd57-1498dc8b88a6), [Get\-Item&#91;PSITPro4\_Management&#93;](assetId:///4ed2b1e1-fde4-4425-90a0-87774477fefa), [Get\-ChildItem&#91;PSITPro4\_Management&#93;](assetId:///75cf79bb-4db6-4a67-8c36-3d20754e2190), and [Invoke\-Item&#91;PSITPro4\_Management&#93;](assetId:///61bc0652-39d8-44fe-9ff4-476ae75c38c8) cmdlets.  
  
 In addition, Windows PowerShell Security module \(Microsoft.PowerShell.Security\), which includes the Certificate provider, also includes cmdlets to get and set Authenticode signatures and to get certificates. For a list of cmdlets in the Security module, type "[Get\-Command&#91;PSITPro4\_Core&#93;](assetId:///59c6d302-6e8c-48b7-a6f6-f0172df936ad) \-module \*security".  
  
## CAPABILITIES  
 ShouldProcess  
  
## EXAMPLES  
  
### Navigating the Cert: Drive  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the Set\-Location cmdlet to change the current location to the Cert: drive.  
  
```  
set-location cert:  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the Set\-Location command to change the current location to the Root certificate store in the LocalMachine store location. Use a backslash \(\\\) or a forward slash \(\/\) to indicate a level of the Cert: drive.  
  
```  
set-location -path LocalMachine\Root  
  
```  
  
 If you are not in the Cert: drive, begin the path with the drive name.  
  
### Displaying the Contents of the Cert: Drive  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the Get\-ChildItem cmdlet to display the certificate stores in the CurrentUser certificate store location.  
  
```  
get-childitem -path cert:\CurrentUser  
  
```  
  
 If you are in the Cert: drive, you can omit the drive name.  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the Get\-ChildItem cmdlet to display the certificates in the My certificate store.  
  
```  
get-childitem -path cert:\CurrentUser\My  
  
```  
  
 If you are in the Cert: drive, you can omit the drive name.  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 3 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the Get\-Item cmdlet to get the "My" certificate store and the Property parameter of Format\-List with a wildcard character \(\*\) to display all of the properties of the store.  
  
```  
get-item -path cert:\CurrentUser\My | format-list *  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 4 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command gets a certificate and displays all of its properties. It uses the Get\-ChildItem cmdlet to get the certificate and the Property parameter of Format\-List with a wildcard character \(\*\) to display all of the properties of the certificate.  
  
 The certificate is identified by its thumbprint.  
  
```  
get-childitem -path cert:\LocalMachine\my\6B8223358119BB08840DEE50FD8AF9EA776CE66B | format-list -property *  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 5 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command displays the web hosting properties of all certificates in the LocalMachine certificate store location.  
  
 It uses the Recurse parameter of the Get\-ChildItem cmdlet to get all certificates in all stores of the LocalMachine store location. A pipeline operator sends the certificates to the Format\-Table command, which displays the selected properties of each certificate in a table.  
  
```  
Get-ChildItem -Path cert:\LocalMachine -Recurse | Format-Table -Property DnsNameList, EnhancedKeyUsageList, NotAfter, SendAsTrustedIssuer  
  
```  
  
### Opening the Certificates MMC Snap\-in  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command opens the Certificates MMC snap\-in to manage the specified certificate.  
  
```  
invoke-item cert:\CurrentUser\my\6B8223358119BB08840DEE50FD8AF9EA776CE66B  
  
```  
  
### Getting Selected Certificates  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the CodeSigningCert and Recurse parameters of the Get\-ChildItem cmdlet to get all of the certificates on the computer that have code\-signing authority.  
  
```  
Get-ChildItem -Path cert: -CodeSigningCert -Recurse  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the DNSName parameter of the Get\-ChildItem cmdlet to get all of the certificates in the WebHosting store whose domain names contain "Fabrikam".  
  
```  
Get-ChildItem -Path cert:\LocalMachine\WebHosting -DNSName "*fabrikam*"  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 3 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the ExpiringInDays parameter of the Get\-ChildItem cmdlet to get certificates that will expire within the next 30 days.  
  
```  
Get-ChildItem -Path cert:\LocalMachine\WebHosting -ExpiringInDays 30  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 4 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the Invoke\-Command cmdlet to run a Get\-ChildItem command on the Srv01 and Srv02 computers. A value of zero \(0\) in the ExpiringInDays parameter gets certificates on the Srv01 and Srv02 computers that have expired.  
  
```  
Invoke-Command -ComputerName Srv01, Srv02 {Get-ChildItem -Path cert:\* -Recurse -ExpiringInDays 0}  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 5 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the SSLServerAuthentication parameter of the Get\-ChildItem cmdlet to get all  
  
 Server SSL Certificates in the My and WebHosting stores.  
  
```  
Get-ChildItem -Path cert:\LocalMachine\My, cert:\LocalMachine\WebHosting -SSLServerAuthentication  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 6 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command gets all certificates in the LocalMachine store location that have "fabrikam" in their DNS name, "Client Authentication" in their EKU, a value of $true for the SendAsTrustedIssuer property, and do not expire within the next 30 days.  
  
```  
Get-ChildItem -Path cert:\* -Recurse  -DNSName "*fabrikam*" -EKU "*Client Authentication*" | Where-Object {$_.SendAsTrustedIssuer -and $_.NotAfter -gt (get-date).AddDays.(30)}  
  
```  
  
 The NotAfter property stores the certificate expiration date.  
  
### Moving Certificates  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the Move\-Item cmdlet to move a certificate from the My store to the WebHosting store.  
  
 Move\-Item will not move certificate stores and it will not move certificates to a different store location, such as moving a certificate from LocalMachine to CurrentUser. Also, Move\-Item moves certificates, but it does not move private keys.  
  
```  
Move-Item -Path cert:\LocalMachine\My\5DDC44652E62BF9AA1116DC41DE44AB47C87BDD0 -Destination cert:\LocalMachine\WebHosting  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the SSLServerAuthentication parameter of the Get\-ChildItem cmdlet to get SSL server authentication certificates in the MY certificate store.  
  
 It uses a pipeline operator to send the certificates to the Move\-Item cmdlet, which moves the certificates to the WebHosting store.  
  
```  
Get-ChildItem -Path cert:\LocalMachine\My -SSLServerAuthentication | Move-Item -Destination cert:\LocalMachine\WebHosting  
  
```  
  
### Deleting Certificates and Private Keys  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command deletes a certificate from the CA certificate store, but leaves the associated private key intact.  
  
 In the Cert: drive, the Remove\-Item cmdlet supports only the DeleteKey, Path, WhatIf, and Confirm parameters. All other parameters are ignored.  
  
```  
Remove-Item -Path cert:\LocalMachine\CA\5DDC44652E62BF9AA1116DC41DE44AB47C87BDD0  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This series of commands enables delegation and then deletes the certificate and associated private key on a remote computer. To delete a private key on a remote computer, you must use delegated credentials.  
  
 The first command uses the Enable\-WSManCredSSP cmdlet to enable Credential Security Service Provider \(CredSSP\) authentication on a client on the S1 remote computer. CredSSP permits delegated authentication.  
  
 The second command uses the Connect\-WSMan cmdlet to connect the S1 computer to the WinRM service on the local computer. When this command completes, the S1 computer appears in the local WSMan: drive in Windows PowerShell.  
  
 The third command uses the Set\-Item cmdlet in the WSMan: drive to enable the CredSSP attribute for the WinRM service.  
  
 The fourth command uses the New\-PSSession cmdlet to start a remote session on the S1 computer with CredSSP authentication. It saves the session in the $s variable.  
  
 The fifth command uses the Invoke\-Command cmdlet to run a Remove\-Item command in the session in the $s variable. The Remove\-Item command uses the DeleteKey parameter to remove the private key along with the specified certificate.  
  
```  
PS C:\>Enable-WSManCredSSP -Role Client -DelegateComputer S1   
  
PS C:\>Connect-WSMan -ComputerName S1 -Credential Domain01\Admin01  
  
PS C:\>Set-Item -Path WSMan:\S1\Service\Auth\CredSSP -Value $true  
  
PS C:\> $s  = New-PSSession S1 -Authentication CredSSP -Credential Domain01\Admin01  
  
PS C:\> Invoke-Command -Session $s { Remove-Item cert:\LocalMachine\My\D2D38EBA60CAA1C12055A2E1C83B15AD450110C2 -DeleteKey  }  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 3 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the ExpiringInDays parameter of the Get\-ChildItem cmdlet with a value of 0 to get certificates in the WebHosting store that have expired.  
  
 It uses a pipeline operator to pass the certificates to the Remove\-Item cmdlet, which deletes them. The command uses the DeleteKey parameter to delete the private key along with the certificate.  
  
```  
Get-ChildItem -Path cert:\LocalMachine\WebHosting -ExpiringInDays 0 | Remove-Item -DeleteKey  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 4 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command deletes all certificates that have a DNS name that contains "Fabrikam".  
  
 It uses the DNSName parameter of the Get\-ChildItem cmdlet to get the certificates and the Remove\-Item cmdlet to delete them.  
  
```  
Get-ChildItem -Path cert:\LocalMachine -DnsName *Fabrikam* | Remove-Item  
  
```  
  
### Creating Certificate Stores  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command creates a new certificate store named "CustomStore" in the LocalMachine store location.  
  
 In the Cert: drive, the New\-Item cmdlet creates certificate stores in the LocalMachine store location. It supports the Name, Path, WhatIf, and Confirm parameters. All other parameters are ignored.  
  
```  
New-Item -Path cert:\LocalMachine\CustomStore  
  
```  
  
 The command returns a System.Security.Cryptography.X509Certificates.X509Store that represents the new certificate store.  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command creates a new certificate store named "HostingStore" in the LocalMachine store location on the Server01 computer.  
  
 The command uses the Invoke\-Command cmdlet to run a New\-Item command on the Server01 computer.  
  
```  
Invoke-Command -ComputerName Server01 { New-Item -Path cert:\LocalMachine\CustomStore }  
  
```  
  
 The command returns a System.Security.Cryptography.X509Certificates.X509Store that represents the new certificate store.  
  
### Deleting Certificate Stores  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 1 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the Remove\-Item cmdlet to delete the Test1 certificate store. It uses the Recurse parameter to delete the certificates in the Test1 store.  
  
 In the Cert: drive, the Remove\-Item cmdlet deletes user\-created certificate stores from the LocalMachine store location. You cannot use the Remove\-Item cmdlet to delete Windows system certificate stores.  
  
 In the Cert: drive, the Remove\-Item cmdlet supports only the Path, WhatIf, and Confirm parameters. All other parameters are ignored.  
  
```  
Remove-Item -Path cert:\LocalMachine\TestStore -Recurse  
  
```  
  
 If the certificate store contains certificates and you omit the Recurse parameter, Remove\-Item prompts you for confirmation before deleting any items.  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 2 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command uses the Invoke\-Command cmdlet to run a Remove\-Item command on the S1 and S2 computers. The Remove\-Item command includes the Recurse parameter, which deletes the certificates in the store before it deletes the store.  
  
```  
Invoke-Command -ComputerName S1, S2 { Remove-Item -Path cert:\LocalMachine\TestStore  -Recurse}  
  
```  
  
#### \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\- EXAMPLE 3 \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
 This command deletes all certificate stores in the LocalMachine store location that have "Test" in their names.  
  
```  
Remove-Item -path cert:\LocalMachine\*test* -Recurse  
  
```  
  
## DYNAMIC PARAMETERS  
 Dynamic parameters are cmdlet parameters that are added by a Windows PowerShell provider and are available only when the cmdlet is being used in the provider\-enabled drive.  
  
### CodeSigningCert \<System.Management.Automation.SwitchParameter\>  
 Gets only those certificates with code\-signing authority.  
  
 This parameter gets certificates that have "Code Signing" in their EnhancedKeyUsageList property value.  
  
 Because certificates that have an empty EnhancedKeyUsageList can be used for all purposes, searches for code signing certificates also return certificates that have an empty EnhancedKeyUsageList property value.  
  
 This parameter is valid in all subdirectories of the Certificate provider, but it is effective only on certificates.  
  
#### Cmdlets supported:  
  
-   [Get\-Item&#91;PSITPro4\_Management&#93;](assetId:///4ed2b1e1-fde4-4425-90a0-87774477fefa)  
  
-   [Get\-ChildItem&#91;PSITPro4\_Management&#93;](assetId:///75cf79bb-4db6-4a67-8c36-3d20754e2190)  
  
### DnsName \<Microsoft.PowerShell.Commands.DnsNameRepresentation\>  
 Gets certificates that have the specified domain name or name pattern in the DNSNameList property of the certificate.  
  
 The value of this parameter can either be Unicode or ASCII. Punycode values are converted to Unicode. Wildcard characters \(\*\) are permitted.  
  
 This parameter is valid in all subdirectories of the Certificate provider, but it is effective only on certificates.  
  
 This parameter was introduced in Windows PowerShell 3.0.  
  
#### Cmdlets supported:  
  
-   [Get\-ChildItem&#91;PSITPro4\_Management&#93;](assetId:///75cf79bb-4db6-4a67-8c36-3d20754e2190)  
  
### EKU \<System.String\>  
 Gets certificates that have the specified text or text pattern in the EnhancedKeyUsageList property of the certificate. Wildcard characters \(\*\) are permitted. The EnhancedKeyUsageList property contains the friendly name and the OID fields of the EKU.  
  
 Because certificates that have an empty EnhancedKeyUsageList can be used for all purposes, all EKU searches return certificates that have an empty EnhancedKeyUsageList property value.  
  
 This parameter is valid in all subdirectories of the Certificate provider, but it is effective only on certificates.  
  
 This parameter was introduced in Windows PowerShell 3.0.  
  
#### Cmdlets supported:  
  
-   [Get\-ChildItem&#91;PSITPro4\_Management&#93;](assetId:///75cf79bb-4db6-4a67-8c36-3d20754e2190)  
  
### ExpiringInDays \<System.Int32\>  
 Gets certificates that are expiring in or before the specified number of days. Enter an integer. A value of 0 \(zero\) gets certificates that have expired.  
  
 This parameter is valid in all subdirectories of the Certificate provider, but it is effective only on certificates.  
  
 This parameter was introduced in Windows PowerShell 3.0.  
  
#### Cmdlets supported:  
  
-   [Get\-ChildItem&#91;PSITPro4\_Management&#93;](assetId:///75cf79bb-4db6-4a67-8c36-3d20754e2190)  
  
### SSLServerAuthentication \<System.Management.Automation.SwitchParameter\>  
 Gets only server certificates for SSL web hosting. This parameter gets certificates that have "Server Authentication" in their EnhancedKeyUsageList property value.  
  
 Because certificates that have an empty EnhancedKeyUsageList can be used for all purposes, SSLServerAuthentication searches also return certificates that have an empty EnhancedKeyUsageList property value.  
  
 This parameter is valid in all subdirectories of the Certificate provider, but it is effective only on certificates.  
  
 This parameter was introduced in Windows PowerShell 3.0.  
  
#### Cmdlets supported:  
  
-   [Get\-ChildItem&#91;PSITPro4\_Management&#93;](assetId:///75cf79bb-4db6-4a67-8c36-3d20754e2190)  
  
### DeleteKey \<System.Management.Automation.SwitchParameter\>  
 Deletes the associated private key when it deletes the certificate.  
  
 To delete a private key that is associated with a user certificate in the Cert:\\CurrentUser store on a remote computer, you must use delegated credentials. When using the [Invoke\-Command&#91;PSITPro4\_Core&#93;](assetId:///906b4b41-7da8-4330-9363-e7164e5e6970) cmdlet to run a [Remove\-Item&#91;PSITPro4\_Management&#93;](assetId:///0fe3ff11-a1f7-43b9-8c85-f92d52641395) command remotely, after considering the security risks, use the CredSSP parameter to enable delegation.  
  
 This parameter is valid in all subdirectories of the Certificate provider, but it is effective only on certificates.  
  
 This parameter was introduced in Windows PowerShell 3.0.  
  
#### Cmdlets supported:  
  
-   [Remove\-Item&#91;PSITPro4\_Management&#93;](assetId:///0fe3ff11-a1f7-43b9-8c85-f92d52641395)  
  
## See Also  
 [about\_Providers](../Topic/about_Providers.md)   
 [about\_Signing](../Topic/about_Signing.md)   
 [Get\-AuthenticodeSignature&#91;PSITPro4\_Security&#93;](assetId:///36e5e640-2125-476e-98d9-495977315f14)   
 [Set\-AuthenticodeSignature&#91;PSITPro4\_Security&#93;](assetId:///f3c13299-4463-48af-83ea-86de4a239509)   
 [Get\-PfxCertificate&#91;PSITPro4\_Security&#93;](assetId:///2f08fac8-2872-4a11-930e-af03a8c4a00d)