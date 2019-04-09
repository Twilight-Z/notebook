# MySQL疑难杂症

### 1、数据库乱码
```
mysql> SET charset gbk;
```
设置数据库编码
<br><br><br>


### 2、数据显示不对齐
```
mysql --default-character-set=latin1 -uroot -p
mysql --default-character-set=gbk -uroot -proot
```
设置中文字符集
<br><br><br>

