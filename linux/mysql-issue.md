##Mysql中文乱码问题
###创建数据库的时候
```
CREATE DATABASE `test`;
CHARACTER SET 'utf8';
COLLATE 'utf8_general_ci';
```


###创建表的时候
```
CREATE TABLE `database_user` (
`ID` varchar(40) NOT NULL default '',
`UserID` varchar(40) NOT NULL default '',
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

###连接的时候
```
import MySQLdb as mysql
mdb = mysql.connect(host='localhost',user='user',passwd='password', db='test', charset="utf8")
connenction = mdb.cursor()
connection.execute("SET NAMES utf8")
```


##MySQLdb-python安装

```
sudo apt-get install mysql
sudo apt-get install libmysqld-dev
sudo apt-get install python-dev
sudo pip install MySQLdb-python
```

