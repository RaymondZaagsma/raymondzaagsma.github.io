---
title: "AVD Finding Azure VM SKU Powershell"
subtitle: ""
date: 2023-02-12T12:37:20+02:00
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
- AVD
categories:
- AVD

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




If you are working with Azure virtual machines, you may need to find the SKU (stock-keeping unit) of the images you want to use. The SKU is an important parameter because it determines the size, capacity, and capabilities of the virtual machine. 

To find the SKUs of Azure VM images, you can use PowerShell, a command-line interface that allows you to manage Azure resources. Here is a step-by-step guide on how to find the SKUs of Azure VM images using PowerShell.

Step 1: Open PowerShell

First, open PowerShell by clicking the Windows Start button and typing "PowerShell" in the search bar. Then, click on the Windows PowerShell app to open it.

Step 2: Connect to Azure

Next, you need to connect to your Azure account using PowerShell. To do this, type the following command in the PowerShell window:

```powershell
Connect-AzAccount
```

This will prompt you to sign in to your Azure account. Once you have signed in, you can proceed to the next step.

Step 3: Find the VM image

To find the SKU of an Azure VM image, you need to use the Get-AzVMImageSku cmdlet. This cmdlet retrieves the list of SKUs for a given image publisher, offer, and SKU name. 

To use this cmdlet, you need to provide the following parameters:

- Publisher: The name of the image publisher.
- Offer: The name of the image offer.
- Skus: The name of the SKU.

For example, to find the SKUs for the Windows 10 AVD image, you would use the following command:

```powershell
Get-AzLocation | select location,displayname

$locName = "West Europe"

 Get-AzVMImagePublisher -Location $locName | where-object {$_.PublisherName -like "*windows*"} | ft
 PublisherName,Location

$pubName="MicrosoftWindowsDesktop"

Get-AzVMImageOffer -Location $locName -PublisherName $pubName | ft Offer,PublisherName,Location

$offerName="Windows-10"

get-azvmimagesku -Location $locName -PublisherName $pubName -Offer $offerName | ft Skus,Offer,PublisherName,Location

$skuName="win10-22h2-avd-g2"

 Get-AzVMImage -Location $locName -PublisherName $pubName -Skus $skuName -Offer $offerName

```

This command will return a list of SKUs for the Windows 10 AVD image, along with their properties.


Conclusion

Finding the SKUs of Azure VM images is an important task if you want to create virtual machines with the right size and capacity. Using PowerShell, you can easily retrieve the SKUs for a given image publisher, offer, and SKU name. By filtering the results based on specific criteria, you can narrow down the list of SKUs to find the one that best meets your needs.