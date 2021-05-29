# 3-2 分布式语义：Term-document矩阵（count-based）

## Count-based approach：Term-document matrix
 基于计数的方法：术语-文档矩阵
● If word *u* appears in document *d*, *d*is a context of *u*

	1. Collect许多文档(from, e.g. Wikipedia)
	2. 数一数词u和文档d共同出现了多少次
	3. 词u的meaning是一个向量[count(u,d1), count(u,d2), …]
	
	![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/page3image3830240.png)
	ps: 这里的列指的是Shakespeare plays
 
### Term-document matrix：Document vectors
有两种方式从矩阵中提取信息
	1. ::Column-wise：一个文档用一个|V|-dim向量来表示(V: 词汇量)::
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.33.00.png)
	广泛应用于信息检索：
		* 查找相似文档 find similar documents 
		* 查找接近查询的文件 find documents close to a query 

	* 查找相似文档：
	Two documents that are similar will tend to have similar words
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.34.08.png)
	* 查找close to a query的文档
	Consider a query as a document
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.34.54.png)

	2. ::Row-wise：一个单词由|D|-dim向量表示(D:文档集)::
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.36.37.png)

## Count-based approach：Term-term matrix
* 我们以前见过（共同出现向量Co-cocurrence vectors）：统计一个词u和一个词v一起出现的次数
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.39.20.png)

### Count-based approach：raw frequency is bad 原始的频率是不好的
	* 并不是所有的contextual words都一样重要
	* 哪些词是重要的，哪些不是？
		* ~不常见的词比常见的词更重要~
		* ~相关的词比不相关的词更重要~
		* …
-> weighing schemes（TF-IDF, PMI, …）
>   
> hbx: 所以要将原市的频率处理为TF-IDF频率  
>   
### 单词重要性的评估方法: TF-IDF (for term-document matrix)
给单词分配权重：使用TF-IDF
	* tf (term frequency)：frequency count
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.53.24.png)
	* idf (inverse document frequency)：popular terms (terms that appear in many documents) are down weighed 热门词汇（出现在很多文档的词汇）权重会降低
		* [逆文档频率_百度百科](https://baike.baidu.com/item/%E9%80%86%E6%96%87%E6%A1%A3%E9%A2%91%E7%8E%87/11018305)
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.56.24.png)
	* TF-IDF：
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.57.17.png)

![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.59.15.png)
- - - -
> TF-IDF（用以评估一字词对于一个文件集或一个语料库中的其中一份文件的重要程度。字词的重要性随着它在文件中出现的次数成正比。  
>   
> TFIDF的主要思想是：如果某个词或短语在一篇文章中出现的频率TF高，并且在其他文章中很少出现，则认为此词或者短语具有很好的类别区分能力，适合用来分类。  
>   
> TFIDF实际上是：TF * IDF，TF词频(Term Frequency)，IDF反文档频率(Inverse Document Frequency)。  
> TF表示词条在文档d中出现的频率。  
>   
> IDF的主要思想是：  
> 		如果包含词条t的文档越少，也就是n越小，IDF越大，则说明词条t具有很好的类别区分能力。  
> 		如果某一类文档C中包含词条t的文档数为m，而其它类包含t的文档总数为k，显然所有包含t的文档数n=m+k，当m大的时候，n也大，按照IDF公式得到的IDF的值会小，就说明该词条t类别区分能力不强。  
>   
> 但是实际上，如果一个词条在一个类的文档中频繁出现，则说明该词条能够很好代表这个类的文本的特征，这样的词条应该给它们赋予较高的权重，并选来作为该类文本的特征词以区别与其它类文档。这就是IDF的不足之处。  

* TF-IDF 计算公式：
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.57.17%202.png)
其中：
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.53.24%202.png)
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2010.56.24%202.png)

![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-05-25%2013.05.07.png)
Pratical - Question 20，



- - - -

### Count-based approach：so many 0s
![](3-2%20%E5%88%86%E5%B8%83%E5%BC%8F%E8%AF%AD%E4%B9%89%EF%BC%9ATerm-document%E7%9F%A9%E9%98%B5%EF%BC%88count-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2011.04.12.png)
	* 虽然许多单词组应该有>0的counts，但是由于缺少数据（数据稀少），它们对应的矩阵项是0
	-> 拉普拉斯平滑：每一个条目上加1（伪数 pseudocount）
> 为了缓和这种情况，有的人会在矩阵上加上一些smoothing methods   

### 使用这些count-based approach, term-document matrix的优点
	1. Simple and intuitive ::简单和符合直觉的::
	
	2. 维度是有意义的(e.g. 每一个维度都是一个文档或一个语境词)
	Dimensions are meaningful (e.g. each dim is a document / a contextual word 
	-> ::更易于debug和解释::

### 缺点
	1. ::词/文档向量是sparse稀疏的（dims为|V|，词汇量大小，或|D|，文档数量，通常从2k到10k）→对机器学习算法来说是困难的::
	
	2. ::在一个特定的语境下要如何表示词的meaning？::

从稀疏的向量到密集的向量 From sparse vectors to dense vectors 
	* 采用降维 dimensionality reduction（如潜在语义分析--LSA）
	* 使用一个不同的方法：prediction (coming up next)
