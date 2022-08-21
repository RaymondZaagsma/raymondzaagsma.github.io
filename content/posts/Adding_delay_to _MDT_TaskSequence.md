---
title: "Adding a delay to MDT Task Sequence"
date: 2022-08-20T13:36:04+02:00
draft: false
---


When receiving the error, “A connection to the deployment share (\\mdt\DeploymentShare) could not be made.”

![litetouch.wsf](/images/connectionerror.jpg)

The solution is to add a delay to a task sequence.

In the deployment share , scripts folder edit the Litetouch.wsf script.  

```
Function ValidateDeployRootWithRecovery
  Dim sARF
  Dim sNetworkErrorHint
  DIm iRetVal
  Dim sLTISuspend
  'Delay wait for DHCP  
  wscript.sleep 5000
  If oUtility.ValidateConnectionEx(oEnvironment.Item("DeployRoot"), True) = Success then
   ValidateDeployRootWithRecovery = SUCCESS
   exit function
  End if
```
