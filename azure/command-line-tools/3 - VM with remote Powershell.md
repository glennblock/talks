#Create a VM and enable remote Powershell!
```powershell
# Using this script installs the generated cert into your local cert store which allows 
# PowerShell to verify it is communicating with the correct endpoint. 
# This REQUIRES PowerShell run Elevated
. "C:\Scripts\WAIaaSPS\RemotePS\InstallWinRMCert.ps1"
 
$user = ""
$pwd = ""
$svcName = ""
$VMName = "webfe1"
$location = "West US"
 
$credential = Get-Credential
 
New-AzureVMConfig -Name $VMName -InstanceSize "Small" -ImageName $image |
  Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pwd |
  Add-AzureEndpoint -Name "http" -Protocol tcp -LocalPort 80 -PublicPort 80 |
  New-AzureVM -ServiceName $svcName -Location $location -WaitForBoot
 
# Get the RemotePS/WinRM Uri to connect to
$uri = Get-AzureWinRMUri -ServiceName $svcName -Name $VMName
 
# Using generated certs – use helper function to download and install generated cert.
InstallWinRMCert $svcName $VMName
 
# Use native PowerShell Cmdlet to execute a script block on the remote virtual machine
Invoke-Command -ConnectionUri $uri.ToString() -Credential $credential -ScriptBlock {
  $logLabel = $((get-date).ToString("yyyyMMddHHmmss"))
  $logPath = "$env:TEMP\init-webservervm_webserver_install_log_$logLabel.txt"
  Import-Module -Name ServerManager
  Install-WindowsFeature -Name Web-Server -IncludeManagementTools -LogPath $logPath
}
```
