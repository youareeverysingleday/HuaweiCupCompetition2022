
[TOC]

# HuaweiCupCompetition2022

## environment

|编号|名称|版本|
|---|---|---|
|1|python|3.7.9|
|2|tensorflow|2.10.0|
|3|matplotlib|3.4.2|
|4|numpy|1.21.6|
|5|tensorflow_datasets|4.6.0|
|6|Fiona|1.8.20|
|7|geopy|2.2.0|
|8|jieba|0.42.1|
|9|keras|2.8.0|
|10|jupyter|1.0.0|
|11|Markdown|3.3.4|
|12|lightgbm|3.3.0|
|13|networkx|2.6.3|
|14|notebook|6.4.0|
|15|pandas|1.3.0|
|16|scikit-learn|0.24.2|
|17|seaborn|0.11.2|
|18|tensorboard|2.8.0|
|19|tensorflow-probability|0.16.0|
|20|xgboost|1.4.2|
|21|VSCode|1.70.3|
|22|keras-nightly|2.5.0.dev2021032900|
|23|scikit-opt|0.6.5|
|24|scipy|1.7.1|
|25|math|default|
|26|xlrd|2.0.1|
|27|pyecharts|1.9.1|
|28|DGL|0.9.0|

## 需要做的事情

## 题目分析

### A题

排除。

### B题

需要数学建模。主要是约束条件如何表达的问题。是否需要使用到拓扑学的概念还不清楚。
涉及的问题应该是液晶面板的切割问题。

1. 第一个子问题可能需要使用拉格朗日乘子法来实现条件的带入计算。
2. 第二个子问题不知道如何表达。

### C题

好像是一个有约束的图结构问题。每个节点和边都有约束条件，然后对整个图结构进行优化。具体专业知识不清楚。排除。

### D题

排除。好像是一个控制流程的问题。是有个专门的专业来研究流程优化的。具体专业课名称不记得了。

### E题

经纬度都是同一个位置的经纬度。115.375, 44.125

#### E数据概要分析：都需要修改文件名称

1. 附件1、锡林格勒草原概况 基本上没有意义。就只有几个统计数据可能需要保留。
   1. 草原总面积1920万公顷
   2. 草原地貌为高平原
   3. 海拔在800-1200米之间
   4. 地区年日照时数为2603.8h
   5. 年平均温度0.96℃
   6. 年均蒸发量1664.6mm/年
   7. 平均降雨量340mm左右
   8. 降水月际间变异较大，主要集中在6-9月份，约占全年降水量74.4%。
   9. 地带性土壤类型以栗钙土为主
   10. 植物群落以羊草(Leymus chinensis)群落和大针茅(Stipa grandis) 群落分布最广
2. 附件2、锡林郭勒统计年鉴（2016-2021） 中的数据都是PDF格式的，如何读取？
   1. 这数据应该是没法使用的，先看能不能导成word格式。失去意义了，太大了，压根没法处理。
3. 附件3、土壤湿度2022—2012年 都是特征数据，可以方便读取。
4. 附件4、土壤蒸发量2012—2022年 容易读取。
5. 附件5、绿植覆盖率（2020-2022）中所有的经纬度转换为地址的方法。
   1. 使用开源接口。
   2. 使用百度接口。已经连接。
6. 附件6、植被指数-NDVI2012-2022年 特征数据，容易读取。
7. 附件7、锡林郭勒土壤基本数据 是一个单行或者说单列的总体特征数据，需要修改一下格式。
8. 附件8、锡林郭勒盟气候2012-2022 数据都是特征数据，可以方便的处理。
9. 附件9、径流量2012-2022年 特征数据，容易读取。
10. 附件10、叶面积指数（LAI）2012-2022年 容易读取。
11. 附件11、一些历史数据  格式太乱，需要修改格式。
12. 附件12：内蒙古自治区锡林郭勒盟不同牧户生态畜牧业模式群落样方调查数据集
    1. 数据是按照年份-用户-不同草的类型-草的特征，四个维度来分的。格式需要处理。
13. 内蒙古自治区锡林郭勒盟不同示范牧户牲畜数量调查数据集（2018年7月28日-2020年9月30日）
    1. 是已经统计过的总体数据。
    2. 内蒙古锡林郭勒盟牧区进行入户调查
    3. 需要处理格式。
14. 内蒙古自治区锡林郭勒盟典型草原不同放牧强度土壤碳氮监测数据集（2012年8月15日-2020年8月15日）
    1. 特征数据，区分了年份-放牧小区（也就是位置）-放牧强度-特征。
    2. 需要处理格式。
15. 内蒙古自治区锡林郭勒盟典型草原轮牧放牧样地群落结构监测数据集（201
    1. 主要数据集。
    2. 数据量10881行。
    3. 特征数据。
    4. 需要处理格式。
    5. **放牧时间和方式对不同类型草和草相关特征的影响**。

#### 难点

1. ~~需要使用地图~~。
   1. 不需要使用，经纬度都相同。

#### E题目解读

