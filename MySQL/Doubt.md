# MySQL疑难杂症

### 1、数据库乱码
```
mysql> SET charset gbk;
```
设置数据库编码
<br><br><br>


### 2、数据显示不对齐
默认设置：
```
mysql --default-character-set=latin1 -uroot -p
```
万国码设置（中文乱码用这个）：
```
mysql --default-character-set=gbk -uroot -p
```
设置中文字符集
<br><br><br>

### 3、phpMyadmin无法登陆
MySQL返回错误：
```
    SET lc_messages = 'zh_CN';
    #1193 - Unknown system variable 'lc_messages'
```
错误原因:

MySQL版本低于phpMyAdmin要求的最低版本。

##### 1.  安装旧版本phpMyAdmin。
```
    For mySQL 5.5, use phpMyAdmin 4.4.x and above
    For mySQL 5.1, use phpMyAdmin 4.0.x
```
##### 2.  注释限制代码
###### ①注释phpMyAdmin/libraries/common.inc.php中以下代码：
```
    if ($GLOBALS['dbi']->getVersion() < $cfg['MysqlMinVersion']['internal']) {
        Core::fatalError(
            __('You should upgrade to %s %s or later.'),
            array('MySQL', $cfg['MysqlMinVersion']['human'])
        );
    }
```
###### ②注释phpMyAdmin/libraries/classes/DatabaseInterface.php中以下代码：
```
    if (! empty($locale)) {
        $this->query(
            "SET lc_messages = '" . $locale . "';",
            DatabaseInterface::CONNECT_USER,
            self::QUERY_STORE
        );
    }
```
