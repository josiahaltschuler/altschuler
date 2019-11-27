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

[Azure](../azure) | [Bioinformatics](../bioinformatics) | [Git](../git) | [HTML](../html) | [JavaScript](../javascript) | [Linux](../linux) | [Mac](../mac) | [MySQL](../mysql) | PHP | [Python](../python) | [SQL](../sql) | [WordPress](../wordpress)

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
