# Linux
## gzip
### View the contents of a compressed file in Linux
```
gzip -cd my_file.txt.gz
```

Where -c means to write to standard output and -d means to decompress.

This will not create a new decompressed file or change the original compressed file in any way.

# Azure
# WordPress
**Add CSS to a WordPress plugin**  
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
**Create shortcode in WordPress**  
Add the below code to your functions.php file or a plugin.
```
function handle_shortcode() {
    return 'Hello world!';
}
add_shortcode('hello_world', 'handle_shortcode');
```
Now you can use this on any page or post by adding [hello_world] and it will display "Hello world!"

**Shortcode in a WordPress template**  
```
<?php echo do_shortcode("[the_shortcode]"); ?>
```

**Expandable search box with magnifying glass in WordPress**  
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