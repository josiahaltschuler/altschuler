# Linux
## gzip
### View the contents of a compressed file in Linux
`gzip -cd my_file.txt.gz`

Where -c means to write to standard output and -d means to decompress.

This will not create a new decompressed file or change the original compressed file in any way.

# Azure
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
