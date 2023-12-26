---
tags:
  - tabular-editor
created: 2023-09-04 21:34
chapter: 外部工具
import: 3
hard: 1
aliases: []
done:
---
如果我们在筛选器看到存在空值，这就说明事实表中存在维度表中找不到的值，如果表不多的话，我们可以拖出来一张表，包含维度与事实表的关系键，如果表很多，建议通过程序来快速检查。


- 在报表中通过外部工具打开Tabular Editor
- 复制代码到Advanced Scripting
- 点击运行
- 占击+保存为模板，下次可直接从模板中找到并运行
    
    ![](https://secure2.wostatic.cn/static/tQUHgjTnNva3zJRcMhtfpw/image.png?auth_key=1693837455-jhWJSWZUX5Q2imRK5RNKQ7-0-31bc8cb6ad9f4a9a7085e253679c4e76)
    

代码如下

```js
var sb = new System.Text.StringBuilder();
string newline = Environment.NewLine;

sb.Append("FromTable" + '\t' + "ToTable" + '\t' + "BlankRowCount" + newline);

foreach (var r in Model.Relationships.ToList())
{
    bool   act = r.IsActive;
    string fromTable = r.FromTable.Name;
    string toTable = r.ToTable.Name;
    string fromTableFull = r.FromTable.DaxObjectFullName;    
    string fromObject = r.FromColumn.DaxObjectFullName;
    string toObject = r.ToColumn.DaxObjectFullName;
    string dax;
    
    if (act)
    {
        dax = "SUMMARIZECOLUMNS(\"test\",CALCULATE(COUNTROWS("+fromTableFull+"),ISBLANK("+toObject+")))";
    }
    else
    {
        dax = "SUMMARIZECOLUMNS(\"test\",CALCULATE(COUNTROWS("+fromTableFull+"),USERELATIONSHIP("+fromObject+","+toObject+"),ISBLANK("+toObject+")))";
    }
    
    var daxResult = EvaluateDax(dax);
    string blankRowCount = daxResult.ToString();
    
    if (blankRowCount != "Table")
    {
        sb.Append(fromTable + '\t' + toTable + '\t' + blankRowCount + newline);        
    }
}

sb.Output();
```

