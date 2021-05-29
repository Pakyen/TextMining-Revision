# 4-1 to 4-3 Deep Learning

# 4-1 Overview
## Data-driven approaches
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2010.42.56.png)
* 输入：Sequence of tokens(text)
* 可能的任务 Possible tasks：
	* 分类序列（Classify sequence)
	* 标记tokens
	* 生成另一个sequence
	* 从输入中提取token范围
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2010.46.03.png)

* 学习representation的方式：
	* 传统ML：
		* decide on features (expert knowledge) 
		* learn their weight from training data 
	* 深度学习：
		* Learn to extract features from raw input (text, image, audio) 
	 
* Data
	* 现在，我们先不关注这个表征是如何学习的（我们以后会仔细研究）。
	- 简化假设：假设我们将一个NLP任务表达为一组文本输入和预期输出的方式。
	→ 神经网络将学习底层的统计模式，以成功完成任务。
	(提供足够强的信号，有代表性的训练数据，还有很多很多)
	- 我们如何将NLP任务表示为输入/输出对？

*  NLP作为时间序列分析
	序列=时间序列
	时间序列 = 数据点，按时间顺序索引 
	数据点 = 文本中的单词
	时间顺序=文本中出现的顺序

我们将关注：
	- 序列分类
	- 序列标记
	- 序列提取
	- 序列到序列的翻译
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2010.59.54.png)
	 
* 序列分类：
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2010.56.24.png)

* 范围提取（提取序列中每一个token可能的出现和结束范围）
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2010.57.21.png)

* 序列标记（对每一个token，标记他们可能属于的分类）
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2010.57.56.png)

* Sequence to sequence：到目前为止，给定输入输出序列下一个单词的概率分布
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.02.26.png)



# 4-2 Representing & Processing Sequences
分布式表示+神经网络+SGD+反向传播=深度学习
幸运的是，它的大部分已经实现，并准备好与现代DL框架一起使用。
→ Torch、Tensorflow等

## From words to numbers
我们如何获得向量x作为神经网络的输入？
Naive solution：bag of Words Vector
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.10.49.png)

 But -> Bag of words表示损失了单词之间的顺序（一定要有顺序，不然语义不通）
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.12.06.png)

##  Recurrent neural networks 循环神经网络/递归神经网络
* 粗略的想法
	* Feed network token by token
	* 在处理当前token时，用上一个token的输出作为额外的输入
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.14.11.png)
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.15.41.png)
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.15.56.png)
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.16.11.png)
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.16.41.png)

## LSTM：上下文向量
* 上下文，或内存向量C_t，除此之外还有h_t
- 来自 "过去 "的背景信息  计算
- 在任何一个步骤t，LSTM都会学习到有多少的h_t被加到C_t中，还有会学习到有多少的C_t-1被保留
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.18.58.png)

## GRU
* 类似的想法，但参数较少
- 与LSTM性能相似
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.19.45.png)



## RNN:回顾
现在我们可以用RNN做什么？

have包含 "过去 "信息的词的向量表示（左）。

从现在开始，RNN=RNN/LSTM/GRU


## BiRNN
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.21.24.png)
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.23.52.png)
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.24.09.png)
![](4-1%20to%204-3%20Deep%20Learning/%E6%88%AA%E5%B1%8F2021-03-01%2011.24.56.png)

### 计算图
Draw a computational graph of sorts, maybe of an NN or of a simple computation, depending on what makes more sense  

### 损失函数
For example: cross entropy  

### 随机梯度下降
其背后的直观感受是什么
 
### 反向传播
从总误差到节点的误差
 
 
# 4-3  语境化词语嵌入 Contextualised Word Embeddings

<a href='3%20-%20Language%20models%20&%20DL%20Problems.pdf'>3 - Language models & DL Problems.pdf</a>