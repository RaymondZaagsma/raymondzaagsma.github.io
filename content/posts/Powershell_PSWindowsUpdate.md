---
title: "Powershell PSWindowsUpdate"
subtitle: ""
date: 2023-01-28T13:33:10+02:00
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
- Powershell
categories:
- Powershell

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

# Powershell PSWindowsUpdate Module

PSWindowsUpdate is a PowerShell module that allows you to manage Windows updates on your local and remote computers.  
With this module, you can easily check for available updates, download and install them, and even configure update settings. In this blog post, we'll take a closer look at PSWindowsUpdate and how you can use it to manage Windows updates more efficiently.

## Getting started with PSWindowsUpdate

The first step in using PSWindowsUpdate is to install the module. You can do this by running the following PowerShell command:

```powershell
Install-Module PSWindowsUpdate
```

Once the module is installed, you can use the following cmdlets to manage Windows updates:

```
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           Clear-WUJob                                        2.2.0.3    PSwindowsupdate
Alias           Download-WindowsUpdate                             2.2.0.3    PSwindowsupdate
Alias           Get-WUInstall                                      2.2.0.3    PSwindowsupdate
Alias           Get-WUList                                         2.2.0.3    PSwindowsupdate
Alias           Hide-WindowsUpdate                                 2.2.0.3    PSwindowsupdate
Alias           Install-WindowsUpdate                              2.2.0.3    PSwindowsupdate
Alias           Show-WindowsUpdate                                 2.2.0.3    PSwindowsupdate
Alias           UnHide-WindowsUpdate                               2.2.0.3    PSwindowsupdate
Alias           Uninstall-WindowsUpdate                            2.2.0.3    PSwindowsupdate
Cmdlet          Add-WUServiceManager                               2.2.0.3    PSwindowsupdate
Cmdlet          Enable-WURemoting                                  2.2.0.3    PSwindowsupdate
Cmdlet          Get-WindowsUpdate                                  2.2.0.3    PSwindowsupdate
Cmdlet          Get-WUApiVersion                                   2.2.0.3    PSwindowsupdate
Cmdlet          Get-WUHistory                                      2.2.0.3    PSwindowsupdate
Cmdlet          Get-WUInstallerStatus                              2.2.0.3    PSwindowsupdate
Cmdlet          Get-WUJob                                          2.2.0.3    PSwindowsupdate
Cmdlet          Get-WULastResults                                  2.2.0.3    PSwindowsupdate
Cmdlet          Get-WUOfflineMSU                                   2.2.0.3    PSwindowsupdate
Cmdlet          Get-WURebootStatus                                 2.2.0.3    PSwindowsupdate
Cmdlet          Get-WUServiceManager                               2.2.0.3    PSwindowsupdate
Cmdlet          Get-WUSettings                                     2.2.0.3    PSwindowsupdate
Cmdlet          Invoke-WUJob                                       2.2.0.3    PSwindowsupdate
Cmdlet          Remove-WindowsUpdate                               2.2.0.3    PSwindowsupdate
Cmdlet          Remove-WUServiceManager                            2.2.0.3    PSwindowsupdate
Cmdlet          Reset-WUComponents                                 2.2.0.3    PSwindowsupdate
Cmdlet          Set-PSWUSettings                                   2.2.0.3    PSwindowsupdate
Cmdlet          Set-WUSettings                                     2.2.0.3    PSwindowsupdate
Cmdlet          Update-WUModule                                    2.2.0.3    PSwindowsupdate
```


1. Get-WindowsUpdate

The Get-WindowsUpdate cmdlet allows you to check for available updates on your local or remote computers. By default, this cmdlet only lists important and security updates. However, you can use the -All switch to list all available updates. Here's an example:

```powershell
Get-WindowsUpdate -ComputerName <ComputerName> -All
```

2. Install-WindowsUpdate

The Install-WindowsUpdate cmdlet allows you to download and install available updates on your local or remote computers. By default, this cmdlet only installs important and security updates. However, you can use the -AcceptAll switch to install all available updates. Here's an example:

```powershell
Install-WindowsUpdate -ComputerName <ComputerName> -AcceptAll
```

3. Get-WUServiceManager

The Get-WUServiceManager cmdlet allows you to view and configure Windows Update settings. By default, this cmdlet lists the Windows Update service and its status. However, you can use the following cmdlets to configure update settings:

- Set-WUServiceManager -ConfigDownloadMode: allows you to configure the download mode for updates (such as automatic or manual).

- Set-WUServiceManager -ConfigAutoUpdate: allows you to enable or disable automatic updates.

## Here's an example:

```powershell
Get-WUServiceManager -ComputerName <ComputerName>
Set-WUServiceManager -ComputerName <ComputerName> -ConfigDownloadMode Manual
Set-WUServiceManager -ComputerName <ComputerName> -ConfigAutoUpdate Disabled
```

## Conclusion

PSWindowsUpdate is a powerful tool that allows you to manage Windows updates more efficiently. With this module, you can easily check for available updates, download and install them, and even configure update settings. By using PowerShell commands, you can automate update management and save time and effort. If you're responsible for managing updates on your local or remote computers, PSWindowsUpdate is definitely worth exploring.