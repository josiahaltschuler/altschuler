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

[Azure](../azure) | [Bioinformatics](../bioinformatics) | [Git](../git) | [HTML](../html) | [JavaScript](../javascript) | [Linux](../linux) | [Mac](../mac) | [MySQL](../mysql) | [PHP](../php) | [Python](../python) | SQL | [WordPress](../wordpress)

# SQL
### Replace a value in a table column using SQL
```
UPDATE my_table SET `my_column`=NULL WHERE my_column='0';
```

This will replace all values of 0 with NULL in a column called "my_column"