1. 建立模型，不同模型。
2. 通过第一问，如何提炼/量化“放牧策略不变”。或者就不需要确定不变，直接预测就可以了。
3. 不同模型对要求进行预测。
4. 建立数学公式上的联系。形式化公式。将和问题3中的模型进行决策选择/权重选择之类的操作。
5. 没什么要说的，就是在“可持续发展”的条件下求牧羊的数量。也就是建立一个公式，然后求导数等于0的地方。然后确定是不是最大值。
6. 可视化。

#### 对应问题的解决思路

1. 泰勒展开
2. 时序预测
3. 定义优化函数和目标函数。
4. 还不太清楚，没明确思路。
5. 可能用拉格朗日乘子法来带入条件。
6. 可视化。

### F题

#### 数据分析

1. 附件1：长春市COVID-19疫情期间病毒感染人数数据。1是新增本土感染者，2是新增无症状感染者。
   1. 与时间相关的新增本土感染者和新增无症状感染者的数值型数据。
   2. 格式有些不规整需要调整。
2. 附表2：长春市9个区隔离人口数量与生活物资投放点数量。有个注释：注：上述九个区域是全市的部分区域，因此全市总计人数大于等于九个区域人数总和。
   1. 总体统计数据。数据非常简单。
   2. 格式需要调整。
3. 附件3：长春市9个区交通网络数据和主要小区相关数据
   1. 地理位置特征数据。应该可以建立基于位置的交通信息权重。
   2. 包含不同位置的经纬度信息。
   3. 格式需要处理。
4. 附件4：长春市疫情期间每日生活物资相关数据
   1. 数据非常复杂，格式严重混乱。
   2. 实际上主要是提取几个excel表格的数据，主要是把数据格式要处理好。
   3. 和时间序列相关的数据。
   4. 主要是3张表
      1. 1.XX月XX日长春市重点民生商品供应情况表(0316模板）
      2. 2.XXXX长春市生活物资保障体系基本情况表
      3. 111点调重点企业主要生活必需品价格情况表
5. 附件5：长春市疫情期间每日各区蔬菜包相关数据
   1. 格式相同。
   2. 排列混乱。主要就是处理数据。

#### 大致思路

解题思路

1. 题目：“病毒感染人数数据及其它附件数据或你们能搜集到的数据对长春市实行发放蔬菜包前后效果进行判别与分析”
   1. 理解为对数据特征的相关性进行分析。
   2. 先将新冠人数的变化趋势列出来，每个数据作为标签数据；然后将蔬菜包的各种特征数据作为输入变量。建立模型。分析数据之间的相关性。间接的相关性特征也可以。
2. 题目：
   1. “投放点数量的合理性分析，并做适当的优化”
      1. 这一个问题完全转化为了图结构下的节点（node prediction）问题。首先建图，然后对节点的特征进行embedding，然后在对节点的类别进行预测。
   2. “考虑未来疫情、自然灾害等特殊事件，对于政府储备物资和大规模物资分拣场所的位置与数量规模进行合理规划，并提出最优的选址数量、规模及其潜在的备用场所位置。”
      1. 在上一个问题的基础上，添加“未来疫情、自然灾害”的特征表示，然后重新对图结构模型进行训练，然后重新对节点进行预测。
      2. 在题目要求的情况下，通过$\Delta l$超参数的控制下，对题目要求的多个特征进行量化表述。**请务必将相关结果以表格的形式放置在正文中,其中主要参数包括选址位置及所属区域、选址半径、管辖范围小区个数及管辖范围内人口数等关键信息应该体现在表格中**
3. 题目：“**请依据附件5分析蔬菜包需求、发放规律**，并根据附件3中的各小区位置与人口信息，评价并调整4月10日至4月15日蔬菜包供应方案”
   1. 对蔬菜包的需求和发放做一个分析。也就是做供需关系分析。
      1. 这个问题和问题2和问题4并不直接相关。而是做的一个特征分析问题。
   2. 调整方案，基于第2问对模型做一个改进。在模型中可以把需求和供给加上去。需求和供给可以通过采购来源地进行等特征进行调整。
      1. 这个问题和问题2和问题4并不直接相关。而是做的一个特征分析问题。
4. 题目：
   1. “特殊时期保障居民生活物资供应的详细预案（有序网络图）”。第2问和第3问只是做一个整体的分配数量即可。
      1. 实际上是一个图结构划分的问题，也就是一个图的路径相似度推荐问题。使用deepwalk算法来找出相似度相似的路径完成推荐。
   2. “请进一步考虑用卡车运送物资，大卡车每辆可装10吨，小卡车每辆可装4吨,观察预案有无显著不同”
      1. 添加超参数变量，增加一个边上的权重特征。然后对图模型重新训练，然后比较前后生成的节点类型矩阵的差异度。

#### 麻烦的地方

1. 附件中的数据格式严重不统一。表达相同内容文件中的数据单元的格式也严重不一致。
2. 没有使用公开的经纬度，使用的是虚拟经纬度。所以无法使用很多已经开源的地理信息处理库，只能人工手动处理。
