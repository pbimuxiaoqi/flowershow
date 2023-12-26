---
tags:
  - dax函数
  - 时间智能
  - 上下文转换
created: 2023-11-16 19:55
chapter: dax基础
keyword: 
des: 计算与当前季度末对应的日期的指定表达式
return: 标量
import: 1
hard: 1
aliases: 
done: 
url: https://dax.guide/closingbalancequarter/
---

```dataview
list 
without id
url
where file.name = this.file.name
```


## 语法

```js
CLOSINGBALANCEQUARTER ( <Expression>, <Dates> [, <Filter>] )
```

|PARAMETER |ATTRIBUTES|DESCRIPTION |
|---|---|---|
|Expression||The expression to be evaluated.  <br>要计算的表达式。|
|Dates ||The name of a column containing dates or a one column table containing dates.  <br>包含日期的列或包含日期的单列表的名称。|
|Filter | 可选|A boolean (True/False) expression or a table expression that defines a filter.  <br>定义过滤器的布尔（True/False）表达式或表表达式。|

## 返回值
 #标量 任何类型的单个值

一个标量值，表示在当前上下文中季度的最后一个日期计算的表达式。
## 备注

日期参数可以是以下任意一个：
- 对日期/时间列的引用。仅在这种情况下，上下文转换才适用，因为列引用被替换为[[CALCULATETABLE]]( [[DISTINCT]] ( <Dates> ) )  
- 返回单列日期/时间值的表表达式。
- 定义日期/时间值的单列表的布尔表达式。

结果表仅包含日期列中存在的日期。
等同于
```js
CALCULATE (
    <Expression>,
    ENDOFQUARTER ( <Dates> )
    [, <Filter>]
)
```

## 示例

```js
DEFINE
    MEASURE Sales[Sales YTD] =
        CALCULATE ( [Sales Amount], DATESYTD ( 'Date'[Date] ) )
    MEASURE Sales[Sales OBQ] =
        OPENINGBALANCEQUARTER ( [Sales YTD], 'Date'[Date] )
    MEASURE Sales[Sales CBQ] =
        CLOSINGBALANCEQUARTER ( [Sales YTD], 'Date'[Date] )
EVALUATE
CALCULATETABLE (
    SUMMARIZECOLUMNS (
        'Date'[Calendar Year Month Number],
        "Sales", [Sales Amount],
        "Sales YTD", [Sales YTD],
        "Sales OBQ", [Sales OBQ],
        "Sales CBQ", [Sales CBQ]
    ),
    'Date'[Calendar Year Month Number] <= 200709
)
ORDER BY 'Date'[Calendar Year Month Number]
```

## 重点文章
```dataview
list
where contains(keyword, this.file.name)
```
![](https://s2.loli.net/2023/11/16/YGJdi7OBDbsPARr.png)

## 相关函数

[[CLOSINGBALANCEMONTH]]
[[CLOSINGBALANCEYEAR]] 