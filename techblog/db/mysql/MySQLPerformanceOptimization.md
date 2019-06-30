# MySQL 性能优化

[TOC]

## 何谓性能优化


- 优化简介

所谓 **MySQL 性能优化**，一方面是指通过调整系统参数、合理安排资源使得MySQL的运行速度更快、更加节省资源，另一方面，也指优化我们通常使用的SQL语句——尤其是查询语句，来提高MySQL的性能。

- 基本原则

MySQL 性能优化的基本原则是：

1. 减少系统瓶颈；
2. 减少资源占用；
3. 提高系统反应速度。

- 常用方法

MySQL 性能优化通常从以下几个方面入手：

1. 找出系统瓶颈，提高MySQL数据库整体的性能；
2. 合理的结构设计和参数调整，提高数据库操作的相应速度；
3. 最大限度节省系统资源，以便系统可以提供更大负荷的服务。

例如：

1. 通过优化文件系统，来提高磁盘I/O的独写速度；
2. 通过优化操作系统的调度策略，提高MySQL在高负荷情况下的负载能力；
3. 通过优化表结构、索引、查询语句等使得查询响应更快。

## 查看MySQL性能参数

在MySQL中可以使用`SHOW STATUS`语句来查看MySQL数据库的性能参数，我们可以根据这些性能参数来了解MySQL数据库的状态，并制定合理的优化策略。

执行`show status;`可以查看所有的性能参数，执行`show status like '参数名称';`可以查看指定参数名称的性能参数，一般某一类参数都有相同的前缀。

下面是`show status;`语句的返回结果，有356个，这里省略了大部分：
```sql
mysql> show status;
+-----------------------------------------------+--------------------------------------------------+
| Variable_name                                 | Value                                            |
+-----------------------------------------------+--------------------------------------------------+
| Aborted_clients                               | 0                                                |
| Aborted_connects                              | 2
| Bytes_received                                | 256                                              |
| Bytes_sent                                    | 185                                              |
| **这里省略了一部分......**                                                                          |
| Threads_running                               | 1                                                |
| Uptime                                        | 1038207                                          |
| Uptime_since_flush_status                     | 1038207                                          |
+-----------------------------------------------+--------------------------------------------------+
356 rows in set (0.00 sec)
```

