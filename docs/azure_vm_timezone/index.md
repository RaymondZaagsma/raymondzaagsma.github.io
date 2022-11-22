# Azure VM TimeZone


<!--more-->

## Changing the Time Zone of Azure VMs
\
![Azure VM Locked Time](/images/AzureVMTimeLocked.png)
\
When you create a VM in Azure it’s always set to the UTC timezone. There are some times when that doesn’t work and it needs to be set for a specific time zone
\
The standard process to change the timezone for a Windows server doesn’t work as expected.   
You can change the time zone by right-clicking on the clock and selecting "Adjust Date and Time".   
If you change the time zone here, it doesn’t actually do anything. It may also change for a short period of time and then revert back to UTC.  
\
If you use PowerShell to change the timezone the change will work, even if the VM is deallocated and reallocated.
\
### Step 1 : See what timzones are available 

```
Get-TimeZone -ListAvailable
```
\
The list of every time zone possible is very long, you can filter the list down as you probably know the name of the time zone you’re looking for.  
In most of my cases the server is created in the Europe Time Zone, So I filtered it down by the word Europe.
\
### Step 2 : Narrow down timezones

```
Get-TimeZone -ListAvailable | where ({$_.Id -like "*europe*"})
```

### Step 3 : Set the new timezone

Use the cmdlet Set-TimeZone to change the time zone of the VM.  
Use the "Id" to set the timezone of your choice.  

```
Set-TimeZone -Id "W. Europe Standard Time"
```
\
![Powershell Get Timezones](/images/PowershellGetTimezones.png)

---

> Author: Raymond Zaagsma  
> URL: https://raymondzaagsma.github.io/azure_vm_timezone/  

