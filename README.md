# MySQL_8.0_Reference_Manual_Chinese
本项目为MySQL 8.0官方参考手册的译作，[官网原文链接.](https://dev.mysql.com/doc/refman/8.0/en/)

项目树形结构说明：

```
.
|   README.md
|
+---chapter01
|   |   xx.md ("./chapter01/xx.md"表示第1章内容)
|   |
|   +---01
|   |   |   xx.md ("./chapter01/01/xx.md"表示第1.1节内容)
|   |   |
|   |   \---01
|   |           xx.md ("./chapter01/01/01/xx.md"表示第1.1.1节内容)
|   |  
|   \---02
|       xx.md ("./chapter01/02/xx.md"表示第1.2节内容)
|
\---chapter02
```

# 目录
-   [第11章：数据类型](./chapter11/Data%20Types.md)  
    -   [11.1：数值类型](./chapter11/01/Numeric%20Data%20Types.md)  
        -   [11.1.1：数值类型语法](./chapter11/01/01/Numeric%20Data%20Type%20Syntax.md)  
        -   [11.1.2：整型（精确值）- INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT](./chapter11/01/02/Integer%20Types.md)
        -   [11.1.3：定点型（精确值）- DECIMAL, NUMERIC](./chapter11/01/03/Fixed-Point%20Types.md)
        -   [11.1.4：浮点型（近似值）- FLOAT, DOUBLE](./chapter11/01/04/Floating-Point%20Types.md)  
        -   [11.1.5：位值型 - BIT](./chapter11/01/05/Bit-Value%20Type.md)  
        -   [11.1.6：数值类型属性](./chapter11/01/06/Numeric%20Type%20Attributes.md)  
        -   [11.1.7：超出范围和溢出处理](./chapter11/01/07/Out-Of-Range%20and%20Overflow%20Handling.md)
    -   [11.2：日期与时间类型](./chapter11/02/Date%20and%20Time%20Data%20Types.md)  
        -   [11.2.1 日期与时间类型语法](./chapter11/02/01/Date%20and%20Time%20Data%20Type%20Syntax.md)  
        -   [11.2.2 DATE, DATETIME与TIMESTAMP类型](./chapter11/02/02/The%20DATE%2C%20DATETIME%2C%20and%20TIMESTAMP%20Types.md)  
        -   [11.2.3 TIME类型](./chapter11/02/03/The%20TIME%20Type.md)  
        -   [11.2.4 YEAR类型](./chapter11/02/04/The%20YEAR%20Type.md)  
        -   [11.2.5 TIMESTAMP与DATETIME的自动初始化和更新](./chapter11/02/05/Automatic%20Initialization%20and%20Updating%20for%20TIMESTAMP%20and%20DATETIME.md)  
        -   [11.2.6 时间值中的小数秒](./chapter11/02/06/Fractional%20Seconds%20in%20Time%20Values.md)  
        -   [11.2.7 日期与时间类型之间转换](./chapter11/02/07/Conversion%20Between%20Date%20and%20Time%20Types.md)  
        -   [11.2.8 日期中的两位数字年份](./chapter11/02/08/2-Digit%20Year%20in%20Dates.md)  
    -   [11.3：字符串类型](./chapter11/03/String%20Data%20Types.md)  
        -   [11.3.1 字符串类型语法](./chapter11/03/01/String%20Data%20Type%20Syntax.md)  
        -   [11.3.2 11.3.2 CHAR与VARCHAR类型](./chapter11/03/02/The%20CHAR%20and%20VARCHAR%20Types.md)  
        -   [11.3.3 BINARY与VARBINARY类型](./chapter11/03/03/The%20BINARY%20and%20VARBINARY%20Types.md)  
        -   [11.3.4 BLOB与TEXT类型](./chapter11/03/04/The%20BLOB%20and%20TEXT%20Types.md)  
        -   [11.3.5 ENUM类型](./chapter11/03/05/The%20ENUM%20Type.md)  
        -   [11.3.6 SET类型](./chapter11/03/06/The%20SET%20Type.md)  
    -   [11.4：空间类型](./chapter11/04/Spatial%20Data%20Types.md)  
        -   [11.4.1 空间类型](./chapter11/04/01/Spatial%20Data%20Types.md)
        -   [11.4.2 OpenGIS几何模型](./chapter11/04/02/The%20OpenGIS%20Geometry%20Model.md)  
            -   [11.4.2.1 几何类的继承层次](./chapter11/04/02/01/The%20Geometry%20Class%20Hierarchy.md)  
            -   [11.4.2.2 Geometry类](./chapter11/04/02/02/Geometry%20Class.md)  
            -   [11.4.2.3 Point类](./chapter11/04/02/03/Point%20Class.md)  
            -   [11.4.2.4 Curve类](./chapter11/04/02/04/Curve%20Class.md)  
            -   [11.4.2.5 LineString类](./chapter11/04/02/05/LineString%20Class.md)  
            -   [11.4.2.6 Surface类](./chapter11/04/02/06/Surface%20Class.md)  
            -   [11.4.2.7 Polygon类](./chapter11/04/02/07/Polygon%20Class.md)  
            -   [11.4.2.8 GeometryCollection类](./chapter11/04/02/08/GeometryCollection%20Class.md)  
            -   [11.4.2.9 MultiPoint类](./chapter11/04/02/09/MultiPoint%20Class.md)  
            -   [11.4.2.10 MultiCurve类](./chapter11/04/02/10/MultiCurve%20Class.md)  
            -   [11.4.2.11 MultiLineString类](./chapter11/04/02/11/MultiLineString%20Class.md)  
            -   [11.4.2.12 MultiSurface类](./chapter11/04/02/12/MultiSurface%20Class.md)  
            -   [11.4.2.13 MultiPolygon类](./chapter11/04/02/13/MultiPolygon%20Class.md)  
        -   [11.4.3 支持的空间数据格式](./chapter11/04/03/Supported%20Spatial%20Data%20Formats.md)  
        -   [11.4.4 几何的良好成型性和有效性](./chapter11/04/04/Geometry%20Well-Formedness%20and%20Validity.md)  
        -   [11.4.5 空间参考系统支持](./chapter11/04/05/Spatial%20Reference%20System%20Support.md)  
        -   [11.4.6 创建空间列](./chapter11/04/06/Creating%20Spatial%20Columns.md)  
        -   [11.4.7 填充空间列](./chapter11/04/07/Populating%20Spatial%20Columns.md)  
        -   [11.4.8 获取空间数据](./chapter11/04/08/Fetching%20Spatial%20Data.md)  
        -   [11.4.9 优化空间分析](./chapter11/04/09/Optimizing%20Spatial%20Analysis.md)  
        -   [11.4.10 创建空间索引](./chapter11/04/10/Creating%20Spatial%20Indexes.md)  
        -   [11.4.11 使用空间索引](./chapter11/04/11/Using%20Spatial%20Indexes.md)  
    -   [11.5：JSON类型](./chapter11/05/The%20JSON%20Data%20Type.md)  
    -   [11.6：数据类型默认值](./chapter11/06/Data%20Type%20Default%20Values.md)  
    -   [11.7：数据类型存储要求](./chapter11/07/Data%20Type%20Storage%20Requirements.md)
    -   [11.8：选择适合于列的类型](./chapter11/08/Choosing%20the%20Right%20Type%20for%20a%20Column.md)  
    -   [11.9：使用其它数据库引擎中数据类型](./chapter11/09/Using%20Data%20Types%20from%20Other%20Database%20Engines.md)  

