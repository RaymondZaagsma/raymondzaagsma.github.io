+++
title = "Install Visual C++ Redistributables with VcRedist"
date = 2022-08-20T13:36:04+02:00
draft = false
description = ""
tags = ['MDT']
Categories = ['MDT']
+++

This powershell module can download, install or import the Visual C++ Redistributables into MDT.
I use this Powershell Module to install VCRedist during the task sequence, i made a small adjustment to the script because the installation of the Powershell Module needs Nuget to work properly.

I add this powershell script as an application into MDT and add it to the task sequence.

```

$installedPackageProvider = Get-PackageProvider
if ($installedPackageProvider.Name -notmatch "NuGet") {
    Install-PackageProvider -Name NuGet -force
     Write-Host("Install powershell module NuGet")
}


$path = "C:\VcRedist"
If(!(test-path $path))
{
      New-Item -ItemType Directory -Force -Path $path
}

Install-Module VcRedist -Force 
Write-Host("Install powershell module VcRedist")

Import-Module VcRedist 
Write-Host("import powershell module VcRedist")

$VcList = Get-VcList | Get-VcRedist -Path "C:\VcRedist"
$VcList | Install-VcRedist -Path C:\VcRedist
```

This script is originally created by Aaron Parker, see link below for the original article.


[Original Article](https://stealthpuppy.com/vcredist-powershell-module/)
