# ----Start of file showPowers-----------------------------------------------------------------
# PowerShell command list
# Get-Help Logical assistance
```ps1
    Get-Help Set-ExecutionPolicy -online # pulls up set execution documentation
    Get-Help about_* # about_cmdlet gets the description for the cmdlet, * gets all cmdlets
    Get-Help Get-Help -Examples # Provides examples of the Get-Help cmdlet
    # Get-Help [[-Name] <System.String>] [-Full] [-Examples] [-Detailed] [-Online] [-ShowWindow] [<CommonParameters>]]
# Cmdlet References
    Get-Command #[-listImported | -All  
    Get-Member  # Quick inspect via cmdlet: 
    $obj | Get-Member (shows TypeName at the top). # Gets the members of objects (properties and methods)
#Session Cmdlets
    Get-ExecutionPolicy # Get script permissions
    Get-Process # Gets the running processes
    Get-Verb # Shows typical verb rules for functions or cmdlet
    Get-Variable # Gets the variables in the current session
    Get-Unique # Gets unique items from a sorted list
    Get-TypeData # Gets the extended type data in the current session
    Get-Service # Gets the services on a local or remote machine
    Get-Runspace # Gets the runspaces in the current session
    Get-RunspaceDebugging # Gets the runspace debugging settings
    Get-History # Gets the command history
    Get-Alias # Gets the aliases in the current session
# Variable Cmdlets
    New-Variable # Creates a new variable in the current session
    Set-Variable # Sets the value of a variable in the current session
    Clear-Variable # Deletes the contents of the specified variable
    Get-MarkdownOption
    Set-MarkdownOption
    Remove-Variable # Deletes the specified variable
# Write commands
    Write-Progress # Displays a progress bar in the PowerShell console
    Write-Host # Displays messages in the PowerShell console
    Write-Output # Sends the specified objects to the next command in the pipeline
    Write-Error # Writes an error message to the error stream
    Write-Warning # Writes a warning message to the warning stream
    Write-Debug # Writes a debug message to the debug stream
    Write-Verbose # Writes a verbose message to the verbose stream
    Write-Information # Writes an information message to the information stream
# Query Cmdlets
    Select-Object # Selects specific properties of an object or set of objects
    Sort-Object # Sorts objects by property values
    Group-Object # Groups objects by property values
    Measure-Object # Calculates the numeric properties of objects
    Out-Default # Sends output to the default output stream
    Out-File # Sends output to a file
    Out-Host # Sends output to the host
    Out-Null # Deletes output instead of sending it to the console
    Out-Printer # Sends output to a printer
    Where-Object # Selects objects from a collection based on their property values
#Misc Commands
    Tee-Object # Sends output to both the console and a file or variable
    Install-Package # Installs one or more software packages
    Send-MailMessage # Sends an email message
    Get-PSHost # Gets the PowerShell host information
    Get-PSHostProcessInfo # Gets information about PowerShell host processes
    Invoke-WebRequest # Makes HTTP and HTTPS requests to a web page or web service
    Invoke-RestMethod # Sends HTTP and HTTPS requests to Representational State Transfer (REST) web services
    Install-PackageProvider # Installs one or more package providers
    Find-PackageProvider # Finds package providers available in registered package sources
    Find-Package # Finds software packages available in registered package sources    
    Save-Module # Saves a module from an online gallery to a local path
    Save-PSSession # Saves the current PowerShell session to a file
    New-PSSession # Creates a new PowerShell session
    New-ModuleManifest # Creates a new module manifest file
    New-Item # Creates a new item at the specified location
    New-ItemProperty # Creates a new property for an item
    New-Alias # Creates a new alias for a cmdlet or function
    New-Object # Creates an instance of a .NET Framework or COM object
    New-Module # Creates a new module in the current session
    New-Service # Creates a new service
    New-WebServiceProxy # Creates a web service proxy object
    New-Variable # Creates a new variable in the current session
# Test Cmdlets
    Test-Connection # Sends ICMP echo request packets (pings) to one or more computers
    Test-FileCatalog # Tests the integrity of files in a file catalog
    Test-Json # Tests whether a string is valid JSON
    Test-ModuleManifest # Tests the syntax of a module manifest file
    Test-PSSessionConfigurationFile # Tests the syntax of a PowerShell session configuration file
    Test-PSScriptInfo # Tests the syntax and structure of a PowerShell script file
    Test-PSScriptFileInfo # Tests the integrity of a PowerShell script file

# Set Cmdlets
    Set-ExecutionPolicy # Sets the user preference for the PowerShell script execution policy
    Set-Item # Sets the value of an item at the specified location
    Set-ItemProperty # Sets the properties of a specified item
    Set-Location # Sets the current working location to a specified location
    Set-PSDebug # Enables or disables script debugging in the current session
    Set-StrictMode # Configures the strict mode settings for the current session
    Set-Variable # Sets the value of a variable in the current session
    Set-Clipboard # Sets the content of the clipboard
    Set-Content # Sets the content of a file
    Set-File # Sets the content of a file
    Set-FileProperty # Sets the properties of a specified file
    Set-Culture # Sets the culture for the current session
    Set-Date # Sets the system date and time
    Set-ExecutionPolicy # Sets the user preference for the PowerShell script execution policy
    Set-JobTrigger # Sets the trigger for a scheduled job
    Set-LocalGroup # Sets the properties of a local group
    Set-LocalUser # Sets the properties of a local user account
    Set-Process # Sets the properties of a process
    Set-Service # Sets the properties of a service
    Set-PSBreakpoint # Sets a breakpoint in a script or command
    Set-TraceSource # Sets the trace source for a script or command
    Set-User # Sets the properties of a user account
    Set-Variable # Sets the value of a variable in the current session
    Set-PSReadLineKeyHandler # Sets a key handler for the PSReadLine module
    Set-PSReadLineOption # Sets options for the PSReadLine module
    Set-RuleOption # Sets options for a Windows Defender Application Control rule
    Set-ScheduledJob # Sets the properties of a scheduled job
    Set-ScheduledJobOption # Sets options for a scheduled job
    Set-SecurityPolicy # Sets the properties of a security policy
    Set-UserPolicy # Sets the properties of a user policy
    Set-SecureBootUEFI # Sets the Secure Boot UEFI settings
    Set-RuleOption # Sets options for a Windows Defender Application Control rule
    Set-VHD # Sets the properties of a virtual hard disk (VHD)
    Set-VM # Sets the properties of a virtual machine (VM)
    Set-VMBios # Sets the BIOS properties of a virtual machine (VM)
    Set-VMHost # Sets the properties of a Hyper-V host
    Set-WinGetUserSettings # Sets user settings for the Windows Package Manager (WinGet)
# Imports
    Import-PSD1 # Imports a PowerShell data file (.psd1) and creates a hashtable
    Import-PowerShellDataFile # Imports a PowerShell data file (.psd1) and creates a hashtable
    Import-Certificate # Imports a certificate into a certificate store
    Import-Module # Imports a module into the current session
    Import-Clixml # Imports a Common Language Infrastructure (CLI) XML file and creates an object
    Import-PSSession # Imports commands from another PowerShell session
    Import-Counter # Imports performance counter data from a performance counter log file
    Import-Csv # Imports a comma-separated value (CSV) file and creates table-like custom objects
    Import-Excel # Imports data from an Excel spreadsheet
    Import-WinhttpProxySettings # Imports WinHTTP proxy settings into the current session
# Exports
    Export-ModuleMember # Exports functions, aliases, variables, and cmdlets from a module
    Export-PowerShellDataFile # Exports a hashtable to a PowerShell data file (.psd1)
    Export-Certificate # Exports a certificate from a certificate store to a file
    Export-Clixml # Exports an object to a Common Language Infrastructure (CLI) XML
    Export-PSSession # Exports commands from the current session to a PowerShell session configuration file
    Export-Counter # Exports performance counter data to a performance counter log file
    Export-Csv # Exports objects to a comma-separated value (CSV) file
    Export-Excel # Exports data to an Excel spreadsheet
# Query in PowerShell
    Microsoft.PowerShell.Utility\Select-Object
    Microsoft.PowerShell.Utility\Where-Object
    Get-Command -Module Microsoft.PowerShell.* | Select-Object Name, ModuleName
 # Type Inspection
    # Use the .NET method: 
    $obj.GetType() (returns a System.Type).
    # Common details: 
    $obj.GetType().FullName, .Name, or .AssemblyQualifiedName.
    # Pipeline object 
    ($PSItem/$_): ... | ForEach-Object { $_.GetType().FullName }
    # Type check (related): 
    $obj -is [string] (returns $true/$false).
# Elevate Session to Admin
    Start-Process pwsh -Verb RunAs # Start process calls a new powershell ran as the admin
# Variables
  # Profile Scope
    $host # ex of your powershell window and details
    $PSVersionTable # Executing Powershell version details
    $PSVersionTable.PSEdition # Desktop or Core
    $PROFILE # file path to Powershell profile config file
    $ErrorActionPreference # Setting for when an exception is encountered.
    $env:UserName # Environment variable for current user
    $env:ComputerName # Environment variable for current computer name
    $env:UserDomain # Environment variable for current user domain
    $env:CommonProgramFiles # Environment variable for common program files path
    $env:ProgramFiles # Environment variable for program files path
    $PWD # Present Working Directory
    $env:OneDrive # Environment variable for OneDrive path
    $env:SystemRoot # Environment variable for System Root path
    $env:TEMP # Environment variable for Temp path
    $env:PATH # # semicolon delimited list of open paths
    $env:COLORTERM # Environment variable for terminal color support

# Terminal Input/Output # Newline character is `n
    $pathPartTwo = Read-Host "Where do you want to go?"
    Write-Output "Lets go `n$pathPartOne$pathPartTwo"
