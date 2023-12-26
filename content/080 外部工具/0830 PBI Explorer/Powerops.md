---
tags:
  - 外部工具
created: 2023-11-21 23:33
chapter: 外部工具
keyword: 
des: 
return: 
import: 
hard: 
aliases: 
done: 
url:
---
最近OpenAI的政判属实是比权力的游戏还要反转，身为不明真相吃瓜群众的我只希望别影响我继续使用就行。。。

在之前介绍过SQLBI和联合Tabular Editor的作者开发两款工具，其中一款开源免费的[[PBI Explorer]]主打的就是让我们更加了解报表，包括视觉对象，表，书签等。
就在刚刚，又发现了另一款功能和[[PBI Explorer]]类似，但是比它更美观，且个人体验下来更好用的web 工具，[Powerops](https://portal.powerops.app/)

![](https://s2.loli.net/2023/11/21/DJg8rXjyhU9KmxW.png)

## 申请试用
目前该工具可以申请试用，打开网站，点击试用或者点击登录，目前有两种方式，github或者[ Azure DevOps](https://learn.microsoft.com/zh-cn/azure/devops/user-guide/what-is-azure-devops?view=azure-devops)。github是最大的同性交友网站不用过多介绍，Azure DevOps可以简单理解为微软出的类似github的东西，也是为了版本控制和协同开发。

![](https://s2.loli.net/2023/11/21/odeOp2tVgDZzwxH.png)

国际版server端工作区早已支持配置git或者Azure DevOps
![](https://s2.loli.net/2023/11/21/GSQTuY9oNJsCx5i.png)

## 上传文件
登录成功后会先让创建一个分支，

![](https://s2.loli.net/2023/11/21/5lbvSDj9MRXJpEK.png)

创建完分支之后可以上传文件，这里要注意需要将pbi文件另存为pbip才可以，这里有三种选项，我这里选的完全报表，包含数据集和报表。（这里再吐槽下微软，都官宣把数据集改名为语义模型了，为什么另存为pbip后还是叫数据集）

![](https://s2.loli.net/2023/11/21/nXANKQMwlBgC8TH.png)
![](https://s2.loli.net/2023/11/21/qhfB9Ajs5XcrYGH.png)

对比PBI Explorer，真的太喜欢Powerops的界面了，而且是PBI Explorer有的功能它都有
![](https://s2.loli.net/2023/11/22/a1PQ28odg7JUEWf.png)

其他功能就不说了，最最最惊喜的是它可以查看书签的内容，可以明显看出每个书签做了哪些操作，这简单不要太好。Power BI维护自己开发的书签都已经很难了，更别说经常要维护别人开发书签了，简直是灾难。
![](https://s2.loli.net/2023/11/22/eIqYTfOQXcVsWNF.png)

## 其他功能

PowerOps基本上可以查看Power BI报表中所有内容，不仅限于视觉对象、书签、数据模型、度量值等，也支持版本比较，以直观的方式，比较两个版本的不同
![](https://s2.loli.net/2023/11/22/CacZotTDXKez24g.png)
同样版本对比时，不仅可以比较模型的变化，也可以比较报表，可以直观看出增减的内容
![](https://s2.loli.net/2023/11/22/C2ThO5gcnSlzv8x.png)
此外，还支持优化建议，这和使用Tablular Editor差别倒是不大，除了内置的规则也都可以自定义规则，
![](https://s2.loli.net/2023/11/22/D83KOnl5NoMfaVQ.png)
![](https://s2.loli.net/2023/11/22/zv9sbudeLpkABWI.png)

## 总结

PowerOps有很多功能，因为有些功能其他外部工具或者软件早就有了，就没过多介绍，最喜欢的是可以查看书签的内容，这点目前是我已知外部工具里唯一一款，对了PBI Explorer说未来也会支持。要说不满意的地方，那就是版本对比时不能比较同一分支下不同版本，这git的意义好像就不大了。或许是我不会用。
再次吐槽微软，为什么官方就不能有这些功能呢，别再说是为了有更多精力去打造更好的产品，Power BI有多少bug，你们不知道吗？