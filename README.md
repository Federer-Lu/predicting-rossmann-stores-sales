# predicting-rossmann-stores-sales
Uda数据挖掘毕业项目

### 概述
这个项目源自kaggle竞赛[Rossmann Store Sales](https://www.kaggle.com/c/rossmann-store-sales),我们需要根据Rossmann药妆店的信息（比如促销，竞争
对手，节假日）以及在过去2-3年的销售情况，来预测Rossmann未来6周的销售额。

我最终的RMSPE得分为***0.11077***，在Private Leaderboard中排名第***26***位，详见[kaggle排行榜](https://www.kaggle.com/c/rossmann-store-sales/leaderboard)

### 开发环境与所需工具
* 开发环境：Windows10, anaconda5.3.0, jupyter notebook5.7.2, python3.7

* 库：numpy, pandas, matplotlib, seaborn, time, lightgbm

### 数据集
此数据集可从[kaggle下载](https://www.kaggle.com/c/rossmann-store-sales/data)

### 方法
1. 数据预处理

* ‘CompetitionDistance’用均值填充，‘CompetitionOpenSinceMonth’、‘CompetitionOpenSinceYear’用临近值填充；

* 测试集中‘Open’字段填充为‘1’，其余缺失值填充为‘0’；

* ***将后六周数据***作为验证集，训练集中其它数据作为训练集。

2. 特征工程

* 将‘Date’字段拆分（加入***WeekOfYear***），新增‘CompetitionOpen’和‘PromoOpen’字段；

* 将‘PromoInterval’字段转化为数字特征‘IsPromoMonth’，将标签进行对数转换。

3. 模型训练与调优

* 使用lgb建模，重写rmspe函数并传入eval_metric，catogorical_feature参数、early_stopping_rounds参数的设置；

* 参数优化，偏差校正系数，模型融合（加权平均）。

## 总结与收获
1. 训练集与验证集划分方式的选择；

2. 时间类型特征的处理；

3. 偏差校正（尤其是***细致偏差校正***对结果提升明显），模型融合（加权融合略优于均值融合）。





