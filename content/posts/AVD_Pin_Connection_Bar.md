---
title: "AVD Pin Connection Bar"
subtitle: ""
date: 2023-03-11T11:26:45+02:00
draft: false
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

# Azure Virtual Desktop Pin Connection Bar

PinConnectionBar is a feature in Remote Desktop Services (RDS) that allows users to pin the Remote Desktop Connection bar to the top of the screen, providing quick and easy access to the most commonly used RDS features. In this blog post, we'll explore what PinConnectionBar is, how it works, and how to enable it in RDS.

## What is PinConnectionBar in AVD?

PinConnectionBar is a feature in RDS that allows users to pin the Remote Desktop Connection bar to the top of the screen, providing quick and easy access to the most commonly used RDS features. This feature is especially useful for users who frequently switch between multiple RDS sessions, as it provides a consistent and easy-to-access interface.

## How does PinConnectionBar work in AVD?

PinConnectionBar works by allowing users to pin the Remote Desktop Connection bar to the top of the screen. Once pinned, the Connection bar stays visible, even when the RDS session is in full-screen mode. This provides easy access to features such as disconnecting from the RDS session, accessing the Remote Desktop Connection settings, and more.

How to enable PinConnectionBar in RDS

### Values Explanation 
	0 The connection bar should not be pinned to the top of the remote session. 
	1 The connection bar should be pinned to the top of the remote session.

To enable PinConnectionBar in RDS, follow these steps:

Option 1 : 

1. Open the Remote Desktop Connection app on your client computer.

2. Click on the Show Options button.

3. Click on the Display tab.

4. Check the box next to "Pin the connection bar to the top of the screen."

5. Click on the Connect button to connect to your RDS session.

Option 2 : Add Value to Registry

1. Open the Registry Editor on your client computer

2. In HKEY_CURRENT_USER\Software\Microsoft\Terminal Server Client add a DWORD value PinConnectionBar

3. Set registry key value - 	1 The connection bar should be pinned to the top of the remote session.

Option 3 : Edit the RDP file

1. Open the .RDP file with Notepad++

2. Add a line with the following syntax - 	pinconnectionbar:i:<value>

3. Set Value - 	1 

Once connected, the Connection bar will be pinned to the top of the screen, providing easy access to the most commonly used RDS features.

## Conclusion

PinConnectionBar is a useful feature in RDS that allows users to pin the Remote Desktop Connection bar to the top of the screen, providing quick and easy access to the most commonly used RDS features. By following the steps outlined above, users can easily enable PinConnectionBar in RDS and improve their productivity by streamlining the RDS workflow. With PinConnectionBar, RDS users can quickly and easily switch between multiple sessions and access important features with ease.