下面是对部分性能参数的说明，详细的说明请访问
[Github开源Blog](https://github.com/ijiangtao/blog/blob/master/techblog/db/mysql/MySQLServeStatusVariables.md) : https://github.com/ijiangtao/blog/blob/master/techblog/db/mysql/MySQLServeStatusVariables.md

<table cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<p><strong>状态名</strong></p>
</td>
<td>
<p><strong>作用域</strong></p>
</td>
<td>
<p><strong>详细解释</strong></p>
</td>
</tr>
<tr>
<td>
<p>Aborted_clients</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>由于客户端没有正确关闭连接导致客户端终止而中断的连接数</p>
</td>
</tr>
<tr>
<td>
<p>Aborted_connects</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>试图连接到MySQL服务器而失败的连接数</p>
</td>
</tr>
<tr>
<td>
<p>Handler_read_prev</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>按照键顺序读前一行的请求数。该读方法主要用于优化ORDER BY ... DESC。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_read_rnd</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>根据固定位置读一行的请求数。如果你正执行大量查询并需要对结果进行排序该值较高。你可能使用了大量需要MySQL扫描整个表的查询或你的连接没有正确使用键。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_read_rnd_next</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在数据文件中读下一行的请求数。如果你正进行大量的表扫描，该值较高。通常说明你的表索引不正确或写入的查询没有利用索引。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_rollback</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>内部ROLLBACK语句的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_savepoint</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在一个存储引擎放置一个保存点的请求数量。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_savepoint_rollback</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在一个存储引擎的要求回滚到一个保存点数目。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_update</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在表内更新一行的请求数。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_write</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在表内插入一行的请求数。</p>
</td>
</tr>
<tr>
<td>
<p>Last_query_cost</p>
</td>
<td>
<p>Session</p>
</td>
<td>
<p>用查询优化器计算的最后编译的查询的总成本。用于对比同一查询的不同查询方案的成本。默认值0表示还没有编译查询。&nbsp;默认值是0。Last_query_cost具有会话范围。</p>
</td>
</tr>
<tr>
<td>
<p>Max_used_connections</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>服务器启动后已经同时使用的连接的最大数量。</p>
</td>
</tr>
<tr>
<td>
<p>Open_tables</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>当前打开的表的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_free_memory</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>用于查询缓存的自由内存的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_hits</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>查询缓存被访问的次数。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_inserts</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>加入到缓存的查询数量。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_total_blocks</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>查询缓存内的总块数。</p>
</td>
</tr>
<tr>
<td>
<p>Queries</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>服务器执行的请求个数，包含存储过程中的请求。</p>
</td>
</tr>
<tr>
<td>
<p>Questions</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>已经发送给服务器的查询的个数。</p>
</td>
</tr>
<td>
<p>Select_full_join</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>没有使用索引的联接的数量。如果该值不为0,你应仔细检查表的索引</p>
</td>
</tr>
<tr>
<td>
<p>Select_full_range_join</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在引用的表中使用范围搜索的联接的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Select_range</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在第一个表中使用范围的联接的数量。一般情况不是关键问题，即使该值相当大。</p>
</td>
</tr>
<tr>
<td>
<p>Select_range_check</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在每一行数据后对键值进行检查的不带键值的联接的数量。如果不为0，你应仔细检查表的索引。</p>
</td>
</tr>
<tr>
<td>
<p>Select_scan</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>对第一个表进行完全扫描的联接的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Slave_running</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>如果该服务器是连接到主服务器的从服务器，则该值为ON。</p>
</td>
</tr>
<tr>
<td>
<p>Slow_queries</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>查询时间超过long_query_time秒的查询的个数。</p>
</td>
</tr>
<tr>
<td>
<p>Sort_range</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在范围内执行的排序的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Sort_rows</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>已经排序的行数。</p>
</td>
</tr>
<tr>
<td>
<p>Sort_scan</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>通过扫描表完成的排序的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Table_locks_immediate</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>立即获得的表的锁的次数。</p>
</td>
</tr>
<tr>
<td>
<p>Table_locks_waited</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>不能立即获得的表的锁的次数。如果该值较高，并且有性能问题，你应首先优化查询，然后拆分表或使用复制。</p>
</td>
</tr>
<tr>
<td>
<p>Threads_cached</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>线程缓存内的线程的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Threads_connected</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>当前打开的连接的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Threads_created</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>创建用来处理连接的线程数。如果Threads_created较大，你可能要增加thread_cache_size值。缓存访问率的计算方法Threads_created/Connections。</p>
</td>
</tr>
<tr>
<td>
<p>Threads_running</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>激活的（非睡眠状态）线程数。</p>
</td>
</tr>
<tr>
<td>
<p>Uptime</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>服务器已经运行的时间（以秒为单位）。</p>
</td>
</tr>
</tbody>
</table>

## MySQL查询优化

查询是数据库中最频繁的操作，优化查询可以很有效的提高MySQL的数据库性能。

### 分析查询语句

我们可以使用`explain`或者`describe`关键字来分析查询语句，语法如下：
1. `explain [extended] SELECT SelectOptions`
2. `describe [extended] SELECT SelectOptions`
3. `desc [extended] SELECT SelectOptions`

```sql
mysql> explain extended SELECT id, name, ip_address, `action`, create_time FROM t_user_action_log where id=11;
+----+-------------+-------------------+------------+-------+---------------+---------+---------+-------+------+----------+-------+
| id | select_type | table             | partitions | type  | possible_keys | key     | key_len | ref   | rows | filtered | Extra |
+----+-------------+-------------------+------------+-------+---------------+---------+---------+-------+------+----------+-------+
|  1 | SIMPLE      | t_user_action_log | NULL       | const | PRIMARY       | PRIMARY | 8       | const |    1 |   100.00 | NULL  |
+----+-------------+-------------------+------------+-------+---------------+---------+---------+-------+------+----------+-------+
1 row in set, 2 warnings (0.00 sec)

mysql> describe extended SELECT id, name, ip_address, `action`, create_time FROM t_user_action_log where id=11;
+----+-------------+-------------------+------------+-------+---------------+---------+---------+-------+------+----------+-------+
| id | select_type | table             | partitions | type  | possible_keys | key     | key_len | ref   | rows | filtered | Extra |
+----+-------------+-------------------+------------+-------+---------------+---------+---------+-------+------+----------+-------+
|  1 | SIMPLE      | t_user_action_log | NULL       | const | PRIMARY       | PRIMARY | 8       | const |    1 |   100.00 | NULL  |
+----+-------------+-------------------+------------+-------+---------------+---------+---------+-------+------+----------+-------+
1 row in set, 2 warnings (0.00 sec)
```

1. id ：id是select标识符，查询的序列号。
2. select_type ：select_type表示查询语句的类型。例如`SIMPLE`表示不包括连接查询和子查询的的简单查询。
3. table : table表示查询的表。
4. type: 表示连接的类型
5. possible_keys：表示可能使用到的索引。
6. rows：表示进行查询需要检查的行数。
7. Extra：表示进行查询的详细信息。

### 索引的使用

之前在[MySQL索引与查询优化](https://github.com/ijiangtao/blog/blob/master/techblog/db/mysql/MySQLIndex.md)一文中详细讲解了使用索引的优点和注意事项。这里再补充几个注意点。

1. like查询使用索引

如果在like语句中，匹配字符串的第一个字符是%不会走索引，只有%不在第一个位置索引才会起作用。

因此对于MySQL中的字符串，建议使用统一的前缀而不是后缀。

```sql
mysql> explain SELECT id, ip_address FROM t_user_action_log where ip_address like '7%';
+----+-------------+-------------------+------------+-------+----------------+----------------+---------+------+------+----------+-------------+
| id | select_type | table             | partitions | type  | possible_keys  | key            | key_len | ref  | rows | filtered | Extra       |
+----+-------------+-------------------+------------+-------+----------------+----------------+---------+------+------+----------+-------------+
|  1 | SIMPLE      | t_user_action_log | NULL       | range | ip_address_idx | ip_address_idx | 51      | NULL |    2 |   100.00 | Using where |
+----+-------------+-------------------+------------+-------+----------------+----------------+---------+------+------+----------+-------------+
1 row in set, 1 warning (0.00 sec)

mysql> explain SELECT id, ip_address FROM t_user_action_log where ip_address like '%0';
+----+-------------+-------------------+------------+------+---------------+------+---------+------+------+----------+-------------+
| id | select_type | table             | partitions | type | possible_keys | key  | key_len | ref  | rows | filtered | Extra       |
+----+-------------+-------------------+------------+------+---------------+------+---------+------+------+----------+-------------+
|  1 | SIMPLE      | t_user_action_log | NULL       | ALL  | NULL          | NULL | NULL    | NULL |   41 |    11.11 | Using where |
+----+-------------+-------------------+------------+------+---------------+------+---------+------+------+----------+-------------+
1 row in set, 1 warning (0.00 sec)
```

2. or关键字查询语句

如果查询条件中使用了or关键字，那么只有or前后的条件都加了索引，索引才会生效。

3. 优化子查询

MySQL通过子查询实现了嵌套查询，即一个查询的结果可以作为另一个查询的条件。子查询可以让一条SQL语句实现逻辑上需要多个步骤才能完成的SQL条件。

子查询虽然很灵活，但是执行效率不高。原因是子查询需要为内层的查询建立一个临时表，然后外层查询再从临时表中查询结果。查询完毕以后，再撤销这张临时表。

在MySQL中可以通过JOIN查询来代替子查询。因为连接查询不需要建立临时表，而且如果查询中使用索引的话，效率将会更高。


## 优化数据库结构

一个优秀的数据库结构设计，不仅可以让数据库占用更小的磁盘空间，而且能够使查询速度更快。

数据库结构的设计要考虑：
- 数据冗余
- 查询和更新速度
- 字段的数据类型
- 等等……

下面提供几个数据库结构设计的优化策略。

### 将字段很多的表拆成多张表

一个字段很多的表，其中很多字段的使用频率很低，因为这些不常用的字段会降低数据库的查询和更新速度，所以可以考虑将这些字段分离出来形成新的表。

例如商品表，可以将商品不常用的相关属性和分类信息，独立成其他的表。这样在查询商品的主要信息的时候，只需要查询必要的字段即可。如果需要商品的详细信息，可以使用连接查询，将商品的详细信息汇总在一起返回。

### 增加中间表

通常我们设计一张表，是基于某种逻辑与业务上的隔离原则进行的。例如用户表里面是用户的信息，订单表是用户的交易信息，商品表中是商品的信息，促销表是商品可以参与的打折和优惠活动的信息。

但有时候我们需要经常将一些表的信息连接起来查询，这个时候，为了提高查询效率，可以将这些经常需要连接查询的字段组成一张新的中间表，每次查询只需要查一张表，从而提高查询效率。

但需要注意的是，当更新主表的时候，中间表必须同时更新，即两个动作必须在一个事务里。

### 增加冗余字段

在设计数据库表时应该尽量遵循范式理论的规约，尽可能减少冗余字段，让数据库的设计更加精简。

但是，合理的增加冗余字段，可以提高查询速度。

比如表的规范化程度越高，表与表之间需要连接查询的情况就越多，因此合理地增加冗余字段，可以减少连接查询，提高查询速度。

跟增加中间表一样，冗余字段是为了减少连接查询，同样也需要注意数据库记录一致性的问题。

## 优化插入记录的速度

在插入数据的时候，影响插入速度的主要是索引、唯一性校验、一次插入的条数等因素。

基于这几个维度，下面提供几个优化策略。

### MyISAM引擎的表

1. 禁用索引

对于MyISAM引擎的非空表，在插入数据的时候，MySQL会根据表的索引对插入的数据建立索引，如果插入大量数据会降低插入的效率。

因此可以在插入记录前关闭索引，在插入结束以后再建立索引。

- 禁用索引：
```sql
alter table t_user_action_log_oneline disable keys;
```

- 开启索引：
```sql
alter table t_user_action_log_oneline enable keys;
```


2. 禁用唯一性检查

插入数据的时候MySQL会进行唯一性检查，降低插入的速度，因此可以在数据保证唯一性的前提下，在插入之前关闭唯一性检查，插入以后再打开唯一性检查。

- 禁用唯一性检查：
```sql
set unique_checks=0;
```

- 开启唯一性检查：
```sql
set unique_checks=1;
```

3. 使用批量插入

使用一条insert语句插入多条记录，比使用多条插入语句插入多条记录效率更高。

4. 使用load data infile

load data infile可以更加高效地实现数据的导入。

原始数据可以手动写入，可以通过 outfile 语句导出，但是使用outfile语句要注意，可能出现如下错误：
```sql
mysql> select * from t_user_action_log into outfile "/data/mysql/t_user_action_log.sql";
ERROR 1290 (HY000): The MySQL server is running with the --secure-file-priv option so it cannot execute this statement
```

这个时候要找到secure-file-priv指定的目录进行导出：
```sql
mysql> show global variables like '%secure%';
+--------------------------+------------------------------------------------+
| Variable_name            | Value                                          |
+--------------------------+------------------------------------------------+
| require_secure_transport | OFF                                            |
| secure_auth              | ON                                             |
| secure_file_priv         | C:\ProgramData\MySQL\MySQL Server 5.7\Uploads\ |
+--------------------------+------------------------------------------------+
3 rows in set, 1 warning (0.01 sec)
```

指定导出的数据使用逗号分隔结果：
```sql
select * from t_user_action_log into outfile "C:/ProgramData/MySQL/MySQL Server 5.7/Uploads/t_user_action_log.sql" fields terminated by ',';
```

t_user_action_log.sql文件的内容如下：
```
50,LiSi,9.8.8.2,0,2019-06-30 20:46:21
51,LiSi,7.8.8.2,5,2019-06-30 11:56:43
```

使用load data infile进行批量插入数据：
```sql
load data infile "C:/ProgramData/MySQL/MySQL Server 5.7/Uploads/t_user_action_log.sql" into table t_user_action_log fields terminated by ',';
```


### InnoDB引擎的表

1. 禁用唯一性检查

这个和前面MyISAM引擎表一样。

2. 禁用外键检查

插入之前关闭外键检查：
```sql
set foreign_key_checks=0;
```

插入以后开启外键检查：
```sql
set foreign_key_checks=1;
```

3. 禁用自动提交

插入之前关闭自动提交：
```sql
set autocommit=0;
```

插入以后开启自动提交：
```sql
set autocommit=1;
```

## 分析、检查和优化表

1．分析表

MySQL中使用`ANALYZE TABLE`语句来分析表，该语句的基本语法如下：
`ANALYZE TABLE 表名1 [,表名2…] ;`

使用`ANALYZE TABLE`分析表的过程中，数据库系统会对表加一个只读锁。在分析期间，只能读取表中的记录，不能更新和插入记录。

`ANALYZE TABLE`语句能够分析 InnoDB 和 MyISAM 类型的表。

```sql
mysql> analyze table t_user_action_log;
+--------------------------------------------+---------+----------+----------+
| Table                                      | Op      | Msg_type | Msg_text |
+--------------------------------------------+---------+----------+----------+
| ijiangtao_local_db_mysql.t_user_action_log | analyze | status   | OK       |
+--------------------------------------------+---------+----------+----------+
1 row in set (0.02 sec)
```

- Table：表示表的名称；
- Op：表示执行的操作。analyze表示进行分析操作。check表示进行检查查找。optimize表示进行优化操作；
- Msg_type：表示信息类型，其显示的值通常是状态、警告、错误和信息这四者之一；
- Msg_text：显示信息。

2．检查表

MySQL中使用CHECK TABLE语句来检查表。CHECK TABLE语句能够检查InnoDB和MyISAM类型的表是否存在错误。而且该语句还可以检查视图是否存在错误。

该语句的基本语法如下：
`CHECK TABLE 表名1 [,表名2…] [option] ;`

其中，option参数有5个参数，分别是QUICK、FAST、CHANGED、MEDIUM和EXTENDED。这5个参数的执行效率依次降低。

option选项只对MyISAM类型的表有效，对InnoDB类型的表无效。CHECK TABLE语句在执行过程中也会给表加上只读锁。

```sql
mysql> check table t_user_action_log;
+--------------------------------------------+-------+----------+----------+
| Table                                      | Op    | Msg_type | Msg_text |
+--------------------------------------------+-------+----------+----------+
| ijiangtao_local_db_mysql.t_user_action_log | check | status   | OK       |
+--------------------------------------------+-------+----------+----------+
1 row in set (0.01 sec)
```

3．优化表

MySQL中使用OPTIMIZE TABLE语句来优化表。该语句对InnoDB和MyISAM类型的表都有效。但是，OPTILMIZE TABLE语句只能优化表中的VARCHAR、BLOB或TEXT类型的字段。

OPTILMIZE TABLE语句的基本语法如下：
`OPTIMIZE TABLE 表名1 [,表名2…] ;`

通过OPTIMIZE TABLE语句可以消除删除和更新造成的磁盘碎片，从而减少空间的浪费。OPTIMIZE TABLE语句在执行过程中也会给表加上只读锁。

如果一个表使用了TEXT或者BLOB这样的数据类型，那么更新、删除等操作就会造成磁盘空间的浪费。因为，更新和删除操作后，以前分配的磁盘空间不会自动收回。使用OPTIMIZE TABLE语句就可以将这些磁盘碎片整理出来，以便以后再利用。

优化表有很多方式实现： OPTIMIZE TABLE语句、mysqlcheck工具（服务器要运行）或myisamchk（服务器没有运行或表中没有交互）

随着MySQL的使用，包括BLOB和VARCHAR字节的表将变得比较繁冗，因为这些字段长度不同，对记录进行插入、更新或删除时，会占有不同大小的空间，记录就会变成碎片，且留下空闲的空间。像具有碎片的磁盘，会降低性能，需要整理，因此要优化。

```sql
mysql> optimize table t_user_action_log;
+--------------------------------------------+----------+----------+-------------------------------------------------------------------+
| Table                                      | Op       | Msg_type | Msg_text                                                          |
+--------------------------------------------+----------+----------+-------------------------------------------------------------------+
| ijiangtao_local_db_mysql.t_user_action_log | optimize | note     | Table does not support optimize, doing recreate + analyze instead |
| ijiangtao_local_db_mysql.t_user_action_log | optimize | status   | OK                                                                |
+--------------------------------------------+----------+----------+-------------------------------------------------------------------+
2 rows in set (0.11 sec)
```

## MySQL服务器优化

优化MySQL服务器性能，主要从以下几个方面进行考虑：

1. 配置足够大的内存
2. 配置高度磁盘系统，以减少读盘等待时间
3. 合理分配磁盘I/O，把磁盘I/O分散在多个设备上，以减少资源竞争，提高并行操作能力。
4. 配置多处理器，MySQL是多线程数据库，多处理器可以同时处理多个线程。
5. 优化MySQL参数，例如通过key_buffer_size参数配置索引缓冲区的大小。


## 总结

本文从多个方面介绍了使用MySQL数据库的优化方案，但具体实践还需要对每个优化方案的利弊进行深入了解，并结合具体情况分析，从而设计出适合自己的最优方案。


## 相关文章

- [位运算与SQL实现](https://juejin.im/post/5c7a46dff265da2d84109e2b)
- [MySQL索引与查询优化](https://juejin.im/post/5cb1dec9f265da0382610968)
- [Windows操作系统安装MySQL解压版](https://juejin.im/post/5c878687f265da2db414606e)
- [MySQL 主键自增 Auto Increment用法](https://juejin.im/post/5c99e5a8e51d45650678ac7a)
- [MySQL数据库存储引擎简介](https://juejin.im/post/5c8785baf265da2dd2190707)

------

![Wechat-westcall](https://ipictures.github.io/category/writing/wechat-westcall/westcall-1.png)
