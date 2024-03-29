# Project 2 Note 

## 文献笔记(比较特殊的一篇)
有一个老师写的发表的文章，他的核心参考论文有5篇。

文章[链接](https://doi.org/10.1016/j.sste.2023.100579): https://doi.org/10.1016/j.sste.2023.100579
### 摘要
本文调查了
- 英格兰第一波和第二波大流行期间 
  - COVID-19 死亡率的
    - **时空模式**及
    - 其
      - **社会经济**
      - 和**环境决定**因素。

分析中使用了 
- 2020 年 3 月至 2021 年 4 月 
  - 中超产出地区 (middle super output area)的
    -  COVID-19 死亡率。
 - SaTScan 用于
   - 分析 COVID-19 死亡率的
     - 时空模式，
 - 并使用**地理加权泊松回归 (GWPR) **调查
   - 与社会经济和环境因素的关联。

结果表明，
- COVID-19 死亡热点
  - 存在显着的**时空变化**，
  - 热点从 COVID-19 爆发的地区移动，
    - 然后传播到该国其他地区。 

- GWPR 分析显示，(也即是说有横向比较（类型）也有纵向比较（时间）)
  - 年龄构成、
  - 种族构成、
  - 贫困、
  - 养老院和
  - 污染
    - 都与 COVID-19 死亡率有关。
    - 尽管这种关系因空间而异，
    - 但与这些因素的关联在第一波和第二波中
      - 相当一致。



### 介绍
```
本章节是以时间为脉络，介绍了新冠在英国的发展。
```
新冠的全球状态-->英国新冠-->6轮新冠-->详细介绍-->英国官方动作-->动作详细与新冠感染高峰(-->有疫苗-->2022-->2022年解封)-->本文重要性-->过往研究
#### 过往研究
- 确实有新冠确诊以及死亡率的空间模式的研究
- 也有关于新冠空间流行动态的研究
  - 但是这些研究一般是全球大陆或者国家层面,或者是县市级别
  - 在社区层面开展的研究比较少
    - 有的要么是说这种研究是很大地理范围的,比如**地方当局**在一个**国家or地区**在空间上是异质的(中-大)
    - 要么是在**邻里层面**进行,但是在特定区域,比如伦敦(这样的范围)(小-中)
- 还有他们的研究一般处于新冠的早期阶段
  - 而不是扩展到空间格局可能非常不同的后期
- 只有有限数量的研究关注了covid-19死亡率和感染
- 因此，本文基于 **14 个月的小区域数据**，(小)
  - 通过调查*英格兰***第一波和第二波大流行**中 (大)(也就是说研究粒度小,研究区域大)
    - COVID-19 死亡率的时空模式
    - 及其社会经济和环境决定因素，
    - 填补了这一空白。 
  - 我们使用
    - 空间扫描统计（Kulldorff，1997）
      - 来分析 COVID-19 死亡率的局部集群，
    - 并使用地理加权泊松回归来
      - 检查影响空间格局的因素，
      - 同时考虑到空间异质性。

### 数据
```
首先介绍数据源,然后介绍对于各种数据源的指标的处理,然后介绍环境变量以及部分数据的赋值(插值)
```
数据清单:

- 新冠 死亡率 ONS
- 地理边界 MOSA
- 年龄构成 - ONS -2018
- 种族和过度拥挤数据 2021 census
- 收入 IMD
- 养老院床位
处理方法:
- 不同种族的占比
- 过度拥挤是指的是一个房间住着多个人
- 收入剥夺来自IMD
- 人口数据用来计算老年人(大于65岁)比例
- 病毒暴露来自英格兰数据
- 环境污染数据 分辨率是1km*1km
  - 被插值进了MOSA
- 健康相关的使用了肥胖率

### 方法
```
主要方法1. 空间扫描统计, 2. GWR 值得注意的是其实内部有很多**细节**
```
#### Space Scan Statistic Method 空间扫描统计方法
- 空间扫描统计方法
  - 分析和确定**新冠死亡率集聚**发生的位置
  - 由于预计新冠死亡人数与当地人口成正比,因此选择**泊松分布**来解释每个社区的人口
  - 空间扫描统计的扫描窗口是一个地理基础上的圆形窗口
    - 以MOSA的质心之一为中心,半径大小从0变化到指定的最大值
  - 本次研究中,对于每个月的新冠死亡数据**重复使用了空间扫描统计**
  - 为了避免大集群,最大空间集群大小设置为风险人口的百分之三
  - 根据一个约内在MOSA或者弄个观察到的病例数和人口规模,计算每个圆圈的可能性以确定观察到的死亡病例数是否超过预期病例数
  - 观察到的确诊与预期确诊的比率表示窗口内的风险,
    - 相对风险表示窗口内的风险与窗口外的风险相比
  - 使用数据集的999个随机复制组成的蒙特卡罗模拟评估统计显著性

#### GWR 地理加权回归
为了确定什么因素决定了新冠死亡率,使用了GWR
- GWR考虑了空间异质性,因此每个区域的因变量都有自己的关系
- GWR 框架内的泊松分布目前最适合疾病数据，尤其是在特定区域观察到的病例数较低时（Nakaya 等人，2005 年）。
  - **因变量**在地理加权泊松回归 (GWPR) 中指定为每个 MSOA 观察到的 COVID-19 死亡人数，
  - **偏移变量**指定为每个 MSOA 的人数。全局和局部泊松回归模型的解释变量是相同的变量。
  - 每个 MSOA 的质心用作输入坐标。
  - 然后 GWPR 模型利用内核并为每个坐标拟合回归方程，其中内核中心的坐标是回归点。
  - 内核中的数据点从内核的中心到内核的边缘加权。
  - 核外的数据点的权重为零，因此被排除在回归方程中。

### 结果
- 数据统计概述
- 分Wave 讲述 1 , 2 
  - 内部特点
    - 人口结构与收入
  - 热点分析
    - 热点分析结果
- 全局泊松模型
- 按两者分成了2 model
- 全局则只看大概
- AIC goodness-of-fit statistic 说明有空间异质性
- 分析

### 讨论
- 总体的结果
- 新冠的传播
- 两轮之间一致的数据
- 差异
  - 南北
  - 城乡
- 不足
  - 不足总结
  

### 结论
- 其实就是和摘要也差不多


# Gloassary

## age-standardised mortality rate 年龄标准化死亡率
TODO 这里的标准化需要计算


## 负二项式模型

- [一个博客](https://zhangzhenhu.github.io/blog/glm/source/%E8%B4%9F%E4%BA%8C%E9%A1%B9%E6%A8%A1%E5%9E%8B/content.html)

## Geographically Weighted Panel Regression GWPR 地理加权面板回归
```
https://cran.r-project.org/web/packages/GWPR.light/vignettes/introduction_of_GWPR.html
```
## Possion Distribution 泊松分布
这个教程很棒：  
```
https://www.ruanyifeng.com/blog/2015/06/poisson-distribution.html 
```

## 地理加权回归
- 一个很棒的教程,讲述了相关的原理以及实现,并附有相关实践
  - GWR就是不同区域都有一个OLS(可以这么理解),
    - 因为OLS是全局回归,肯定会有不好拟合的
      - 可以想象成椭球体,就几个参数
    - ,而GWR是由地理属性的,每一个地方的变量的回归系数都不一样,
      - 可以想象成重力模型,每个地方的都不一样
```
https://blogs.ubc.ca/cpotiergeob479/labs/lab-3-introduction-to-geographically-weighted-regression/ 
```

- Arcgis 的原理说明(包括参数选择)
GWR 可提供三种类型的回归模型：**连续、二进制和计数**。 在统计文献中，这些回归类型分别被称为**高斯、逻辑和泊松**。 应基于因变量的测量和汇总方式及其包含的值范围，为您的分析选择模型类型.
**连续（高斯）**
- 如果因变量可以采用温度或总销售额等**大范围的值**，则请使用**连续（高斯）模型类型**。 
- 理想情况下，因变量将是正态分布的。 您可以**针对因变量创建直方图**，以验证它是否为正态分布的。 如果直方图是**对称的钟形曲线**，则请使用高斯模型类型。 大多数值将聚类在均值附近，很少有值与均值完全脱离。 均值左边的值应该与右边的值一样多，所以分布的均值和中值相同。 
- 如果因变量似乎不是正态分布的，则请考虑将其重新分类为二进制变量。 例如，如果您的因变量是平均家庭收入，您可以将其重新编码为二进制变量，其中 1 表示高于国家收入中位数，0（零）表示低于国家收入中位数。 使用计算字段工具中的重分类帮助程序函数可以将连续字段重分类为二进制字段。

**二进制（逻辑）**
如果因变量可以采用两个可能值中的一个（如成功和失败，或者存在和不存在），则请使用二进制（逻辑）模型类型。 包含因变量的字段必须为数字且仅包含 1 和 0。 如果您将感兴趣的事件（例如成功或动物存在）编码为 1，则回归将模拟 1 的概率，因此结果将更容易解释。 全局和本地数据中的 1 和 0 必须存在变化。 如果针对因变量创建直方图，则它应该仅显示 1 和 0。 可以使用“按圆选择” 工具选择地图上的不同区域并确保每个区域中都存在 1 和 0 的组合，以检查局部变化。

**计数（泊松）**
如果因变量是离散的，并且表示事件的出现次数（如犯罪数量），则应考虑使用**计数（泊松）模型类型**。 如果**因变量表示一个比率，并且该比率的分母是固定值（如每月销售额或每 10,000 人口中患癌症的人数），则也可以使用计数模型**。 计数（泊松）模型假设因变量的均值和方差相等，并且因变量的值不能为负数或包含小数。
```
https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-statistics/how-geographicallyweightedregression-works.htm
```
中文版的
```
https://pro.arcgis.com/zh-cn/pro-app/latest/tool-reference/spatial-statistics/how-geographicallyweightedregression-works.htm
```
- 布里斯托的教程
  - OLS的一个假设就是每个地方的自变量和因变量之间的关系是相同的
  - 如果经过残差校验,发现残差有空间分布模式,那么就证明OLS的前提假设就不成立,意味着需要使用更加精确的算法.比如GWR.
  - GWR 背后的基本思想是探索因变量 (Y) 与一个或多个自变量 (X) 之间的关系如何在地理上发生变化。它不是假设单个模型可以适用于整个研究区域(比如OLS就这样)，而是寻找地理差异。
  - GWR,对于N个数据点的数据,会分析其中N个点,对于每一个点,会有一个搜索范围当搜索窗口位于样本点上时，它周围和搜索窗口内的所有其他点都会被识别。然后将回归模型拟合到该数据子集，为最接近中心点的点赋予最大权重.
    - 这里的搜索范围有两种定义
      - 实际地理距离
      - 邻居(比较常用,也被称之为**自适应窗口**)
  - 还需要看关系的聚类是否是偶然的
    - 如果是

```
https://www.bristol.ac.uk/media-library/sites/cmpo/migrated/documents/gwr.pdf 
```
