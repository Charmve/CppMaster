# 1.★★☆ 手写 SQL 语句，特别是连接查询与分组查询

复习sql

# 2.★★☆ 连接查询与子查询的比较

**连接查询**是将两个或多个的表按某个条件连接起来，从中选取需要的数据，连接查询是同时查询两个或两个以上的表的使用的。当不同的表中存在相同意义的字段时，可以通过该字段来连接这几个表。

SQL 的四种连接查询

内连接
inner join 或者 join

外连接
1. 左连接 left join 或者 left outer join

2. 右连接 right join 或者 right outer join

3. 完全外连接 full join 或者 full outer join

**子查询**是将一个查询语句嵌套在另外一个查询语句中，内层查询语句的查询结果，可以为外层查询语句提供查询条件。


# 3.★★☆ drop、delete、truncate 比较

## I.作用
DELETE 删除表中 WHERE 语句指定的数据。

<div align="center"> <img src="https://diycode.b0.upaiyun.com/photo/2019/f2cdb010e07c176688bc5bae2bbd41be.png" width=""/> </div><br>

TRUNCATE 清空表，相当于删除表中的所有数据。

<div align="center"> <img src="https://diycode.b0.upaiyun.com/photo/2019/c3983ada399b68d5b5854729aa28299b.png" width=""/> </div><br>

DROP 删除表结构。

<div align="center"> <img src="https://diycode.b0.upaiyun.com/photo/2019/78c1ca2a5baf04f6ebf2509dec863904.png" width=""/> </div><br>

## II.事务

- DELETE 会被放到日志中以便进行回滚；  
- TRUNCATE 和 DROP 立即生效，不会放到日志中，也就不支持回滚。

## III.删除空间

- DELETE 不会减少表和索引占用的空间；
- TRUNCATE 会将表和索引占用的空间恢复到初始值；
- DROP 会将表和索引占用的空间释放。

## IV.耗时

通常来说，DELETE < TRUNCATE < DROP。

# 4.★★☆ 视图的作用，以及何时能更新视图

视图是虚拟的表，本身不包含数据，也就不能对其进行索引操作。

对视图的操作和对普通表的操作一样。

视图具有如下好处：

- 简化复杂的 SQL 操作，比如复杂的连接；
- 只使用实际表的一部分数据；
- 通过只给用户访问视图的权限，保证数据的安全性；
- 更改数据格式和表示。

```sql
CREATE VIEW myview AS
SELECT Concat(col1, col2) AS concat_col, col3*col4 AS compute_col
FROM mytable
WHERE col5 = val;
```

# 5.★☆☆ 理解存储过程、触发器等作用

**存储过程**可以看成是对一系列 SQL 操作的批处理。

使用存储过程的好处：

- 代码封装，保证了一定的安全性；
- 代码复用；
- 由于是预先编译，因此具有很高的性能。

命令行中创建存储过程需要自定义分隔符，因为命令行是以 ; 为结束符，而存储过程中也包含了分号，因此会错误把这部分分号当成是结束符，造成语法错误。

包含 in、out 和 inout 三种参数。

给变量赋值都需要用 select into 语句。

每次只能给一个变量赋值，不支持集合的操作。

```sql
delimiter //

create procedure myprocedure( out ret int )
    begin
        declare y int;
        select sum(col1)
        from mytable
        into y;
        select y*y into ret;
    end //

delimiter ;
```

```sql
call myprocedure(@ret);
select @ret;
```

**触发器**会在某个表执行以下语句时而自动执行：DELETE、INSERT、UPDATE。

触发器必须指定在语句执行之前还是之后自动执行，之前执行使用 BEFORE 关键字，之后执行使用 AFTER 关键字。BEFORE 用于数据验证和净化，AFTER 用于审计跟踪，将修改记录到另外一张表中。

INSERT 触发器包含一个名为 NEW 的虚拟表。

```sql
CREATE TRIGGER mytrigger AFTER INSERT ON mytable
FOR EACH ROW SELECT NEW.col into @result;

SELECT @result; -- 获取结果
```

DELETE 触发器包含一个名为 OLD 的虚拟表，并且是只读的。

UPDATE 触发器包含一个名为 NEW 和一个名为 OLD 的虚拟表，其中 NEW 是可以被修改的，而 OLD 是只读的。

MySQL 不允许在触发器中使用 CALL 语句，也就是不能调用存储过程。

