---
title: "MDT Task Sequence Variables Powershell"
subtitle: ""
date: 2023-02-18T12:12:06+02:00
draft: False
author: "Raymond Zaagsma"
authorLink: ""
authorEmail: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- MDT
categories:
- MDT

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
resources:
- name: featured-image
  src: featured-image.jpg
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []

repost:
  enable: true
  url: ""

# See details front matter: https://fixit.lruihao.cn/theme-documentation-content/#front-matter
---

<!--more-->

# MDT Task Sequence Variables passthru Powershell

MDT Task Sequence Variables are an important component of the MDT (Microsoft Deployment Toolkit) task sequence. They allow administrators to configure and customize the deployment process based on a range of different variables, such as the computer model, the operating system, and more. In this blog post, we'll explore how MDT Task Sequence Variables can be used as scripts to further customize and automate the deployment process.

What are MDT Task Sequence Variables?

MDT Task Sequence Variables are variables that can be used to configure and customize the deployment process in MDT. These variables are defined in the task sequence itself and can be used to perform a range of different actions, such as installing applications, configuring settings, and more. Some examples of MDT Task Sequence Variables include:

- %Model%: Specifies the computer model being deployed.
- %OSDComputerName%: Specifies the name of the computer being deployed.
- %OSDDomainName%: Specifies the name of the domain being joined.
- %OSDInstallLanguage%: Specifies the language used for the installation.

## How can MDT Task Sequence Variables be used as scripts?

Using Task Sequence variables in a running Task Sequence by script.  
The first step is to create an instance of Microsoft.SMS.TSEnvironment. As this is a COM automation object.  

In the following code example all Task sequence variables are being passthru to powershell to backup the autopilot csv file to a share on the MDT server.

$SRV =  Servername of MDT server  
$share = Share where autopilot backup files are placed  
$clabel = Customer label, abbreviation of customer name  


```
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment
 
# Convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }


& $DEPLOYROOT\applications\get-windowsautopilotinfo\Get-WindowsAutoPilotInfo.ps1 -OutputFile "\\$SRV\$share\$clabel\$env:COMPUTERNAME.csv" -GroupTag "$OrderIdentifier"  
```


Conclusion

MDT Task Sequence Variables are a powerful tool for customizing and automating the deployment process in MDT. By using these variables as scripts, administrators can further customize the deployment process based on a range of different variables, making it easier to deploy and manage Windows operating systems and applications. With the ability to automate complex tasks, administrators can save time and ensure consistent and accurate deployments across their organization.