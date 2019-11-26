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

# Bioinformatics
### How to Install fastStructure on Linux
The following are instructions on how to install fastStructure (https://github.com/rajanil/fastStructure) on Linux. Make sure you are using Python 2 - not Python 3

#### 1. Install required modules
```
pip install numpy==1.16.5
pip install cython==0.27.3
pip install scipy==1.2.1
```

#### 2. Install GSL (GNU Scientific Library) module
Download the GSL module
```
wget ftp://ftp.gnu.org/gnu/gsl/gsl-1.9.tar.gz
tar -xf gsl-1.9.tar.gz
cd gsl-1.9
```

  Create a directory where you will install GSL (substitute the directory paths with your own desired paths):  
```
mkdir ~/bin/gsl
./configure --prefix=/homes/altschuler/bin/gsl
make
make check
make install
```

  Add the following lines to your .bashrc file (substitute the directory paths where you installed gsl):
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/homes/altschuler/bin/gsl/lib
export CFLAGS="-I/homes/altschuler/bin/gsl/include"
export LDFLAGS="-L/homes/altschuler/bin/gsl/lib"
```

  Now source your .bashrc file  
```
source ~/.bashrc
```

#### 3. Install fastStructure
Change directory to where you want to install fastStructure
```
cd ~/scripts
wget --no-check-certificate https://github.com/rajanil/fastStructure/archive/master.tar.gz
tar -xf master.tar.gz
cd fastStructure-master/vars
python setup.py build_ext -f --inplace
cd ..
python setup.py build_ext -f --inplace
```

#### 4. You should now be able to run structure.py
```
python structure.py
```

# Git
### Add a folder to .gitignore
To ignore a folder named my_folder add this to your .gitignore file:
```
my_folder/
```

### Merge branch into master branch
```
git checkout master
git merge mybranch
```

This will merge mybranch into master

# HTML
### HTML telephone link
```
<a href="tel:1-123-456-7890">1-123-456-7890</a>
```

### Make an hr element dotted
```
hr.dotted {
  border: none;
  border-top: .1em dotted; /* Change the size of the dots here from .1em to your preferred size */
  background-color: transparent;
  height: 1px;
  margin-bottom: 0;
  color: black; /* Change this to your preferred color */
}
```

### Make Font Awesome icons have a circle background
```
<style>
#social [class*="fab fa-"] {
 	background-color: #2A00FF;
 	border-radius: 40px;
 	color: #fff;
 	height: 40px;
  	line-height: 40px;
 	margin: auto 3px;
 	width: 40px;
 	font-size: 24px;
  	text-align: center;
}
</style>

<div id="social">
	<i class="fab fa-instagram"></i>
	<i class="fab fa-facebook-f"></i>
	<i class="fab fa-twitter"></i>
</div>
```

### Make the bootstrap sub menu full-width
```
body {
  overflow-x: hidden;
}


ul.dropdown-menu {
  padding: 0 1000em;
  margin: 0 -1000em;
}
```

# JavaScript
### Add jQuery to HTML
```
<head>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
</head>
```

### Change date from WordPress REST API to another format using JavaScript
```
var published_date = new Date(iso_format_date);
var date = published_date.getDate();
var month = published_date.getMonth(); 
var year = published_date.getFullYear();

var new_format_date = month + '/' + date + '/' + year; // This is your new format. It can be anything you want.
```
Where iso_format_date is the date received from the WordPress REST API, which is in ISO format (2018-08-23T16:12:54)

### Find the sum of the even-valued terms in a Fibonacci sequence whose values do not exceed 4,000,000 in JavaScript
```
/**
 * @file Even Fibonacci Numbers
 * @author Josiah Altschuler <josiah.altschuler@gmail.com>
 *
 * The following code finds the sum of the even-valued terms in a Fibonacci sequence
 * whose values do not exceed 4,000,000. The result is 4,613,732.
 *
 * The solution is found by chaining three functions together:
 * 1. fibonacci() is a custom function that takes in a maximum number parameter, and
 *    returns a Fibonacci sequence array consisting of values less than or equal to 
 *    that number.
 * 2. A filter function is called on the resulting array from fibonacci() to filter
 *    out odd numbers, keeping the even ones.
 * 3. A reduce function is called on the resulting array from the filter to sum up all
 *    values.
 *
 * The code could be made more extensible by putting everything into a class. The
 * fibonacci() function could be one method, and other methods could be built to
 * filter even values or to sum all values of the array. This will allow for more
 * modularized unit testing and the class could also be extended as a subclass.
 */

