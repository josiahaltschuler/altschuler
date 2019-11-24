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
### Resume upload of a folder to a remote server using LFTP
```
lftp -e 'mirror -c -R /path/to/local/folder /path/to/remote/folder' -u 'your_username,your_password' the-remote-ftp-server.com
```

-c means resume the upload where you left off the last time you ran lftp before it got terminated.

-R means reverse mirror. This will tell lftp to upload from local to remote, instead of download from remote to local.

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
### Create shortcode in WordPress
Add the below code to your functions.php file or a plugin.
```
function handle_shortcode() {
    return 'Hello world!';
}
add_shortcode('hello_world', 'handle_shortcode');
```
Now you can use this on any page or post by adding [hello_world] and it will display "Hello world!"

### Shortcode in a WordPress template
```
<?php echo do_shortcode("[the_shortcode]"); ?>
```

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