# xComputerManagement

The **xComputerManagement** module contains the following resources:

* xComputer - allows you to configure a computer by changing its name and
  modifying its domain or workgroup.
* xOfflineDomainJoin - allows you to join computers to an AD Domain using
  an [Offline Domain Join](https://technet.microsoft.com/en-us/library/offline-domain-join-djoin-step-by-step(v=ws.10).aspx)
  request file.
* xScheduledTask - used to define basic recurring scheduled tasks on the
  local computer.
* xPowerPlan - specifies a power plan to activate.
* xVirtualMemory - used to set the properties of the paging file on the
  local computer.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/)
or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any
additional questions or comments.

## Branches

### master

[![Build status](https://ci.appveyor.com/api/projects/status/cg28qxeco39wgo9l/branch/master?svg=true)](https://ci.appveyor.com/project/PowerShell/xsqlserver/branch/master)
[![codecov](https://codecov.io/gh/PowerShell/xComputerManagement/branch/master/graph/badge.svg)](https://codecov.io/gh/PowerShell/xComputerManagement/branch/master)

This is the branch containing the latest release - no contributions should be made
directly to this branch.

### dev

[![Build status](https://ci.appveyor.com/api/projects/status/cg28qxeco39wgo9l/branch/dev?svg=true)](https://ci.appveyor.com/project/PowerShell/xComputerManagement/branch/dev)
[![codecov](https://codecov.io/gh/PowerShell/xComputerManagement/branch/dev/graph/badge.svg)](https://codecov.io/gh/PowerShell/xComputerManagement/branch/dev)

This is the development branch to which contributions should be proposed by contributors
as pull requests. This development branch will periodically be merged to the master
branch, and be released to [PowerShell Gallery](https://www.powershellgallery.com/).

## Contributing

Please check out common DSC Resources [contributing guidelines](https://github.com/PowerShell/DscResource.Kit/blob/master/CONTRIBUTING.md).

## xComputer

xComputer resource has following properties:

* Name: The desired computer name
* DomainName: The name of the domain to join
* JoinOU: The distinguished name of the organizational unit that the computer
  account will be created in
* WorkGroupName: The name of the workgroup
* Credential: Credential to be used to join or leave domain
* CurrentOU: A read-only property that specifies the organizational unit that
  the computer account is currently in

## xOfflineDomainJoin

xOfflineDomainJoin resource is a [Single Instance](https://msdn.microsoft.com/en-us/powershell/dsc/singleinstance)
resource that can only be used once in a configuration and has following properties:

* IsSingleInstance: Must be set to 'Yes'. Required.
* RequestFile: The full path to the Offline Domain Join request file. Required.

## xScheduledTask

xScheduledTask resource is used to define basic recurring scheduled tasks on the
local computer.
Tasks are created to run indefinitely based on the schedule defined.
xScheduledTask has the following properties:

* TaskName: The name of the task
* TaskPath: The path to the task - defaults to the root directory
* Description: The task description
* ActionExecutable: The path to the .exe for this task
* ActionArguments: The arguments to pass the executable
* ActionWorkingPath: The working path to specify for the executable
* ScheduleType: When should the task be executed
  ("Once", "Daily", "Weekly", "AtStartup", "AtLogOn")
* RepeatInterval: How many units (minutes, hours, days) between each run of this
  task?
* StartTime: The time of day this task should start at - defaults to 12:00 AM.
  Not valid for AtLogon and AtStartup tasks
* Ensure: Present if the task should exist, false if it should be removed - defaults
  to Present.
* Enable: True if the task should be enabled, false if it should be
  disabled
* ExecuteAsCredential: The credential this task should execute as. If not
  specified defaults to running as the local system account
* DaysInterval: Specifies the interval between the days in the schedule. An
  interval of 1 produces a daily schedule. An interval of 2 produces an
  every-other day schedule.
* RandomDelay: Specifies a random amount of time to delay the start time of the
  trigger. The delay time is a random time between the time the task triggers
  and the time that you specify in this setting.
* RepetitionDuration: Specifies how long the repetition pattern repeats after
  the task starts.
* DaysOfWeek: Specifies an array of the days of the week on which Task Scheduler
  runs the task.
* WeeksInterval: Specifies the interval between the weeks in the schedule. An
  interval of 1 produces a weekly schedule. An interval of 2 produces an
  every-other week schedule.
* User: Specifies the identifier of the user for a trigger that starts a task
  when a user logs on.
* DisallowDemandStart: Indicates whether the task is prohibited to run on demand
  or not. Defaults to $false
* DisallowHardTerminate: Indicates whether the task is prohibited to be terminated
  or not. Defaults to $false
* Compatibility: The task compatibility level. Defaults to Vista. Possible
  values: "AT","V1","Vista","Win7","Win8"
* AllowStartIfOnBatteries: Indicates whether the task should start if the machine
  is on batteries or not. Defaults to $false
* Hidden: Indicates that the task is hidden in the Task Scheduler UI. Defaults
  to $false
* RunOnlyIfIdle: Indicates that Task Scheduler runs the task only when the
  computer is idle.
* IdleWaitTimeout: Specifies the amount of time that Task Scheduler waits for an
  idle condition to occur. DateTime ;
* NetworkName: Specifies the name of a network profile that Task Scheduler uses
  to determine if the task can run. The Task Scheduler UI uses this setting for
  display purposes. Specify a network name if you specify theRunOnlyIfNetworkAvailable
  parameter.
* DisallowStartOnRemoteAppSession: Indicates that the task does not start if the
  task is triggered to run in a Remote Applications Integrated Locally (RAIL) session.
* StartWhenAvailable: Indicates that Task Scheduler can start the task at any
  time after its scheduled time has passed.
* DontStopIfGoingOnBatteries: Indicates that the task does not stop if the
  computer switches to battery power.
* WakeToRun: Indicates that Task Scheduler wakes the computer before it runs the
  task.
* IdleDuration: Specifies the amount of time that the computer must be in an idle
  state before Task Scheduler runs the task.
* RestartOnIdle: Indicates that Task Scheduler restarts the task when the computer
  cycles into an idle condition more than once.
* DontStopOnIdleEnd: Indicates that Task Scheduler does not terminate the task if
  the idle condition ends before the task is completed.
* ExecutionTimeLimit: Specifies the amount of time that Task Scheduler is allowed
  to complete the task.
* MultipleInstances: Specifies the policy that defines how Task Scheduler handles
  multiple instances of the task. Possible values: "IgnoreNew","Parallel","Queue"
* Priority: Specifies the priority level of the task. Priority must be an integer
  from 0 (highest priority) to 10 (lowest priority). The default value is 7.
  Priority levels 7 and 8 are used for background tasks. Priority levels 4, 5,
  and 6 are used for interactive tasks.
* RestartCount: Specifies the number of times that Task Scheduler attempts to
  restart the task.
* RestartInterval: Specifies the amount of time that Task Scheduler attempts to
  restart the task.
* RunOnlyIfNetworkAvailable: Indicates that Task Scheduler runs the task only
  when a network is available. Task Scheduler uses the NetworkID parameter and
  NetworkName parameter that you specify in this cmdlet to determine if the
  network is available.

## xPowerPlan

xPowerPlan resource has following properties:

* IsSingleInstance: Specifies the resource is a single instance, the value must
  be 'Yes'.
* Name: The name of the power plan to activate.

## xVirtualMemory

xVirtualMemory resource is used to set the properties of the paging file on the
local computer.
xVirtualMemory has the following properties:

* Type: The type of the paging settings, mandatory, out of "AutoManagePagingFile",
  "CustomSize","SystemManagedSize","NoPagingFile"
* Drive: The drive to enable paging on, mandatory. Ignored for "AutoManagePagingFile"
* InitialSize: The initial size in MB of the paging file. Ignored for Type
  "AutoManagePagingFile" and "SystemManagedSize"
* MaximumSize: The maximum size in MB of the paging file. Ignored for Type
  "AutoManagePagingFile" and "SystemManagedSize"

## Versions

### Unreleased

* xComputer: Changed comparison that validates if we are in the correct AD
  Domain to work correctly if FQDN wasn't used.
* Updated AppVeyor.yml to use AppVeyor.psm1 module in DSCResource.Tests.
* Removed Markdown.md errors.
* Added CodeCov.io support.
* xScheduledTask
  * Fixed incorrect TaskPath handling - [Issue #45](https://github.com/PowerShell/xComputerManagement/issues/45)
* Change examples to meet HQRM standards and optin to Example validation
  tests.

### 2.0.0.0

* Updated resources
  * BREAKING CHANGE: xScheduledTask: Added nearly all available parameters for tasks
* xVirtualMemory:
  * Fixed failing tests.

### 1.10.0.0

* Added resources:
  * xVirtualMemory

### 1.9.0.0

* Added resources
  * xPowerPlan

### 1.8.0.0

* Converted AppVeyor.yml to pull Pester from PSGallery instead of
  Chocolatey.
* Changed AppVeyor.yml to use default image
* xScheduledTask: Fixed bug with different OS versions returning repeat interval
  differently

### 1.7.0.0

* Added support for enabling or disabling scheduled tasks
* The Name parameter resolves to $env:COMPUTERNAME when the value is localhost

### 1.6.0.0

* Added the following resources:
  * MSFT_xOfflineDomainJoin resource to join computers to an AD Domain using an
    Offline Domain Join request file.
  * MSFT_xScheduledTask resource to control scheduled tasks on the local server
* MSFT_xOfflineDomainJoin: Corrected localizedData.DomainAlreadyJoinedhMessage name.
* xComputer: Changed credential generation code in tests to avoid triggering
  PSSA rule PSAvoidUsingConvertToSecureStringWithPlainText.
  Renamed unit test file to match the name of Resource file.

### 1.5.0.0

* Update Unit tests to use the standard folder structure and test templates.
* Added .gitignore to prevent commit of DSCResource.Tests.

### 1.4.0.0

* Added validation to the Name parameter
* Added the JoinOU parameter which allows you to specify the organizational unit
  that the computer account will be created in
* Added the CurrentOU read-only property that shows the organizational unit that
  the computer account is currently in

### 1.3.0

* xComputer
  * Fixed issue with Test-TargetResource when not specifying Domain or
    Workgroup name
  * Added tests

### 1.2.2

* Added types to Get/Set/Test definitions to allow xResourceDesigner validation
  to succeed

### 1.2

* Added functionality to enable moving computer from one domain to another
* Modified Test-DscConfiguration logics when testing domain join

### 1.0.0.0

* Initial release with the following resources:
  * xComputer

## Examples

### Set the Name and the Workgroup Name

This configuration will set the computer name to 'Server01'
and make it part of 'ContosoWorkgroup' Workgroup.

```powershell
Configuration Example
{
    param
    (
        [Parameter()]
        [System.String[]]
        $NodeName = 'localhost'
    )

    Import-DscResource -Module xComputerManagement

    Node $NodeName
    {
        xComputer NewNameAndWorkgroup
        {
            Name          = 'Server01'
            WorkGroupName = 'ContosoWorkgroup'
        }
    }
}
```

### Switch from a Workgroup to a Domain

This configuration sets the machine name to 'Server01' and
joins the 'Contoso' domain.
Note: this requires an AD credential to join the domain.

```powershell
Configuration Example
{
    param
    (
        [Parameter()]
        [System.String[]]
        $NodeName = 'localhost',

        [Parameter(Mandatory = $true)]
        [ValidateNotNullorEmpty()]
        [System.Management.Automation.PSCredential]
        $Credential
    )

    Import-DscResource -Module xComputerManagement

    Node $NodeName
    {
        xComputer JoinDomain
        {
            Name       = 'Server01'
            DomainName = 'Contoso'
            Credential = $Credential # Credential to join to domain
        }
    }
}
```

### Set the Name while staying on the Domain

This example will set the machines name 'Server01' while remaining
joined to the current domain.
Note: this requires a credential for renaming the machine on the
domain.

```powershell
Configuration Example
{
    param
    (
        [Parameter()]
        [System.String[]]
        $NodeName = 'localhost',

        [Parameter(Mandatory = $true)]
        [ValidateNotNullorEmpty()]
        [System.Management.Automation.PSCredential]
        $Credential
    )

    Import-DscResource -Module xComputerManagement

    Node $NodeName
    {
        xComputer NewName
        {
            Name       = 'Server01'
            Credential = $Credential # Domain credential
        }
    }
}
```

### Set the Name while staying on the Workgroup

This example will set the machine name to 'Server01' while remaining
in the workgroup.

```powershell
Configuration Example
{
    param
    (
        [Parameter()]
        [System.String[]]
        $NodeName = 'localhost'
    )

    Import-DscResource -Module xComputerManagement

    Node $NodeName
    {
        xComputer NewName
        {
            Name = 'Server01'
        }
    }
}
```

### Switch from a Domain to a Workgroup

This example switches the computer 'Server01' from a domain and joins it
to the 'ContosoWorkgroup' Workgroup.
Note: this requires a credential.

```powershell
Configuration Example
{
    param
    (
        [Parameter()]
        [System.String[]]
        $NodeName = 'localhost',

        [Parameter(Mandatory = $true)]
        [ValidateNotNullorEmpty()]
        [System.Management.Automation.PSCredential]
        $Credential
    )

    Import-DscResource -Module xComputerManagement

    Node $NodeName
    {
        xComputer JoinWorkgroup
        {
            Name          = 'Server01'
            WorkGroupName = 'ContosoWorkgroup'
            Credential    = $Credential # Credential to unjoin from domain
        }
    }
}
```

### Join a Domain using an ODJ Request File

This example will join the computer to a domain using the ODJ
request file C:\ODJ\ODJRequest.txt.

```powershell
configuration Example
{
    param
    (
        [Parameter()]
        [System.String[]]
        $NodeName = 'localhost'
    )

    Import-DscResource -ModuleName xComputerManagement

    Node $NodeName
    {
        xOfflineDomainJoin ODJ
        {
          RequestFile = 'C:\ODJ\ODJBlob.txt'
          IsSingleInstance = 'Yes'
        }
    }
}
```

### Run a PowerShell script every 15 minutes on a server

This example will create a scheduled task that will call PowerShell.exe every 15
minutes to run a script saved locally.
The script will be called as the local system account

```powershell
Configuration Example
{
    param
    (
        [Parameter()]
        [System.String[]]
        $NodeName = 'localhost'
    )

    Import-DscResource -ModuleName xComputerManagement

    Node $NodeName
    {
        xScheduledTask MaintenanceScriptExample
        {
          TaskName           = "Custom maintenance tasks"
          ActionExecutable   = "C:\windows\system32\WindowsPowerShell\v1.0\powershell.exe"
          ActionArguments    = "-File `"C:\scripts\my custom script.ps1`""
          ScheduleType       = 'Once'
          RepeatInterval     = [datetime]::Today.AddMinutes(15)
          RepetitionDuration = [datetime]::Today.AddHours(10)
        }
    }
}
```

### Set Page File to be 2GB on C Drive

Example script that sets the paging file to reside on
drive C with the custom size 2048MB

```powershell
Configuration Example
{
    param
    (
        [Parameter()]
        [System.String[]]
        $NodeName = 'localhost'
    )

    Import-DSCResource -ModuleName xComputerManagement

    Node $NodeName
    {
        xVirtualMemory pagingSettings
        {
            Type        = 'CustomSize'
            Drive       = 'C'
            InitialSize = '2048'
            MaximumSize = '2048'
        }
    }
}
```
