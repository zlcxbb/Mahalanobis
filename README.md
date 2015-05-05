#Mahalanobis距离
-------
**Mahalanobis**距离（马氏距离）是多维空间中两点相似性的度量，它本身不是聚类或者分类算法。
Mahalanobis距离与Euclidean距离（欧氏距离）类似，不过还需除以空间的协方差矩阵。
如果协方差矩阵是单位矩阵，则Mahalanobis距离退化为Euclidean距离。

-------
程序基本思路如下：
> * 整理数据集，获取数据集单一变量
> * 计算协方差矩阵函数
> * 计算协方差矩阵的逆矩阵函数
> * 计算Euclidean距离
> * 计算Mahalanobis距离

------
##整理数据集，获取数据集单一变量
```matlab
m = input_data_from_file;
X = m(:,1);
Y = m(:,2);
Z = m(:,3);
```

##计算协方差矩阵函数

###为什么需要协方差
标准差和方差一般是用来描述一维数据的，但现实生活中我们常常会遇到含有多维数据的数据集，最简单的是大家上学时免不了要统计多个学科的考试成绩。面对这样的数据集，我们当然可以按照每一维独立的计算其方差，但是通常我们还想了解更多，比如，一个男孩子的猥琐程度跟他受女孩子的欢迎程度是否存在一些联系。协方差就是这样一种用来度量两个随机变量关系的统计量:
$$cov(X,Y) = \frac{\sum_{i=1}^{n}{(X_{i}-\overline{X})(Y_{i}-\overline{Y})}}{n-1}$$
协方差的结果有什么意义呢？如果结果为正值，则说明两者是正相关的（从协方差可以引出“相关系数”的定义），也就是说一个人越猥琐越受女孩欢迎。如果结果为负值， 就说明两者是负相关，越猥琐女孩子越讨厌。如果为0，则两者之间没有关系，猥琐不猥琐和女孩子喜不喜欢之间没有关联，就是统计上说的“相互独立”。
###协方差矩阵
前面提到的猥琐和受欢迎的问题是典型的二维问题，而协方差也只能处理二维问题，那维数多了自然就需要计算多个协方差，比如n维的数据集就需要计算
$$\frac{n!}{(n-2)!*2}$$
个协方差，那自然而然我们会想到使用矩阵来组织这些数据。给出协方差矩阵的定义：
$$C_{mxn}=(C_{ij} , C_{ij}=cov(Dim_{i},Dim_{j}) )$$
这个定义还是很容易理解额，我们可以举一个三维的例子，假设数据集有三个维度，则协方差矩阵为：
$$C = \lgroup \begin{array} 
cov(x,x) & cov(x,y) & cov(x,z)\\
cov(y,x) & cov(y,y) & cov(y,z)\\
cov(z,x) & cov(z,y) & cov(z,z)
\end{array} \rgroup$$
可见，协方差矩阵是一个对称的矩阵，而且对角线是各个维度的方差。

##计算协方差矩阵的逆矩阵函数
```matlab
inv_C = inv(C);
```

##计算Euclidean距离
欧氏距离是最易于理解的一种距离计算方法，源自欧氏空间中两点间的距离公式。
(1)二维平面上两点a(x1,y1)与b(x2,y2)间的欧氏距离：
$$ d = \sqrt{(x_{1}-x{2})^2+(y_{1}-y_{2})^2}$$
(2)两个n维向量a(x11,x12,…,x1n)与 b(x21,x22,…,x2n)间的欧氏距离：
$$ d = \sqrt{\sum_{k=1}^{n}{(x_{1k}-x_{2k})^2}} $$
也可以表示成向量运算的形式：
$$d=\sqrt{(a-b)(a-b)^{T}}$$


##计算Mahalanobis距离
Mahalanobis距离 = Euclidean距离 * 空间协方差矩阵的逆矩阵







