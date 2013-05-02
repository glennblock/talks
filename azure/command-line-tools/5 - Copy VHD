#Copy VHD across regions

```powershell
# Source VHD (West US)
$srcUri = "http://<yourweststorage>.blob.core.windows.net/vhds/myosdisk.vhd"     
 
# Target Storage Account (East US)
$storageAccount = "<youreaststorage>"
$storageKey = "<youreaststoragekey>"
 
$destContext = New-AzureStorageContext  –StorageAccountName $storageAccount `
                                        -StorageAccountKey $storageKey 
 
# Container Name
$containerName = "vhds"
 
New-AzureStorageContainer -Name $containerName -Context $destContext
 
$blob = Start-AzureStorageBlobCopy -srcUri $srcUri `
                                   -DestContainer $containerName `
                                   -DestBlob "testcopy1.vhd" `
                                   -DestContext $destContext  
                                     
$blob | Get-AzureStorageBlobCopyState
```
