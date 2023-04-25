# 11.1 数值类型

MySQL支持所有标准的SQL数值类型，这些类型包括精确的数值类型（INTEGER、SMALLINT、DECIMAL 和 NUMERIC），也包括近似（非精确）的数值类型（FLOAT、REAL 和 DOUBLE PRECISION）。INT是INTEGER的同义词，而DEC和FIXED是DECIMAL的同义词。MySQL将DOUBLE视为DOUBLE PRECISION的同义词（非标准扩展）。同时，MySQL也将REAL视为DOUBLE PRECISION的同义词（非标准变体），除非SQL启用了REAL_AS_FLOAT模式。 

BIT类型存储比特值，并支持MyISAM、MEMORY、InnoDB和NDB表。  

对于MySQL如何将超出范围的赋值给列和表达式求值期间溢出处理的有关信息，请看[“11.1.7 超出范围和溢出处理”](#)。 

对于数值类型存储要求的有关信息，请看[“11.7 数据类型存储要求”](#)。  

对于数值运算函数的相关描述，请看[“12.6 数值函数和运算符”](#)。对于数值操作数计算之后结果所使用的数据类型，取决于操作数的类型和对它们执行的操作。更多信息请看[“12.6.1 算术运算符”](#)  

上一节 << [ch11 数据类型](../Data%20Types.md)  
下一节 >> [11.1.1 数值类型语法](./01/Numeric%20Data%20Type%20Syntax.md)