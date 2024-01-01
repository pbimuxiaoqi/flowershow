---
tags:
  - dax函数
  - 时间智能
  - 标量
created: 2023-11-12 23:23
chapter: dax基础
keyword: 
des: 在当前月份的最后一个日期计值的表达式
return: 标量
import: 1
hard: 1
aliases: 
done: 
url: https://dax.guide/closingbalancemonth/
dg-publish: true
---

```dataview
list 
without id
url
where file.name = this.file.name
```

在当前月份的最后一个日期计值的表达式。

## 语法

```js
CLOSINGBALANCEMONTH ( <表达式>, <日期列>, [<筛选器>] )
```

| **参数** | **属性** | **描述**           |
| -------- | -------- | ------------------ |
| 列名     |          | 包含要计数的值的列 |

## 返回值

#标量  一个任意类型的值
该值来自在当前上下文中该月份最后一个日期计算的表达式
## 备注

- 对日期/时间列的引用。只有在这种情况下才应用上下文转换，因为列引用被替换为[[CALCULATETABLE]] ( [[DISTINCT]] ( <日期列> ) )  
- 返回单列日期/时间值的表表达式  
- 定义日期/时间值的单列表的布尔表达式  
- 结果表中仅包含日期列中存在的日期
语法等同于下面
```js
CALCULATE (
    <Expression>,
    ENDOFMONTH ( <Dates> )
    [, <Filter>]
)
```

## 示例

```js
DEFINE
    MEASURE Sales[Sales YTD] =
        CALCULATE ( [Sales Amount], DATESYTD ( 'Date'[Date] ) )
    MEASURE Sales[Sales OBQ] =
        OPENINGBALANCEMONTH ( [Sales YTD], 'Date'[Date] )
    MEASURE Sales[Sales CBQ] =
        CLOSINGBALANCEMONTH ( [Sales YTD], 'Date'[Date] )
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
![](https://s2.loli.net/2023/11/14/wERYd7VKUmga2Iy.png)

## 重点文章
```dataview
list
where contains(return, this.file.name)
```

## 相关函数

- [[CLOSINGBALANCEQUARTER]]
- [[CLOSINGBALANCEYEAR]]