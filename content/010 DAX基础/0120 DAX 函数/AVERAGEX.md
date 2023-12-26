---
tags:
  - 标量
  - 聚合
  - dax函数
  - 迭代
created: 2023-11-05 20:04
chapter: DAX基础
keyword: 
des: 返回列中所有数字的平均值（算术平均值）
return: 标量
import: 
hard: 
aliases: 
done: 
url: https://dax.guide/averagex/
---

```dataview
list 
without id
url
where file.name = this.file.name
```

返回列中所有数字的平均值（算术平均值）

## 语法

```DAX
AVERAGE ( <ColumnName> )
```

| **参数** | **属性** | **描述**                 |
| -------- | -------- | ------------------------ |
| 表名     |          | 使用表达式每行计值的表   |
| 表达式   |          | 为表的每一行求值的表达式 |

## 返回值

#标量 一个货币或者小数类型的值

## 备注
- AVERAGEX 函数能够为表的每一行计算表达式，获取所有结果并计算其算术平均值。 因此，函数支持将表作为第一参数，表达式作为第二参数。 
- 在其他方面，AVERAGEX 遵循与 [[AVERAGE]] 相同的规则。 不能包含非数值或空单元格。  
- 表参数和表达式参数都是必需的，不能省略。  
- 如果没有要聚合的行，该函数将返回空白。  


## 示例

```js
--  AVERAGEX is required when you need to iterate over
--  a table an average the result of a measure
DEFINE
    MEASURE Sales[Sales Amount] = SUMX ( Sales, Sales[Quantity] * Sales[Net Price] )
    MEASURE Sales[AVG Customer] = AVERAGEX ( Customer, [Sales Amount] )
EVALUATE
SUMMARIZECOLUMNS (
    'Customer'[Continent],
    "AVG Customer", [AVG Customer]
)
```

需要迭代一张表或者表变量
```js
--  AVERAGEX is needed to iterate the content of a variable
DEFINE
    MEASURE Sales[Sales Amount] =
        SUMX ( Sales, Sales[Quantity] * Sales[Net Price] )
    MEASURE Sales[AVERAGE Monthly Sales] =
        VAR MonthlySales =
            ADDCOLUMNS (
                DISTINCT ( 'Date'[Calendar Year Month] ),
                "@MonthlySales", [Sales Amount]
            )
        VAR FilteredSales =
            FILTER ( MonthlySales, [@MonthlySales] > 10000 )
        VAR Result =
            -- Iterator required to aggregate the @MonthlySales column       
            AVERAGEX ( FilteredSales, [@MonthlySales] )
        RETURN
            Result
EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Color],
    "AVERAGE Monthly Sales", [AVERAGE Monthly Sales]
)
```

忽略空值，但是会考虑0
```js
--  AVERAGEX ignores blanks, it considers zeroes
EVALUATE
    VAR ValsWithBlank = { 1, 2, 3, BLANK () }
    VAR ValsWithZero  = { 1, 2, 3, 0        }
RETURN
    {
        ( "Average with BLANK", AVERAGEX ( ValsWithBlank, [Value] ) ),
        ( "Average with zero",  AVERAGEX ( ValsWithZero,  [Value] ) )
    }
```
![](https://s2.loli.net/2023/11/05/AurT3N6dvEL8ySB.png)

## 相关函数

[[AVERAEA]]
[[AVERAGE]]