

### 数据类型

| 数据类型  |            长度            |
| :-------: | :------------------------: |
|  tinyint  |      1byte 有符号整数      |
|  smalint  |      2byte 有符号整数      |
|    int    |      4byte 有符号整数      |
|  bigint   |      8byte 有符号整数      |
|  boolean  | 布尔类型， true 或者 false |
|   float   |        单精度浮点数        |
|  double   |        双精度浮点数        |
|  string   |  字符序列 单引号或双引号   |
| timestamp |   整数，浮点数，或字符串   |
|  binary   |          字节数组          |
|  struct   |           结构体           |
|    map    |       Key-Value集合        |
|   array   |          数组类型          |

```sql
-- 不同数据类型使用和自动以分隔符 案例
CREATE TABLE employees(
	name string,
    salary float,
    subordinates array<string>,
    deductions map<string,float>,
    address struct<street:string, city:string, state:string, zip:int>
)
ROW FORMAT DELIMITED				
FIELDS TERMINATED BY '\001'				-- 列分隔符 \001(^A 的八进制数) 
COLLECTION ITEMS TERMINATED BY '\002'	-- 集合元素分隔符 \002(^B 的八进制数)
MAP KEYS TERMINATED BY '\003'			-- MAP的键和值分隔符 \003(^C 的八进制数)
LINES TERMINATED BY '\n'				-- 行分隔符
STORES AS TEXTFILE;						-- 存储用 textfile 文件格式
```

### DDL

#### Database

```sql

-- 查询所有数据库
SHOW DATABASES;

-- 正则表达式 筛选 库名
SHOW DATABASES LIKE 'd.*';

-- 数据库所在目录位于  hive.metastore.warehouse.dir 配置中  默认值  /user/hive/warehouse
-- 创建数据库 并指定位置
CREATE DATABASE test LOCATION '/hive/test';

--创建数据库，如果不存在 , 默认 存在会抛出错误信息
CREATE DATABASE test IF NOT EXISTS test;

-- 创建数据库 配置描述信息
-- Hive会对应创建一个 hdfs://localhost:9000/user/hive/warehouse/test2.db 目录
CREATE DATABASE test2 COMMENT 'test2 database';

--为数据库添加 Key-Value 对属性信息
CREATE DATABASE test3 WITH DBPROPERTIES ('creator'='huwei' , 'date'='2018-06-05');

--修改数据库
ALTER DATABASES test3 SET DBPROPERTIES('editedBy'='zhangsan');

--查询数据库信息
DESCRIBE DATABASE test;

--查询数据库信息 含Key-Value属性
DESCRIBE DATABASE EXTENDED test3;

--设置当前工作数据库
USE test3;

--显示当前数据库下所有表
SHOW TABLES;

--设置提示符里面显示当前所在数据库
hive> set hive.cli.print.current.db=true;
hive (default)> use test3;
OK
Time taken: 0.022 seconds
hive (test3)> 


--删除数据库 如果存在
DROP DATABASES IF EXISTS test;

--默认Hive不允许删除一个含有表的数据库
--方案一 先删除所有表，再删除数据库
--方案二 DROP 最后 添加关键字 CASCADE(层叠)
DROP DATABASE IF EXISTS test CASCADE;

```



#### Table

```sql



```

