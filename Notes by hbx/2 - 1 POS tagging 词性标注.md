# 2 - 1 POS tagging 词性标注

参考：
[斯坦福大学-自然语言处理入门 笔记 第十二课 词性标注（Part-of-speech tagging）_苏三慎的博客-CSDN博客](https://blog.csdn.net/kunpen8944/article/details/83241051)

[词性标记缩写集](https://blog.csdn.net/u010099495/article/details/46776617?utm_source=blogxgwz0)
- - - -
## NLP Pipelines
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/%E6%88%AA%E5%B1%8F2021-02-16%2016.32.34.png)

- - - -
POS Tagging就是给每一个token分配词性

## 一、Part of Speech Tagging 词性标注
* 词性 Part of Speech：
	* 名词 Nouns
	* 代词 Pronouns
	* 动词 Verbs
	* 形容词 Adjectives
	* 副词 Adverbs
	* 限定词 Determiners
	* 连接词 Conjunctions
	* 介词 Prepositions

* 词性可以分为：
	1. 开放类 open class
	2. 闭合类 closed class
	
其中，闭合类只有一些固定的词，不会再增加其他的词，如：
	* 限定词(determiners)：a, an, the
	* 代词(pronouns)：she, he, I
	* 介词(prepositions)：on, under, over, near, by

而开放类的词是会增加的，包含：
		* Nouns, Verbs, Adjectives, Adverbs

这些类还可以细分为其他小类：
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/6F2AAF8D-49E7-4159-8C77-1BAAD203E24D.png)
一个单词可能有不止一个词性，如back（见下图）。所以所谓的词性标注是指在具体上下文环境中的单词的词性标注:
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/918EFD4A-A112-42E5-80A5-7A3F48F898E8.png)

# 二、词性标注（Part-of-speech tagging）
### 词性标注是什么
* 将POS tags分配给各个token
* 通常在这之前会先进行分词（Tokenisation)（虽然有些方法是将Tokenisation和POS tagging同时进行的）
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/%E6%88%AA%E5%B1%8F2021-02-17%2013.58.27.png)
词性标注就是对具体的句子中的单词进行标注，例子如下
	* 输入：Plays well with others
	* 输出：Plays/VBZ well/RB with/IN others/NNS
	* 这里使用的词性标记叫做Penn Treebank POS tags。具体的词性标记缩写和对应的介绍，可以查看这个博客（ [(自然语言处理文档系列)Penn Treebank词性标记集](https://blog.csdn.net/u010099495/article/details/46776617?utm_source=blogxgwz0) ）
### tagsets 标注集
用于注释单词及其词性部分的标签来自标签集，如：
[Penn Treebank](https://www.ling.upenn.edu/courses/Fall_2003/ling001/penn_treebank_pos.html)
[Universal Scheme](https://universaldependencies.org/u/pos/all.html)
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/%E6%88%AA%E5%B1%8F2021-02-17%2008.52.40.png)
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/%E6%88%AA%E5%B1%8F2021-02-17%2008.52.51.png)
### Challenges 难点
	* Syntactic ambiguity（语法歧义）
		* duck（action，verb）
		* duck（bird，noun)
	* Different syntactic roles（不同的语法角色）
		* To **walk** || go for a **walk**
		* **Old** people || the **old**
		* They **referee** the matches || The **referee** starts the match
	* 在Brown语料库中有11%的单词类型无法直接判断词性。这个其中有一些是非常常见的单词，比如that
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/3B2DB935-C574-4A61-A14D-3CF09F43FD3B.png)
	* 所以，在实际文本中有40%的token是无法直接进行判断的

#### 如何消除歧义？
观察语法歧义
-当token独立时发生
-与其他单词结合时消失
-但有时也不能消除
 如They can fish（他们捕鱼 or 他们把鱼做成罐头）
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/%E6%88%AA%E5%B1%8F2021-02-17%2014.06.08.png)
	* 如果前一个词是限定词，则该词不太可能是动词
	* 如果一个词前面是to，那么它不太可能是名词
	* 当一个名词后面跟着一个普通名词时，那么token更有可能是一个物主代词
		* He stroked her cat
	* …but not always

### 词性标注的目的
将词性标注分配给每一个token
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/%E6%88%AA%E5%B1%8F2021-02-17%2014.11.03.png)


### 词性标注的作用
> 参考  
	* 帮助我们对单词的发音做判断（在不同的词性是单词的发音是不同的）
	* 对输出结果我们可以写正则表达式，比如(Det) Adj* N+
	* 把这个作为句法分析（praser）的输入可以加快分析
	* 在其他的任务中，我们可以不用单词本身而是直接使用它的词性，这样的话就可以减少特征稀疏的情况。
### 词性标注程序的表现
> 参考  
	* 目前表现最好的程序的正确率是97%
	* 但是一个基础程序（baseline）的正确率也可以达到90%（假设每个单词的标记都是它出现频率最高的标记，不认识的单词就标记为名词）
	* 词性标记这么容易取得很高的正确率的原因是：很多单词的词性都是很清晰的，我们可以依据标点符号，a，the等这些来进行判断。比如：
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/A92AFDC8-8994-4BB9-A152-9BF447D8BCF6.png)

## 词性标注的方法
* 制定rule-based的机制，体现语法知识。
* 或者，采用基于语料库corpus（文本收集）证据的statistical统计方法。
 
### POS Corpus 词性语料库
* Text collection，每个token都被贴上正确的（gold standard）POS标签
* 由语言专家手动贴上标签
* 由一个文本文件组成，有2种常见格式。
(1) 每行对应一个<token-POS标签>对，或
(2) 每行一句话，每句话后附加POS标签。
 
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/%E6%88%AA%E5%B1%8F2021-02-17%2014.17.55.png)
Treebank 是一种深加工语料库，其可被用于对句子进行分词、 词性标注 和句法 结构 关系的标注。
https://hyper.ai/wiki/3665

![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/%E6%88%AA%E5%B1%8F2021-02-17%2014.18.27.png)
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/%E6%88%AA%E5%B1%8F2021-02-17%2014.18.43.png)
[Penn Treebank (Wall Street Journal news articles)](https://catalog.ldc.upenn.edu/docs/LDC95T7/cl93.html)
[GENIA Corpus (biomedical scientific articles)](https://github.com/spyysalo/genia-pos)

## 三、如何构建词性标注模型
### 判断词性标注的主要信息来源
	* 周边单词的信息：限定词后面主要是名词
	* 单词本身出现的概率：man一般出现都是名词
	* 一般而言，第二种信息是更有用，但是第一种信息也是有帮助的
### 特征构建：一些特征
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/20181021125717848.png)
### 模型构建和对应的正确率
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/20181021131638469.png)
* 如何提升有监督模型的结果：构造更好的模型
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/20181021132020752.png)
* 直接使用分类模型而不是序列模型我们也可以得到很好的效果
![](2%20-%201%20POS%20tagging%20%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8/20181021132240224.png)
# 四、总结
* 对于标注而言，从生成模型改为判别模型不会导致很大的提升。存在的有一个收益是解决了特征重叠存在的问题（比如单词本身和前缀）。
* 另外，判别模型的一个优势是高正确率，但是以更慢的训练速度为代价的



