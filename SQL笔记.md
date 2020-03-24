

# **一、工具环境安装**

链接：https://pan.baidu.com/s/1b5WEtBrHhKoG76ZB3C8dEg 

提取码：2c5a

下载并安装mysql及其可视化工具navicatformysql

# **二、SQL概述**

## **2.1 数据库基础**

### **2.1.1 数据库**

- 数据库

数据库是一个以某种有组织的方式存储的数据集合

- 数据库软件

数据库软件也称为数据库管理系统（DBMS，Data Base Manage System）

- 数据模型

数据库按照数据结构来组织、存储和管理数据，实际上，数据库一共有三种模块

- 层次模型：其数据结构看起来像一棵树
- 网状模型：其数据结构看起来像很多城市之间的网路
- 关系模型：其数据模型看起来像一张Excel表，任何数据可通过行号+列号来唯一确定

- `SQL`

`SQL`用来实现以某种方式与数据库打交道。`SQL`是结构化查询语言的缩写(Structured Query Language)，用来访问和操作数据库系统

- `SQL`语言定义了3种操作数据库的能力
  - `DDL`(Data Definition Language)：允许用户定义数据，即创建表、删除表、修改表结构这些操作
  - `DML`(Data Manipulation Language)：为用户提供添加、删除、更新数据的能力，这些是对数据库的日常操作
  - `DQL`(Data Query Language)：允许用户查询数据，最为频繁的数据库操作

### **2.1.2 表**

- 表

表是一种结构化文件，可用来存储某种特定类型的数据。表可以用来保存用户清单、产品目录、学生信息等。

- 表名

同一数据库中不能出现2个一样的表名

- 模式

关于数据库和表的布局及特性的信息。可以用来描述数据库中特定的表，也可以用来描述整个数据库

### **2.1.3列和数据类型**

- 列

表中的某个字段。存储表中某部分信息

- 数据类型

所允许的数据的类型。每个表列都有相应的数据类型，限制了该列中存储的数据

- 常用数据类型

| 名称         | 类型           | 说明                                   |
| ------------ | -------------- | -------------------------------------- |
| int          | 整型           | 4字节整数类型，范围约+/-21亿           |
| bigint       | 长整型         | 8字节整数类型，范围约+/-922亿          |
| float/real   | 浮点型         | 4字节浮点数，范围约+/-10的38次方       |
| double       | 浮点型         | 8字节浮点数                            |
| decimal(M,N) | 高精度小数     | 由用户指定精度的小数                   |
| char(N)      | 定长字符串     | 存储指定长度的字符串                   |
| varchar(N)   | 变长字符串     | 存储可变长度的字符串                   |
| boolean      | 布尔类型       | 存储ture或false                        |
| date         | 日期类型       | 存储日期，如：2019-12-22               |
| time         | 时间类型       | 存储时间，如：12:20:49                 |
| datetime     | 日期和时间类型 | 存储日期+时间，如：2019-12-22 12:20:49 |

### **2.1.4 行**

- 行

表中的一个记录（`item/record`）

## **2.2 关系模型**

### **2.2.1 主键**

- 主键

唯一标识表中每行的列称为主键；主键不能重复

### **2.2.2 外键**

- 外键

关系型数据库中的一条记录中有若干个属性，若其中某一个属性组(注意是组)能唯一标识一条记录，该属性组就可以成为一个主键 

比如： 

学生表(学号，姓名，性别，班级) 

其中每个学生的学号是唯一的，学号就是一个主键 

课程表(课程编号,课程名,学分) 

其中课程编号是唯一的,课程编号就是一个主键 

成绩表(学号,课程号,成绩) 

成绩表中单一一个属性无法唯一标识一条记录，学号和课程号的组合才可以唯一标识一条记录，所以学号和课程号的属性组是一个主键 

成绩表中的学号不是成绩表的主键，但它和学生表中的学号相对应，并且学生表中的学号是学生表的主键，则称成绩表中的学号是学生表的外键 

同理，成绩表中的课程号是课程表的外键 

- 外键并不是通过列名实现的，而是通过定义外键约束实现的
- 关系数据库通过外键可以实现一对多、多对多和一对一的关系。外键既可以通过数据库来约束，也可以不设置约束，仅依靠应用程序的逻辑来保证。

### **2.2.3 索引**

- 索引是关系数据库中对某一列或多个列的值进行预排序的数据结构，大大加快了查询速度
- 通过创建唯一索引，可以保证某一列的值具有唯一性
- 数据库索引对于用户和应用程序来说都是透明的
- 创建索引

