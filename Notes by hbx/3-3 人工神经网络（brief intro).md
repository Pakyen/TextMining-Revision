# 3-3 人工神经网络（brief intro)

## 机器学习（有监督的情况下）
	* Given an input x, find an output y
	* Classification: y is on of N classes
![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.14.10.png)
~Training~ ：learn function y=f(x) given n examples D_train = {(x1,y1),… (xn,yn)}
~Modelling~ ：f(x;θ)通常是参数化的（e.g. 一个神经网络）
~Testing~：f(“I’m a big fan of Tom Hanks”;θ)=？

## Neurons 神经元
人工神经元是一个计算单元，它的灵感来自于生物神经元
![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.17.54.png)
## 激活函数
**引入激活函数是为了增加神经网络模型的非线性。**. 没有激活函数的每层都相当于矩阵相乘。. 就算你叠加了若干层之后，无非还是个矩阵相乘罢了
![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.18.12.png)

## 多层神经网络
![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.18.41.png)
* 隐藏层的意义就是把输入数据的特征，抽象到另一个维度空间，来展现其更抽象化的特征，这些特征能更好的进行线性划分
* 多个隐藏层其实是对输入特征多层次的抽象，最终的目的就是为了更好的线性划分不同类型的数据（隐藏层的作用)

## 我们需要多少个隐藏层？
	* 理论上，一个隐藏层就足够了：两层神经网络是universal approximators通用近似器（它们能够将任何连续函数近似到任何所需的精确程度）。
![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.20.15.png)
	* 在实践中（深度学习），”deep "结构更受欢迎
![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.21.17.png)
## 分类任务 Classification task
![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.31.56.png)

## 训练一个神经网络（for classification)
![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.33.15.png)

##  (Minibatch) 随机梯度下降 (Stochastic gradient descent)
![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.33.41.png)

##  计算梯度：误差反向传播
> 反向传播算法（back propagation，简称BP模型）是1986年由Rumelhart和McClelland为首的科学家提出的概念，是一种按照误差逆向传播算法训练的多层前馈神经网络，是目前应用最广泛的神经网络  
>   

![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.33.59.png)

![](3-3%20%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%EF%BC%88brief%20intro)/%E6%88%AA%E5%B1%8F2021-02-22%2011.34.38.png)