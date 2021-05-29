# 1-2Sentence Segmentation
![](1-2Sentence%20Segmentation/%E6%88%AA%E5%B1%8F2021-02-16%2016.32.34.png)
句子分割其实就是把一份text，分成一个个句子
## Task
	* 确定句子之间的界限
	* 在后续NLP任务中使用的句子
	* 检测到句号就够了吗？
		* 可能是句末标记(EOS) end-of-sentence marker 
		* 或缩写标记的结束 
		* Or both?

## 句子划分的方法
	* 正则表达式
	* 字典（如缩写列表）
	* Hand-crafted rules
	* 统计学和机器学习方法
	* 混合方法
![](1-2Sentence%20Segmentation/%E6%88%AA%E5%B1%8F2021-02-09%2010.31.56.png)
![](1-2Sentence%20Segmentation/%E6%88%AA%E5%B1%8F2021-02-09%2010.36.11.png)
![](1-2Sentence%20Segmentation/%E6%88%AA%E5%B1%8F2021-02-09%2010.36.30.png)
* OpenNLP Sentence Detection 可以判断一个符号是不是句子的结束

![](1-2Sentence%20Segmentation/%E6%88%AA%E5%B1%8F2021-02-09%2010.36.41.png)
* spaCy是一个基于统计学的句子分割器

 