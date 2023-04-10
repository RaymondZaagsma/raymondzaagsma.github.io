# Liquit Start Windows App


<!--more-->

# Liquit Start Windows App

Liquit Workspace is a comprehensive solution for application and desktop management. With Liquit, you can deploy and manage various types of applications, including Windows Store apps. In this blog post, we'll show you how to create a Windows Store app in Liquit Workspace.

Step 1: Create a new application

To create a Windows Store app in Liquit Workspace, you need to start by creating a new application. You can do this by following these steps:

1. Log in to the Liquit console.
2. Click on "Manage" in the left-hand menu.
3. Click on the "Packages".
4. Create Custom Package.
5. Enter the name of the application.
6. Add entitlement
7. Finish

Step 2: Configure the application

After you have created the application, you need to configure it by following these steps:

1. Go to Actions
2. Create Action Set
3. Select Install

Step 2: Configure the application Launch

1. Go to Actions
2. Create Action Set
3. Select Launch

## Finding Start Windows App Values

To start a Windows App from Liquit two values are required :

1. Package Family Name
2. Application Id

![Connection information](/images/Liquit_Start_Windows_App.png)

Open the “Run” dialog box using the Win + R key combination

![Open Run](/images/Liquit_Start_Windows_App_open_run.png)

In the text field, type the command shell:AppsFolder, and hit “Enter”. This opens File Explorer with a list of the Microsoft Store apps installed on your PC.

![Shell Apps Folder](/images/Liquit_Start_Windows_App_shell_apps_folder.png)

Right Click on empty space in explorer
Show more Options
Sort by - More
Enable the AppUserModelid 

![Explorer More Details](/images/Liquit_Start_Windows_App_Explorer_More_Details.png)

Example TrueDWG Viewer

![Example TrueDWG Viewer](/images/Liquit_Start_Windows_App_TrueDWG.png)

Package Family Name : 

89006A2E.AutoCAD360_8.43.0.0_x64__tf1gferkr813w

Application Id (everything after the !) : 

eUWPAutoCAD

Example Company Portal

![Example Company Portal](/images/Liquit_Start_Windows_App_Company_Portal.png)

Package Family Name : 

Microsoft.CompanyPortal_8wekyb3d8bbwe

Application Id (everything after the !) : 

App

Enter the Package Family Name and App Id into the liquit - Start Windows App

![Example TrueDWG Viewer Done](/images/Liquit_Start_Windows_App_TrueDWG_Done.png)


## Conclusion

Creating and deploying Windows Store apps in Liquit Workspace is a straightforward process. By following the steps outlined in this blog post, you can quickly create and deploy Windows Store apps to your users. With Liquit, you can manage all of your applications from a single console, making it easier to keep your software up-to-date and secure.

---

> Author: Raymond Zaagsma  
> URL: https://raymondzaagsma.github.io/liquit_start_windows_app/  

