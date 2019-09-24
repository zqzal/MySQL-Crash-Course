# MySQL-Crash-Course
**MySQL必知必会读书记录**

**读《MySQL必知必会》遇到的问题一(环境问题以及数据源问题)**
**https://mp.weixin.qq.com/s/GhrZ3aq3bgX51ZT5kBA5Hg**




**一起学习**



![扫一扫](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MzI5NjY2Nzk1MQ==&mid=2247483654&idx=1&sn=59305dd60579cf8e10a6c11c3293a559&send_time= "你一关注我就更来劲了!")



**MySQL下载地址**
**https://www.mysql.com/downloads/**

**样例表下载地址**
**https://forta.com/books/0672327120/**

# 第4章 检索数据
## 4.1 selcet语句
## 4.2 检索单个列
`select prod_name from products;`
## 4.3 检索多个列
`select prod_id,prod_name,prod_price from products;`
## 4.4 检索所有的列
`select * from products;`
## 4.5 检索不同的行
`select vend_id from products;`

`select distinct vend_id from products; (检索出不同值的列表)`

## 4.6 限制结果
`select prod_name from products limit 5;`

`select prod_name from products limit 5,5;`

# 第5章 排序检索数据
## 5.1 排序数据
`select prod_name from products;`

`select prod_name from products order by prod_name;`
## 5.2 按多个列排序
`select prod_id,prod_price,prod_name from products order by prod_price,prod_name;`
## 5.3 指定排序方向
`select prod_id,prod_price,prod_name from products order by prod_price desc;`

`select prod_id,prod_price,prod_name from products order by prod_price desc, prod_name;`

`select prod_price from products order by prod_price desc limit 1;`

* order by字句的位置：在给出order by子句时，应该保证它位于from子句之后。如果使用limit，它必须位于order by
之后。使用子句的次序不对将产生错误信息。

# 第6章 过滤数据
## 6.1使用where子句

`select prod_name,prod_price from products where prod_price = 2.50;`

## 6.2 where子句操作符

`= 等于; <> 不等于; != 不等于; < 小于; <=小于等于; > 大于; >= 大于等于 ; between 在指定的两个值之间`

### 6.2.1 检查单个值
`select prod_name,prod_price from products where prod_name = 'fuses';`

`select prod_name,prod_price from products where prod_price < 10;`

`select prod_name,prod_price from products where prod_price <= 10;`

### 6.2.2 不匹配检查
`select vend_id,prod_name from products where vend_id <> 1003;`

`select vend_id,prod_name from products where vend_id != 1003;`

### 6.2.3 范围值检查
`select prod_name,prod_price from products where prod_price between 5 and 10;`

### 6.2.4 空值检查
`select prod_name from products where prod_price is null;`

`select cust_id from customers where cust_email is null;`

# 第7章 数据过滤
## 7.1 组合where子句
* 第6章中 介绍的所有where子句在过滤数据时使用的都是单一的条件。为了进行更强的过滤控制，Mysql允许给出多个where子句。
* 这些子句可以两种方式使用：以and子句的方式或or子句的方式使用。
### 7.1.1 and操作符
`select prod_id,prod_price,prod_name from products where vend_id = 1003 and prod_price <= 10;`
### 7.1.2 or操作符
`select prod_name,prod_price from products where vend_id = 1002 or vend_id =1003;`
### 7.1.3 计算次序
`select prod_name,prod_price from products where (vend_id = 1002 or vend_id =1003) and prod_price >= 10;`

## 7.2 in操作符
`select prod_name,prod_price from products where vend_id in (1002,1003) order by prod_name;`

`select prod_name,prod_price from products where vend_id = 1002 or vend_id = 1003 order by prod_name;`
* in where子句中用来指定要匹配值的清单的关键字，功能与or相当

## 7.3 not操作符
`select prod_name,prod_price from products where vend_id not in (1002,1003) order by prod_name;`
* mysql中的not  mysql支持使用not对in、between和exists子句中取反，这与多数其他DBMS允许使用NOT对各种各样取反右很大的差别

