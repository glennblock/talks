```powershell
$source = "C:\vmstorage\myosdisk.vhd"
$destination = "https://<yourstorage>.blob.core.windows.net/vhds/myosdisk.vhd"
 
Add-AzureVhd -LocalFilePath $source -Destination $destination -NumberOfUploaderThreads 5
Add-AzureDisk -DiskName 'myosdisk' -MediaLocation $destination -Label 'mydatadisk' -OS Windows 
```
