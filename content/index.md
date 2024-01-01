---
tags:
  - gardenEntry
created: 2023-12-28 16:49
author: 小七
dg-publish: true
dg-home: true
---
# Power BI木小桼  | [[1 函数导航|DAX函数]]  |  [[关于我|关于我]] | 

## 工具  | [SQLBI](https://sqlbi.com/) |---| [[Power BI资源推荐|Power BI]] |---| [[AI资源推荐|AI]] |
---


>[!tip]- 三省  
> - [x] 早上吃啥
> - [x] 中午吃啥
> - [x] 晚上吃吗


---

#  最近文章

```dataview
table tags 
sort file.ctime desc
limit 10

```
---

## 标签云

```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: WordCloud

#-----------------#
#- chart data    -#
#-----------------#
data: | 
  dataviewjs: 
  return (() => {
    const tags = this.app.metadataCache.getTags();
   
    let dataArray = [];
    Object.keys(tags).forEach(key => dataArray.push ({tag: key.replace("#",""),count: tags[key]}));
    return dataArray;
   })();


#-----------------#
#- chart options -#
#-----------------#
options:
  wordField: "tag"
  weightField: "count"
  colorField: "tag"
style:
  backgroundColor: "translucent"

#-----------------------------------------------#
#--- 可选择多彩颜色(colorField) 或单色 (color) ---#
#---  colorField: "tag" ---#
#---  color: "#bb5548" ---#
#-----------------------------------------------#

  wordStyle:
    rotation: 0
```

---