如果要经常根据'`score`'列进行查询，就可以对`score`列创建索引

```sql
alter table students
add index idx_score (score)
;
```

- 创建唯一索引

```sql
alter table students
add unique index uni_name(name)
;
```

通过unique关键字创建唯一索引

# **三、查询数据**

## **3.1 基本查询**

```sql
select * from table_name   ---- 从某个表中查询所有列
```

```sql
select coulum_name from table_name   ---- 从某个表中查询指定列
```

## **3.2 条件查询**

```sql
---- 从某个表中查询满足某个条件的所有列
select * from table_name 
where <条件表达式>
```

## **3.3 投影查询**

- 使用`select 列1，列2，列3`返回指定列的操作称为投影

```sql
---- 查询3月21日用户的身份和平台
select client_id,mode
from user_profile
where dt = '20200321'
;
```

## **3.4 排序**

- 排序：`order by` 
- 默认：升序；`desc`：降序

```sql
select id,name,gender,score
from students
order by score desc
;
```

## **3.5 分页查询**

- 分页

  使用`select`查询时，如果数据集数据量很大，比如几万行数据，放在一页上显示数据量太大，不如分页显示，每页显示100条。分页实际上就是从结果集中截取出第M~N条记录。这个查询可以通过<font color=red>`limit <M> offset <N>`</font>实现

  ```sql
  -- 按成绩从高到低的顺序将所有学生信息取出
  select id, name, gender, score
  from students
  order by score desc
  
  -- 将上述结果分页，每页显示3条，用limit 3 offset 0 查询第一页
  select id, name, gender, score
  from students
  order by score desc
  limit 3 offset 0       -- 注意：SQL记录集从0开始
  ;
  
  -- 查询第2页
  select id, name, gender, score
  from students
  order by score desc
  limit 3 offset 3
  ;
  
  -- 查询第3页
  select id, name, gender, score
  from students
  order by score desc
  limit 3 offser 6
  ;
  
  -- 查询第4页
  select id, name, gender, score
  from students
  order by score desc
  limit 3 offset 9   -- limit 3 表示最多显示3条
  ;
  ```

- 分页的关键

  分页的关键在于首先要确定每页需要显示的结果数量`pageSize`，然后根据当前页的索引`pageIndex`(从1开始)，确定`limit`和`offset`应该设置的值

  - `limit`总是设定为`pageSize`
  - `offset`计算公式为`pageSize * (pageIndex - 1)`

  - <font color=red>注意</font>

    - `offset`是可选的，如果只`写limit 15`，其相当于`limit 15 offset 0`
    - 在MySQL中，`limit 15 offset 30`还可简写成`limit 30, 15`
    - 使用`limit <M> offser <N>`分页时，随着`N`越来越大，查询效率也会越来越

## 3.6 聚合查询

- 聚合查询

  `SQL`提供了一些函数快速实现了聚合查询。如统计一张数据库表总共有多少条记录，便可用`count()`来取

  ```sql
  count(*) 查询所有列的行数
  select count(*)
  from students
  ;
  ```

- 聚合函数

  除了`count()`函数外，`SQL`还提供了以下聚合函数

  | 函数 | 说明                                 |
  | ---- | ------------------------------------ |
  | sum  | 计算某列的合计值，该列必须为数值类型 |
  | avg  | 计算某列的平均值，该列必须为数值类型 |
  | max  | 计算某列的最大值                     |
  | min  | 计算某列的最小值                     |

  <font color=red>注：</font>`max()`和`min()`函数并不局限于数值类型。如果是字符类型，`max()`和`min()`会返回排序最后和排序最前的字符

  例：使用聚合函数计算男生的平均成绩

  ```sql
  select avg(acore) average
  from students
  where gender = 'M'
  ;
  ```

- <font color=red>注意</font>

  如果聚合查询的`wherd`条件没有匹配到任何行，`count()`会返回0，而`sum()`、`avg()`、`max()`和`min()`会返回`null`

## 3.7 多表查询

- `select` 查询不但可以查询一张表，还可以从多张表中同时查询。查询多张表的语法为：`select * from <table1><table2>`。如同时从`students`表和`classes`表的笛卡儿积中查询数据可写为：`select * from students, classes;`

- `from`子句给表设置别名的语法是`from <table1><别名1>,<table2><别名2>`，多表查询也可以添加`where`条件