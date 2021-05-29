# 3-1 分布式语义：word-word矩阵（count-based）
## 学习计划
1. Distributional Semantics 分布式语义

2. Word Embeddings 词嵌入
	* Count-based approach 

	* Brief introduction to neural networks 

	* Prediction-based approach 

3. Word Sense Disambiguation 词义消歧

4. Lab Exercise 3 Overview 

5. Introduction to Coursework 1 
- - - -
##  学习目标
1. 理解词汇语义学（lexical semantics）、分布语义学（distributional semantics）、词义消歧（word sense disambiguation）的概念及其在NLP中的重要性。
2. 了解基于术语-文档矩阵、术语-术语矩阵和简单神经网络的几种词向量模型的思想和机制。
3. 能够将词嵌入可视化（例如调试）。 
- - - -
我们是如何学习一个新词的？
* 查字典
* pointing to an object by images

## 分布式语义
* 在week3的第一个video中，老师用了很多例句举例我们是如何认识一个单词的。大意其实就是，我们是通过语境来认识一个新词的
* 词的meaning其实就是它在语言中的使用
* 如果一个新词和一个旧的词在使用上是没有区别的，那么computer is called fool 也无所谓
	*  How to make ~computers~ smart? 
	* How to make a ~fool~ smart? 

### 分布式假说（history, cont.）

* 如果A和B的环境几乎相同，我们说它们是同义词。Zellig Harris(1954)
* 我们将通过它的同伴来了解一个词。We shall know a word by the company it keeps. Firth (1957)
  
### 分布式假说 Distributional hypothesis (formalisation)
给定一个词w，及和它一起出现的所有语境contexts C(w) = {c1, c2, …}
那么就有：
`meaning(w) = f(c1,c2,...)`
其中f是将C(w)的一些统计量压缩成一个向量的函数
The ultimate goal: find f !

那么我们要如何learn和define f呢？
一个方法是使用word-word matrixes，也叫作Co-occurrence vectors

#### Co-occurrence vectors：也叫作 word-word matrixes
（ 共同出现向量：词-词矩阵）
Steps:
1. Collect 许多文档/句子(from, e.g. Wikipedia)
![](3-1%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9Aword-word%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2009.43.56.png)
2. 应用基本的预处理步骤：lowercase, tokenisation, lemmatisation 小写、符号化、词法化
3. 数一数词u和词v共同出现了多少次
![](3-1%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9Aword-word%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2009.45.35.png)
4. 词u的meaning是一个向量 [count(u,v1), count(u,v2), …]
![](3-1%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9Aword-word%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2009.46.36.png)

#### 优点（having these vectors的优点）
词的含义用一个向量（命名为词向量）来表示，所以
	1. **我们可以计算出词义之间的相似性（similarities）**
![](3-1%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9Aword-word%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2009.50.57.png)
如果一个维度是pie，一个维度是computer，我们可以发现digital和information的角度很接近
要判断两个单词的相似度，我们可以使用余弦夹角来表示，角度越小，相似度越高

	2. **我们可以将单词的含义可视化（visualise word meanings）**
![](3-1%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9Aword-word%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/page17image545264.png) 
[Demo: word visualisation](https://projector.tensorflow.org)

	3. **我们可以直接将单词作为大多数机器学习算法的输入内容**

#### 缺点（使用分布式语义向量 Distributional Semantics vectos的缺点）
1. whether those distributional semantics can present or can capture the semantic beyond the words？
这些分布式语义是否能够呈现或能够捕捉到词语之外的语义？

2. 分布式语义学能不能抓住语义学的所有方面？


### SUMMARY
* 分布式语义源于分布式假说 
	* Tell me who your friends are, I’ll tell you who you are 

* A word is represented by a co-occurrence word vector 
一个词用一个共同出现词向量表示

* Pros: 共同出现词向量可以用来:
	* 检测词之间的相似性
	* 词义可视化
	* 输入到机器学习模型

* Cons:但它们真的能抓住所有语义学的所有方面吗？它们能捕捉到语义之外的东西吗？
 
 
