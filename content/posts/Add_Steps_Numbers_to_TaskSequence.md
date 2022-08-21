---
title: "Add Steps numbers to Task Sequence"
date: 2022-08-20T13:36:04+02:00
draft: false
---

In order to add steps numbers to the task sequence you will have to modify the ZTIUtility.vbs file.

Make a copy of the ZTIUtility.vbs , then in the original ZTIUtility.vbs replace the code mentioned below.


![Progrssbar with steps numbers](/images/progressbar.JPG)



## Original ReportProgress Function in ZTIUtility.vbs

```
Public Function ReportProgress(sMsg, iPercent)

		Dim iMaxPercent
		Dim oProgress
		Dim uStep
		Dim uMaxStep

		CreateEntry "Update progress [ " & iPercent & " ] : " & sMsg , LogTypeVerbose


		' Try to create the progress UI object

		On Error Resume Next
		Set oProgress = CreateObject("Microsoft.SMS.TSProgressUI")
		If Err then
			Err.Clear

			' Record the progress in the registry

			oShell.RegWrite "HKLM\Software\Microsoft\Deployment 4\ProgressPercent", iPercent, "REG_DWORD"
			oShell.RegWrite "HKLM\Software\Microsoft\Deployment 4\ProgressText", sMsg, "REG_SZ"

			on error goto 0
			Exit Function
		End if
		On Error Goto 0


		' Update the progress

		On Error Resume Next

		iMaxPercent = 100
		uStep = CLng(oEnvironment.Item("_SMSTSNextInstructionPointer"))
		uMaxStep = CLng(oEnvironment.Item("_SMSTSInstructionTableSize"))
		Call oProgress.ShowActionProgress(oEnvironment.Item("_SMSTSOrgName"), oEnvironment.Item("_SMSTSPackageName"), oEnvironment.Item("_SMSTSCustomProgressDialogMessage"), oEnvironment.Item("_SMSTSCurrentActionName"), (uStep), (uMaxStep), sMsg, (iPercent), (iMaxPercent))
		If Err then
			CreateEntry "Unable to update progress: " & Err.Description & " (" & Err.Number & ")", LogTypeInfo
			ReportProgress = Failure
			Err.Clear
			Exit Function
		End if

		On Error Goto 0


		' Dispose of the object

		Set oProgress = Nothing

	End Function
```

## Modified ReportProgress Function in ZTIUtility.vbs

```
Public Function ReportProgress(sMsg, iPercent)

		Dim iMaxPercent
		Dim oProgress
		Dim uStep
		Dim uMaxStep

		'Region http://www.systanddeploy.com/2018/02/add-complete-progression-status-to.html
		Dim uStatus, uStep_Division, uStep_Division_Round, uStep_Percent
		'End Region

		CreateEntry "Update progress [ " & iPercent & " ] : " & sMsg , LogTypeVerbose


		' Try to create the progress UI object

		On Error Resume Next
		Set oProgress = CreateObject("Microsoft.SMS.TSProgressUI")
		If Err then
			Err.Clear

			' Record the progress in the registry

			oShell.RegWrite "HKLM\Software\Microsoft\Deployment 4\ProgressPercent", iPercent, "REG_DWORD"
			oShell.RegWrite "HKLM\Software\Microsoft\Deployment 4\ProgressText", sMsg, "REG_SZ"

			on error goto 0
			Exit Function
		End if
		On Error Goto 0


		' Update the progress

		On Error Resume Next

		iMaxPercent = 100
		uStep = CLng(oEnvironment.Item("_SMSTSNextInstructionPointer"))
		uMaxStep = CLng(oEnvironment.Item("_SMSTSInstructionTableSize"))
		'Region http://www.systanddeploy.com/2018/02/add-complete-progression-status-to.html
		uStep_Division = uStep / uMaxStep * 100  
		uStep_Division_Round = Round(uStep_Division)
		uStep_Percent = uStep_Division_Round & " % completed"
		uStatus = oEnvironment.Item("_SMSTSCurrentActionName") & " - " & " Step " & uStep & " on " & uMaxStep & " - " & uStep_Percent

		Call oProgress.ShowActionProgress(oEnvironment.Item("_SMSTSOrgName"), oEnvironment.Item("_SMSTSPackageName"), oEnvironment.Item("_SMSTSCustomProgressDialogMessage"), uStatus, (uStep), (uMaxStep), sMsg, (iPercent), (iMaxPercent))
		'End Region
		
		If Err then
			CreateEntry "Unable to update progress: " & Err.Description & " (" & Err.Number & ")", LogTypeInfo
			ReportProgress = Failure
			Err.Clear
			Exit Function
		End if

		On Error Goto 0


		' Dispose of the object

		Set oProgress = Nothing

	End Function
```
