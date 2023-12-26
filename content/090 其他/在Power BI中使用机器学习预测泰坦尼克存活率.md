---
tags:
  - 机器学习
created: 2023-09-17 19:58
chapter: 
keyword: 
des: 
return: 
import: 
hard: 
aliases: []
done:
---
其实，在之前已经介绍过Power BI中强大的AI功能，但基本是依赖于Power BI Desktop来实现的，比如分解树，智能叙述，快速度量。而今天要介绍的就是Azure云服务中的机器学习。
打开Power BI Server,进行工作区后（必须是高级容量的工作区，此演示用的工作区为PPU的工作区）新建数据流
![](https://s2.loli.net/2023/09/17/7ecil1pOPbBgvJ4.png)

![](https://s2.loli.net/2023/09/17/qlu1SH6mnk5xzDJ.png)
接下来就是导入数据，之后选择定义新表，
![](https://s2.loli.net/2023/09/17/CdBRUvNTXl4uZbk.png)
这里我使用的是存放于onedive的csv文件，该测试文件来源于Kaggle, [Titanic Tutorial | Kaggle --- 泰坦尼克号教程|卡格尔](https://www.kaggle.com/code/alexisbcook/titanic-tutorial)感兴趣的可自取。
![](https://s2.loli.net/2023/09/17/9q5O4FHcvAj2yrS.png)
![](https://s2.loli.net/2023/09/17/6BkzA9PbpFm4yWE.png)
这之后的步骤和在Power BI Desktop中的加载数据差不多，选择文件，加载文件就可以了。加载好测试数据集和训练数据集后选择保存并关闭，回到工作区
![](https://s2.loli.net/2023/09/17/3Q4VAFlUkC2Bjtd.png)
选择训练数据集上的应用ML模型按钮就可以添加机器学习模型了
![](https://s2.loli.net/2023/09/17/YjAGX9oZQVPtLsb.png)
选择要预测的列
![](https://s2.loli.net/2023/09/17/GqsF8BIKJ3Z6AiM.png)
选择要用到的模型，这里自动推荐了二进制预测，也可以选择其他模型
![](https://s2.loli.net/2023/09/17/2LDNc8RIxnUZK61.png)
![](https://s2.loli.net/2023/09/17/6ICPXHs1Ry28dTe.png)
选择需要的列，如果有在Kaggle上或者其他平台接触过该数据集的应该知道票价高的存活率高些的。但也不要太拘泥，这里我们按自己的理解选择相关列就好，如果模型表现不理解再次修改模型重新预测就好。
接下就就是选择模型训练的时间，通常训练时间越久越好的，相对来说耗用的资源越多，按需来就好。
![](https://s2.loli.net/2023/09/17/JwYuLI4dTRniOle.png)
查看训练报表，如果模型训练完了，则再次单击应用ML模型按钮时就可以查看训练集的报表了。
![](https://s2.loli.net/2023/09/17/9nDVGLR2aYAOUZs.png)
![](https://s2.loli.net/2023/09/17/gk1hD2N7rnPvHyB.png)
相应的也可以查看测试数据集的结果，也可以使用Power BI Desktop连接该结果表进一步的展现。
![](https://s2.loli.net/2023/09/17/uNH5tS7QU6Oayc3.png)

今年ChatGPT4的成功，微软也加大了Power BI中AI投入，比如目前快速度量值建议使用的就已经是ChatGPT了，再加上整合微软云资源的Fabric，可见微软的野心。身为技术人员，或者业务人员，还能说什么呢，拿来为我所用就行了。
