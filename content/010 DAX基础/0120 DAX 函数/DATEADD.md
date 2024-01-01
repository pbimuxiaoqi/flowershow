---
tags:
  - dax函数
  - 时间智能
  - 表函数
created: 2023-11-14 22:44
chapter: dax基础
keyword: 
des: 按指定的时间间隔移动给定的日期集
return: 表
import: 
hard: 
aliases: 
done: 
url: https://dax.guide/dateadd/
dg-publish: true
---

```dataview
list 
without id
url
where file.name = this.file.name
```


## 语法

```js
DATEADD ( <日期列>, <偏移量>, <偏移单位> )
```

| **参数** | **属性** | **描述**     |
| -------- | -------- | ------------ |
| 日期列   |          | 包含日期的列 |
|   偏移量      |          |     一个整数，         |
|    偏移单位      |          |    Day,Month,Quarter,Year          |

## 返回值

#表 包含单列日期的表

## 备注

- 对日期/时间列的引用。只有在这种情况下才应用上下文转换，因为列引用被替换为[[CALCULATETABLE]] ( [[DISTINCT]] ( <日期列> ) )  
- 返回单列日期/时间值的表表达式  
- 定义日期/时间值的单列表的布尔表达式  
- 结果表中仅包含日期列中存在的日期
  



## 示例

```js
--  DATEADD is a more generic functions.
--  It shifts a period back and forth over time using
--  DAY, MONTH, QUARTER, YEAR
--  This example produces the same result as SAMEPERIODLASTYEAR
EVALUATE
VAR StartDate = DATE ( 2008, 07, 25 )
VAR EndDate =   DATE ( 2008, 07, 31 )
RETURN
    CALCULATETABLE (
        DATEADD ( 'Date'[Date], -1, YEAR ),
        'Date'[Date] >= StartDate &&
        'Date'[Date] <= EndDate
    )
ORDER BY [Date]
```
![](https://s2.loli.net/2023/11/14/Aa28bWIMVCzygci.png)

```JS

   --  DATEADD has a quite complex logic to move months and quarters
--  the right way, handling months with different dates.
EVALUATE
VAR StartDate = DATE ( 2008, 02, 25 )
VAR EndDate =   DATE ( 2008, 02, 29 )
RETURN
    CALCULATETABLE (
        DATEADD ( 'Date'[Date], +1, MONTH ),
        'Date'[Date] >= StartDate &&
        'Date'[Date] <= EndDate
    )
ORDER BY [Date]
```
![](https://s2.loli.net/2023/11/14/Vp6IkQriBMxLuqC.png)


```JS

 --  This example shows the sales in the current and previous month.
--  It also reports sales in the same month in the previous quarter and year.
DEFINE
    MEASURE Sales[Same period last month] =
        CALCULATE (
            [Sales Amount],
            DATEADD ( 'Date'[Date], -1, MONTH )
        )
    MEASURE Sales[Same period last quarter] =
        CALCULATE (
            [Sales Amount],
            DATEADD ( 'Date'[Date], -1, QUARTER )
        )
    MEASURE Sales[Same period last year] =
        CALCULATE (
            [Sales Amount],
            SAMEPERIODLASTYEAR ( 'Date'[Date] )
        )
EVALUATE
SUMMARIZECOLUMNS (
    'Date'[Calendar Year Month Number],
    'Date'[Calendar Year Month],
    "Sales Amount", [Sales Amount],
    "Same period last month", [Same period last month],
    "Same period last quarter", [Same period last quarter],
    "Same period last year", [Same period last year]
)
ORDER BY [Calendar Year Month Number]
```

![](https://s2.loli.net/2023/11/14/PQpNohc6ibnX721.png)

## 重点文章
```dataview
list
where contains(return, this.file.name)
```

## 相关函数

[[PARALLELPERIOD]]