#Copy blobs

```powershell
$destContext = New-AzureStorageContext  –StorageAccountName $storageAccount `
                                        -StorageAccountKey $storageKey
 
New-AzureStorageContainer -Name $containerName
 
$blob1 = Start-CopyAzureStorageBlob -srcUri $srcUri1 `
                                 -DestContainer $containerName `
                                 -DestBlob $fileName1 `
                                 -DestContext $destContext
 
$blob2 = Start-CopyAzureStorageBlob -srcUri $srcUri2 `
                                 -DestContainer $containerName `
                                 -DestBlob $fileName2 `
                                 -DestContext $destContext
 
$blob3 = Start-CopyAzureStorageBlob -srcUri $srcUri3 `
                                 -DestContainer $containerName `
                                 -DestBlob $fileName3  `
                                 -DestContext $destContext
 
$blob1 | Get-AzureStorageBlobCopyState
$blob2 | Get-AzureStorageBlobCopyState
$blob3 | Get-AzureStorageBlobCopyState
