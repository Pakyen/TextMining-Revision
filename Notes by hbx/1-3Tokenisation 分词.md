# 1-3Tokenisation 分词
![](1-3Tokenisation%20%E5%88%86%E8%AF%8D/%E6%88%AA%E5%B1%8F2021-02-16%2016.32.34.png)
tokenisation其实就是将句子划分成一个个Token
- - - -
[一文看懂NLP里的分词-Tokenization（中英文区别+3大难点+3种典型方法）](https://easyai.tech/ai-definition/tokenization/#3ways)

将输入--通常是一个句子-- ~分解成3个主要的标记~ ，通常被认为是3个主要类别的标记 
	* Morphosyntactic word 形容词
	* Punctuation mark or special symbol 标点符号或特殊符号 
	* A number 数字

这些够吗？其他类型的token？
	* 缩写的结尾, e.g., “*’re*” in “*we’re*” 
	* 复合词和多义词 (e.g., daughter-in-law) 
- - - -

##  Challenges
Character encoding 
	* ASCII only? 
	* Unicode (UTF-8)
ASCII-fication or romanisation of texts 
	* Transliterations
Results from OCR may be poor 
	* Pre-processing to detect/correct errors 
	* OCR errors may appear as correct text (but not intended text) 

 
## Challenges: Writing Systems
![](1-3Tokenisation%20%E5%88%86%E8%AF%8D/%E6%88%AA%E5%B1%8F2021-02-09%2011.19.43.png)
如中文、日文之间没有white spaces
![](1-3Tokenisation%20%E5%88%86%E8%AF%8D/%E6%88%AA%E5%B1%8F2021-02-09%2011.20.16.png)
Hyphenation 连字符
![](1-3Tokenisation%20%E5%88%86%E8%AF%8D/%E6%88%AA%E5%B1%8F2021-02-09%2011.20.54.png)
![](1-3Tokenisation%20%E5%88%86%E8%AF%8D/%E6%88%AA%E5%B1%8F2021-02-09%2011.30.27.png)
![](1-3Tokenisation%20%E5%88%86%E8%AF%8D/%E6%88%AA%E5%B1%8F2021-02-09%2011.30.49.png)
Tokenisation是要知道什么时候去split（而不是什么时候去combine）


## Annotation Formats 注释格式
* **Annotation Formats: Boundary Notation**
![](1-3Tokenisation%20%E5%88%86%E8%AF%8D/%E6%88%AA%E5%B1%8F2021-05-25%2006.49.11.png)

* **Annotation Formats: Inline markup language elements**
![](1-3Tokenisation%20%E5%88%86%E8%AF%8D/%E6%88%AA%E5%B1%8F2021-05-25%2006.49.18.png)

* **Annotation Formats: Stand-off annotations**
![](1-3Tokenisation%20%E5%88%86%E8%AF%8D/%E6%88%AA%E5%B1%8F2021-05-25%2006.49.25.png)