---
description: How to completely remove the ThermoFlex™ Python API and its Python runtime.
---

# Uninstall ThermoFlex™ API

We get it — sometimes you just need a clean slate. Whether you're troubleshooting an issue or preparing a fresh install for your next big demo, here’s how to completely remove the ThermoFlex™ Python API and its Python runtime.

This guide walks you through uninstalling:

* The `thermoflex` Python package
* Python itself
* Any residual environment variables or cached data

> ⚠️ **Note:** These steps are intended for Windows users. Please run all commands from **PowerShell** with administrator privileges.

***

### Step 1: Uninstall the ThermoFlex™ Python Package

If Python is still installed, open PowerShell and run:

```powershell
pip uninstall thermoflex
```

If you’re running a specific Python version (e.g. 3.11), use:

```powershell
py -3.11 -m pip uninstall thermoflex
```

Run it again until it confirms the package is no longer installed.

***

### Step 2: Uninstall Python

#### Option A: Uninstall via PowerShell

```powershell
Get-WmiObject -Class Win32_Product | Where-Object { $_.Name -like "Python*" } | ForEach-Object {
    $_.Uninstall()
}
```

This will attempt to remove all Python distributions registered with Windows Installer.

#### Option B: Uninstall via Windows UI

If the PowerShell method doesn’t find anything, you can:

1. Press `Win + R`, type `appwiz.cpl`, and hit Enter
2. Scroll to any Python entries and click **Uninstall**

***

### Step 3: Clean Up Leftover Folders

Remove any leftover files, caches, or manually installed versions:

```powershell
Remove-Item "$env:LocalAppData\Programs\Python" -Recurse -Force
Remove-Item "$env:AppData\Python" -Recurse -Force
Remove-Item "$env:LocalAppData\pip" -Recurse -Force
```

You can also check for:

```powershell
Remove-Item "$env:ProgramFiles\Python*" -Recurse -Force -ErrorAction SilentlyContinue
Remove-Item "$env:ProgramFiles (x86)\Python*" -Recurse -Force -ErrorAction SilentlyContinue
```

***

### Step 4: Remove Environment Variables

Python sometimes leaves behind entries in your system PATH. To clean those:

```powershell
$envVars = [System.Environment]::GetEnvironmentVariable("Path", "User") -split ";"
$filtered = $envVars | Where-Object { $_ -notmatch "Python" -and $_ -notmatch "pip" }
[System.Environment]::SetEnvironmentVariable("Path", ($filtered -join ";"), "User")
```

Then, clear any custom variables:

```powershell
[System.Environment]::SetEnvironmentVariable("PYTHONPATH", $null, "User")
[System.Environment]::SetEnvironmentVariable("PYTHONHOME", $null, "User")
```

***

### Step 5: Confirm It’s Gone

Back in PowerShell, run:

```powershell
where python
```

If it returns nothing, you’re fully clean.

***

### Next Steps

When you're ready, you can [reinstall Python](https://www.python.org/downloads/) and follow our [Getting Started Guide](https://docs.deltaroboticsinc.com/tutorials/thermoflex-tm/getting-started-with-our-evaluation-kit) to set up your environment again — fresh and conflict-free.
