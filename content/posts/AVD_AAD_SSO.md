+++ 
draft = false
date = 2022-08-26T07:43:25+02:00
title = "AVD Azure AD SSO"
slug = "" 
tags = ["AVD"]
categories = []
thumbnail = "images/tn.png"
description = ""
+++

## How to enable Azure Virtual Desktop Hybrid single sign-on.  

##### NOTE : This currently only work for Windows 11 22h2 insider preview build.

login into the Azure Portal.  
Go to Azure Virtual Desktop.  
Open one of the created hostpools.  
Select RDP Properties.  

Configure : RDP will attempt to use Azure AD authentication to sign in

![RDP Properties](/images/rdpproperties.jpg)


Go to the advanced tab.  
The property that has been added is : enablerdsaadauth:i:1  

![RDP Properties Advanced](/images/rdppropadvanced.jpg)

Configure Azure AD Keberos  

[Azure AD Kerberos](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-authentication-passwordless-security-key-on-premises#install-the-azure-ad-kerberos-powershell-module)


```
# First, ensure TLS 1.2 for PowerShell gallery access.
[Net.ServicePointManager]::SecurityProtocol = [Net.ServicePointManager]::SecurityProtocol -bor [Net.SecurityProtocolType]::Tls12

# Install the Azure AD Kerberos PowerShell Module.
Install-Module -Name AzureADHybridAuthenticationManagement -AllowClobber
```

Select one of the example scenarios that fits your organization, is this blog i used example one.

```
# Specify the on-premises Active Directory domain. A new Azure AD
# Kerberos Server object will be created in this Active Directory domain.
$domain = $env:USERDNSDOMAIN

# Enter an Azure Active Directory global administrator username and password.
$cloudCred = Get-Credential -Message 'An Active Directory user who is a member of the Global Administrators group for Azure AD.'

# Enter a domain administrator username and password.
$domainCred = Get-Credential -Message 'An Active Directory user who is a member of the Domain Admins group.'

# Create the new Azure AD Kerberos Server object in Active Directory
# and then publish it to Azure Active Directory.
Set-AzureADKerberosServer -Domain $domain -CloudCredential $cloudCred -DomainCredential $domainCred
```

This script will create a user account and a computer account object in the onprem Active Directory, to redirect all authentication requests over to Azure AD.  


![Azure AD Kerberos Server user account for this domain](/images/krbtAzureAD.jpg)

![Azure AD Kerberos Server computer account for this domain](/images/AzureADKeberos.jpg)