# 第8章 用通配符进行过滤

## 8.1 like操作符
### 8.1.1 百分号（%）通配符
`select prod_id,prod_name from products where prod_name like 'jet%';`

`select prod_id,prod_name from products where prod_name like '%anvil%';`

`select prod_name from products where prod_name like 's%e';`

### 8.1.2 下划线（_）通配符

`select prod_id,prod_name from products where prod_name like '_ ton anvil';`

`select prod_id,prod_name from products where prod_name like '% ton anvil';`

# 第9章 用正则表达式进行搜索
## 9.1 正则表达式介绍

## 9.2 使用MySQL正则表达式
### 9.2.1 基本字符匹配
`select prod_name from products where prod_name regexp '1000' order by prod_name;`

`select prod_name from products where prod_name regexp '.000' order by prod_name;`
### 9.2.2 进行OR匹配
`select prod_name from products where prod_name regexp '1000|2000' order by prod_name;`
### 9.2.3 匹配几个字符之一
`select prod_name from products where prod_name regexp '[123] Ton' order by prod_name;`
`select prod_name from products where prod_name regexp '[1|2|3] Ton' order by prod_name;`
### 9.2.4 匹配范围
`select prod_name from products where prod_name regexp '[1-5] Ton' order by prod_name;`
### 9.2.5 匹配特殊字符
`select vend_name from vendors where vend_name regexp '\\.' order by vend_name;`

### 9.2.6 匹配字符类

* [:alnum:] 任意字母和数字（同[a-z A-Z 0-9]）
* [:alpha:] 任意字符(同[a-z A-Z])
* [:blank:] 空格和制表(同[\\t])
* [:cntrl:] ASCII控制字符(ASCII 0到31和127)
* [:digit:] 任意数字(同[0-9])
* [:graph:] 与[:print:]相同，但不包括空格
* [:lower:] 任意小写字母 (同[a-z])
* [:print:] 任意可打印字符
* [:punct:] 既不在[:alunm:]又不在[:cntrl:]中的任意字符
* [:space:] 包括空格在内的任意空白字符 (同[\\f \\n \\r \\t \\v])
* [:xdight:] 任意十六进制数字 (同[a-f A-F 0-9])

### 9.2.7 匹配多个实例
`select prod_name from products where prod_name regexp '\\([0-9] sticks?\\)' order by prod_name;`

`select prod_name from products where prod_name regexp '[:digit:]' order by prod_name;`

`select prod_name from products where prod_name regexp '[:digit:]{4}' order by prod_name;`

`select prod_name from products where prod_name regexp '[0-9][0-9][0-9][0-9]' order by prod_name;`

### 9.2.8 定位符
* ^ 文本的开始  $ 文本的结尾  [[:<:]] 词的开始   [[:>:]] 词的结尾
`select prod_name from products where prod_name regexp '^[0-9\\.]' order by prod_name;`


like匹配整个串而regexp匹配子串

# 第10章  创建计算字段

## 10.1 计算字段(field)

## 10.2 拼接字段
`select Concat(vend_name,' (',vend_country,')') from vendors order by vend_name;`
* Concat()拼接串，即把多个串连接起来形成一个较长的串。
* Concat()需要一个或多个指定的串，各个串之间用逗号分隔。

`select Concat(vend_name,' (',vend_country,')') as vend_title from vendors order by vend_name;`

`select Concat(RTrim(vend_name),' (',RTrim(vend_country),')') as vend_title from vendors order by vend_name;`
使用别名
`select Concat(RTrim(vend_name),' (',RTrim(vend_country),')') as vend_title from vendors order by vend_name;`

## 10.3 执行算术计算
`select prod_id,quantity,item_price from orderitems where order_num = 20005;`

`select prod_id,quantity,item_price,quantity*item_price as expanded_price from orderitems where order_num = 20005;`


# 第11章 使用数据处理函数