# Pathing
    Set-Location -Path "..\"
    cd "$fullPath"
    $PSCommandPath # Full path of the script being ran # alternate: $MyInvocation.MyCommand.Path
    $PSScriptRoot # Directory of the script being ran
    Get-Location # Gets current location
    Get-ChildItem -Path "$fullPath" # Lists items in the specified path
    $thisScriptsParent = $PSScriptRoot # calls parent directory of the script being ran.
    $Profile1Path = Get-ChildItem -Path "$env:USERPROFILE" -Filter "Profile-1.ps1" -Recurse -ErrorAction SilentlyContinue

# File Management
    New-Item -Path "C:\Users\rmedi\Scripts\TestScript.ps1" -ItemType File # Error if file exists, -ItemType can be File/Directory
    Set-Content -Path "C:\Users\rmedi\Scripts\TestScript.ps1" -Value 'Write-Output "Hello I overwrite file content."'
    Add-Content -Path "C:\Users\rmedi\Scripts\TestScript.ps1" -Value 'Write-Output "Hello I append file content."'
    Get-Content -Path "C:\Users\rmedi\Scripts\TestScript.ps1" # Outputs the content to the terminal
    notepad "C:\Users\rmedi\Scripts\TestScript.ps1" # Pulls up the file in notepad
    Remove-Item -Path "C:\Users\rmedi\Scripts\TestScript.ps1" # Deletes the file
    New-Item # Creates a new item at the specified location
    Get-Item # Gets the item at the specified location # works with files, registry, etc.
    Get-ItemProperty # Gets the properties of a specified item
    Set-ItemProperty # Sets the properties of a specified item
    Remove-Item # Deletes the specified item
    Clear-Item # Deletes the contents of the specified item
