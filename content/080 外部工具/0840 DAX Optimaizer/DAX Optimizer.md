---
tags:
  - 外部工具
  - dax优化
  - dax-optimizer
created: 2023-10-19 22:02
chapter: 外部工具
keyword: 
des: 
return: 
import: 
hard: 
aliases: []
done:
---
## 软件简介
同[[PBI Explorer]]一样，这是SQLBI和tabular editor作者联合开发的另一款工具，一如该工具的slogan，该工具是为了查找Power BI模型中存在的问题并给予建议，从而释放Power BI模型的性能。详细的介绍可以参考官方文档，这里不再赘述[Introducing DAX Optimizer – Tabular Tools](https://www.tabulartools.com/blog/introducing-dax-optimizer/)
工具是个好工具，但贵也是真贵，即使是目前有活动，每月的订阅价格也要高达40美元，于我个人而言，我宁愿选择只有19美元的chatgpt4
![](https://s2.loli.net/2023/10/19/Rn3SyFLMAJHWTVD.png)

不过，好在官方终于出了示例，可以用来体验该工具的功能，只需要在设置里打开样例模型
![](https://s2.loli.net/2023/10/19/ZQyFswbpR2OdV9S.png)

## 度量值建议

像意大利人一样写DAX，是官方在一场活动上的宣传语，实际体验下来也确实是这样，该工具给出的度量建议都是基于SQLBI的经验总结出的规则。比如随便选择一个警告的度量，左上方可以看到给出的相关文档，并提供了很多示例代码来解释应该怎么优化，并且提供了文档的详细链接，可点击查看详情，比如（[Context transition in iterator](https://kb.daxoptimizer.com/d/100100)）。然后下方列出了写当前度量相关的其他度量。
![](https://s2.loli.net/2023/10/19/7Rx8FejVYHPgI3r.png)
也可以在右侧点击箭头查看该度量的详细影响
![](https://s2.loli.net/2023/10/19/GCBc8SEg9pU7AMd.png)
从功能体验上来说，这确实是一款不错的工具，可以帮助DAX新手，甚至DAX老手解决一些DAX性能优化上的问题。
## 关于性能优化
早在SQLBI的《[DAX圣经](https://www.sqlbi.com/books/the-definitive-guide-to-dax-2nd-edition/)》中就有四个章节是讲关于DAX性能优化的，只是这几个章节多少有些晦涩难懂。
![](https://s2.loli.net/2023/10/19/rJUH1cRtZBPM2Cf.png)
另外，SQLBI还有一套关于DAX性能优化的培训视频--[Optimizing DAX Video Course - SQLBI](https://www.sqlbi.com/p/optimizing-dax-video-course/)。349美元的价格对于国内用户来说还是太过昂贵，像我一样差钱的伙伴可以等他们的新书，SQLBI会将该培训视频中的内容，或者说是该视频中的讲义整理成书于2023年底发布。
![](https://s2.loli.net/2023/10/19/SvTnWmtF4hbe5j3.png)

## 到底要不要买

关键问题来了，到底要不要订阅该工具，个人观点是可以买一个月体验，然后总结出SQLBI关于这些问题的一些经验总结，然后再应用到日常DAX的书写中去。毕竟工具是死的，它只能基于一些既定的规则去评判；一如那句话说的DAX is easy, Calculate make it hard。DAX的性能表现如何有时是需要放到具体的上下文中去的，比如SQLBI关于分析[[DISTINCTCOUNT]]的这篇博客[Analyzing the performance of DISTINCTCOUNT in DAX - SQLBI](https://www.sqlbi.com/articles/analyzing-distinctcount-performance-in-dax/)，不同的上下文下性能表现是不一致的。
另外，DAX性能优化的另一方便，其实是对于DAX函数或者[[DAX引擎]]的理解，减少迭代，使用变量，短短8个字，实际实施的时候并不容易。自上而下的学习，可以让我们更快地做出一些东西，但是自下而上的学习，可以让我走的更稳更远。
那么，如果我想在这条路上走的又快又稳又远呢？那就得微软出手了。DAX Optimizer底层还是根据一些规则去判断度量是否优化，如果把这些规则喂给chatgpt4，甚至未来的chatgpt5,6等等，表现肯定会非常好。然而，微软为了养活第三方工具或者企业，短期内肯定是不会把精力放在这上面的。
如果，你想成为DAX专家，请使用[[DAX Studio]]自己进行优化。

## 相关链接
如果还没有DAX Optimier账号，但是又想了解DAX常见的一些优化方法，可以查看以下知识库内容，以下内容全部来源于DAX Optimier相关的知识库，目前官方还没有一个完整的目录来完整的获取这些内容，希望后续官方可以开放更多内容出来
- [Context transition in iterator](https://kb.daxoptimizer.com/d/100100) 
- [Duplicated measure](https://kb.daxoptimizer.com/d/100200) 
- [Duplicated function](https://kb.daxoptimizer.com/d/100300) 
- [Filtered table as iterator](https://kb.daxoptimizer.com/d/100400) 
- [Filtered table as filter argument (generic)](https://kb.daxoptimizer.com/d/100500) 
- [Summarize extended columns](https://kb.daxoptimizer.com/d/100600) 
- [Function replace GROUPBY/SUMMARIZE](https://kb.daxoptimizer.com/d/100700) 
- [Filter modifier function not used as filter argument](https://kb.daxoptimizer.com/d/100800) 
- [Blank comparison](https://kb.daxoptimizer.com/d/100900) 
- [Function replace IFERROR/DIVIDE](https://kb.daxoptimizer.com/d/101000) 
- [Context transition for aggregator instead of using existing row context](https://kb.daxoptimizer.com/d/101100) 
- [Function usage (LAST/FIRST)NONBLANK(VALUES)](https://kb.daxoptimizer.com/d/101200) 
- [(FIRST/LAST)NONBLANK with constant expression](https://kb.daxoptimizer.com/d/101300) 
- [Function replace DISTINCTCOUNT/HASONEVALUE](https://kb.daxoptimizer.com/d/101400) 
- [Redundant functions HASONEVALUE/SELECTEDVALUE (generic)](https://kb.daxoptimizer.com/d/101500) 
- [SUMX with IF predicate on iterator column](https://kb.daxoptimizer.com/d/101600) 
- [SUMX iterator cardinality reduction to single column](https://kb.daxoptimizer.com/d/101700) 
- [Function usage RELATEDTABLE](https://kb.daxoptimizer.com/d/101800) 
- [SUMX iterator excessive CallbackDataId](https://kb.daxoptimizer.com/d/101900) 
- [Function result invariant to current iterator](https://kb.daxoptimizer.com/d/102000) 