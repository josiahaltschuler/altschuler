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

[Azure](../azure) | [Bioinformatics](../bioinformatics) | [Git](../git) | [HTML](../html) | JavaScript | [Linux](../linux) | [Mac](../mac) | [MySQL](../mysql) | [PHP](../php) | [Python](../python) | [SQL](../sql) | [WordPress](../wordpress)

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
