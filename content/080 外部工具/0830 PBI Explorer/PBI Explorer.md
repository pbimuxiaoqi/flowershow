---
tags:
  - 外部工具
  - pbi_explorer
created: 2023-10-15 16:14
chapter: 外部工具
keyword: 
des: 
return: 
import: 
hard: 
aliases: 
done:
---
## 简介
PBI Explorer 是不免费开源的工具，目前还是预览版，不过已经出到了Beta4，相比前面3版稳定性上有了很大的提升。它是由SQLBI和Tabular Editor联合开发的。他们联合开发的还有另一款订阅制软件DAX Optimizer,主要是用来优化Power BI模型的。
因为是Beta版，目前核心功能还未出完，目前已上线的功能只有两个，审视报表信息和版本比较。
![](https://s2.loli.net/2023/10/15/uhCmNEXysJRUTvS.png)


## 审视报表信息
在这个具之前也是有其他工具来查看报表的一些基本信息，比如报表的布局，每个页面上使用了哪些图表，图表里使用了哪些字段等，[Field Finder Tool ](https://powerbi.tips/product/field-finder-tool/) 。两个工具各有优劣，PBI Explorer可以查看所有使用到的视觉对象的属性、设置、主题、书签等。
比如我们随便打开一个报表文件，就可看到以下概览信息
![](https://s2.loli.net/2023/10/15/j24aBXiFeDMYfn5.png)
也可以对报表中使用的元素进行筛选，在下方有元素的各个属性，也有json模式可供查看原始信息。
![](https://s2.loli.net/2023/10/15/6akGYmr4JvVFWPy.png)
但是，这里也有些遗憾，目前查看书签详情的功能还未上线，如果上线了，那一定是很炸裂。毕竟，很多时候即使不是接收别人的文件而是看自己历史的文件，也会头痛书签到底设置了哪些内容。
## 版本比较
同样在这个工具之前，也是有工具专门用来对比不同版本间的差异的，[ALM Toolkit ](http://alm-toolkit.com/)两个工具的侧重并不相对，ALM Toolkit更侧重于度量的修改，而PBI Explorer则更侧重于页面元素的修改。不过两个工具都支持git集成，可以更方便的比较历史版本。
![](https://s2.loli.net/2023/10/15/xQbPUHptKAlW8OY.png)

## 下一步规划
- 报告分析器，其实DAX Optimizer作为一个专业模型优化器，已经内测很久，一个月前也拿到了内测资格，目前活动价桌面版本订阅每个月也高达40美元，而且更多的也只是给一些建议，而这些产生这些建议的原因，目前可以说是个黑匣子，只有SQLBI知道，所以也有微软员工称这DAX Optimizer是为了让大家像意大利人一样写DAX（SQLBI创始人是两个意大利人）。其实在更早之前微软内部也有员工写了一些优化Power BI模型的规则[Best practice rules to improve your models performance ](https://powerbi.microsoft.com/en-gb/blog/best-practice-rules-to-improve-your-models-performance/)，并且你可以在这些规则上进行修改，定义也适合自己的规则，希望后面这个功能推出后也可以自定义规则。
- 添加对书签的支持，目前对书签的支持还不完整，期待未来可以完整查看每个书签下设置的所有内容，这样后续维护书签时将会变得简单。

## 总结
目前，这个工具还不完整，不急着尝鲜的人可以再等等，等第一个正式版发布的时候再使用，那时应该会成为大多数人必备的外部工具。
这里，再次吐槽下微软，它很多东西都留了接口，可是就是不集成到软件里，而是让第三方工具来实现，比如计算组，推出快三年了，本月的开发规划中终于把桌面版创建计算组提上了日程。。。

## 相关链接
[PBI Explorer](https://www.pbiexplorer.com)
[PBI Explorer github](https://github.com/tabulartools/pbi-explorer)
[Tabular Tools](https://www.tabulartools.com)
