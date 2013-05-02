```powershell
$img = 'b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-12_04_1-LTS-amd64-server-20121218-en-us-30GB'
$user = 'somelinuxuser'
$pass = 'somelinuxpwd!'
$vnet = 'HybridVNET'
$ag = 'WestUSAG'
$svcname = 'mylinuxsvc1'
 
New-AzureVMConfig -Name 'linuxfromps1' -ImageName $img -InstanceSize Small |
    Add-AzureProvisioningConfig -Linux -LinuxUser $user -Password $pass |
    Set-AzureSubnet -SubnetNames 'AppSubnet' | # Optional 
    New-AzureVM -ServiceName $svcname -VNetName $vnet -AffinityGroup $ag
```
