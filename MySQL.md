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

4. union 默认去掉重复数据，若不去重则使用 union all。

5. 
