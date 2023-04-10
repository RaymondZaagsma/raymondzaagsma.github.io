# Intune App Dectection Script


<!--more-->

# Intune Application Detection Scripts

Intune Application Detection Scripts are a powerful feature that allow IT professionals to detect and install applications on managed devices using custom scripts. In this blog post, we'll explore what Intune Application Detection Scripts are, how they work, and how to use them to detect and install applications on managed devices.

## What are Intune Application Detection Scripts?

Intune Application Detection Scripts are custom scripts that can be used to detect whether an application is installed on a managed device. These scripts can be used in combination with Intune application deployment policies to automatically install applications on managed devices if they are not already installed. This feature is particularly useful for organizations that need to deploy applications to a large number of devices quickly and efficiently.

## How do Intune Application Detection Scripts work?

Intune Application Detection Scripts work by executing a custom script on a managed device to detect whether a specific application is installed. This script can be written in PowerShell, VBScript, or any other scripting language that is supported by Windows. Once the script is executed, the results are sent back to the Intune management console, which then determines whether the application needs to be installed or not.

## Examples

### A basic file check
``` 
$File = "C:\windows\system32\notepad.exe"
if (Test-Path $File) {
    write-output "Notepad detected, exiting"
    exit 0
}
else {
    exit 1
}
```

### A registry key (checking both it exists and the value is correct, good for versioning)
```
$Path = "HKLM:\SOFTWARE\7-Zip"
$Name = "Path"
$Type = "STRING"
$Value = "C:\Program Files\7-Zip\"
Try {
    $Registry = Get-ItemProperty -Path $Path -Name $Name -ErrorAction Stop | Select-Object -ExpandProperty $Name
    If ($Registry -eq $Value){
        Write-Output "Detected"
       Exit 0
    } 
    Exit 1
} 
Catch {
    Exit 1
}
```
### Check if a service exists
```
$service = get-service -name "MozillaMaintenance"
if ($service) {
    write-output "MozillaMaintenance detected, exiting"
    exit 0
}
else {
    exit 1
}
```
### Service exists and is running
```
$service = get-service -name "MozillaMaintenance"
if ($service.Status -eq "Running") {
    write-output "MozillaMaintenance detected and running, exiting"
    exit 0
}
else {
   exit 1
}
```
### Both file and service exist
```
$File = "C:\windows\system32\notepad.exe"
$service = get-service -name "MozillaMaintenance"
if (($service) -and (Test-Path $File)) {
    write-output "MozillaMaintenance and Notepad detected, exiting"
    exit 0
}
else {
    exit 1
}
```
### File is of a certain version
```
$fileversion = (Get-Command C:\Windows\System32\notepad.exe).Version
$build = 19041
$detectedbuild = $fileversion.Build
if ($detectedbuild -eq $build) {
    write-output "Detected"
    exit 0
}
else {
    exit 1
}
```

### Or even the file was last modified today
```
$filedate = (Get-Item C:\Windows\System32\notepad.exe).LastWriteTime
if ($filedate -gt (Get-Date).AddDays(-1)) {
    write-output "Detected"
    exit 0
}
else {
    exit 1
}
```
### File is of a certain version
```
$fileversion = (Get-Command C:\ClickShareApp\ClickShare\ClickShare_native.exe).FileVersionInfo
$build = "4.27.2.4"
$detectedbuild = $fileversion.productversion
if ($detectedbuild -eq $build) {
	write-output "Detected"
	exit 0
}
else {
	exit 1
}
```
### Version Check
```
$APPINSTALL = Get-ItemProperty “HKLM:\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*” | where {$_.DisplayName -like “*APPNAME*”}

IF(Test-Path “$APPINSTALL .PSPath”)
{
IF($APPINSTALL .DisplayVersion -ge “3.0.279”)
{
write-host “Install Success”
exit 0
}

ELSE
{
Write-Host “Installed Version Not Match, Upgrade Failed”
exit 1
}

}

ELSEIF(!(Test-Path “$APPINSTALL .PSPath”))
{
Write-Host “Install failed!”
exit 1
}
```

## Conclusion

Intune Application Detection Scripts are a powerful feature that can save IT professionals time and effort when deploying applications to managed devices. By following the steps outlined above, organizations can easily detect and install applications on managed devices using custom scripts. With Intune Application Detection Scripts, IT professionals can ensure that all managed devices have the necessary applications installed, improving productivity and efficiency across the organization.

---

> Author: Raymond Zaagsma  
> URL: https://raymondzaagsma.github.io/intune_app_dectection_script/  

