# 2 - 4 关系抽取 Relation extraction

# Relation extraction
* 关系抽取就是辨别本中实体之间的关系
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2013.34.40.png)

## 关系的类型：预定义
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2013.38.18.png)

## 关系抽取的方法
* ::Pattern-based 基于模式的关系抽取::
* ::Statistical/machine learning-based 基于统计学/机器学习的关系抽取::

### 基于模式pattern的关系抽取
	* ::使用正则表达式::
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2013.42.02.png)
可以通过修改Regex来加入实体约束，但这也可能存在问题，它会漏掉：
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2013.43.44.png)
#### 如何减少假阴性
两个选择：
	* 放松pattern（略过特定的词）
	* 扩展pattern集（同时保持准确度）

![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-05-25%2010.26.21.png)


## 步步为营法  Bootstrapping （基于pattern的关系提取）
	1. 从一组小的seed patterns和seed tuples开始
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2013.50.26.png)
	2. 在文档语料库中搜索seed tuples中的元组
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2013.56.19.png)
	3. 使用查询结果来提取新模式patterns
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2013.58.40.png)
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2013.59.17.png)
4. 使用新patterns来搜索额外的tuples（来扩展tuple集）
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2014.02.32.png)

## 基于机器学习的关系提取
### 子任务1：两个实体是否都参与到一个关系中？
	* 一个binary分类任务
	* 正examples：实体被annotated为相关的
	* 负examples：(一个句子中的)实体没有被annotated为相关的

### 子任务2：什么类型的关系成立？
	* 一个多类分类任务
	* 一些方法结合/联合学习子任务1（包括一个 no_relation类）
	* 特征类型：
		* 已命名的实体特征：entity type，head word
		* 语境context：words between, words before the first entity, words after the second entity (within a fixed window)
		* 语法结构：依存路径 dependency paths
#### 依存路径 Dependency Paths
在基于机器学习和基于模式的关系提取中都很有用
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-02-19%2014.14.52.png)

## 模型评估方法
### 1. Kappa coefficient（Kappa系数）
Kappa系数是一个用于一致性检验的指标，也可以用于衡量分类的效果。因为对于分类问题，所谓一致性就是模型预测结果和实际分类结果是否一致。
kappa系数的计算是基于混淆矩阵的，取值为-1到1之间,通常大于0。
[kappa系数简介 - 知乎](https://zhuanlan.zhihu.com/p/67844308)

* Kappa = (pa-pe)/(1-pe)
其中：
	* acc，pa = 正对角线元素之和 / 总元素和 

	* pe = 所有类别分别对应的“实际与预测数量的乘积”，之总和，除以“样本总数的平方”。
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-05-25%2010.34.17.png)
e.g.1
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-05-25%2010.36.11.png)
e.g.2
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-05-25%2010.38.05.png)


### 2. Precision and Recall 精确率和召回率
* 精确率：正确且被注释的，在所有被注释的中的比例
* 召回率：正确且被注释的，在所有正确的中的比例（不管是否注释）

* TP：被模型预测为好瓜的好瓜（是真正的好瓜，而且也被模型预测为好瓜）
* TN：被模型预测为坏瓜的坏瓜（是真正的坏瓜，而且也被模型预测为坏瓜）
* FP：被模型预测为好瓜的坏瓜（瓜是真正的坏瓜，但是被模型预测为了好瓜）
* FN：被模型预测为坏瓜的好瓜（瓜是真正的好瓜，但是被模型预测为了坏瓜）

![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-05-25%2010.42.13.png)
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/v2-129d7b63bb994ca0a708b67d3fbe34ee_1440w.jpg.png)
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/8BFF30A0-0674-4C85-9571-BCADFFBD1175.png)


### 3. F-score，也称为F-measure，或F1-score
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-05-25%2010.43.44.png)
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-05-25%2010.44.06.png)

### 4.  多分类评价指标：微平均 vs 宏平均
宏平均（Macro-averaging）和微平均（Micro-averaging）

* 宏平均：Macro-averaging
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-05-25%2010.45.59.png)
	* 先平均一下多个类别的P和R，然后再用P和R算F1-score

* 微平均：Micro-averaging
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/%E6%88%AA%E5%B1%8F2021-05-25%2010.48.48.png)
	* 重新计算多类别的P和R，然后再计算F1-score



* 比较：
	* 宏观平均法**不考虑**class的不平衡性。
	* 微观平均法对不平衡**不那么敏感**

	* 加权平均
		* 根据每个类别的真实实例数量加权的平均数











- - - -
# 补充：
# 一、简介
* 关系抽取就是从文档中抽取关系（实体之间的关系），例子如下： 
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019101242829.png)
* 为什么进行关系抽取
	* 创建新的关系型知识库（knowledge bases）
	* 增强目前的知识库（knowledge bases）
	* 支持问题回答（question answering）
* 一些例子
	* 自动内容抽取（Automated Content Extraction (ACE)）
		* 2008年关系抽取任务的17种关系
		* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019101915552.png)
		* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019102045225.png)
	* UMLS: Unified Medical Language System
	* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019102400101.png)
	* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019102454407.png)
* 如何建立关系抽取器
	* 人工定义的模式
	* 有监督的机器学习
	* 半监督与无监督
		* 利用种子（seed）进行bootstrapping
		* 远程监督（Distant supervision）
		* 从网页进行无监督学习
