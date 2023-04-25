# 11.1.1 数值类型语法  

对于整数类型，***M*** 表示最大显示宽度。最大显示宽度为255。显示宽度与类型可以存储的值的范围无关，正如[“11.1.6 数值类型属性”](#)中所述。  

对于浮点数和定点数类型，***M*** 表示可以存储的总位数。  

从MySQL 8.0.17版本开始，不推荐在整数类型中使用显示宽度属性，并且在未来版本中将移除对它的支持。

如果你为数值列指定了ZEROFILL属性，MySQL会自动给该列添加UNSIGNED属性。

从MySQL 8.0.17版本开始，不推荐在数值类型中ZEROFILL属性，并且在未来版本中将移除对它的支持。可以考虑使用替代方案来产生相同属性效果。例如，应用程序可以使用LPAD()函数将数字用零填充到所需宽度，或者将格式化的数字存储到CHAR类型列中。

允许使用UNSIGNED属性的数值类型也允许使用SIGNED属性，默认就是SIGNED。因此，显式地设置SIGNED没有任何影响。

从MySQL 8.0.17版本开始，不推荐在FLOAT、DOUBLE和DECIMAL（包括它们的同义词）中UNSIGNED属性，并且在未来版本中将移除对它的支持。在这些字段中，可以考虑使用简单的CHECK约束来代替该属性。

SERIAL是BIGINT UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE的别名。

在整型字段定义中，SERIAL DEFAULT VALUE是NOT NULL AUTO_INCREMENT UNIQUE的别名。

> Warning！  
> 当你使用整数值之间的减法运算时，若其中一个值是UNSIGNED类型，则结果无符号的，除非SQL启用了NO_UNSIGNED_SUBTRACTION模式。详情请看[“12.11 转换函数和运算符”](#)。  

-   BIT[ (***M***) ]  
位值类型。***M*** 表示每个值的二进制位数，从1到64。如果省略 ***M***，则默认为1。

-   TINYINT[ (***M***) ] [UNSIGNED] [ZEROFILL]  
数值非常小的整数类型。有符号数值的范围是$-128$到$127$，无符号数值的范围是$0$到$255$。

-   BOOL, BOOLEAN  
该类型是TINYINT(1)的同义词。零值被认为是false，非零值被认为是true：
```mysql
 mysql> SELECT IF(0, 'true', 'false')  
 +------------------------+  
 | IF(0, 'true', 'false') |  
 +------------------------+  
 | false                  |  
 +------------------------+  
 mysql> SELECT IF(0, 'true', 'false')  
 +------------------------+  
 | IF(1, 'true', 'false') |  
 +------------------------+  
 | true                   |  
 +------------------------+  
 mysql> SELECT IF(0, 'true', 'false')  
 +------------------------+  
 | IF(2, 'true', 'false') |  
 +------------------------+  
 | true                   |  
 +------------------------+  
```
然而，TRUE和FALSE分别只是数值0和1的别名，如下所示：
```mysql
 mysql> SELECT IF(0 = FALSE, 'true', 'false')  
 +--------------------------------+  
 | IF(0 = FALSE, 'true', 'false') |  
 +--------------------------------+  
 | true                           |  
 +--------------------------------+  
 mysql> SELECT IF(1 = TRUE, 'true', 'false')  
 +-------------------------------+  
 | IF(1 = TRUE, 'true', 'false') |  
 +-------------------------------+  
 | true                          |  
 +-------------------------------+  
 mysql> SELECT IF(2 = TRUE, 'true', 'false')  
 +-------------------------------+  
 | IF(2 = TRUE, 'true', 'false') |  
 +-------------------------------+  
 | false                         |  
 +-------------------------------+  
  mysql> SELECT IF(2 = FALSE, 'true', 'false')  
 +--------------------------------+  
 | IF(2 = FALSE, 'true', 'false') |  
 +--------------------------------+  
 | false                          |  
 +--------------------------------+ 
```  
最后两条语句显示了所示的结果，是因为2即不等于1也不等于0。  

-   SAMLLINT[ (***M***) ] [UNSIGNED] [ZEROFILL]  
数值较小的整数类型。有符号数值的范围是$-32768$到$32767$，无符号数值的范围是$0$到$65535$。  

-   MEDIUMINT[ (***M***) ] [UNSIGNED] [ZEROFILL]  
中等数值大小的整数类型。有符号数值的范围是$-8388608$到$8388607$，无符号数值的范围是$0$到$16777215$。  

-   INT[ (***M***) ] [UNSIGNED] [ZEROFILL]  
正常数值大小的整数类型。有符号数值的范围是$-2147483648$到$2147483647$，无符号数值的范围是$0$到$4294967295$。  

-   INTEGER[ (***M***) ] [UNSIGNED] [ZEROFILL]  
该类型是INT的同义词。

-   BIGINT[ (***M***) ] [UNSIGNED] [ZEROFILL]  
数值非常大的整数类型。有符号数值的范围是$-9223372036854775808$到$9223372036854775807$，无符号数值的范围是$0$到$18446744073709551615$。  
SERIAL是BIGINT UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE的别名。  
在使用BIGINT字段时，有一些需要注意的事项：  
    -   所有算术运算都使用有符号的BIGINT或DOUBLE值来完成运算，因此除非位函数，否则不应该使用值大于9223372036854775807（63位）的无符号大整数。如果这样做，由于将BIGINT值转换为DOUBLE类型时存在舍入误差，会导致结果中最后几位可能是错误的。  
    MySQL可以处理以下情形的BIGINT类型：  
        -   在BIGINT字段中使用整数来存储大的无符号数值时。
        -   在MIN(*col_name*)或MAX(*col_name*)中，其中 ***col_name*** 指向BIGINT字段时。
        -   在使用操作符（+、-、*等）且两个操作数都是整数时。
    -   你总是可以在存储到BIGINT类型字段中时，通过使用字符串来存储确切的数值。在这种情况下，MySQL会执行字符串到数字的转换，中间不涉及任何双精度表示。  
    -   当两个操作数都是整数时，+、-和*运算符会使用BIGINT算术运算。这意味着，当两个大整数（或由函数返回的整数结果）的乘积大于9223372036854775807时，你可能会得到意想不到的结果。  

-   DECIMAL[ (***M***[, ***D***]) ] [UNSIGNED] [ZEROFILL]  
“精确”的定点数类型。***M*** 表示数字总位数（精度），***D*** 表示小数点后的位数（标度），其中小数点和负号（对于负数）不计入 ***M*** 值。如果 ***D*** 为0，则数值没有小数点或小数部分。DECIMAL支持的 ***M*** 最大为65，***D*** 最大为30。如果省略 ***D***，则默认为0；如果省略 ***M***，则默认为10。（DECIMAL类型字面值的文本长度是有限制的，详情请看[“12.25.3 表达式处理”](#)。  
如果指定了UNSIGNED，则不允许出现负值。从MySQL 8.0.17版本开始，不推荐在DECIMAL（包括同义词）中使用UNSIGNED属性，并且在未来版本中将移除对它的支持。在这些字段中，可以考虑使用简单的CHECK约束来代替该属性。  
所有使用DECIMAL字段进行的基本运算（+、-、*、/），其精度均为65位。  

-   DEC[ (***M***[, ***D***]) ] [UNSIGNED] [ZEROFILL],  NUMERIC[ (***M***[, ***D***]) ] [UNSIGNED] [ZEROFILL],  FIXED[ (***M***[, ***D***]) ] [UNSIGNED] [ZEROFILL]  
这些类型都是DECIMAL的同义词。FIXED是为了与其他数据库系统兼容而提供的。  

-   FLOAT[ (***M***, ***D***) ] [UNSIGNED] [ZEROFILL]  
数值较小的（单精度）浮点数类型。允许值的范围是$-3.402823466E{+38}$到$-1.175494351E{-38}$, $0$ 和 $1.175494351E{-38}$到$3.402823466E{+38}$。这些是基于IEEE标准的理论极限，实际范围可能会稍小一些，具体取决于你的硬件或操作系统。  
其中，***M*** 是总位数，***D*** 是小数点后的位数。如果省略 ***D*** 和 ***M*** ，则可以存储的值受到硬件允许的限制。单精度浮点数精确到小数点后7位左右。
FLOAT(***M***, ***D***)是MySQL的非标准扩展。从MySQL 8.0.17版本开始，不推荐使用该语法，并且在未来版本中将移除对它的支持。  
如果指定了UNSIGNED，则不允许出现负值。从MySQL 8.0.17版本开始，不推荐在FLOAT（包括同义词）中使用UNSIGNED属性，并且在未来版本中将移除对它的支持。在这些字段中，可以考虑使用简单的CHECK约束来代替该属性。  
在MySQL中，所有的计算都是使用双精度来完成的，因此使用FLOAT类型可能会导致一些意想不到的问题。详情请看[“附录B.3.4.7 解决找不到匹配行的问题”]。  

-   FLOAT(***p***) [UNSIGNED] [ZEROFILL]  
浮点数类型。***P*** 表示精度（以比特为单位），但MySQL仅使用此值来确定使用FLOAT还是DOUBLE类型。如果 ***p*** 介于0到24之间，则字段类型是没有 ***M*** 和 ***D*** 参数的FLOAT类型。如果 ***p*** 介于25到53之间，则字段类型是没有 ***M*** 和 ***D*** 参数的DOUBLE类型。上述所得字段值的范围与本章节中讲述的FLOAT单精度浮点类型和DOUBLE双精度浮点类型值的范围相同。  
如果指定了UNSIGNED，则不允许出现负值。从MySQL 8.0.17版本开始，不推荐在FLOAT（包括同义词）中使用UNSIGNED属性，并且在未来版本中将移除对它的支持。在这些字段中，可以考虑使用简单的CHECK约束来代替该属性。  
FLOAT(***p***) 是为了兼容ODBC而提供的。  

-   DOUBLE[ (***M***, ***D***) ] [UNSIGNED] [ZEROFILL]  
正常数值大小的（双精度）浮点数类型。允许值的范围是$-1.7976931348623157E{+308}$到$-2.2250738585072014E{-308}$, $0$ 和 $2.2250738585072014E{-308}$到$1.7976931348623157E{+308}$。这些是基于IEEE标准的理论极限，实际范围可能会稍小一些，具体取决于你的硬件或操作系统。  
其中，***M*** 是总位数，***D*** 是小数点后的位数。如果省略 ***D*** 和 ***M*** ，则可以存储的值受到硬件允许的限制。双精度浮点数精确到小数点后15位左右。  
DOUBLE(***M***, ***D***)是MySQL的非标准扩展。从MySQL 8.0.17版本开始，不推荐使用该语法，并且在未来版本中将移除对它的支持。  
如果指定了UNSIGNED，则不允许出现负值。从MySQL 8.0.17版本开始，不推荐在DOUBLE（包括同义词）中使用UNSIGNED属性，并且在未来版本中将移除对它的支持。在这些字段中，可以考虑使用简单的CHECK约束来代替该属性。

-   DOUBLE PRECISION[ (***M***, ***D***) ] [UNSIGNED] [ZEROFILL],  REAL[ (***M***, ***D***) ] [UNSIGNED] [ZEROFILL]  
这些类型都是DOUBLE的同义词。特殊情况：如果SQL启用了REAL_AS_FLOAT模式，则REAL是FLOAT的同义词，而不是DOUBLE的。  

上一节 << [11.1 数值类型](../Numeric%20Data%20Types.md)  
下一节 >> [11.1.2 整形](../02/Integer%20Types.md)