## 11.1 函数

## 11.2 使用函数

### 11.2.1 文本处理函数

`select vend_name,Upper(vend_name) as vend_name_upcase from vendors order by vend_name;`

#### 常用的文本处理函数
* Left() 返回串左边的字符
* Length() 返回串的长度
* L ocate() 找出串的一个字串
* Lower() 将串转换为小写
* LTrim() 去掉串左边的空格
* Right() 返回串右边的字符
* RTrim() 去掉串右边的空格
* Soundex() 返回串的SOUNDEX值
* SubString() 返回字串的字符
* Upper() 将串转换为大写

`select cust_name,cust_contact from customers where soundex(cust_contact) = soundex('Y Lie');`

## 11.2.2 日期和时间处理函数

* AddDate() 增加一个日期（天、周等）
* AddTime() 增加一个时间（时、分等）
* CurDate() 返回当前日期
* CurTime() 返回当前时间
* Date()    返回日期时间的日期部分
* DateDiff() 计算两个日期之差
* Date_Add()高度灵活的日期运算函数
* Date_Format() 返回一个格式化的日期或时间串
* Day()     返回一个日期的天数部分
* Dayofweek() 对于一个日期，返回对应的星期几
* Hour()    返回一个小时的小部分
* Minute()  返回一个时间的分钟部分
* Month()   返回一个日期的月份部分
* Now()    返回当前日期的时间
* Second() 返回一个时间的秒部分
* Time()   返回一个时间的时间部分
* Year()   返回一个日期的年份部分




`select cust_id,order_num from orders where order_date = '2005-09-01';`

`select cust_id,order_num from orders where Date(order_date) = '2005-09-01';`

书中未写出的
`select cust_id,order_num from orders where Time(order_date) = '00:00:00';`

`select * from orders where Date(order_date) >= '2005-09-01';`

`select cust_id,order_num from orders where Date(order_date) between '2005-09-01' and '2005-09-30';`

`select cust_id,order_num from orders where year(order_date) = 2005 and month(order_date) = 9;`
## 11.2.3 数值处理函数

* Abs()  返回一个数的绝对值
* Cos()  返回一个角度的余弦
* Exp()  返回一个数的指数值
* Mod() 返回除操作的余数
* Pi()     返回圆周率
* Rand() 返回一个随机数
* Sin()  返回一个角度的正弦
* Sqrt() 返回一个数的平方根
* Tan()  返回一个角度的正切

# 第12章  汇总数据

## 12.1 聚集函数 (aggregate function) 运行在行组上，计算和返回单个值的函数

* AVG()  返回某个列的平均值
* COUNT() 返回某列的行数
* MAX() 返回某列的最大值
* MIN() 返回某列的最小值
* SUM() 返回某列值之和

## 12.1.1 AVG() 函数

`select AVG(prod_price) as avg_price from products;`

`select avg(prod_price) as avg_price from products where vend_id = 1003;`

## 12.1.2 COUNT()函数

`select count(*) as num_cust from customers;`

`select count(cust_email) as num_cust from customers;`


## 12.1.3 MAX()函数

`select max(prod_price) as max_price from products;`

## 12.1.4 MIIN()函数

`select min(prod_price) as min_price from products;`

## 12.1.5 SUM()函数

`select sum(quantity) as items_ordered from orderitems where order_num = 20005;`

`select sum(item_price*quantity) as total_price from orderitems where order_num = 20005;`

## 12.2 聚集不同值
`select avg(distinct prod_price) as avg_price from products where vend_id = 1003;`

## 12.3 组合聚集函数
```
select count(*) as num_items,
          min(prod_price) as price_min,
          max(prod_price) as price_max,
          avg(prod_price) as price_avg
from products;
```
# 第13章  分组数据

## 13.1 数据分组
`select count(*) as num_prods from products where vend_id = 1003;`

## 13.2 创建分组
`select vend_id,count(*) as num_prods from products group by vend_id;`

