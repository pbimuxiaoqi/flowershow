---
tags:
  - 订阅
created: 2023-11-05 12:38
chapter: 软件基础
keyword: 
des: 
return: 
import: 
hard: 
aliases: 
done: true
---


```
= this.file.tags
```


不可否认，在商业BI软件中Power BI是最强大的，在2023年的Gartner的魔力象限中Power BI又是第一名[Microsoft named a Leader in the 2023 Gartner® Magic Quadrant™ for Analytics and BI PlatformsI](https://powerbi.microsoft.com/zh-cn/blog/microsoft-named-a-leader-in-the-2023-gartner-magic-quadrant-for-analytics-and-bi-platforms/)
![image.png](https://s2.loli.net/2023/05/21/FxvZehCLQolAYpj.png)

目前还没有使用Power BI的，甚至已经在用Power BI的企业都会这样的疑问，各个版本间有啥区别，公司应该使用哪个版本最合适。
## 免费版
首先，Power BI Desktop是免费下载使用的，但是如果要在线导入第三方图表（也可将图表文件下载下来，然后导入图表）或者发布到server端是需要注册Power BI账号的。且免费版是不支持共享报表给其他用户的，但可以发布到web(有链接的人都可以查看)
2023年微软修改在Power BI在国内的售卖策略，目前世纪互联版的Power BI已经不支持自助式的注册试用
![image.png](https://s2.loli.net/2023/05/21/XgFdVlKfpJbBSjC.png)
这里还没有账号的个人用户建议注册国际版，国际版注册需要使用企业邮箱，没有企业邮箱的可以先试用M365,这样会得到一个自定义域名的邮箱账号，然后使用该账号注册Power BI
[Microsoft 365(原Office 365)中小企业版云办公软件功能对比-Microsoft 365](https://www.microsoft.com/zh-cn/microsoft-365/business/compare-all-microsoft-365-business-products?&activetab=tab:primaryr2)
当然也可以注册M365开发者账号，可参考之前的文章，不再赘述，友情提醒，某宝上的Power BI Pro账号基本上都是免费的M365账号，不建议花冤枉钱。
## Power BI Pro
Power BI Pro是按月付费的许可证，世纪互联代理的是七百多一年，也可更低价格拿入，就看你的购买渠道了。
此外，Power BI Pro是包含在M365 E5订阅中的，做过很多外企的BI项目，他们企业本身就是M365 E5订阅，并且他们报表不会存在大量的且复杂的表格数据，所有这个Pro就足够他们使用了。
拥有Power BI Pro的用户可以互相共享报表内容，并进行权限管理。也可在sharepoint、ppt、teams、excel等微软生态中使用。

## PPU
PPU的全称是Power BI Premium Per User，它包括所有 Power BI Pro 许可证功能，并包括 XMLA 终结点、AI 和其他仅面向高级订阅者的功能，PPU工作区的报表Pro订阅是看不了的，用户也需要具有PPU许可证。
[Power BI Premium Per User - Power BI | Microsoft Learn](https://learn.microsoft.com/zh-cn/power-bi/enterprise/service-premium-per-user-faq)
所以，PPU在价格上会比Pro订阅更贵些，每个月150左右，个人用户想体验高级版的功能，PPU无疑是最合算的，企业的话，建议选配Embedded或者Premium。
## Power BI Embedded
Power BI Embedded同PPU一样，也属于减配版的Premium，Power BI Embedded 是一种包含 A SKU 的 Azure 产品/服务。如果企业没有使用M365生态，需要使用报表的用户又非常多，Power BI Embedded是最好的选择，企业只需要至少购买一个Power BI Pro许可证+Power BI Embedded服务就可以了。微软提供了完备的API接口，可以嵌入到门户网站、企业微信、钉钉、飞书等等
Power BI Embedded作为Azure云服务也是支持缩放的，比如在高频时段将服务从A1升级为A3,低频时段从A3降为A1甚至关闭都是可以的。所以如果企业没有M365生态，A1又可以满足要求，通常超过80个用户使用，从成本考虑就建议企业选择Power BI Embedded
![image.png](https://s2.loli.net/2023/05/21/A14fUqnLzG8YQOd.png)

[Power BI 嵌入式分析概述 - Power BI | Microsoft Learn](https://learn.microsoft.com/zh-cn/power-bi/developer/embedded/embedded-analytics-power-bi)

## Power BI Premium
Power BI Premium拥有更强大的性能与更多的功能，如果企业拥有庞大的用户群，比如1000个用户，那Power BI Premium是最佳的选择，目前服务过的企业中也只有一家企业购买的有Power BI Premium，而且是买了好几个订阅，只能感叹一句是真有钱。
[什么是 Power BI Premium？ - Power BI | Microsoft Learn](https://learn.microsoft.com/zh-cn/power-bi/enterprise/service-premium-what-is)

## Power BI Report Server
一个本地报表服务器，其中包含一个可显示和管理报表和 KPI 的 Web 门户。 要使用Power BI Report Server需要购买Sql Server许可证或者Power BI Premium（## Power BI Report Server仅包含在 P SKU 中。 它不包含在 EM SKU 中）。
[什么是 Power BI 报表服务器？ - Power BI | Microsoft Learn](https://learn.microsoft.com/zh-cn/power-bi/report-server/get-started)
对于已经购买过Sql Server的企业且不希望数据上云的企业，多数会选择该方案。这里也要注意Power BI Report Server在功能上有很多限制的，且更新频率上为每年3次，是远远落后于Power BI Desktop的月更的。
[比较 Power BI 报表服务器和 Power BI 服务 - Power BI | Microsoft Learn](https://learn.microsoft.com/zh-cn/power-bi/report-server/compare-report-server-service)
![image.png](https://s2.loli.net/2023/05/21/6Kkmeh5TVf1bSys.png)

## 各版本详细对比
| 功能                                                 | Power BI 免费 | Power BI  Pro | Power BI  Premium Per User | Power BI  Premium | Power BI Report  Server |
| ---------------------------------------------------- | ------------- | ------------- | -------------------------- | ----------------- | ----------------------- |
| 移动应用访问                                         | 已包含        | 已包含        | 已包含                     | 已包含            | 已包含                  |
| 发布报表以共享和协作                                 |               | 已包含        | 已包含                     |                   | 已包含                  |
| 分页 (RDL) 报表                                      |               | 已包含        | 已包含                     | 已包含            | 已包含                  |
| 在没有每用户许可证的情况下使用内容                   |               |               |                            | 已包含            |                         |
| 使用 Power BI 报表服务器进行本地报告                 |               |               |                            | 已包含            | 已包含                  |
| 模型内存大小限制5                                    | 1 GB          | 1  GB         | 100  GB                    | 400  GB           | 依赖服务器空间的限制    |
| 刷新率                                               |               | 8/天          | 48/天                      | 48/天             | 无限制                  |
| 连接到 100 多个数据源                                | 已包含        | 已包含        | 已包含                     | 已包含            | 已包含                  |
| 利用 Power BI Desktop 创建报表和可视化效果           | 已包含        | 已包含        | 已包含                     | 已包含            |                         |
| 嵌入 API 和控件                                      |               | 已包含        | 已包含                     | 已包含            |                         |
| AI 视觉对象                                          |               | 已包含        | 已包含                     | 已包含            |                         |
| 高级 AI（文本分析、图像检测、自动化机器学习）        |               |               | 已包含                     | 已包含            |                         |
| XMLA 终结点读/写连接                                 |               |               | 已包含                     | 已包含            |                         |
| 数据流（直接查询、链接和计算的实体、增强的计算引擎） |               |               | 已包含                     | 已包含            |                         |
| 数据市场创建                                         |               |               | 已包含                     | 已包含            |                         |
| 数据安全和加密                                       |               | 已包含        | 已包含                     | 已包含            |                         |
| 内容创建、使用和发布的指标                           |               | 已包含        | 已包含                     | 已包含            |                         |
| 应用程序生命周期管理                                 |               |               | 已包含                     | 已包含            |                         |
| 多地理位置部署管理                                   |               |               |                            | 已包含            |                         |
| 创建自己的密钥 (BYOK)                                |               |               |                            | 已包含            |                         |
| 自动缩放加载项可用性                                 |               |               |                            | 已包含            |                         |
| 最大存储                                             | 10 GB/用户    | 10  GB/用户   | 100  TB                    | 100  TB           | 依赖服务器空间的限制    |
| python/R                                             | 已包含        | 已包含        | 已包含                     | 已包含            |                         |

## 版本选择
对于企业而且，Power BI Free肯定是不行的，虽然可以通过pbi文件的形式共享报表，但这样就失去了安全性，安全性才是企业选择BI方案的首要考虑。
如果企业已经订阅了M365 E3则建议升级为E5订阅，这样每个用户就都有Power BI Pro了。
如果企业没有订阅M365，且用户数超过了80个，则建议Power BI Embedded。
如果企业用户数上千人，建议采用Power BI Premium。
具体采用Power  BI Embedded或者Power BI Premium的哪个价位，可以参考进行压力测试
[Power BI Embedded: Stress Testing & Capacity Planning – Data on Wheels – Steve & Kristyna Hughes --- Power BI Embedded： Stress Testing & Capacity Planning – Data on Wheels – Steve & Kristyna Hughes (wordpress.com)](https://dataonwheels.wordpress.com/2022/02/22/power-bi-embedded-stress-testing-capacity-planning/)

无论采用哪种订阅，数据的安全性都是必不可少的。