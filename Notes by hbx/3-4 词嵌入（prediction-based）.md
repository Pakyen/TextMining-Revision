# 3-4 词嵌入（prediction-based）

## 复习
* Two major count-based approach methods: term-document matrix and term-term matrix 

* Raw frequency is bad 
	* Using weighing schemes to “correct” counts 

	* Using smoothing to take into account “unseen” events 

## Formalisation
假设:
	* 每个词w ∈ V由矢量v ∈ R^d表示（d通常小于3k）。
	* 有一种机制可以计算目标词w出现在语境（u1，u2，...，ul）中的事件概率Pr（w|u1，u2，...，ul）。
 
任务：
	为每个单词w找到一个向量v，使这些概率对于每个w及其上下文(u ，u ，......，u )尽可能高

> 我们使用参数θ的神经网络，通过最小化交叉熵损失来计算概率（cross-entropy）  
![](3-4%20%E8%AF%8D%E5%B5%8C%E5%85%A5%EF%BC%88prediction-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2011.51.27.png)

## 2003年的language modelling
	* language modelling：从前m-1个的词中预测下一个词 Pr(wt|wt-1,...,wt-m+1)
	* 每一个词w都用一个向量v表示
![](3-4%20%E8%AF%8D%E5%B5%8C%E5%85%A5%EF%BC%88prediction-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2011.53.54.png)

## 2013年：连续词袋模型CBOW（continuous bag of words)
从周围的词中预测一个词（一个语境是目标词wt的前m个词和后m个词）
![](3-4%20%E8%AF%8D%E5%B5%8C%E5%85%A5%EF%BC%88prediction-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2011.56.27.png)

## Benigo et al.(2003) vs. CBOW
* 两个模型看起来很相似
* 然而他们使用的语境类型不同:
	* Bengio等人（2003年）在目标词前使用m-1个词→语言建模（根据历史预测下一个词）；
	* CBOW在目标词前和目标词后各使用m个词（即2m个词的窗口）。
* CBOW更简单，因为它少了一层

## Mikolov et al. (2013)另一个model: Skip-gram 
* 预测给定target word的周边词
每一个target wird用一列矩阵W_in表示
y = w_t
然后在y上使用softmax函数，得到结果
![](3-4%20%E8%AF%8D%E5%B5%8C%E5%85%A5%EF%BC%88prediction-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2011.57.48.png)
* 当我们对比Skip-gram model和CBOW model，我们可以发现它们使用了不同的策略：Skip-gram model预测的是 contextual words而不是target word
![](3-4%20%E8%AF%8D%E5%B5%8C%E5%85%A5%EF%BC%88prediction-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2011.57.58.png)
而且我们可以发现，Skip-gram model和CBOW model是很相关的。

## word2vec
如果搜索word to vectors，很多人用的都是skip-gram
* Skip-gram model 

* “a baby step in Deep Learning but a giant leap towards Natural Language Processing” 因为用word -> vector，我们可以取得很多成就in NLP

* can capture linear relational meanings (i.e., analogy): 
可以捕捉到可以获取线性关系的含义
			`king - man + woman = queen`

![](3-4%20%E8%AF%8D%E5%B5%8C%E5%85%A5%EF%BC%88prediction-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2012.05.50.png)
![](3-4%20%E8%AF%8D%E5%B5%8C%E5%85%A5%EF%BC%88prediction-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2012.05.58.png)
## word vectors的问题
然而，word vectors也存在一些问题，如果数据是biases的，结果也会是biases的
	* 词嵌入是从数据中学习出来的 → 它们也能捕捉到隐含在数据中出现的偏差
	* 性别误差：
		* ‘computer_programmer’更接近于’man’而不是’woman’
		* ‘homemaker’更接近于’woman’而不是’man’
	* 种族误差：
		* African-American names与不愉快的单词联系在一起（比起其他族裔，他们的名字更容易让人产生厌恶感）
	* …
→ 去除词嵌入的偏见（误差）是一个热点（也是非常需要的）研究课题
 
![](3-4%20%E8%AF%8D%E5%B5%8C%E5%85%A5%EF%BC%88prediction-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2012.10.56.png)

## 处理未知词汇
* 很多词都不在字典里
* 每天都有新词被发明出来
* 解决办法1：对所有未知词使用特殊标记`#UNK#`
* 解决办法2：用字符/子字代替单词。
字符(‘c-o-m-p-u-t-e-r’ instead of ‘computer’)
子词(‘com-omp-mpu-put-ut-ter’ instead of ‘computer’)
 
##  特定语境下的词嵌入
* 一个词单独存在的意义可能与它在具体语境中的意义不同。
	* He lost all of his money when the ~bank~ failed. 
	* He stood on the ~bank~ of Amstel river and thought about his future. 
* Solution：
![](3-4%20%E8%AF%8D%E5%B5%8C%E5%85%A5%EF%BC%88prediction-based%EF%BC%89/%E6%88%AA%E5%B1%8F2021-02-22%2020.29.09.png)
* Solution 1： f对于c来说是连续的（contextual embeddings, e.g. ELMO, BERT, -week4学习）
* Solution 2： f对于c来说是离散的（e.g. word sense disambiguation - 下一节介绍）
- - - -
## 总结
* Prediction-based approaches require neural network models, which are not intuitive as count-based ones 

* Low dimensional vectors (about 200-400 dimensions) 

	* Dimensions are not easy to interpret 
* Robust performance for NLP tasks 
 