## 13.3 过滤分组

`select cust_id,count(*) as orders from orders group by cust_id having count(*) >= 2;`

`select vend_id,count(*) as num_prods from products where prod_price >= 10 group by vend_id having count(*) >= 2;`

`select vend_id,count(*) as num_prods from products group by vend_id having count(*) >= 2;`

## 13.4 分组和排序

        order by                            group by
       排序产生的输出                     分组行。但输出可能不是分组的顺序

      任意列都可以使用                    只可能使用选择列或表达式列，而且必须使用
    (甚至非选择的列也可以使用)            每个选择列表达式

        不一定需要                         如果与聚集函数一起使用列（或表达式），则必须使用

`select order_num,sum(quantity*item_price) as ordertotal from orderitems group by order_num having sum(quantity*item_price) >= 50;`

`select order_num,sum(quantity*item_price) as ordertotal from orderitems group by order_num having sum(quantity*item_price) >= 50 order by ordertotal;`

## 13.5  select子句顺序

        子句               说明               是否必须使用
       select        要返回的列或表达式             是
       from          从中检索数据的表              仅在从表选择数据时使用
       where         行级过滤                     否
       group by      分组说明                 仅在按组计算聚集时使用
       having        组级过滤                     否
       order by      输出排序顺序                  否
       limit         要检索的行数                  否

# 第14章  使用子查询

## 14.1 子查询
* select语句是sql的查询。迄今为止我们所看到的所有select语句都是简单的查询，即从单个数据库表中检索数据的单条语句
* 查询(query) 任何sql语句都是查询。但此术语一般指select语句。
## 14.2 利用子查询进行过滤

`select order_num from orderitems where prod_id = 'TNT2';`

`select cust_id from orders where order_num in (20005,20007);`

`select cust_id from orders where order_num in (select order_num from orderitems where prod_id = 'TNT2');`

`select cust_name,cust_contact from customers where cust_id in (10001,10004);`

`select cust_name,cust_contact from customers where cust_id in (select cust_id from orders where order_num in (select order_num from orderitems where prod_id = 'TNT2'));`

* 这里给出的代码有效并获得所需的结果。但是，使用子查询并不总是执行这种类型的数据检索的最有效的方法。更多的
论述，请参考第15章，其中将再次给出这个例子。

## 14.3 作为计算字段使用子查询
`select cust_name,cust_state,(select count(*) from orders where orders.cust_id = customers.cust_id) as orders  from customers order by cust_name;`

# 第15章 联结表

## 15.1 联结

### 15.1.1 关系表

* 外键(foreign key)  外键为某个表中的一列，它包含另一个表的主键值，定义了两个表之间的关系。
* 可伸缩行(scale) 能够适应不断增加的工作量而不失败。设计良好的数据库或应用程序称之为可伸缩性好(scale well)。

### 15.1.2 为什么使用联结

 * 联结是一种机制，用来在一条select语句中关联表，因此称之为联结。使用特殊的语法，可以联结多个表返回
 * 一组输出，联结在运行时关联表中正确的行。

## 15.2 创建联结
`select vend_name,prod_name,prod_price from vendors,products where vendors.vend_id = products.vend_id order by vend_name,prod_name;`

* 完全限定列名：在引用的列可能出现二义性时，必须使用完全限定列名（用一个点分隔的表明和列名）。如果
* 引用一个没有用表名限定的具有二义性的列名，Mysql将返回错误。

### 15.2.1 where子句的重要性

* 笛卡尔积(cartesian product) 由没有联结条件的表关系返回的结果为笛卡尔积。检索出的行的数目将是第一个表
* 中的行数乘以第二个表中的行数。

* 不要忘了where子句：应该保证所有联结都有where子句，否则mysql将返回比想要的数据多得多的数据。同理，
* 应该保证where子句的正确性。不正确的过滤条件将导致mysql返回不正确的数据。

### 15.2.2 内部联结

`select vend_name,prod_name,prod_price from vendors inner join products on vendors.vend_id = products.vend_id;`

