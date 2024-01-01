---
tags:
  - 聚合
  - dax函数
  - 标量
created: 2023-11-05 20:10
chapter: DAX基础
keyword: 
des: 统计指定列具有非空值的行数。
return: 标量
import: 5
hard: 1
aliases: 
done: 
url: https://dax.guide/count
dg-publish: true
---
```dataview
list 
without id
url
where file.name = this.file.name
```

统计指定列具有非空值的行数。

## 语法

```DAX
COUNT ( <ColumnName> )
```

| **参数** | **属性** | **描述**           |
| -------- | -------- | ------------------ |
| 列名     |          | 包含要计数的值的列 |

## 返回值

#标量  一个整数 

## 备注
COUNT 只允许使用列作为参数，可以对包含以下类型的值的行进行计数：  
- 数字  
- 日期  
- 字符串  
如果未找到任何要计数的行，则返回空白。  
  
COUNT 跳过空白值。 不支持 TRUE/FALSE 值。如果要计算 TRUE/FALSE 值的列，请使用 [[COUNTA]] 函数。  
  
COUNT 函数在内部执行 [[010 DAX基础/0120 DAX 函数/COUNTX]]，两者没有任何性能差异。  


## 示例

```js
--  COUNT is the short version of COUNTX, when used with one column only
--  In DAX, there are no differences between COUNTA and COUNT
--  COUNTX can be expressed in a more explicit way by using CALCULATE
--  and COUNTROWS
DEFINE
    MEASURE Customer[# Customers]     = COUNTROWS ( Customer )
    MEASURE Customer[# Individuals 1] = COUNT ( Customer[Customer Name] )
    MEASURE Customer[# Individuals 2] = COUNTX ( Customer, Customer[Customer Name] )
    MEASURE Customer[# Individuals 3] =
        CALCULATE (
            COUNTROWS ( Customer ),
            NOT ISBLANK ( Customer[Customer Name] )
        )
EVALUATE
SUMMARIZECOLUMNS (
    Customer[Continent],
    "# Customers",     [# Customers],
    "# Individuals 1", [# Individuals 1],
    "# Individuals 2", [# Individuals 2],
    "# Individuals 3", [# Individuals 3]
)
```
![](https://s2.loli.net/2023/11/08/8roGI52QTZ6yiRW.png)


不计算空值，但是会计算空字符串
```js
--  COUNT does not count blanks, but it counts empty strings
--  using the CALCULATE version, the code is clearer
DEFINE
    MEASURE Customer[# COUNT] = COUNT ( Customer[Customer Name] )
    MEASURE Customer[# NO BLANKS] =
        CALCULATE (
            COUNTROWS ( Customer ),
            NOT ISBLANK ( Customer[Customer Name] )
        )
    MEASURE Customer[# NO BLANKS / EMPTY STRINGS] =
        CALCULATE (
            COUNTROWS ( Customer ),
            Customer[Customer Name] <> ""
        )
EVALUATE
SUMMARIZECOLUMNS (
    Customer[Continent],
    "# COUNT", [# COUNT],
    "# NO BLANKS", [# NO BLANKS],
    "# NO BLANKS / EMPTY STRINGS", [# NO BLANKS / EMPTY STRINGS]
)
```
![](https://s2.loli.net/2023/11/05/LRYI2SxuZt3E9WC.png)

## 相关函数

[[COUNTA]]
[[COUNTX]]
[[COUNTAX]]