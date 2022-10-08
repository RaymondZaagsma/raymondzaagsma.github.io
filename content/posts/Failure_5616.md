+++
title = "Failure 5616"
date =  2022-08-20T13:36:04+02:00
draft = false
description = ""
tags = ['MDT']
Categories = ['MDT']
+++

Windows 10 deployments using the Microsoft Deployment Toolkit (MDT) build 8456 fail when used with the Windows Assessment and Deployment Kit (ADK) for Windows 10 and 11.
The BIOS firmware type is incorrectly identified as UEFI resulting in failures when refreshing an existing computer with a new version of Windows.
When this issue occurs, the smsts.log will record the following entry:
UEFI: true
Errors resembling the following are then recorded at the end of the process.

The following update to resolve this problem is available for download from the Microsoft Download Center:

[Download this update now.](https://download.microsoft.com/download/3/0/6/306AC1B2-59BE-43B8-8C65-E141EF287A5E/KB4564442/MDT_KB4564442.exe)

1.	Close the Deployment Workbench.
2.	Backup the existing x86 and x64 versions of the Microsoft.BDD.Utility.dll file in the following locations.
    %ProgramFiles%\Microsoft Deployment Toolkit\Templates\Distribution\Tools\x86\
    %ProgramFiles%\Microsoft Deployment Toolkit\Templates\Distribution\Tools\x64\
3.	Copy the new files extracted from MDT_KB4564442.exe over the old versions.
4.	For each deployment share that you have created, repeat the file replacement (e.g. C:\DeploymentShare\Tools\x86, C:\DeploymentShare\Tools\x64, etc.).
5.	Open the Deployment Workbench, select the Deployment Share and choose the Update Deployment Share option, choosing to completely regenerate the boot image.  
    Perform this step for each deployment share to ensure each one is updated with the correct binaries.


![Failure 5616](/images/5616.jpg)