### 15.2.3 联结多个表

`select prod_name,vend_name,prod_price,quantity from orderitems,products,vendors where products.vend_id = vendors.vend_id and orderitems.prod_id = products.prod_id and order_nmu = 20005;`

`select cust_name,cust_contact from customers where cust_id in (select cust_id from orders where order_num in (select order_num from orderitems where prod_id = 'TNT2'));`
* 子查询并不总是执行复杂select操作的最有效的方法，下面是使用联结的相同查询：

`select cust_name,cust_contact from customers,orders,orderitems where customers.cust_id = orders.cust_id and orderitems.order_num = orders.order_num and prod_id = 'TNT2';`


## 15.3 小结

* 联结是sql中最重要最强大的特性，有效地使用联结需要对关系数据库设计有基本的了解。本章随着对联结的介绍讲述
* 了关系数据库设计的一些基本知识，包括等值联结（也称为内部联结）这种最经常使用的联结形式。

# 第16章 创建高级联结

## 16.1 使用表别名

`select concat(RTrim(vend_name),' (',RTrim(vend_country),')') as vend_title from vendors order by vend_name;`

* 别名除了用于列名和计算字段外，sql还允许给表名起别名。这样做有两个主要理由
1. 缩短sql语句
2. 允许在单条select语句中多次使用相同的表

`select cust_name,cust_contact from customers as c, orders as o, orderitems as oi where c.cust_id = o.cust_id and oi.order_num = o.order_num and prod_id = 'TNT2';`

## 16.2 使用不同类型的联结
* 迄今为止，我们使用的只是称为内部联结或等值联结（equijoin）的简单联结。现在来看3种其他联结，它们分别是自联结、自然联结和外部联结。
### 16.2.1 自联结

`select prod_id,prod_name from products where vend_id = (select vend_id from products where prod_id = 'DTNTR');`

```
+---------+----------------+
| prod_id | prod_name      |
+---------+----------------+
| DTNTR   | Detonator      |
| FB      | Bird seed      |
| FC      | Carrots        |
| SAFE    | Safe           |
| SLING   | Sling          |
| TNT1    | TNT (1 stick)  |
| TNT2    | TNT (5 sticks) |
+---------+----------------+
```

`select p1.prod_id,p1.prod_name from products as p1,products as p2 where p1.vend_id = p2.vend_id and p2.prod_id = 'DTNTR';`

```
+---------+----------------+
| prod_id | prod_name      |
+---------+----------------+
| DTNTR   | Detonator      |
| FB      | Bird seed      |
| FC      | Carrots        |
| SAFE    | Safe           |
| SLING   | Sling          |
| TNT1    | TNT (1 stick)  |
| TNT2    | TNT (5 sticks) |
+---------+----------------+
```

### 16.2.2 自然联结

`select c.*,o.order_num,o.order_date,oi.prod_id,oi.quantity,oi.item_price from customers as c,orders as o,orderitems as oi where c.cust_id = o.cust_id and oi.order_num = o.order_num and prod_id = 'FB';`


```
+---------+-------------+----------------+-----------+------------+----------+--------------+--------------+-----------------+-----------+---------------------+---------+----------+------------+
| cust_id | cust_name   | cust_address   | cust_city | cust_state | cust_zip | cust_country | cust_contact | cust_email      | order_num | order_date          | prod_id | quantity | item_price |
+---------+-------------+----------------+-----------+------------+----------+--------------+--------------+-----------------+-----------+---------------------+---------+----------+------------+
|   10001 | Coyote Inc. | 200 Maple Lane | Detroit   | MI         | 44444    | USA          | Y Lee        | ylee@coyote.com |     20005 | 2005-09-01 00:00:00 | FB      |        1 |      10.00 |
|   10001 | Coyote Inc. | 200 Maple Lane | Detroit   | MI         | 44444    | USA          | Y Lee        | ylee@coyote.com |     20009 | 2005-10-08 00:00:00 | FB      |        1 |      10.00 |
+---------+-------------+----------------+-----------+------------+----------+--------------+--------------+-----------------+-----------+---------------------+---------+----------+------------+
```

