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

[Linux](../linux)

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
