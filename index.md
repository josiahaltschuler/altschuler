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
### Transfer file from local to Azure blob storage using AzCopy on Linux
```
./azcopy copy "my_file.txt" "https://my-storage-account-name.blob.core.windows.net/my-container-name/path/to/folder/"
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
# JavaScript
### Change date from WordPress REST API to another format using JavaScript
```
var published_date = new Date(iso_format_date);
var date = published_date.getDate();
var month = published_date.getMonth(); 
var year = published_date.getFullYear();

var new_format_date = month + '/' + date + '/' + year; // This is your new format. It can be anything you want.
```
Where iso_format_date is the date received from the WordPress REST API, which is in ISO format (2018-08-23T16:12:54)

### Get the base URL of the current page in JavaScript
```
function getBaseUrl() {
  var re = new RegExp(/^.*\//);
  return re.exec(window.location.href);
}
```
# Linux
## gzip
### View the contents of a compressed file in Linux
```
gzip -cd my_file.txt.gz
```

Where -c means to write to standard output and -d means to decompress.

This will not create a new decompressed file or change the original compressed file in any way.
## lftp
### Put a single file into a subfolder on a remote server using LFTP on the command line
```
lftp -e 'cd my_remote_subfolder; put /path/to/my/local/file.txt; bye' -u 'my_username,my_password' example.com
```

### Create a large file using fallocate
```
fallocate -l 5GB my_large_file
```

This will create a 5GB file called my_large_file.

### If rm command gives 'Argument list too long' error message
```
find . -name '*' | xargs rm -f
```

This finds all the files in the current directory and pipes them one by one to the rm command.

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

### Search for a directory in Linux and then save the search results to a file
```
find /path/to/directory/to/search -type d -iname '*my_directory_name*' > my_search_results.txt
```

Where -type d specifies to look for a directory. (If it was -type f then it would mean to look for a file instead)

-iname specifies to make the search case-insensitive.

### Search for a file in Linux and then save the search results to a file
```
find /path/to/directory/to/search -type f -iname '*my_file_name*' > my_search_results.txt
```

Where -type f specifies to look for a file. (If it was -type d then it would mean to look for a directory instead.)

-iname specifies to make the search case-insensitive.

### rsync from one folder to another recursively
```
rsync -a /folder/to/copy/from/ /folder/to/copy/to
```

Where the -a option is a combination flag, standing for "archive," preserving symbolic links, special and device files, modification times, group, owner, and permissions. It also syncs recursively.

Make sure to keep the ending slash (/) on the source directory. If it's not there the source directory will be created within the target directory, instead of syncing with it.

### Set permissions recursively to all directories and files
```
find /path/to/directory -type f -exec chmod 664 {} + -o -type d -exec chmod 775 {} +
```

# PHP
### Capitalize the first word of a string in PHP
```
$capitalized_string = ucfirst("my string.");
```

$capitalized_string will be "My string."

### Extract an array of properties from an array of objects in PHP
```
$my_array_of_properties = array_column($my_array_of_objects, 'the_property_name_to_extract');
```
### Remove character from string in PHP
```
$new_string = str_replace('_', ' ', $string_with_character);
```

In this example an underscore (_) is removed from the string and replaced with a space.

# Python
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
### Shortcode in a WordPress template
```
<?php echo do_shortcode("[the_shortcode]"); ?>
```
