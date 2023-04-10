# MDT Disable F8


<!--more-->

## How to disable F8 MDT

MDT, or Microsoft Deployment Toolkit, is a powerful tool used by IT professionals to automate the deployment of Windows operating systems and applications. However, sometimes the F8 key can interfere with the deployment process, leading to a less than optimal experience. In this blog post, we'll explore how to disable the F8 key during MDT deployment to ensure a smoother process.

The F8 key is a useful tool in Windows, allowing users to access the Advanced Boot Options menu when they encounter startup issues or need to troubleshoot problems. However, during MDT deployment, pressing F8 can interrupt the deployment process and take users out of the automated deployment environment. This can cause frustration for IT professionals and slow down the deployment process.

To disable the F8 key during MDT deployment, follow these steps:

Step 1: Open the the winpeshl.ini file found in the C:\Program Files\Microsoft Deployment Toolkit\Templates directory of your MDT installation.

Step 2: Replace /Bootstrap with /BootstrapNoSF8 in these text files.

Now, when deploying Windows using MDT, the F8 key will be disabled, and users will not be able to interrupt the deployment process by accessing the Advanced Boot Options menu.

It's important to note that disabling the F8 key can impact troubleshooting efforts if issues arise during deployment. IT professionals should weigh the pros and cons of disabling the F8 key before implementing this change.

In conclusion, disabling the F8 key during MDT deployment can help streamline the deployment process and ensure a smoother experience for IT professionals. By following the steps outlined above, you can easily disable the F8 key in MDT and ensure a successful deployment.

---

> Author: Raymond Zaagsma  
> URL: https://raymondzaagsma.github.io/mdt_disable_f8/  

