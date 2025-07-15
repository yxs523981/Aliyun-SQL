本学习笔记为阿里云天池龙珠计划sql训练营的学习内容，学习链接为：https://tianchi.aliyun.com/specials/promotion/aicampsql

SQL学习笔记：SELECT语句基础与聚合查询
一、学习知识点概要
SELECT语句基础语法结构

算术运算符与比较运算符

逻辑运算符（NOT/AND/OR）与三值逻辑

聚合函数（COUNT/SUM/AVG/MAX/MIN）

使用GROUP BY进行分组查询

使用HAVING对分组结果筛选

使用ORDER BY对结果排序

SQL语句执行顺序与注意事项

二、学习内容
2.1 SELECT语句基础
2.1.1 从表中选取数据
SELECT语句用于从表中选取数据

基本结构包含SELECT和FROM两个子句

SELECT子句指定要查询的列名

FROM子句指定数据来源的表名

2.1.2 从表中选取符合条件的数据
WHERE子句用于指定查询条件

WHERE子句跟在FROM子句之后

2.1.3 相关法则
星号(*)表示选取所有列

SQL语句可以随意换行（不可插入空行）

汉语别名需使用双引号("")括起来

DISTINCT关键字用于删除重复行

注释分为单行注释(--)和多行注释(/* */)

2.2 算术运算符和比较运算符
2.2.1 算术运算符
四则运算运算符：+（加）、-（减）、*（乘）、/（除）

2.2.2 比较运算符
常见比较运算符：=（等于）、<>（不等于）、>=（大于等于）、>（大于）、<=（小于等于）、<（小于）

2.2.3 常用法则
SELECT子句可使用常数或表达式

注意不等号和等号的位置

字符串类型按字典顺序排序

使用IS NULL选取NULL记录

使用IS NOT NULL选取非NULL记录

2.3 逻辑运算符
2.3.1 NOT运算符
表示否定，不能单独使用

2.3.2 AND运算符和OR运算符
AND表示"并且"（取交集）

OR表示"或者"（取并集）

2.3.3 通过括号优先处理
使用括号改变运算优先级

2.3.4 真值表
使用真值表理解复杂逻辑关系

SQL采用三值逻辑（真/假/不确定）

2.3.5 含有NULL时的真值
NULL的真值为不确定(UNKNOWN)

三值逻辑下的真值表

2.4 对表进行聚合查询
2.4.1 聚合函数
常用聚合函数：COUNT（计数）、SUM（求和）、AVG（平均值）、MAX（最大值）、MIN（最小值）

COUNT(*)包含NULL记录，COUNT(列名)不包含NULL记录

2.4.2 使用聚合函数删除重复值
在聚合函数中使用DISTINCT删除重复值

2.4.3 常用法则
聚合函数排除NULL（COUNT(*)除外）

SUM/AVG只适用于数值类型

MAX/MIN适用于几乎所有数据类型

2.5 对表进行分组
2.5.1 GROUP BY语句
使用GROUP BY子句进行分组汇总

GROUP BY子句指定聚合键（分组列）

2.5.2 聚合键中包含NULL时
NULL作为特殊分组处理

2.5.3 GROUP BY书写位置
子句顺序：SELECT → FROM → WHERE → GROUP BY

2.5.4 在WHERE子句中使用GROUP BY
先通过WHERE筛选，再进行分组

2.5.5 常见错误
SELECT子句中的列名必须是GROUP BY子句中指定的列名（聚合键）

GROUP BY子句中不能使用列的别名

WHERE子句中不能使用聚合函数

2.6 为聚合结果指定条件
2.6.1 用HAVING得到特定分组
使用HAVING子句对分组进行过滤

2.6.2 HAVING特点
HAVING子句可使用数字、聚合函数和GROUP BY中指定的列名

2.7 对查询结果进行排序
2.7.1 ORDER BY
使用ORDER BY子句对结果排序

默认升序(ASC)，降序需指定DESC

多个排序键用逗号分隔

NULL值会在开头或末尾汇总

2.7.2 ORDER BY中列名可使用别名
ORDER BY子句中可以使用SELECT子句定义的别名

因执行顺序：GROUP BY在SELECT之前，ORDER BY在SELECT之后

三、学习问题与解答
问题：WHERE子句和HAVING子句的区别？
解答：WHERE用于筛选行（在分组前），HAVING用于筛选分组（在分组后）。

问题：GROUP BY子句为什么不能使用别名？
解答：因为GROUP BY执行时，SELECT子句的别名尚未生效。

问题：三值逻辑中如何处理NULL？
解答：NULL参与逻辑运算时结果为UNKNOWN，可能影响最终结果。

问题：COUNT()和COUNT(列名)的区别？
解答：COUNT()统计所有行数（包含NULL），COUNT(列名)只统计该列非NULL的行数。

四、学习思考与总结
技术层面：SQL查询是数据处理的核心，掌握SELECT语句的各种子句组合至关重要。特别是理解执行顺序（FROM→WHERE→GROUP BY→HAVING→SELECT→ORDER BY）对编写正确查询很有帮助。

学习方法：通过概念学习+实践验证的方式效果最佳。先理解各子句的功能和限制，再通过实际编写SQL加深理解。

注意事项：特别注意NULL值的特殊处理方式，以及不同子句中别名的可用性差异。

总结：SQL查询能力的提升需要不断练习，重点掌握条件筛选（WHERE）、分组聚合（GROUP BY+HAVING）和结果排序（ORDER BY）的配合使用。