# Casting
    $stringVar = "25"
    $stringCast = ([int]$stringVar + 10)
    $stringCast = Write-Output "[string]$stringCast back to a string"
# Profile ex) C:\Users\rmedi\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
    $PROFILE # Shows your profile path and file
    # edit profile: notepad $PROFILE
# Variables
    #". " notation makes every variable part of the parents scope, even local
    $Global:globalVar = "I live everywhere" # Scope: Global | Description: Lives across the entire PowerShell session (console or host).
    $Script:runningScriptPath = "$PSScriptRoot\TestScript.ps1"# Scope: Script | Description: Exists within a single .ps1 file or module (.psm1).
    $Local:Count = 10 (usually just $Count = 10)# Scope: Local | Description: Exists within the current scope — default for most variables (functions, loops, etc.).
    $Private:Token = "secret" # Scope: Private | Description: Visible only inside the current scope, even if a parent scope exists.
    #$Env:Path += ";C:\Tools" # Scope: Env | Description: Maps to system environment variables (like %PATH% or $Env:USERNAME).
    # Scope: Session | Description: Applies only in PowerShell 7 remoting / sessions (PSSessions).

# Functions
# & lets you call a function by its string name

# Try / Catch Exception Handling
    Try {
        # Code that may throw an exception
        $result = 10 / 0
        Write-Host "Result: $result"
    } Catch {
        # Handle the exception
        # $PSItem is an automatic variable representing the current error object
        # $_ is an alias for $PSItem
        # $.Exception → the underlying .NET exception (use .Message, .GetType().FullName)
        # $.CategoryInfo → error category/context
        # $.FullyQualifiedErrorId → stable error identifier
        # $.InvocationInfo → command, position, script line info
        # $.TargetObject → object involved in the error
        # $.ScriptStackTrace → PowerShell stack trace
        Write-Host "An error occurred: $($_.Exception.Message)"
        #customUtilities #Write-Host $(Get-ExceptionDetails -Exception $_ -ErrorActionPreference SilentlyContinue)
    } Finally {
        # Code that runs regardless of success or failure
        Write-Host "Execution completed."
    }

