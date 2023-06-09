# 11.2 日期和时间类型  

用于表示时间的日期和时间类型包括DATE、TIME、DATETIME、TIMESTAMP和YEAR。每种时间类型都有一定范围的有效值，以及一个“零”值。当你指定了MySQL无法表示的无效值时，将会使用“零”值。TIMESTAMP和DATETIME类型具有特殊的自动更新行为，详请请看[“11.2.5 TIMESTAMP和DATETIME的自动初始化和更新”](#)。  

有关日期和时间类型的存储需求的信息，请看[“11.7 数据类型存储要求”](#)。  

有关操作时间值的函数的描述，请看[“12.7 日期和时间函数”](#)。  

在处理日期和时间类型时，请牢记以下常见的考虑事项：  

-   MySQL以标准输出格式检索给定日期或时间类型的值，但它会尝试解释你提供的各种输入值的格式（例如，当你指定一个值要去分配或与日期或与时间类型进行比较时）。有关日期和时间类型允许的格式的描述，请看[“9.1.3 日期和时间字面值”]()。预期你提供有效的值。如果使用其他格式的值，则可能会出现不可预测的结果。

虽然MySQL尝试以多种格式解释值，但日期部分必须始终按照年-月-日的顺序给出（例如，“98-09-04”），而不是按照其他地方常用的月-日-年或日-月-年的顺序（例如，“09-04-98”，“04-09-98”）。若要将其他顺序的字符串转换为年-月-日的顺序，则可使用STR_TO_DATE()函数。

包含两位数字年份的日期是不明确的，因为世纪是未知的。MySQL使用以下规则解释两位数年份：

在70-99范围内的年份值变为1970-1999。

在00-69范围内的年份值变为2000-2069。

另请参见第11.2.8节“日期中的两位数年份”。

从一种时间类型转换为另一种时间类型的值的转换遵循第11.2.7节“日期和时间类型之间的转换”的规则。

如果值在数字上下文中使用，MySQL会自动将日期或时间值转换为数字，反之亦然。

默认情况下，当MySQL遇到超出范围或其他类型无效的日期或时间类型的值时，它会将该值转换为该类型的“零”值。例外情况是超出范围的时间值会被修剪为时间范围的适当端点。

通过将SQL模式设置为适当的值，可以更精确地指定你想要MySQL支持的日期类型。 （请参见第5.1.11节“服务器SQL模式”。）你可以通过启用ALLOW_INVALID_DATES SQL模式来使MySQL接受特定的日期，

上一节 << [11.1.7 超出范围和溢出处理](../01/07/Out-Of-Range%20and%20Overflow%20Handling.md)
下一节 >> [11.2.1 日期与时间类型语法](./01/Date%20and%20Time%20Data%20Type%20Syntax.md)