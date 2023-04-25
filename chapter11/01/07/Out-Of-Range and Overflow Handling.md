# 11.1.7 超出范围和溢出处理

当MySQL将一个超出类型允许范围的值存储到数值字段中时，其结果取决于当前生效的SQL模式：
-   如果启用了严格SQL模式，MySQL将依据SQL标准拒绝超出范围的值，插入失败。  
-   如果没有启用限制性模式，MySQL将截断到字段类型允许的极限值，并将结果存储下来。

    当将一个超出范围的值分配给整数字段时，MySQL会存储相应类型所允许范围的端点值。  

    当将一个超出指定（或默认）精度和小数位数的值分配给浮点数或定点数字段时，MySQL会存储相应类型所允许范围的端点值。  

假设表t1具有以下定义：
```mysql  
CREATE TABLE t1 (i1 TINYINT, i2 TINYINT UNSIGNED);  
```  

启用严格SQL模式后，会发生超出范围的错误：
```mysql  
mysql> SET sql_mode = 'TRADITIONAL';  
mysql> INSERT INTO t1 (i1, i2) VALUES(256, 256);  
ERROR 1264 (22003): Out of range value for column 'i1' at row 1  
mysql> SELECT * FROM t1;  
Empty set (0.00 sec)  
```  

不启用严格SQL模式后，会发出警告并进行截断：
```mysql  
mysql> SET sql_mode = '';  
mysql> INSERT INTO t1 (i1, i2) VALUES(256, 256);  
mysql> SHOW WARNINGS;  
+---------+------+---------------------------------------------+  
| Level   | Code | Message                                     |  
+---------+------+---------------------------------------------+  
| Warning | 1264 | Out of range value for column 'i1' at row 1 |  
| Warning | 1264 | Out of range value for column 'i2' at row 1 |  
+---------+------+---------------------------------------------+  
mysql> SELECT * FROM t1;  
+------+------+  
| i1   | i2   |  
+------+------+  
|  127 |  255 |  
+------+------+  
```  

当未启用严格SQL模式时，由于截断引起的字段赋值转换将被报告为ALTER TABLE、LOAD DATA、UPDATE和多行INSERT的警告。在严格SQL模式下，这些语句会失败，并且某些或所有的值不会被插入或更改，这取决于表是否是事务表或其他因素。详情请看[“5.1.11 服务器SQL模式”](../../../chapter05/01/11/ServerSqlModes.md)。  

数值表达式求值过程中发生溢出会导致错误。例如，有符号BIGINT类型的最大值是$9223372036854775807$，因此以下表达式会产生一个错误：  
```mysql  
mysql> SELECT 9223372036854775807 + 1;  
ERROR 1690 (22003): BIGINT value is out of range in '(9223372036854775807 + 1)'  
```  

要使该操作能够成功，可以将值转换为无符号类型：  
```mysql  
mysql> SELECT CAST(9223372036854775807 AS UNSIGNED) + 1;  
+-------------------------------------------+  
| CAST(9223372036854775807 AS UNSIGNED) + 1 |  
+-------------------------------------------+  
|                       9223372036854775808 |  
+-------------------------------------------+  
```  

是否发生溢出取决于操作数的范围，因此处理上述表达式的另一种方法是使用精确值算术，因为DECIMAL类型的值比整数值具有更大的范围：  
```mysql  
mysql> SELECT 9223372036854775807.0 + 1;  
+---------------------------+  
| 9223372036854775807.0 + 1 |  
+---------------------------+  
|     9223372036854775808.0 |  
+---------------------------+  
```  

如果一个整数类型的值是UNSIGNED类型，那么它和另一个整数值做减法运算的结果默认为无符号类型。如果运算结果本应为负数，则发生错误：  
```mysql  
mysql> SET sql_mode = '';  
Query OK, 0 rows affected (0.00 sec)  
  
mysql> SELECT CAST(0 AS UNSIGNED) - 1;  
ERROR 1690 (22003): BIGINT UNSIGNED value is out of range in '(cast(0 as unsigned) - 1)'  
```  

如果SQL启用了NO_UNSIGNED_SUBTRACTION模式，则结果为负值：  
```mysql  
mysql> SET sql_mode = 'NO_UNSIGNED_SUBTRACTION';  
mysql> SELECT CAST(0 AS UNSIGNED) - 1;  
+-------------------------+  
| CAST(0 AS UNSIGNED) - 1 |  
+-------------------------+  
|                      -1 |  
+-------------------------+  
```  

如果该操作的结果用于更新一个UNSIGNED整数字段，则结果被截取为该字段类型的最大值，或者如果启用了NO_UNSIGNED_SUBTRACTION模式，则截取为0。如果启用了严格SQL模式，则会发生错误，并且该字段保持不变。  

上一节 << [11.1.6 数值类型属性](../06/Numeric%20Type%20Attributes.md)  
下一节 >> [11.2 日期与时间类型](../../02/Date%20and%20Time%20Data%20Types.md)  