# Execution Policies
# ---------------------------------------
# Restricted (default): No scripts run.
# RemoteSigned: Local scripts run; downloaded scripts need a signature.
# Unrestricted: All scripts run (not recommended for security).
# Bypass: No restrictions (use only for automation scenarios).
# Scope ExecutionPolicy

# Scope
# ---------------------------------------
# MachinePolicy: Set by Group Policy for all users on the computer; highest precedence.
# UserPolicy: Set by Group Policy for the current user; overrides all except MachinePolicy.
# Process: Applies only to the current PowerShell session; temporary.
# CurrentUser: Applies to the current user across all sessions; stored in user profile.
# LocalMachine: Applies to all users on the computer; stored system-wide.


# Variables
# ---------------------------------------
# See Variables Section

# if syntax
# ---------------------------------------
# 🧩 1. Basic if Syntax
if (<condition>) { <code> }
# Example: 
if ($x -gt 10) { Write-Host "x is greater than 10" }

# ⚙️ 2. if / else Syntax
if (<condition>) { <true code> } else { <false code> }
# Example: 
if ($isReady) { Write-Host "Ready to go!" } else { Write-Host "Not ready yet." }

# 🧭 3. if / elseif / else Chain
if (<condition1>) { <code1> } elseif (<condition2>) { <code2> } else { <default code> }
# Example: 
if ($score -ge 90) { "A" } elseif ($score -ge 80) { "B" } elseif ($score -ge 70) { "C" } else { "F" }

# 🔍 4. Comparison Operators
# -eq (equal) → 
if ($x -eq 5) { }
# -ne (not equal) → 
if ($x -ne 5) { }
# -gt (greater than) → 
if ($x -gt 5) { }
# -ge (greater or equal) → 
if ($x -ge 5) { }
# -lt (less than) → 
if ($x -lt 5) { }
# -le (less or equal) → 
if ($x -le 5) { }
# -like (wildcard match) → 
if ($name -like "A*") { }
# -match (regex match) → 
if ($name -match "^A") { }
# -contains (collection contains item) → 
if (@('a','b') -contains 'a') { }

# 🔢 5. Logical Operators
# -and → both true → 
if (($x -gt 0) -and ($x -lt 10)) { }
# -or → either true → 
if (($color -eq "red") -or ($color -eq "blue")) { }
# -not or ! → negation → 
if (-not $isReady) { } or if (!$isReady) { }

