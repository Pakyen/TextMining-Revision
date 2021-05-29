# 3-5 语义消歧 Word Sense Disambiguation（WSD)

## 复习
* 介绍了两种学习词嵌入的方法
	* 一种count-based，
	* 一种prediction-based
* 简要介绍神经网络，以及如何使用神经网络来学习单词嵌入
* word2vec
 

## 词义 word senses
* 我们假设每个词都有一个meaning/sense
* 事实上，一个词可以有多种senses
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2021.17.04.png)
* 如何定义词义？WordNet
* 如何预测词义？Knowledge-based 和 supervised learning-based methods

## WordNet: A Database of Lexical Relations 
WordNet: 词汇关系数据库
可以找到很多信息，像词典一样，但是在WordNet里面没有发音pronounciation
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2021.21.23.png)
supersenses 超义词
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2021.24.36.png)
sense relations 
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2021.25.22.png)
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2021.32.29.png)

## 语义消歧WSD的方法
### Task definition
* Input:
	* Word in a context 语境中的词
	* A fixed inventory of potential word senses 潜在词义的固定清单
* Output:
	* 根据上下文，正确的词义是
* Two main types:
	* Lexical sample task 词法样本任务
	* All-words tasks：similar to part-of-speech tagging 
	全词任务：类似于词性标签

## Lesk algorithm (Lesk, 1986): WSD baseline 
* 直觉：选择与目标词相近的词的字典解释或定义最相似的词
* Formalisation 形式化
	* 目标词: w
	* w的语境词: w_j（下标）
	* 词义的词汇定义：D(.)
	* 一个词的一组意思：S(.)

* 规则：
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2021.44.17.png)
sim表示similarity，这个公式的意思就是将similarity最大化
* Possible similarity measures 
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2021.48.12.png)


## 举例（如果求similarity between two set)
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2021.49.28.png)

输入句子： ~Waves~ were ~hitting~ the ~steep~ bank.
Bank的senses：
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2021.52.56.png)

语境定义：
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2022.00.45.png)
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2022.01.01.png)

## Lesk algorithm(Cont.)
* Pros：
	* 容易实现
	* 不需要训练数据
* Cons：
	* 并非所有的单词在WordNet中都有定义
	* 需要处理模棱两可的语境词
	* 业绩不佳

##  监督学习：all-word WSD
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2022.07.15.png)

## Feature-based WSD 
* 使用具有多种特征的SVM
	* 语音部分标签
	* 词和n-gram的搭配特点
	* 词语嵌入的加权平均数(一个窗口中所有词语的加权平均数)
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-22%2022.08.54.png)

## Summary 
* WordNet是英语词汇关系的大型数据库 

* WSD的任务是根据上下文来确定一个词的正确意义 

* SemCor 是最大的带有WordNet标签的语料库

* Lesk algorithm, WSD基线，是一种基于知识的方法

* 基于特征的算法，在目标词的上下文中使用部分语音和嵌入词，效果很好

 
- - - -
## WordNet搜索
[WordNet Search - 3.1](http://wordnetweb.princeton.edu/perl/webwn)
可以在WordNet Search中搜索词汇，
可以看到一个词的hyponym等

* hypernym：超名词是指一个包括其他词在内的广泛类别的名称
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-23%2012.19.37.png)
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/5ABD709E-1B98-426B-BC02-0EB4324161A4.png)
![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/35F95FD8-628C-46C6-81EA-0DB5A5CA139B.png)



![](3-5%20%E8%AF%AD%E4%B9%89%E6%B6%88%E6%AD%A7%20Word%20Sense%20Disambiguation%EF%BC%88WSD)/%E6%88%AA%E5%B1%8F2021-02-23%2012.21.07.png)