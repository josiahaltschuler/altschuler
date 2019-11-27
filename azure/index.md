<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-3525542-29"></script>
<script>
	window.dataLayer = window.dataLayer || [];

	function gtag() {
		dataLayer.push(arguments);
	}
	gtag("js", new Date());

	gtag("config", "UA-3525542-29");
</script>

Azure | [Bioinformatics](../bioinformatics) | [Git](../git) | [HTML](../html) | [JavaScript](../javascript) | [Linux](../linux) | [Mac](../mac) | [MySQL](../mysql) | [PHP](../php) | [Python](../python) | [SQL](../sql) | [WordPress](../wordpress)

# Azure
### Bash script to change access tier of all blobs in a Microsoft Azure storage folder to Archive
```
#!/bin/bash
# This script changes the access tier to "Archive" for all blobs in a folder on a Microsoft Azure storage account
#

blobs=($(az storage blob list --num-results "*" --account-name <account_name> -c <container_name> | grep -E '"name": "path/to/folder' | sed -n -e 's/\"name\": \"//p' | sed -n -e 's/\",//p'))

length=${#blobs[@]}

for ((i = 0; i != length; i++)); do
   echo "Changing access tier to Archive for: ${blobs[i]}"
   az storage blob set-tier --account-name <account_name> -c <container_name> -n ${blobs[i]} --tier Archive
done
```

### Bash script to change access tier of blob storage in Azure in bulk and using multiple grep matches
```
#!/bin/bash
# This script changes the access tier for blobs on Microsoft Azure storage account
#

blobs=($(az storage blob list --num-results "*" --account-name wheatgenetics -c rawdata | grep -E '"name": "bulk/jpoland/genome/wheat/sftp_usask/PGSB_Annotation/xxl_align/twelvelines/batch_17|"name": "bulk/jpoland/genome/wheat/sftp_usask/PGSB_Annotation/xxl_align/twelvelines/batch_18' | sed -n -e 's/\"name\": \"//p' | sed -n -e 's/\",//p'))
length=${#blobs[@]}

for ((i = 0; i != length; i++)); do
   echo "Changing access tier to Archive for: ${blobs[i]}"
   az storage blob set-tier --account-name wheatgenetics -c rawdata -n ${blobs[i]} --tier Archive
done
```

### Bash script to change Azure blob access tier to 'Archive' in bulk using Azure CLI 
```
#!/bin/bash
# This script changes the access tier to 'Archive' for blobs on Microsoft Azure storage account
#

blobs=($(az storage blob list --num-results "*" --account-name my_account_name -container-name my_container_name | grep '"name": ' | sed -n -e 's/\"name\": \"//p' | sed -n -e 's/\",//p'))
length=${#blobs[@]}

for ((i = 0; i != length; i++)); do
   echo "Changing access tier to Archive for: ${blobs[i]}"
   az storage blob set-tier --account-name my_account_name -container-name my_container_name --name ${blobs[i]} --tier Archive
done
```

### Change the access tier of a blob on Microsoft Azure using the Azure CLI
```
az storage blob set-tier --account-name my_account_name --container-name my_container_name --name path/to/file --tier Archive
```

Where --tier can be set to Archive, Cold or Hot. In this example it is Archive.

path/to/file is the path to the file you want to change, excluding the container name. For example, if your file path is really my_container/path/to/file, remove "my_container" from the path so that it is just path/to/file.

### Transfer file from local to Azure blob storage using AzCopy on Linux
```
./azcopy copy "my_file.txt" "https://my-storage-account-name.blob.core.windows.net/my-container-name/path/to/folder/"
```

### Transfer folder recursively from local to Azure blob storage using AzCopy on Linux
```
./azcopy copy "/path/to/my/folder" "https://my-storage-account-name.blob.core.windows.net/my-container-name" --recursive
```