### 16.2.3 外部联结

`select customers.cust_id,orders.order_num from customers inner join orders on customers.cust_id = orders.cust_id;`

```
+---------+-----------+
| cust_id | order_num |
+---------+-----------+
|   10001 |     20005 |
|   10001 |     20009 |
|   10003 |     20006 |
|   10004 |     20007 |
|   10005 |     20008 |
+---------+-----------+
```
`select customers.cust_id,orders.order_num from customers left outer join orders on customers.cust_id = orders.cust_id;`

```
+---------+-----------+
| cust_id | order_num |
+---------+-----------+
|   10001 |     20005 |
|   10001 |     20009 |
|   10002 |      NULL |
|   10003 |     20006 |
|   10004 |     20007 |
|   10005 |     20008 |
+---------+-----------+
```

`select customers.cust_id,orders.order_num from customers right outer join orders on orders.cust_id = customers.cust_id;`

```
+---------+-----------+
| cust_id | order_num |
+---------+-----------+
|   10001 |     20005 |
|   10001 |     20009 |
|   10003 |     20006 |
|   10004 |     20007 |
|   10005 |     20008 |
+---------+-----------+
```

## 16.3 使用带聚集函数的联结
`select customers.cust_name,customers.cust_id,count(orders.order_num) as num_ord from customers inner join orders on customers.cust_id = orders.cust_id group by customers.cust_id;`

`select customers.cust_name,customers.cust_id,count(orders.order_num) as num_ord from customers left outer join orders on customers.cust_id = orders.cust_id group by customers.cust_id;`

## 16.4 使用联结和联结条件

* 注意所使用的联结类型。一般我们使用内部联结，但使用外部联结也是有效的
* 保证使用正确的联条件，否则将返回不正确的数据
* 应该总是提供联结条件，否者会得出笛卡尔积
* 在一个联结中可以包含多个表，甚至对于每个联结可以采用不同的联结类型。虽然这样做是合法的，一般也很有用，但应该在一起测试它们前，分别测试每个联结。这将使故障排除更为简单。

# 第17章 组合查询

## 17.1 组合查询
* 组合查询和多个where条件 ：多数情况下，组合相同表的两个查询完成的工作与具有多个where子句条件的单条查询完成的工作相同。换句话说，任何具有多个where子句的select语句都可以作为一个组合查询给出，在一下段落中可以看到这一点。这两种技术在不同的查询中性能也不同。因此，应该试一下这两种技术，以确定对特定的查询哪一种性能更好。

## 17.2 创建组合查询


### 17.2.1 使用union

`select vend_id,prod_id,prod_price from products where prod_price <= 5;`

`select vend_id,prod_id,prod_price from products where vend_id in (1001,1002);`

```
select vend_id,prod_id,prod_price from products where prod_price <= 5 
union
select vend_id,prod_id,prod_price from products where vend_id in (1001,1002);
```
`select vend_id,prod_id,prod_price from products where prod_price <=5 or vend_id in (1001,1002);`

### 17.2.2 union规则

* union必须由两条或两条以上的select语句组成，语句之间用关键字union分隔（因此，如果组合4条select语句，将要使用3个union关键字）
* union中的每个查询必须包含相同的列、表达式或聚集函数（不过各个列不需要以相同的次序列出）
* 列数据类型必须兼容：类型不必完全相同，但必须是DBMS可以隐含地转换的类型（例如，不同的数值类型或不同的日期类型）

### 17.2.3 包含或取消重复行

`select vend_id,prod_id,prod_price from products where prod_price <=5 union all select vend_id,prod_id,prod_price from products where vend_id in (1001,1002);`

* union与where ： union几乎总是完成与多个where条件相同的工作。union all为union的一种形式，它完成wherei子句完成不了的工作。如果确实需要每个条件的匹配行全部出现（包括重复行），则必须使用union all 而不是where