# 🧠 6. Truthy / Falsy Rules
# Falsey: 
$false, $null, 0, "", '', @()
# Everything else evaluates to True
# Example: 
if ($null) { "True" } else { "False" } → outputs "False"

# ⚙️ 7. One-Liner if Statements
if ($x -gt 0) { "Positive" } else { "Non-positive" }
# Or inline with semicolons: 
if ($x -gt 0) { "Positive" } elseif ($x -eq 0) { "Zero" } else { "Negative" }

# 💡 8. Ternary Operator (PowerShell 7+)
$result = if ($x -gt 0) { "Positive" } else { "Negative" }
# or shorthand: 
$result = ($x -gt 0) ? "Positive" : "Negative"

# 🧾 9. Example Putting It All Together
$temperature = 72
if ($temperature -gt 90) { "It's hot!" }
elseif ($temperature -gt 70 -and $temperature -le 90) { "Perfect weather." }
else { "A little chilly." }


# for loops Syntax
# ---------------------------------------
# Standard foreach loop:
foreach ($item in $array) { <code> }
# Example: 
foreach ($color in $colors) { Write-Host "Color: $color" }

Pipeline ForEach-Object loop:
$array | ForEach-Object { Write-Host "Item: $_" }

# Difference:
foreach ($x in $array) → keyword (faster, in-memory)
ForEach-Object { ... } → cmdlet (streaming, used with pipelines)

# Index-based loop:
for ($i = 0; $i -lt $array.Length; $i++) { Write-Host "Index $i = $($array[$i])" }

# Nested foreach example:
foreach ($row in $matrix) { foreach ($cell in $row) { Write-Host "Cell: $cell" } }

# Flow control:
if ($num -eq 5) { continue }  # skip iteration
if ($num -gt 8) { break }     # exit loop

# One-liner style:
# @("Red","Green","Blue") | ForEach-Object { Write-Host "[$_]" }

function Say-Hello {
    param([string]$Name = "Human")
    Write-Host "Hello, $Name!"
}

# 
# PowerShell 5 Excel Read/Write Options
# ------------------------------------------------------------------------------------
# Create a new Excel application object
$excel = New-Object -ComObject Excel.Application

# Make Excel visible (optional, useful for debugging)
$excel.Visible = $true

# Add a new workbook
$workbook = $excel.Workbooks.Add()

# Get the first worksheet
$worksheet = $workbook.Worksheets.Item(1)

# Write data to a cell
$worksheet.Cells.Item(1, 1).Value = "Hello from PowerShell!"

# Save the workbook
$workbook.SaveAs("C:\Temp\MyExcelFile.xlsx")

# Close the workbook
$workbook.Close()

# Quit the Excel application
$excel.Quit()

# Release COM objects to prevent memory leaks
[System.Runtime.InteropServices.Marshal]::ReleaseComObject($worksheet) | Out-Null
[System.Runtime.InteropServices.Marshal]::ReleaseComObject($workbook) | Out-Null
[System.Runtime.InteropServices.Marshal]::ReleaseComObject($excel) | Out-Null
Remove-Variable excel, workbook, worksheet
# Import excel workbook
# Import-Excel -Path "C:\Temp\MultiSheetExample.xlsx" -WorksheetName "Data"
#
# 1️⃣ COM Automation (requires Excel installed):
# $excel = New-Object -ComObject Excel.Application
# $workbook = $excel.Workbooks.Add()
# $sheet = $workbook.Sheets.Item(1)
# $sheet.Cells.Item(1,1).Value = "Hello"
# $workbook.SaveAs("C:\Temp\Test.xlsx")
# $excel.Quit()
#
# 2️⃣ ImportExcel Module (no Excel required):
# Install-Module ImportExcel -Scope CurrentUser
# $data = @(
#   [PSCustomObject]@{Name="Human"; Score=100}
#   [PSCustomObject]@{Name="Alex"; Score=95}
# )
# $data | Export-Excel "C:\Temp\Test.xlsx" -AutoSize
# $imported = Import-Excel "C:\Temp\Test.xlsx"

