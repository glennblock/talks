#Upload a VHD

```powershell
$source = "C:\vmstorage\myosdisk.vhd"
$destination = "https://<yourstorage>.blob.core.windows.net/vhds/myosdisk.vhd"
 
Add-AzureVhd -LocalFilePath $source -Destination $destination -NumberOfUploaderThreads 5
Add-AzureDisk -DiskName 'myosdisk' -MediaLocation $destination -Label 'mydatadisk' -OS Windows 
```

#Copy a VHD locally

```powershell
$source = "https://<yourstorage>.blob.core.windows.net/vhds/myosdisk.vhd"
$destination = "C:\vmstorage\myosdisk.vhd"
Save-AzureVhd -Source $source -LocalFilePath $destination -NumberOfThreads 5 
```
