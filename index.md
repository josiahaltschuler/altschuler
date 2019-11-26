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
