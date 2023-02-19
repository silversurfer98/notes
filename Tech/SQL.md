
> somethings IDK --> some command backup

```bash
docker run --name test-mysql -p 3306:3306 -p 33060:33060 -e MYSQL_ROOT_HOST='%' -e MYSQL_ROOT_PASSWORD='srag1998' -d mysql/mysql-server:latest

mysql -uraghav -p -h test-mysql -P 3306
```

```sql
CREATE TABLE `testt` (`id` int(11) NOT NULL AUTO_INCREMENT, `name` varchar(255) COLLATE utf8_bin NOT NULL, `email` varchar(255) COLLATE utf8_bin NOT NULL, `status` varchar(255) COLLATE utf8_bin NOT NULL, PRIMARY KEY (`id`)) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin AUTO_INCREMENT=1 ;
```

```sql
CREATE TABLE `edbv2` (`i` int(11) NOT NULL AUTO_INCREMENT,
`id` varchar(255) COLLATE utf8_bin NOT NULL,
`empno` varchar(255) COLLATE utf8_bin NOT NULL, 
`name` varchar(255) COLLATE utf8_bin NOT NULL, 
`age` varchar(255) COLLATE utf8_bin NOT NULL, 
`email` varchar(255) COLLATE utf8_bin NOT NULL,
`status` varchar(255) COLLATE utf8_bin NOT NULL,
`hno` varchar(255) COLLATE utf8_bin NOT NULL, 
`olane` varchar(255) COLLATE utf8_bin NOT NULL, 
PRIMARY KEY (`i`)) 
ENGINE=InnoDB DEFAULT
CHARSET=utf8 COLLATE=utf8_bin AUTO_INCREMENT=1 ;


ALTER USER 'raghav'@'%' IDENTIFIED WITH mysql_native_password BY '1998';
```







