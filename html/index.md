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
