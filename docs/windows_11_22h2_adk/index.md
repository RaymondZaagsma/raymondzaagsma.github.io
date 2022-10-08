# Windows 11 22H2 ADK


<!--more-->

## Update MDT with Windows 11 22H2 ADK

Download the Windows 11 ADK version 22H2 at the following link 

[Windows 11 ADK 22H2](https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install)

The biggest change is it has no more 32 bit x86 support, that means the ADK no longer contains the 32 bit x86 version of Windows PE.

# MMC Error

After updating to the windows 11 22H2 ADK the MDT console crashes when opening the Windows PE tab of the deploytment share settings.

![MDT Error ADK 22H2](/images/MMCErrorADK22H2MDT.jpg)

To fix this error we need to create a folder

```
MkDir "C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\x86\WinPE_OCs"
```

# HTA applications report Script error

After updating the boot image, and booting into the Lite Touch x64 boot image another error is generated.

![Deployment Wizard Task Sequence Script Error](/images/scripterrortasksequence.jpg)

To resolve this error we need to edit the Unattend_PE_x64.xml 

HTA applications rely on MSHTML and starting with Windows 11, version 22H2, the default legacy scripting engine was changed.

To work around this issue you need to add the following registry value in WinPE:

```
reg.exe add "HKLM\Software\Microsoft\Internet Explorer\Main" /t REG_DWORD /v JscriptReplacement /d 0 /f
```

To enable this change in MDT, we recommend that you back up the following file: C:\Program Files\Microsoft Deployment Toolkit\Templates\Unattend_PE_x64.xml and to modify it as follows:

```
<unattend xmlns="urn:schemas-microsoft-com:unattend">
   <settings pass="windowsPE">
       <component name="Microsoft-Windows-Setup" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" xmlns:wcm="http://schemas.microsoft.com/WMIConfig/2002/State">
           <Display>
               <ColorDepth>32</ColorDepth>
               <HorizontalResolution>1024</HorizontalResolution>
               <RefreshRate>60</RefreshRate>
               <VerticalResolution>768</VerticalResolution>
           </Display>
           <RunSynchronous>
               <RunSynchronousCommand wcm:action="add">
                   <Description>Lite Touch PE</Description>
                   <Order>1</Order>
                   <Path>reg.exe add "HKLM\Software\Microsoft\Internet Explorer\Main" /t REG_DWORD /v JscriptReplacement /d 0 /f</Path>
               </RunSynchronousCommand>
               <RunSynchronousCommand wcm:action="add">
                   <Description>Lite Touch PE</Description>
                   <Order>2</Order>
                   <Path>wscript.exe X:\Deploy\Scripts\LiteTouch.wsf</Path>
               </RunSynchronousCommand>
           </RunSynchronous>
       </component>
   </settings>
</unattend>
```

# WDS multicast stops working

After you updated your MDT boot image to ADK for Windows 11 22H2 and you are using multicast popups appear prompting wdscommonlib.dll and imagelib.dll are missing in WinPE.

The right way to add WDS multicast to WinPE is to install WinPE-WDS-Tools OC (WinPE optional components) into WinPE.

Follow this example to install WinPE-WDS-Tools OC in WinPE (assuming the mount folder E:\mnt exists).

```
Dism /mount-wim /WimFile:"E:\DeploymentShare\Boot\LiteTouchPE_multicast_x64.wim" /Index:1 /MountDir:E:\mnt
Dism /Image:"E:\mnt" /Add-Package /PackagePath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-WDS-Tools.cab"
Dism /Image:"E:\mnt" /Add-Package /PackagePath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"
Dism /Unmount-Wim /MountDir:E:\mnt /Commit
```
Add or replace the multicast enabled boot image in WDS snap-in for Microsoft Management Console (MMC).

### The content of this blog was inspirid by the following information

Michael Niehaus "Get ready (and get MDT ready) to deploy Windows 11 22H2" Out of Office Hours
https://oofhours.com/2022/10/06/get-ready-and-get-mdt-ready-to-deploy-windows-11-22h2/

Johan Arwidmark "Notes from the Lab on Windows ADK for Windows 11 22H2"
https://www.deploymentresearch.com/notes-from-the-lab-on-windows-adk-for-windows-11-22h2/

Microsoft "Microsoft Docs memdocs"
https://github.com/MicrosoftDocs/memdocs/blob/main/memdocs/configmgr/mdt/known-issues.md




---

> Author:   
> URL: https://raymondzaagsma.github.io/windows_11_22h2_adk/  