# Launch Excel
# $excel = New-Object -ComObject Excel.Application
# $excel.Visible = $true  # Optional

# # Create a new workbook
# $workbook = $excel.Workbooks.Add()

# # Get the first sheet (created by default)
# $sheet1 = $workbook.Sheets.Item(1)
# $sheet1.Name = "Summary"
# $sheet1.Cells.Item(1,1).Value = "Hello from Sheet 1"

# # Add another worksheet
# $sheet2 = $workbook.Sheets.Add()
# $sheet2.Name = "Data"
# $sheet2.Cells.Item(1,1).Value = "Hello from Sheet 2"

# # Add a third worksheet
# $sheet3 = $workbook.Sheets.Add()
# $sheet3.Name = "Logs"
# $sheet3.Cells.Item(1,1).Value = "Hello from Sheet 3"

# # Save and quit
# $path = "C:\Temp\MultiSheetExample.xlsx"
# $workbook.SaveAs($path)
# $excel.Quit()

# Write-Host "Saved workbook with 3 sheets to $path"

function Export-CsvFromExcel {
    Try{
        $excelPath = "C:\Temp\MultiSheetExample.xlsx"
        $outputCsv = "C:\Temp\CombinedSheets.csv"

        $excel = New-Object -ComObject Excel.Application
        $workbook = $excel.Workbooks.Open($excelPath)

        $allData = @()

        foreach ($sheet in $workbook.Sheets) {
            Write-Host "Reading worksheet: $($sheet.Name)"

            # Find last used row and column
            $usedRange = $sheet.UsedRange
            $rows = $usedRange.Rows.Count
            $cols = $usedRange.Columns.Count

            # Read cell values
            for ($r = 1; $r -le $rows; $r++) {
                $row = @{}
                for ($c = 1; $c -le $cols; $c++) {
                    $header = "Col$c"
                    if ($r -eq 1) { $header = $sheet.Cells.Item($r, $c).Text }
                    else { $row[$header] = $sheet.Cells.Item($r, $c).Text }
                }
                if ($r -ne 1) {
                    $row["Sheet"] = $sheet.Name
                    $allData += [PSCustomObject]$row
                }
            }
        }
        # Save to CSV
        $allData | Export-Csv -Path $outputCsv -NoTypeInformation -Encoding UTF8

        $workbook.Close()
        $excel.Quit()

        Write-Host "Combined worksheets into '$outputCsv'"
    }
    Catch{
        Write-Host $(Get-ExceptionDetails -Exception $_ -ErrorActionPreference "Stop")
    }
}
# End excel section
# --------------------------------------------------------------------------------
# Output streams
<command> 1> out.txt 2> err.txt 3> warn.txt 4> verbose.txt 5> debug.txt 6> info.txt

Each number corresponds to a stream:
1 → Output

2 → Error

3 → Warning

4 → Verbose

5 → Debug

6 → Information

Get-Process nosuchprocess `
1> .\output.log `
2> .\errors.log `
3> .\warnings.log `
4> .\verbose.log `
5> .\debug.log `
6> .\info.log


# Define log directory and files
$LogRoot = "$home\.logs"
New-Item -ItemType Directory -Force -Path $LogRoot | Out-Null

$LogFiles = @{
    Output = Join-Path $LogRoot "output.log"
    Error = Join-Path $LogRoot "error.log"
    Warning = Join-Path $LogRoot "warning.log"
    Verbose = Join-Path $LogRoot "verbose.log"
    Debug = Join-Path $LogRoot "debug.log"
    Info = Join-Path $LogRoot "info.log"
}

# Preferences so Verbose/Debug/Info actually emit output
$VerbosePreference = "Continue"
$DebugPreference = "Continue"
$InformationPreference = "Continue"

