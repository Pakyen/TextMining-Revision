# CW1 BOW思路记录

tokenization后，目前有两个东西

一是每个句子的token（每一行）
![](CW1%20BOW%E6%80%9D%E8%B7%AF%E8%AE%B0%E5%BD%95/%E6%88%AA%E5%B1%8F2021-03-05%2016.54.00.png)
二是word_to_index，里面包含了每个单词对应的索引
![](CW1%20BOW%E6%80%9D%E8%B7%AF%E8%AE%B0%E5%BD%95/%E6%88%AA%E5%B1%8F2021-03-05%2016.54.48.png)

但是索引为0的单词应该是unknown words

然后每一个单词都由一个1x5的向量表示，里面是五个随机数（由word embedding生成）[x,x,x,x,x]
![](CW1%20BOW%E6%80%9D%E8%B7%AF%E8%AE%B0%E5%BD%95/%E6%88%AA%E5%B1%8F2021-03-05%2016.56.04.png)
假设unknown索引是0，对应第0行
school索引是100，
students索引是98

如果一个句子里包含了school和students两个单词，那么这个句子的向量就等于
= vec(100)+ vec(98)
然后这个vec()再除以句子的总Token数，就会得到vec_bow(s)，/取模/
- - - -


## stop_words

1. 去除what、how、when、why、who、whom、where、which、whose
2. token和token_of_sentences都去除其余停用词
