# Installing and Updating the Azure Az PowerShell module (vs. AzureRM) 
====================================================================

## Remove the AzureRM PowerShell module 
------------------------------------

To install the Az PowerShell module, you must first remove the AzureRM
module.  You can [check which
version(s)](https://docs.microsoft.com/en-us/powershell/azure/migrate-from-azurerm-to-az?view=azps-4.1.0)
of AzureRM you already have installed.

PowerShell

    Get-InstalledModule -Name AzureRM -AllVersions
 
If you see a message like the following, then you’re ready to install
the Az PowerShell module.

> `PackageManagement\Get-Package : No match was found for the specified search criteria and module names 'AzureRM'.`

 
If you don’t see that, then you need to [uninstall
AzureRM](https://docs.microsoft.com/en-us/powershell/azure/uninstall-az-ps?view=azps-4.1.0#uninstall-the-azurerm-module)
first.

PowerShell

    Uninstall-Module AzureRM

  
or

PowerShell

    Uninstall-AzureRm

If neither of those options work, try the following.

PowerShell

    $versions = (Get-InstalledModule AzureRM -AllVersions | Select-Object
    Version) \$versions | foreach { Uninstall-AllModules -TargetModule
    AzureRM -Version (\$\_.Version) -Force }

## Install the Azure PowerShell module
-----------------------------------

Then running the following code to install Az should succeed.

PowerShell

    if (Get-Module -Name AzureRM -ListAvailable) { Write-Warning -Message
    'Az module not installed. Having both the AzureRM and Az modules
    installed at the same time is not supported.' } else { Install-Module
    -Name Az -AllowClobber -Scope CurrentUser }

## Update the Azure PowerShell module
----------------------------------

If you already have the Az PowerShell module installed, you can update
it with the following code.

PowerShell

    Update-Module -Name Az

## Reinstall the Azure PowerShell module 
-------------------------------------

If you have any issues updating using PowershellGet, then you
should **reinstall**, rather than **update**. Reinstalling is done the
same way as installing, but you need to add the `-Force` parameter:

PowerShell

    if (Get-Module -Name AzureRM -ListAvailable) { Write-Warning -Message
    'Az module not installed. Having both the AzureRM and Az modules
    installed at the same time is not supported.' } else { Install-Module
    -Name Az -AllowClobber -Force }

## Check the version of the Azure PowerShell module 
------------------------------------------------

PowerShell

    Get-InstalledModule -Name Az -AllVersions

-  