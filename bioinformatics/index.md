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

[Azure](../azure) | Bioinformatics | [Git](../git) | [HTML](../html) | [JavaScript](../javascript) | [Linux](../linux) | [Mac](../mac) | [MySQL](../mysql) | [PHP](../php) | [Python](../python) | [SQL](../sql) | [WordPress](../wordpress)

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

### How to Submit GBS Data to the NCBI Sequence Read Archive (SRA)
There are three steps in submitting sequence data to the NCBI Sequence Read Archive (SRA):

1. Create a BioProject submission.
2. Create a BioSample submission.
3. Create a Sequence Read Archive submission.
