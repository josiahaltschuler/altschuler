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
