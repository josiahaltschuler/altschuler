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

[Linux](./linux)

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
