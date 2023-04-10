---
title: "AVD Registry GPO Hide Drives"
subtitle: ""
date: 2022-11-29T12:50:36+01:00
draft: false
author: "Raymond Zaagsma"
authorLink: ""
authorEmail: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0
images : [https://raymondzaagsma.github.io/images/RegistryCreateNoDrivesValue.png]

tags:
- AVD , GPO
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

## How to hide a drive using Registry

![Hide Drive Registry](/images/RegistryCreateNoDrivesValue.png)

Hide a particular drive on your computer using the Registry.


1. Use the Windows key + R keyboard shortcut to open the Run command.
2. Type regedit, and click OK to open the registry.
3. Browse the following path:HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\ Explorer
4. Right-click on the right side, select New, and click on DWORD (32-bit) Value.
5. Name the new DWORD NoDrives and press Enter.
6. Double-click the newly created DWORD.
7. Under "Base," select the Decimal option.
8. On "Value data" enter the decimal number that represents the drive letter you want to hide. 

In this blog post, we'll be using value 32, because we're hiding the F: drive.  
If you want to hide multiple drives, you'll need to add the decimal numbers.  
For example, if you're trying to hide drive A:, B: , C: , D: , E: and F:, you'll need to add 1 + 2 + 4 + 8 + 16 + 32, which means that the value you need to enter is 63.  
\
These decimal numbers as reference to hide specific drives:  
A: 1  
B: 2  
C: 4   
D: 8   
E: 16   
F: 32   
G: 64  
H: 128   
I: 256   
J: 512   
K: 1024   
L: 2048   
M: 4096   
N: 8192   
O: 16384   
P: 32768   
Q: 65536   
R: 131072   
S: 262144   
T: 524288   
U: 1048576   
V: 2097152   
W: 4194304   
X: 8388608   
Y: 16777216   
Z: 33554432   
ALL: 67108863  