/**
 * Return an array consisting of a Fibonacci sequence whose values do not exceed a maximum value.
 *
 * @param {Number} maxValue - Maximum value allowed for the Fibonacci sequence.
 * 
 * @return {Array} A Fibonacci sequence whose values do not exceed a given maximum value (maxValue).
 */
const fibonacci = maxValue => {
  let arr = [0, 1]; // Start with a Fibnacci base sequence of 0, 1
  let i = 2; // Start counting at the third value of the Fibonacci sequence
  
  while (arr[arr.length-1] <= maxValue) {
    arr[i] = arr[i-2] + arr[i-1];
    i++;
  }
  arr.pop();
  
  return arr;
};

// Run the fibonacci() function. Then filter the resulting array for even values, and then get the sum of those values. 
console.log(fibonacci(4000000).filter((val) => val % 2 === 0).reduce((a, b) => a + b));


// Jasmine unit test of the fibonacci() function
describe('fibonacci', function() {
  it('should do fibonacci', () => {
    expect(fibonacci(-1)).toEqual([0]);
    expect(fibonacci(0)).toEqual([0]);
    expect(fibonacci(1)).toEqual([0, 1, 1]);
    expect(fibonacci(2)).toEqual([0, 1, 1, 2]);
    expect(fibonacci(10)).toEqual([0, 1, 1, 2, 3, 5, 8]);
  });
});
```

### Get the base URL of the current page in JavaScript
```
function getBaseUrl() {
  var re = new RegExp(/^.*\//);
  return re.exec(window.location.href);
}
```

### If only the home page displays and no subpages display on an Ubuntu server web site
1. Change AllowOverride None to AllowOverride All here in /etc/apache2/apache2.conf:

```
<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride All
  Require all granted
</Directory>
```

2. Do this command: sudo a2enmod rewrite

3. Restart Apache: sudo service apache2 restart

\* If it’s a wordpress site try flushing the permalinks first *

### jQuery to limit number of checkboxes selected to four
```
<form>
    <input type="checkbox" name="my-checkboxes[]" value="0">
    <input type="checkbox" name="my-checkboxes[]" value="1">
    <input type="checkbox" name="my-checkboxes[]" value="2">
    <input type="checkbox" name="my-checkboxes[]" value="3">
    <input type="checkbox" name="my-checkboxes[]" value="4">
    <input type="checkbox" name="my-checkboxes[]" value="5">
</form>

<script>
var limit = 4;
  
$('form input:checkbox').on('change', function(evt) {
  if($(this).siblings(':checked').length >= limit) {
    this.checked = false;
  }
});
</script>
```

### Match until a character but not including it, using Regex in JavaScript
```
myMatch = "Match until a character but not including it, using Regex in JavaScript #JavaScript".match(/[^#]*/);
```

Gives you 'Match until a character but not including it, using Regex in JavaScript '

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

# Mac
### Update Homebrew
```
brew update
```

# MySQL
### Log in to MySQL, add a new user to a database and set their privileges
Login to MySQL via command line

```
mysql -h <hostname> -u <username> -p <database name>
```

Add a user from MySQL command line

```
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
```

Set privileges on database from MySQL command line

```
GRANT SELECT, INSERT, UPDATE, DELETE ON <database name>.* TO 'username'@'%';
```

### Revoke all privileges except for SELECT on a MySQL database
```
REVOKE ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, GRANT OPTION, INDEX, INSERT, LOCK TABLES, REFERENCES, SHOW VIEW, TRIGGER, UPDATE ON `my_database`.* FROM `my_username`;
```

### Revoke privileges from a user in MySQL
```
REVOKE Delete, Insert, Update ON `database_name`.* FROM `username`@`%`;
```

# PHP
### Capitalize the first word of a string in PHP
```
$capitalized_string = ucfirst("my string.");
```

$capitalized_string will be "My string."

### Extract a .tar.gz file in Linux
```
tar -xf my_archive_file.tar.gz
```

Where -x means extract, and f tells it that the filename to extract follows.

### Extract an array of properties from an array of objects in PHP
```
$my_array_of_properties = array_column($my_array_of_objects, 'the_property_name_to_extract');
```

### Print a comma-separated list from an array in PHP
```
echo implode(', ', $my_array);
```

### Remove character from string in PHP
```
$new_string = str_replace('_', ' ', $string_with_character);
```

In this example an underscore (_) is removed from the string and replaced with a space.

# Python
### Install PySpark on Google Colaboratory
```
!pip install pyspark
```

### NumPy and SciPy Statistics Cheat Sheet
**Mean (Average)**  
The sum of all the numbers divided by the number of numbers.

Python example using NumPy:
```
import numpy as np

dataset = [1, 2, 3]
mean = np.mean(dataset)
# mean has a value of 2
```

**Median**  
The middle value in an ordered sequence of numbers. If there is an odd number of numbers, the median is the middle number. If there is an even number of numbers, the median is the average of the two middle numbers.

Python example using NumPy:
```
import numpy as np

dataset = [1, 2, 3, 4, 5]
median = np.median(dataset)
# median has a value of 3
```

**Mode**  
The number that appears most frequently in a set of numbers.

Python example using SciPy (NumPy does not have a mode function):
```
from scipy import stats

dataset = [1, 1, 1, 2, 3, 3]
mode = stats.mode(dataset)
# mode has a value of 1
```

**Range**  
The difference between the lowest and highest values.

Python example using NumPy:
```
import numpy as np

dataset = [1, 2, 3, 4, 5]
range = np.ptp(dataset)
# range has a value of 4
```
# SQL
### Replace a value in a table column using SQL
```
UPDATE my_table SET `my_column`=NULL WHERE my_column='0';
```

This will replace all values of 0 with NULL in a column called "my_column"

# WordPress
### Add a widget area in WordPress
```
<?php dynamic_sidebar( 'my-widget-area' ); ?>
```

### Add CSS to a WordPress plugin
```
function register_my_plugin_scripts() {
  wp_register_style('my-plugin-style', plugins_url('/css/style.css', __FILE__), false, '1.0.0', 'all');
}
add_action('init', 'register_my_plugin_scripts');

function enqueue_my_plugin_scripts(){
  wp_enqueue_style('my-plugin-style');
}
add_action('wp_enqueue_scripts', 'enqueue_my_plugin_scripts');
```

### An example of making ACF relationship fields of two custom post types bidirectional
```
/**
* This is to set up the ACF bidirectional relationship between the Artist and Exhibition custom post types.
* Put this in functions.php of your WordPress theme.
* The code was taken from here: https://www.advancedcustomfields.com/resources/bidirectional-relationships/
*/

function bidirectional_acf_update_value( $value, $post_id, $field  ) {
	// vars
	$field_name = $field['name'];
	$field_key = $field['key'];
	$global_name = 'is_updating_' . $field_name;

	// bail early if this filter was triggered from the update_field() function called within the loop below
	// - this prevents an infinite loop

	if( !empty($GLOBALS[ $global_name ]) ) return $value;
  
	// set global variable to avoid inifite loop
	// - could also remove_filter() then add_filter() again, but this is simpler

	$GLOBALS[ $global_name ] = 1;

	// loop over selected posts and add this $post_id
  if( is_array($value) ) {
		foreach( $value as $post_id2 ) {

      // load existing related posts
			$value2 = get_field($field_name, $post_id2, false);

			// allow for selected posts to not contain a value
			if( empty($value2) ) {	
				$value2 = array();
			}

			// bail early if the current $post_id is already found in selected post's $value2
			if( in_array($post_id, $value2) ) continue;

			// append the current $post_id to the selected post's 'related_posts' value
			$value2[] = $post_id;	

			// update the selected post's value (use field's key for performance)
			update_field($field_key, $value2, $post_id2);
		}
	}

	// find posts which have been removed
	$old_value = get_field($field_name, $post_id, false);

	if( is_array($old_value) ) {	
		foreach( $old_value as $post_id2 ) {

      // bail early if this value has not been removed
			if( is_array($value) && in_array($post_id2, $value) ) continue;

			// load existing related posts
			$value2 = get_field($field_name, $post_id2, false);

			// bail early if no value
			if( empty($value2) ) continue;

			// find the position of $post_id within $value2 so we can remove it
			$pos = array_search($post_id, $value2);

			// remove
			unset( $value2[ $pos] );

			// update the un-selected post's value (use field's key for performance)
			update_field($field_key, $value2, $post_id2);
		}
	}

	// reset global varibale to allow this filter to function as per normal
	$GLOBALS[ $global_name ] = 0;

  // return
  return $value;
}

add_filter('acf/update_value/name=artists_exhibitions', 'bidirectional_acf_update_value', 10, 3);
```

### Check if there are any posts of a custom post type
```
$args = array('post_type'=>array('my_custom_type'));

query_posts($args);

if (have_posts()) {
  // Do something
}
```
### Create shortcode in WordPress
Add the below code to your functions.php file or a plugin.
```
function handle_shortcode() {
    return 'Hello world!';
}
add_shortcode('hello_world', 'handle_shortcode');
```
Now you can use this on any page or post by adding [hello_world] and it will display "Hello world!"

### Expandable search box with magnifying glass in WordPress
```
<style>
input {
	outline: none;
}

input::-webkit-search-decoration,
input::-webkit-search-cancel-button {
	display: none; 
}

input[type=search] {
  	box-sizing: content-box;
	font-family: inherit;
	font-size: 100%;
  	background: #ffffff url(https://static.tumblr.com/ftv85bp/MIXmud4tx/search-icon.png) no-repeat 9px center;
	border: none;
	padding: 9px 10px 9px 32px;
	width: 55px;
	border-radius: 10em;
	transition: all .5s;
  	width: 15px;
  	height: 17px;
	padding-left: 10px;
	color: transparent;
	cursor: pointer;
}

input[type=search]:hover {
	background-color: #ffffff;
}

input[type=search]:focus {
  	background-color: #ffffff;
	width: 80px;
	padding-left: 32px;
	color: #000000;
	cursor: auto;
}

input::placeholder {
	color: transparent;
}
</style>

<form action="/" method="get">
    <input type="search" name="s" id="search" placeholder="Search" value="<?php the_search_query(); ?>" />
</form>
```

### Get all the posts of a custom post type in WordPress
```
<?php 
$args = array(
    'post_type'=> 'my_custom_post_type'
);              

$query = new WP_Query($args);

if ($query->have_posts()) {
    while ($query->have_posts()) {
        $query->the_post();
        // Now you can do something like print out the title using the_title();
    }
}
?>
```

### Get an ACF custom field
```
<?php the_field('my_field_name'); ?>
```

### Get the tags for a post (custom post types too) without the tag term being linked
```
$terms = wp_get_object_terms( $post->ID,  'event_category' );
 
if ( ! empty( $terms ) ) {
  if ( ! is_wp_error( $terms ) ) {
    foreach( $terms as $term ) {
      echo esc_html( $term->name );
    }
  }
}
```

### Register a new sidebar area in WordPress
In functions.php, add:

```
register_sidebar( array(
  'name'          => esc_html__( 'Footer column 1', 'fwm' ),
  'id'            => 'footer-column-1',
  'description'   => esc_html__( 'Add widgets here.', 'fwm' ),
  'before_widget' => '<section id="%1$s" class="widget %2$s">',
  'after_widget'  => '</section>',
  'before_title'  => '<h2 class="widget-title">',
  'after_title'   => '</h2>',
) );

```

### Shortcode in a WordPress template
```
<?php echo do_shortcode("[the_shortcode]"); ?>
```
