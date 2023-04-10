# Intune Dynamic Device Groups


<!--more-->

# Intune Dynamic Device Groups

Microsoft Intune is a cloud-based mobile device management (MDM) and enterprise mobility management (EMM) platform that enables IT professionals to manage and secure mobile devices and applications in their organization. One of the key features of Intune is the ability to create dynamic device groups, which allows for more efficient device management. In this blog post, we'll explore what dynamic device groups are and how they can be used in Intune.

## What are Dynamic Device Groups?

Dynamic device groups in Intune are groups that automatically update their membership based on predefined criteria. This means that the group membership is dynamic and can change over time, based on factors such as device properties, user attributes, or other criteria.

Dynamic device groups can be created for a variety of purposes, such as:

1. Targeting policies: Dynamic device groups can be used to target policies to specific devices or groups of devices based on their properties, such as the device model, operating system version, or device compliance status.

2. Deploying applications: Dynamic device groups can be used to deploy applications to specific devices or groups of devices based on their properties, such as the device model, operating system version, or device compliance status.

3. Reporting and monitoring: Dynamic device groups can be used to monitor and report on the status of devices within the group, such as the number of compliant devices, the number of non-compliant devices, and the number of devices that require attention.

## How to Create Dynamic Device Groups in Intune

To create a dynamic device group in Intune, follow these steps:

1. Log in to the Intune console and navigate to the Devices blade.

2. Click on the Device groups tab and then click on the New Group button.

3. Choose the type of group you want to create (in this case, a dynamic device group).

4. Define the criteria for the group membership, such as device properties, user attributes, or other criteria.

5. Give the group a name and a description, and then click on the Create button to create the group.

Once the group is created, it will automatically update its membership based on the criteria defined in step 4. This means that devices that meet the criteria will be added to the group, while devices that no longer meet the criteria will be removed from the group.

## Examples

### Windows 10 Corporate Devices
```
(device.deviceOSType -startsWith "Windows") and (device.deviceOSVersion -startsWith "10.0") and (device.deviceOwnership -eq "Company")
```
```
(device.deviceOSVersion -startsWith "10.0") and (device.deviceOSType -startsWith "Windows") and (device.managementType -eq "MDM")
```

### iOS BYOD Devices
```
(device.deviceOwnership -eq "Personal") and (device.deviceOSType -eq "iPhone") or (device.deviceOSType -eq "iPad") and (device.deviceOwnership -eq "Personal")
```

### iOS Corporate Devices
```
(device.deviceOwnership -eq "Company") and (device.deviceOSType -eq "iPhone") or (device.deviceOSType -eq "iPad") and (device.deviceOwnership -eq "Company")
```
### DEP devices using a profile named ‘DEP devices’
```
(device.enrollmentProfileName -eq "DEP devices")
```
### Android Personal devices
```
(device.deviceOSType -contains "AndroidForWork") and (device.deviceOwnership -eq "Personal") and (device.managementType -eq "MDM")
```
### Android Enterprise devices
```
(device.deviceOSType -contains "AndroidEnterprise")
```
### Android Enterprise corporate-owned dedicated devices using a profile named ‘Dedicated Android’
```
(device.enrollmentProfileName -match "Dedicated Android")
```
### Corporate-owned Android Enterprise devices
```
(device.deviceOSType -contains "AndroidEnterprise") and (device.deviceOwnership -eq "Company") and (device.enrollmentProfileName -eq null)
```
### Corporate-owned Google Pixel devices
```
device.deviceManufacturer -eq "Google") -and (device.deviceModel -contains "Pixel") -and (device.deviceOwnership -eq "Company")
```


## Conclusion

Dynamic device groups in Intune are a powerful tool that allows IT professionals to efficiently manage and secure mobile devices in their organization. By automating the group membership based on predefined criteria, IT professionals can target policies, deploy applications, and monitor device status more efficiently. With dynamic device groups, IT professionals can save time and reduce the risk of errors, resulting in a more secure and efficient mobile device management environment.

---

> Author: Raymond Zaagsma  
> URL: https://raymondzaagsma.github.io/intune_dynamic_device_groups/  