### 17.2.4 对组合查询结果排序

`select vend_id,prod_id,prod_price from products where prod_price <= 5 union select vend_id,prod_id,prod_price from products where vend_id in (1001,1002) order by vend_id,prod_price;`

## 17.3 小结

# 第18章 全文本搜索

## 18.1 理解全文本搜索
## 18.2 使用全文本搜索

### 18.2.1 使用全文本搜索

### 18.2.2 进行全文搜索

`select note_text from productnotes where match(note_text) against('rabbit');`

`select note_text from productnotes where note_text like '%rabbit%';`

### 18.2.3 使用查询扩展

### 18.2.4 布尔文本搜索

### 18.2.5 全文本搜索的使用说明

## 18.3 小结

# 第19章 插入数据

## 19.1 数据插入

* 插入完成的行
* 插入行的一部分
* 插入多行 
* 插入某些查询的结果

## 19.2 插入完整的行
```
insert into customers values(NULL,
'Pep E. LaPew',
'100 Main Street',
'Los Angeles',
'CA',
'90046',
'USA',
NULL,
NULL);
```

```
insert into customers(cust_name,
cust_address,
cust_city,
cust_state,
cust_zip,
cust_country,
cust_contact,
cust_email) 
values('Pep E. LaPew',
'100 Main Street',
'Los Angeles',
'CA',
'90046',
'USA',
NULL,
NULL);
```

```
insert into customers(cust_name,
cust_contact,
cust_email,
cust_address,
cust_city,
cust_state,
cust_zip,
cust_country) 
values('Pep E.LaPew',
NULL,
NULL,
'100 Main Street',
'Los Angeles',
'CA',
'90046',
'USA');
```

* 一般不要使用没有明确给出列的列表的insert语句。使用列的列表能使sql代码继续发挥作用，即使表结构发生了变化


## 19.3 插入多个行

`insert into customers(cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country) values('Pep E. LaPew','100 Main Street','Los Angeles','CA','90046','USA'); insert into customers(cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country) values('M. Martain','42 Galaxy Way','New York','NY','11213','USA');`


`insert into customers(cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country) values('Pep E. LaPew','100 Main Street','Los Angeles','CA','90046','USA'),('M. MARTIAN','42 Galaxy Way','New York','NY','11213','USA');`

* 提高insert的性能：此技术可以提高数据库处理的性能，因为mysql用单条insert语句处理多个插入比使用多条insert语句快。

## 19.4 插入检索出的数据

`insert into customers(cust_id,cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country) select cust_id,cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country from custnew;`

## 19.5 小结

# 第20章 更新和删除数据
## 20.1 更新数据

* update语句由3部分组成，分别是
1. 要更新的表
2. 列名和它们的新值
3. 确定要更新行的过滤条件

`update customers set cust_email = 'elmer@fudd.com' where cust_id = 10005;`

`update customers set cust_name = 'The Fudds',cust_email = 'elmer@fudd.com' where cust_id = 10005;`

`update customers set cust_email = NULL where cust_id = 10005;`

## 20.2 删除数据
* 两种方式使用Delete
1. 从表中删除特定的行
2. 从表中删除所有行

`delete from customers where cust_id = 10006;`

* truncate table 语句 删除所有行

## 20.3 更新和删除的指导原则


## 20.4 小结

# 第21章 创建和操作表
## 21.1 创建表
### 21.1.1 表创建基础
### 21.1.2 使用null值
### 21.1.3 主键在介绍
### 21.1.4 使用AUTO_INCREMENT
### 21.1.5 指定默认值
### 21.1.6 引擎类型
## 21.2 更新表

`alter table vendors add vend_phone CHAR(20);`

`alter table vendors drop column vend_phone;`


## 21.3 删除表

`drop table customers2;`

## 21.4 重命名表

`rename table customer2 to customers;`

## 21.5 小结

