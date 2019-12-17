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

[Azure](../azure) | [Bioinformatics](../bioinformatics) | [Git](../git) | [HTML](../html) | [JavaScript](../javascript) | [Linux](../linux) | [Mac](../mac) | MySQL | [PHP](../php) | [Python](../python) | [SQL](../sql) | [WordPress](../wordpress)

# MySQL
### Flush privileges
```
FLUSH PRIVILEGES;
```

### Log in to MySQL, add a new user to a database and set their privileges
Login to MySQL via command line

```
mysql -h <hostname> -u <username> -p <database name>
```

Add a user from MySQL command line

```
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
```

Set privileges on database from MySQL command line

```
GRANT SELECT, INSERT, UPDATE, DELETE ON <database name>.* TO 'username'@'%';
```

### Revoke all privileges except for SELECT on a MySQL database
```
REVOKE ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, GRANT OPTION, INDEX, INSERT, LOCK TABLES, REFERENCES, SHOW VIEW, TRIGGER, UPDATE ON `my_database`.* FROM `my_username`;
```

### Revoke privileges from a user in MySQL
```
REVOKE Delete, Insert, Update ON `database_name`.* FROM `username`@`%`;
```