# 二、利用模式（pattern）进行关系抽取
# 1、抽取is-a关系的规则
* X和Y相似的语句规则
* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019104721700.png)
# 2、利用规则抽取更丰富的关系
* 主要思想：关系永远发生在特定实体之间，所以我们使用命名实体标签（named entity tag）来帮助我们进行关系抽取。
* 例子：比如说谁在什么组织做什么事情？
* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019105156990.png)
# 3、人工建立关系模式
* 优点
	* 人工模式会更精确（high precsion)
	* 可以根据特定领域进行修改
* 缺点
	* 人工模式的recall很低
	* 需要花工作来考虑所有可能的模式
	* 但是不要对所有的a都使用这种方法
# 三、监督型关系抽取
# 1、监督型关系抽取的机器学习流程
* 选择一些我们想要抽取的关系
* 选择一些相关的命名实体
* 寻找并标记数据
	* 选择一个有代表性的语料库
	* 在语料库标记命名实体
	* 人工标注这些实体之间的关系
	* 将它分成三个部分（train,development,test)
* 在训练集上训练分类器
	* 找到所有的命名实体对（通常在同一个句子中）
	* 判断两个实体是否相关
	* 如果是的话，就对关系进行分类
	* Question：为什么要分两步来进行分类？
		* 分类训练会比较快，因为第一步会排除大部分的无效对
		* 对每个任务都可以使用合适的特征集
# 2、特征构建
任务：对在一个句子中的两的关系进行分类
![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/2018101911320417.png)
* M１和M2的中心词，以及两者的结合 Airlines，Wagner，Airlines-Wagner
* M1和M2的词袋以及二元组　American, Airlines, Tim, Wagner, American Airlines, Tim Wagner
* M１和M２左边和右边的单词　M2: -1 spokesman，M2: +1 said
* M１和M２中间的单词的词袋和二元组（bigram）a, AMR, of, immediately, matched, move, spokesman, the, unit
* 命名实体的类型　M1: ORG M2: PERSON
* 两个命名实体之间关联：ORG －PERSON
* Ｍ１和M２的实体层级（entity level）一共三类（NAME，NOMINAL-比如the company，PRONOUN-比如it 和这样的代词）：M1 NAME，M2 NAME
* 两个实体之间的单词的基本语法块（syntactic chunk词性序列：NP NP PP VP NP NP
* 两个实体之间的树的成分路径（constituent path）：
* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019132114393.png)
* 依赖路径（dependency path）：Airlines matched Wagner said
* 关于家庭的触发清单（trigger list）：亲戚关系词 parent, wife, husband, grandparent, etc. [from WordNet]
* gazetter：有用的地理词列表，国家名字以及其他子实体名字
# 3、有监督方法的分类器
* 可以使用任何分类器：最大熵、朴素贝叶斯、SVM
* 在训练集上训练，在发展集上调试，在测试集上测试
# 4、有监督关系抽取的评估
* 为每个关系计算precision，recall以及F1
# 5、总结
* 优点：如果有足够的手工标注的数据，并且测试集和训练集相似的话，可以得到很高的正确率
* 缺点：标注大量的训练集是很贵的；有监督模型对其他的类型的泛化能力不足
# 四、半监督或者无监督关系抽取
# 1、关系bootstrapping(Hearst 1992)
* 收集一些关系为R的种子对（seed pair）
* 迭代
	* 找到有这些单词对的句子
	* 找到这些单词对的上下文，泛化成模式（pattern）
	* 找到新的单词对
* 例子1
* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019142319900.png)
* 例子2
* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019142602695.png)
# 2、滚雪球法（snowball）
* 参考文献：E. Agichtein and L. Gravano 2000. Snowball: Extracting Relations
* 和上面的方法一样的迭代算法
* 也和上面一样利用例子（instance）抽取特征，但是不同的是X和Y都必须是命名实体，并且为每个模式计算置信度。
* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019143100919.png)
# 3、远程监督（distant supervision)
* 参考文献
* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019144601129.png)
* 远程监督的思想：假设一个句子包含某对实体，那么这个句子应该蕴含了两个实体间的关系（Freebase中罗列的关系之一），可以将这个句子作为该实体对所对应关系的训练正例。（引自https://blog.csdn.net/wen_fei/article/details/80500654?utm_source=blogxgwz1）
* 
* 具体步骤：
	* 对每个关系（relation）中的每一对元组，在语料库中找到同时包含这两个实体的句子
	* 抽取高频的特征（语法分析、单词等）
	* 用这些模式来训练监督模型
	* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/2018101914533745.png)
# 4、无监督关系抽取
* 参考文献：M. Banko, M. Cararella, S. Soderland, M. Broadhead, and O. Etzioni. 2007. Open information extraction from the web. IJCAI
* 开放信息抽取：在没有训练数据和关系列表的情况下，从网页中抽取关系
	* 利用语法数据（parsed data)训练一个“值得信任的元组”的分类器
	* 抽取所有名词短语之间的关系，并且如果分类器认为值得信任的话，就将之保留
	* 基于这种关系出现的频率来对该关系排序
# 5、对无监督和半监督的评估
* 因为它抽取的都是来自网页的新关系，因此我们无法计算precision（不知道哪些是正确的）和recall（不知道那些是错过的）
* 我们只能大致计算一个precision。计算的方法是，从结果中随机抽取一些关系，人工来判断这些关系是否是正确的。正确关系数比上总的关系数就是估计的precision。
* ![](2%20-%204%20%E5%85%B3%E7%B3%BB%E6%8A%BD%E5%8F%96%20Relation%20extraction/20181019150946835.png)
* 我们也可以基于不同水平的recall来计算precision
	* 前1000个新关系，前10000个新关系，前100000个新关系的precision
	* 每一种都进行随机取样
* 但是没有办法进行recall评估