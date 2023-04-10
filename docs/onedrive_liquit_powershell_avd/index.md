# Install Onedrive via Powershell in Azure Virtual Desktop


<!--more-->

# Install Onedrive via Powershell in Azure Virtual Desktop

OneDrive is a cloud storage service offered by Microsoft, allowing users to store and share files securely. It's an essential tool for businesses and individuals who need to access their files on-the-go, and the process of installing it via PowerShell is straightforward. Here's a guide on how to install OneDrive via PowerShell:

Step 1: Open PowerShell as an administrator
To begin, you'll need to open PowerShell as an administrator. To do this, search for "PowerShell" in the Start menu, right-click on the PowerShell app, and select "Run as administrator."

Step 2: Download and Install OneDrive


```powershell
$OneDriveClient = "https://go.microsoft.com/fwlink/?linkid=844652"
$output = "$ENV:temp"  + '\OneDriveSetup.exe'
$apppath = "C:\Program Files (x86)\Microsoft OneDrive\OneDrive.exe"
$action = New-ScheduledTaskAction -Execute $apppath
$trigger = New-ScheduledTaskTrigger -Once -At (Get-Date)
 
Invoke-WebRequest -Uri $OneDriveClient -OutFile $output
Start-Process -FilePath $output -ArgumentList '/allusers', '/silent'
Start-Sleep -Seconds 60

Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "Launch OneDrive" | Out-Null
Start-ScheduledTask -TaskName "Launch OneDrive"
Start-Sleep -Seconds 5
Unregister-ScheduledTask -TaskName "Launch OneDrive" -Confirm:$false
```

Alternatively, you can run the following command to verify that OneDrive is installed:

```powershell
Get-ChildItem "$env:ProgramFiles(x86)\Microsoft OneDrive\OneDrive.exe" -ErrorAction SilentlyContinue | ForEach-Object FullName
```

This command checks for the existence of the OneDrive.exe file in the Program Files folder.

In conclusion, installing OneDrive via PowerShell is a straightforward process that can be completed in just a few steps. By following this guide, you'll be able to install OneDrive quickly and efficiently, ensuring that you can access your files from anywhere.


---

> Author:   
> URL: https://raymondzaagsma.github.io/onedrive_liquit_powershell_avd/  