# 第22章 使用视图
* 本章将介绍视图究竟是什么，它们怎样工作，何时使用它们。我们还将看到如何利用视图简化前面章节中执行的某些sql操作。


## 22.1 视图
* 视图是虚拟的表。与包含数据的表不一样，视图只包含使用时动态检索数据的查询。

`select cust_name,cust_contact from customers,orders,orderitems where customers.cust_id = orders.cust_id and orderitems.order_num = orders.order_num and prod_id = 'TNT2';`

`select cust_name,cust_contact from productcustomers where prod_id = 'TNT2';`

### 22.1.1 为什么使用视图
### 22.1.2 视图的规则和限制
## 22.2 使用视图
### 22.2.1 利用视图简化复杂的联结
`create view productcustomers as select cust_name,cust_contact,prod_id from customers,orders,orderitems where customers.cust_id = orders.cust_id and orderitems.order_num = orders.order_num;`

`select * from productcustomers;`

`select cust_name,cust_contact from productcustomers where prod_id = 'TNT2';`

### 22.2.2 用视图重新格式化检索出的数据

`select concat(RTrim(vend_name),' (',RTrim(vend_country),')') as vend_title from vendors order by vend_name;`

`create view vendorlocations as select concat(RTrim(vend_name),' (',RTrim(vend_country),')') as vend_title from vendors order by vend_name;`

### 22.2.3 用视图过滤不想要的数据

`create view customeremaillist as select cust_id,cust_name,cust_email from customers where cust_email is not NULL;`

`select * from customeremaillist;`

### 22.2.4 使用视图与计算字段
`select prod_id,quantity,item_price,quantity*item_price as expanded_price from orderitems where order_num = 20005;`

`create view orderitemsexpanded as select prod_id,quantity,item_price,quantity*item_price as expanded_price from orderitems;`

`select * from orderitemsexpanded where order_num = 20005;`

### 22.2.5 更新视图
## 22.3 小结

* 视图为虚拟的表。它们包含的不是数据而是根据需要检索数据的查询。视图提供了一种mysql的select语句层次的封装，可用来简化数据处理以及重新格式化基础数据或保护基础数据。

# 第23章 使用存储过程
## 23.1 存储过程
## 23.2 为什么使用存储过程
## 23.3 使用存储过程
### 23.3.1 执行存储过程
### 23.3.2 创建存储过程
### 23.3.3 删除存储过程
### 23.3.4 使用参数
### 23.3.5 建立智能存储过程
### 23.3.6 检查存储过程
## 23.4 小结

# 第24章 使用游标
## 24.1 游标

## 24.2 使用游标

### 24.2.1 创建游标
### 24.2.2 打开关闭游标
### 24.2.3 使用游标数据

# 第25章 使用触发器
## 25.1 触发器
## 25.2 创建触发器
## 25.3 删除触发器
## 25.4 使用触发器
### 25.4.1 insert触发器
### 25.4.2 delete触发器
### 25.4.3 update触发器
### 25.4.4 关于触发器的进一步介绍
## 25.5 小结

# 第26章 管理事务处理

## 26.1 事务处理
## 26.2 控制事务处理

### 26.2.1 使用rollback
### 26.2.2 使用commit
### 26.2.3 使用保留点
### 26.2.4 更改默认的提交行为

# 第27章 全球化和本地化

## 27.1 字符集和校对顺序

## 27.2 使用字符集和校对顺序

## 27.3 小结

# 第28章 安全管理

## 28.1 访问控制
## 28.2 管理用户
### 28.2.1 创建用户账号
### 28.2.2 删除用户账号
### 28.2.3 设置访问权限
### 28.2.4 更改口令

## 28.3 小结

# 第29章 数据库维护

## 29.1 备份数据

## 29.2 进行数据库维护
## 29.3 诊断启动问题
## 29.4 查看日志文件
## 29.5 小结

# 第30章 改善性能

## 30.1 改善性能
## 30.2 小结
