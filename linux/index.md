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

[Azure](../azure) | [Bioinformatics](../bioinformatics) | [Git](../git) | [HTML](../html) | [JavaScript](../javascript) | Linux | [Mac](../mac) | [MySQL](../mysql) | [PHP](../php) | [Python](../python) | [SQL](../sql) | [WordPress](../wordpress)

# Linux
### A useful wget command for getting a folder from an FTP site
```
nohup wget -r -c -nH --cut-dirs=2 -o your_output_file.txt -l 0 --ftp-user=yourusername --ftp-password='yourpassword' ftp.example.com:/path/to/the/folder &
```

nohup means ignore the HUP (hangup) command (like when your computer logs out)  
-r means recursive  
-c means to continue files where they left off  
-o means create an output file for sterr  
-l 0 means go into nested subfolder levels infinitely  
-nH --cut-dirs=2 means cut two levels of parent directories from the downloaded files  
& means run it in the background

### Add a public SSH key to the remote server for auto-login if the ssh-copy-id command is not available locally
```
ssh myusername@example.com "cat >> ~/.ssh/authorized_keys" < ~/.ssh/id_rsa.pub
```

### chgrp recursively
```
chgrp -R mygroupname /path/to/folder
```

### Bash script to delete files from current folder if they exist in another folder
```
#!/bin/bash
FILES=*

for f in $FILES
do
  echo "Processing $f file..."

  FILE=/path/to/other/folder/$f
   
  if test -f "$FILE"; then
    echo "$FILE exists. Deleting it from this folder."
    rm -f $f
  fi
done
```

### Bash script to go in each directory and run a command in Linux
```
#!/bin/bash

for d in *
do
    (cd "$d" && your-command)
done
```

### chown recursively
```
chown -R yourusername /path/to/folder
```

### Compress a tar file in Linux
```
gzip -9 < my_file.tar > my_file.tar.gz
```

This will keep my_file.tar and create my_file.tar.gz

### Copy a list of files in Linux
```
cp /path/to/file/{file1.txt,file2.txt,file3.txt} /path/to/target/folder/
```

### Copy a range of files
```
cp /path/to/folder/my_file_name{1..10}.txt /path/to/target/folder
```

### Create a large file using fallocate
```
fallocate -l 5GB my_large_file
```

This will create a 5GB file called my_large_file.

### Count the number of files in a folder
```
find . -maxdepth 1 -type f | wc -l
```

### Display the last n number of lines of a file in Linux
```
tail -n 200 my_file.txt
```

Where 200 is the number of lines to display from the end of the file. You can change this number to whatever you want.

### Do an md5sum check
```
md5sum -c md5_sums.txt > md5_sums_checked.txt &
```

-c means read the sums from the file md5_sums.txt

& means do it in the background

### Generate MD5 Checksum on a single file
```
md5sum yourfilename
```

### Generate md5 checksums for multiple files
```
md5sum * > checksums.md5
```

### Get the number of cores on a Linux machine
```
grep -c ^processor /proc/cpuinfo
```

### How to fix 'su: can't run /sbin/nologin' on Synology NAS device
Edit /etc/passwd and replace '/sbin/nologin' with '/bin/sh' for the user you are trying to su to.


### If rm command gives 'Argument list too long' error message
```
find . -name '*' | xargs rm -f
```

This finds all the files in the current directory and pipes them one by one to the rm command.

### If the file list is too long when using the ls command in Linux, pipe it to the more command
```
ls /path/to/folder/with/too/many/files | more
```

This will let you page through the list using the space bar.

### Install md5sum on OSX
```
brew install md5sha1sum
```

You need Homebrew installed to run 'brew' command

After installation you will be able to run the 'md5sum' command

### Kill a process in Linux
```
kill -9 12345
```

Where -9 is the kill signal and 12345 is the process ID number.

### lftp to a remote server
```
lftp -u 'myusername,mypassword' example.com
```

### Lorem Ipsum text example
```
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```

### Put a single file into a subfolder on a remote server using LFTP on the command line
```
lftp -e 'cd my_remote_subfolder; put /path/to/my/local/file.txt; bye' -u 'my_username,my_password' example.com
```

### Put Linux job in background and disown it
Hit CTRL-Z

Type 'bg'

Get the job number by typing 'jobs -l'

Type 'disown 12345' or whatever your job number is. This will be as if you ran the command with 'nohup'

### Resume upload of a folder to a remote server using LFTP
```
lftp -e 'mirror -c -R /path/to/local/folder /path/to/remote/folder' -u 'your_username,your_password' the-remote-ftp-server.com
```

-c means resume the upload where you left off the last time you ran lftp before it got terminated.

-R means reverse mirror. This will tell lftp to upload from local to remote, instead of download from remote to local.

### Move multiple files into a folder using LFTP mmv command
```
mmv -O target_folder myfiles*.JPG
```
-O lets you specify a target folder to move to

\* is a wildcard

### One line command to SFTP multiple files in background from a remote server in Linux
```
nohup sshpass -p "your-password" sftp your-username@sftp.server.name:path/to/files/*.gz > sftp.log &
```

### Search for a directory in Linux and then save the search results to a file
```
find /path/to/directory/to/search -type d -iname '*my_directory_name*' > my_search_results.txt
```

Where -type d specifies to look for a directory. (If it was -type f then it would mean to look for a file instead)

-iname specifies to make the search case-insensitive.

### Secure copy (scp) in Linux
```
scp -r -P 32435 username@example.com:/path/to/file . > log_output.txt
```
### rsync a remote folder to current directory
```
rsync -avz your_username@example.com:/path/to/folder . > rsync.log
```

### rsync from one folder to another recursively
```
rsync -a /folder/to/copy/from/ /folder/to/copy/to
```

Where the -a option is a combination flag, standing for "archive," preserving symbolic links, special and device files, modification times, group, owner, and permissions. It also syncs recursively.

Make sure to keep the ending slash (/) on the source directory. If it's not there the source directory will be created within the target directory, instead of syncing with it.

### Search for a file in Linux and then save the search results to a file
```
find /path/to/directory/to/search -type f -iname '*my_file_name*' > my_search_results.txt
```

Where -type f specifies to look for a file. (If it was -type d then it would mean to look for a directory instead.)

-iname specifies to make the search case-insensitive.

### Set permissions recursively to all directories and files
```
find /path/to/directory -type f -exec chmod 664 {} + -o -type d -exec chmod 775 {} +
```

### Untar a file in linux
```
tar -xvf my_file.tar
```

### Upload a folder to a remote server using LFTP
```
lftp -e 'mirror -R /path/to/local/folder /path/to/remote/folder' -u 'your_username,your_password' the-remote-ftp-server.com
```

-R means reverse mirror. This will tell lftp to upload from local to remote, instead of download from remote to local.

### View the contents of a compressed file in Linux
```
gzip -cd my_file.txt.gz
```

Where -c means to write to standard output and -d means to decompress.

This will not create a new decompressed file or change the original compressed file in any way.