# Your main work section
{
Write-Output "Running diagnostics..."
Write-Warning "Low disk space"
Write-Verbose "Starting operation details"
Write-Debug "Current counter = 42"
Write-Error "Test error occurred"
Write-Information "Completed diagnostics"
} 1> $LogFiles.Output `
2> $LogFiles.Error `
3> $LogFiles.Warning `
4> $LogFiles.Verbose `
5> $LogFiles.Debug `
6> $LogFiles.Info
}
The { … } block is just a script block — anything inside executes with streams redirected.

Each n> operator pipes that stream to the given log file.

Because it’s native redirection, it’s fast, stream-aware, and PowerShell-version-safe.




To append, use >> instead of >:

Write-Output "New run" 1>> .\output.log

1>> $LogFiles.Output `
2>> $LogFiles.Error `
3>> $LogFiles.Warning `
4>> $LogFiles.Verbose `
5>> $LogFiles.Debug `
6>> $LogFiles.Info

All streams
*> all.log


Get-Content $LogFiles.Error
Get-Content $LogFiles.Output | Out-GridView


Structured log entries
function Write-Log {
param(
[Parameter(Mandatory)] [string]$Message,
[ValidateSet('INFO','WARN','ERROR','DEBUG','VERBOSE')] [string]$Level = 'INFO'
)

$timestamp = (Get-Date).ToString('yyyy-MM-dd HH:mm:ss')
$entry = "[{0}] {1,-7} {2}" -f $timestamp, $Level, $Message

switch ($Level) {
'INFO' { Write-Information $entry -InformationAction Continue }
'WARN' { Write-Warning $entry }
'ERROR' { Write-Error $entry }
'DEBUG' { Write-Debug $entry }
'VERBOSE' { Write-Verbose $entry }
}
}

Capturing both file and console output:
Get-Process | Tee-Object -FilePath C:\Logs\output.log

function Invoke-MultiStreamTee {
param(
[Parameter(Mandatory)]
[ScriptBlock]$Script,
[string]$LogRoot = "C:\Logs"
)

if (-not (Test-Path $LogRoot)) { New-Item -ItemType Directory -Path $LogRoot | Out-Null }

$paths = @{
Out = Join-Path $LogRoot 'output.log'
Err = Join-Path $LogRoot 'error.log'
Warn = Join-Path $LogRoot 'warning.log'
Verb = Join-Path $LogRoot 'verbose.log'
Debug = Join-Path $LogRoot 'debug.log'
Info = Join-Path $LogRoot 'info.log'
}

# Enable normally-silent streams
$VerbosePreference = 'Continue'
$DebugPreference = 'Continue'
$InformationPreference = 'Continue'

& $Script *>&1 | ForEach-Object {
switch ($_.GetType().Name) {
'ErrorRecord' {
$_ | Tee-Object -FilePath $paths.Err -Append | Write-Error
}
'WarningRecord' {
$_.Message | Tee-Object -FilePath $paths.Warn -Append | Write-Warning
}
'VerboseRecord' {
$_.Message | Tee-Object -FilePath $paths.Verb -Append | Write-Verbose
}
'DebugRecord' {
$_.Message | Tee-Object -FilePath $paths.Debug -Append | Write-Debug
}
'InformationRecord' {
$_.MessageData | Tee-Object -FilePath $paths.Info -Append | Write-Information -InformationAction Continue
}
default {
$_ | Tee-Object -FilePath $paths.Out -Append
}
}
}
}


Invoke-MultiStreamTee -Script {
Write-Output "Normal output"
Write-Warning "Low memory warning"
Write-Verbose "Detailed trace" -Verbose
Write-Debug "Debug details" -Debug
Write-Error "Simulated failure"
Write-Information "Informational message" -InformationAction Continue
}




Timestamp enhancement 
$timestamp = (Get-Date).ToString('yyyy-MM-dd HH:mm:ss')
"[$timestamp] $($_.Message)" | Tee-Object -FilePath $paths.Warn -Append


function Invoke-Logged {
param([ScriptBlock]$Script, [string]$Path = "C:\Logs\session.log")
& $Script *>&1 | Tee-Object -FilePath $Path -Append
}


Invoke-Logged -Script {
Write-Output "Processing..."
Write-Error "Oops!"
Write-Warning "Watch this!"
Write-Information "Done" -InformationAction Continue
}

```
## ----End of file showPowers-----------------------------------------------------------------