### SQL 基础

1. distinct 用于去重，可以用在 * 符号后。如果域中有 NULL，同样会显示一个 NULL。

2. MySQL 既接受双引号也接受单引号，并且 <> 等价于 !=。

3. where 子句中可以使用小括号。

4. order by 用来对结果排序，后面可以指定多个域作为排序标准，分别用逗号隔开。默认为 asc，可以指定 desc。如果域中有 NULL，按升序排列时 NULL 在前面，反之在后面。

5. insert into tbl_name values(...);    insert into tbl_name (col1, col2, ...) values (val1, val2, ...);

6. 使用 update 时，如果有多列满足条件，那么它们都会被修改。

7. delete [*] from tbl_name; 可以删除表中所有数据，并且保留了表结构。

8. top 子句的功能由 limit 实现，在语句最后使用 limit n 来限制返回的结果数量。

9. where 子句中使用 [not] like 来表示模式匹配。% 表示匹配任意个字符，如果开头和结尾没有 % 符号，则表示开头或结尾就是指定的字符。_ 表示一个任意字符，\ 可以用来转义，或者在最后用 escape '/' 并且在特殊字符前加 /。

10. 使用 [not] regexp 或者 [not] rlike 表示用正则表达式进行匹配。

11. MySQL 默认是不区分大小写的，如果要区分，就使用 binary [r]like。

12. [not] in (val1, ...); 可以用在 where 中查找在值在列表中的记录。

13. [not] between val1 and val2; MySQL 是闭区间获取，即 val1 和 val2 也会被返回。应注意：返回的结果在 val1 和 val2 之间并不仅只比较第一个字符，而是二者的所有字符。

14. 使用别名只要在相应的表名或列名后面添加 as new_name 即可。

### join

1. join 默认为 inner join，语法为：
select tb1.col1, ..., tbl2.col1 from tb1 join tb2 on tb1.colN = tb2.colN;
内连接要求至少有一个匹配时才返回行。

2. left/right join 表示即使没有匹配的的数据，也会返回左/右表中的数据，不存在的字段数据为 NULL。

3. MySQL 本身不支持 full join 的语法。不过可以通过 left join 和 right join 各一次然后 union 来实现 full join的功能。

4. union 默认去掉重复数据，若不去重则使用 union all。union [all] 要求两边的 select 语句必须返回相同的列数且对应列的数据类型相同。

5. MySQL 不支持 select into 语法，可以通过 create table tbl_name(select...); 实现。

### 常用约束

* NOT NULL

* UNIQUE

* PRIMARY KEY

* FOREIGN KEY

* CHECK

* DEFAULT

1. 建表时，多个约束之间不实用逗号分隔。可以直接在字段后面添加 unique，也可以在一个新行里使用 unique(col1, col2, ...)。

2. 对于已经建立的表增加 unique 约束，使用 alter table tbl_name add unique(col); 添加 unique 约束时可以指定约束名，若无指定会自动生成一个（可以通过 show create table tbl_name; 查看）。unique 约束默认在该列上创建索引，要删除 unique 约束需要执行：alter table tbl_name drop index 约束名;

3. 增加主键的语法和 unique 类似，删除主键只需：alter table tbl_name drop primary key;

4. 创建 foreign key 的语法：alter table tbl1 add foreign key(col) references tbl2(col); 相比之前的约束多了 references 关键字。同样可以为外键命名，以上约束（除主键外）命名前需要添加 constraint 关键字。

5. MySQL 不支持 check 的功能，但是可以编译通过，只是没有效果。如果要实现 check 的功能，应该使用触发器来替代。

6. 设置 default 的语法为：alter table tbl_name alter col set default val; 删除的语法为：alter table tbl_name alter col drop default;

### 索引

1. create index idx_name on tbl_name(col1, col2, ...);

2. drop index inx_name on tbl_name; 或 alter table tbl_name drop index idx_name;

### 修改表

1. 修改数据类型的两种方式：

* alter table tbl_name change col_name new_col_name col_type constraint_name;

* alter table tbl_name modify col_name col_type constraint_name;

后者不能修改列名。

2. alter table tb1 add col_name type;   alter table tb1 drop col_name;

3. drop table tbl_name; drop database db_name;

4. 删除表中所有数据：truncate table tbl_name;

### auto_increment 字段

1. 自增字段必须创建在 key 域上。

2. 可以创建自增字段：auto_increment[=start_val]。添加数据时可以不为自增字段指定值。

### having

1. 使用 having 的原因在于 where 无法和聚合函数一同使用。

2. having 可以和 group by 结合使用。

### 锁机制

#### 悲观锁

1. 数据库提供的锁，使用 select ... for update。

2. 针对主键或者创建索引的字段进行 for update 查询，使用 row lock（前提是查找到数据，否则不上锁）。对于其它类型字段或者区间查询（即使是主键或索引字段）使用 table lock。

3. 缺点：对于长事务或者其它长时间加锁情形，会降低程序的并发性。

#### 乐观锁

1. 是一种人工的加锁方式，在表中添加一个用于版本对照的字段（或者是时间戳），每次用户执行第二次 update 之前会再次查询该数据，如果版本号未变（或者时间戳相同），那么可以执行该 update 操作，否则返回错误。

### 为什么使用视图

1. 封装查询（避免数据冗余）

2. 灵活的安全性控制（针对不同的视图设置不同的权限）

### 触发器

    create trigger tgr_name
    before|after
    insert|update|delete
    on tbl_name
    for each row
    begin
       sql clause
    end;

### 存储过程

