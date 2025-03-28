---
title: ML Using Python
layout: post
tags: machine_learning
---

# 第一章 赋予计算机学习数据n能力

机器学习提供了一种从数据中获取知识的方法，同时能够逐步提高预测模型的性能，并将模型应用于基于数据驱动的决策中去。

### 机器学习的三种方法

- 监督学习 supervised learning

  使用有类标(label)的训练数据来构建模型，使用该模型对未来数据进行预测。

  监督 supervised：指训练数据集中的每个样本均有一个已知的输出项。

  - 分类 classification

    这里的类标是离散的、无序的值

  - 回归 regression

    对连续型输出变量进行预测

- 无监督学习 unsupervised learning

  聚类：在没有先验信息的情况下，将数据划分为有意义的小的组别(cluster)

  降维(dimensionality reduction)：在最大程度保留相关信息的情况下将数据压缩到一个维度较小的子空间。

- 强化学习 reinforcement learning

  构建一个系统(agent)，在与环境交互过程中提高系统的性能。

  环境 environment：其当前状态信息中包含一个反馈信号。

### 构建机器学习的步骤

- 数据预处理
- 选择预测模型类型
- 训练模型并验证模型
- 对未知数据进行预测

### Python在机器学习中的包

- pip

  `pip install package`

  `pip install package --upgrade`

- anaconda

  `export PATH=/home/yule/anaconda3/bin:$PATH`

  `conda install package`

  `conda update package`

# 第二章 机器学习分类算法

早期算法：感知器(perceptron)  , 自适应线性神经元(adaptive linear neuron)

### 人造神经元 perceptron

- 神经细胞（MCP神经元模型）

  树突接收多个输入信号，如果累加的信号超过某一阈值，经细胞体的整合就会生成一个二进制输出信号，并通过轴突传递。

- 第一个感知器学习法则：自学习算法

  - 特定的输入值x
    $$
    \mathbf{x} =  \begin{vmatrix} 
    x_1 \\
     ... \\
     x_m\\
    \end{vmatrix}
    $$

  - 相应的权値向量w
    $$
    \mathbf{w} =  \begin{vmatrix} 
    w_1 \\
     ... \\
     w_m\\
    \end{vmatrix}
    $$

  - 净输入z
    $$
    z=w_1x_1+ \ ...\ +w_mx_m\\
    z=w^Tx
    $$

  - 激励函数activation function$\phi(z)$
    $$
    \phi(z)=
    \begin{cases}
    1& z\ge\theta\\
    -1& otherwise\\
    \end{cases}\\
    \theta:阈值
    $$

  - 自学习算法的步骤

    1. 将权重初始化为零

    2. 迭代所有训练样本$x^{(i)}$,计算出输出值$\hat y=\phi(w^Tx)$

    3. 更新权重

        $\Delta w_j=\eta (y^{(i)}-\hat{y}^{(i)})x^{(i)}_j$		$\eta$：学习速率

       $w_j:=w_j+\Delta w_j$

    注：该感知器手链的前提是两个类别必须线性可分


- Python实现感知器

  见：[2.2感知器学习算法.py](./Python机器学习-代码/2.2感知器学习算法.py)



得到结果如下：
![Figure_1](./pics/Figure_1.png)
![Figure_1-1](./pics/Figure_1-1.png)
![Figure_1-2](./pics/Figure_1-2.png)

### 自适应线性神经元 Adaline

这也是一种单层神经网络：Adaptive Linear Neuron, Adaline

- 通过梯度下降最小化代价函数

  算法核心：

  1. 定义一个目标函数$$ J(w)$$（代价函数），其最小化处理

     Adaline中：J = SSE(Sum of Squared Error,误差平方和)

  $$
  J(w)=\frac{1}{2}\sum_i(y^{(i)}-\phi(z^{(i)}))^2权重
  $$
   (前面1/2的系数是为了后面求导方便)
  2. 权重增量：负梯度和学习速率$\eta$的乘积
     $$
     \Delta w=-\eta\Delta J(w) \\
     \Delta w_j=-\eta\frac{\partial J}{\partial w_i}=\eta \sum_i (y^{(i)}-\phi(z^{(i)}))x_j^{(i)}
     $$

  3. 沿着梯度方向做一次权重更新
     $$
     w:=w+\Delta w
     $$

- 使用python实现自适应线性神经元

  见：[2.3自适应线性神经元.py](./Python机器学习-代码/2.3自适应线性神经元.py)



- 当执行注释部分的代码：分别绘制在两个不同的学习速率下，代价函数与迭代次数的图像

    ![Figure_2-1](./pics/Figure_2-1.png)

  - 执行注释后面部分的代码：

    所有样本都被正确分类，但是误差平方和SSE的值仍不为零。（为什么？）

    ![Figure_2-2](./pics/Figure_2-2.png)

    ![Figure_2-3](./pics/Figure_2-3.png)

- 大规模机器学习与随机梯度下降

  - 替代批量梯度下降的算法：（三个名字同一个东西）
    1. 随机梯度下降：stochastic gradient descent
    2. 迭代梯度下降：iterative gradient descent
    3. 在线梯度下降：on-line gradient descent

  - python实现

    见：[2.3随机梯度下降.py](./Python机器学习-代码/2.3随机梯度下降.py)

    结果可以看出，代价函数的均值下降很快

    ![Figure_2-4](./pics/Figure_2-4.png)

    ![Figure_2-5](./pics/Figure_2-5.png)

# 第三章 使用scikit-learn实现机器学习分类算法

- 训练机器学习算法的步骤：
  1. 特征的选择
  2. 确定性能评价指标
  3. 选择分类器和优化算法
  4. 对模型性能的评估
  5. 算法的 调优

### scikit-learn的使用

见：[3.2使用scikit-learn训练感知器](./Python机器学习-代码/3.2使用scikit-learn训练感知器.py)

结果如图：无法完全线性可分

![Figure_3-1](./pics/Figure_3-1.png)

### 逻辑斯谛回归中的类别概率

- 逻辑斯谛回归与条件概率

  - 几率比 (odd ratio)
    $$
    \frac{p}{1-p}   \ \ \ \ \ \ \ \ \ p：正事件发生的概率
    $$

  - logit函数(log-odds,对数几率)
    $$
    logit(p)=log\frac{p}{1-p}
    $$

  - 条件概率，在给定特征x的条件下，某一个样本属于类别1的条件概率：
    $$
    p(y=1|x)
    $$

  - 对数几率：输入特征值的线性表达式
    $$
    logit(p(y=1|x))=w0x0+w1x1+...+w_mx_m=\Sigma_{i=0}^{m}w_ix_i=w^Tx
    $$

  - logistic函数(logit函数的反函数)/sigmoid函数 ( =p )
    $$
    \phi(z)=\frac{1}{1+e^{-z}}
    $$

  - 净输入z，是样本特征和权重的线性组合 ( =logit() )
    $$
    z=w^Tx=w0x0+w1x1+...+w_mx_m
    $$
























  sigmoid函数图像如下：

  ![Figure_3-2](./pics/Figure_3-2.png)

- 通过逻辑斯谛回归模型的代价函数获得权重

  - 最大似然函数**L**
    $$
    L(w)=P(y|x;w)=\Pi_{i=1}^{n}P(y^{(i)}|x^{(i)};w)=(\phi(z^{(i)}))^{y^{(i)}}(1-\phi(z^{(i)}))^{1-y^{(i)}}
    $$
    （在本问题中y可取1或0，从而使得第二项或第一项等于1，得到此时单个的概率）

  - 对数似然函数
    $$
    l(w)=logL(w)=\Sigma_i^n \ y^{(i)}log(\phi(z^{(i)}))+(1-y^{(i)})log(q-\phi(z^{(i)}))
    $$

  - 代价函数

  $$
  J(w)=\Sigma_{i=1}^n -log(\phi(z^{(i)}))-(1-y^{(i)})log(1-\phi(z^{(i)}))
  $$

    - 计算**单个**样本实例的成本

  $$
  J(\phi(z),y;w)=-ylog(\phi(z))-(1-y)log(1-\phi(z))
  $$

  ​	进而可得
  $$
  J(\phi(z),y;w)=
  \begin{cases}
  -log(\phi(z)) & if\ y=1\\
  -log(1-\phi(z)) & if\ y=0\\
  \end{cases}\\
  $$
  ​	图像为：![Figure_3-3](./pics/Figure_3-3.png)

  ​	如果样本正确划分到类别1中，代价将趋于0（蓝线）。

  ​	如果分类错误，代价将趋于无穷。

  - 逻辑斯谛回归中的梯度下降
    $$
    \frac{\partial}{\partial w_j}l(w)=(y\frac{1}{\phi(z)}-(1-y)\frac{1}{1-\phi(z)})\frac{\partial}{\partial w_j}\phi(z)
    $$

    $$
    化简有：\ \ \frac{\partial}{\partial w_j}l(w)=(y-\phi(z))x_j
    $$

    进而更新权重：
    $$
    w_j := w_j + \eta\Sigma_{i=1}^n (y^{(i)}-\phi(z^{(i)}))x^{(i)}
    $$
    $$
    w:=w+\Delta w
    $$

    $$
    \Delta w=-\eta \bigtriangledown J(w) 
    $$

- 使用scikit-learn训练逻辑斯谛回归模型

  代码见：[3.3使用scikit-learn训练逻辑斯谛回归模型](./Python机器学习-代码/3.3使用scikit-learn训练逻辑斯谛回归模型.py)

  得到结果：![Figure_3-4](./pics/Figure_3-4.png)

- 通过正则化解决过拟合问题

  - 偏差-方差衡量(bias-variance tradeoff)：

    通过正则化调整模型的复杂度

  - 正则化：

    解决共线性问题，可以过滤掉数据中的噪声，防止过拟合

    - 原理：

      引入额外的偏差，对极端参数权重做出惩罚

    - L2正则化
      $$
      \frac{\lambda}{2}||w||^2=\frac{\lambda}{2}\Sigma_{j=1}^mw_j^2
      $$
      其中$$\lambda$$是正则化系数

    - 在逻辑斯谛回归中加入正则化项
      $$
      J(w)=\{\Sigma_{i=1}^n -log(\phi(z^{(i)}))-(1-y^{(i)})log(1-\phi(z^{(i)})) \}+\frac{\lambda}{2}||w||^2
      $$
      增加$$\lambda$$可以增强正则化的强度

### 使用SVM最大化分类间隔

感知器：最小化分类误差

SVM：最大化分类间隔。间隔（两个分离的超平面间的距离）。超平面（决策边界）

支持向量：最靠近超平面的训练样本

- 使用松弛变量解决分线性可分问题

  - 松弛系数$$\xi$$

    对于非线性可分的数据，需要放松线性约束条件，以保证在适当的罚项成本下，对错误分类的情况进行优化时能够收敛。

  - 训练一个SVM模型

    代码见：[3.4训练一个线性SVM模型](./Python机器学习-代码/3.4训练一个线性SVM模型.py)

    得到结果：![Figure_3-5](./pics/Figure_3-5.png)

- 使用scikit-learn实现SVM

  数据集非常大的时候，scikit-learn提供了SGDClassifier类。

### 使用核SVM解决非线性问题

- 基本理念

  通过映射函数$\phi()$将样本的原始特征映射到一个使样本线性可分的更高维空间中

- 核函数
  $$
  k(x^{(i)},x^{(j)})=\phi(x^{(i)})^T\phi(x^{(j)})
  $$
  例如：径向基函数核(RBF kernel) / 高斯核(Gaussian kernel)
  $$
  k(x^{(i)},x^{(j)})=exp(-\gamma||x^{(i)}-x^{(j)}||^2)
  $$
  ​	待优化的自有参数
  $$
  \gamma=f\frac{1}{2\sigma^2}
  $$
  核：一对样本之间的相似函数。当完全相同时，值为1；当差异巨大时，值趋于0

- 分离超平面demo

  代码见：[3.5使用核SVM解决非线性问题](./Python机器学习-代码/3.5使用核SVM解决非线性问题.py)

  得到结果：![Figure_3-6](./pics/Figure_3-6.png)

- 分离超平面处理鸢尾花数据

  参数中的$$\gamma$$ (gamma)可以理解为高斯球面的截止参数

  如果增加$$\gamma$$，就会减小i受影响的训练样本的范围，导致决策边界更严格。

  代码见：[3.5使用核技巧在高维空间发现分离超平面](./Python机器学习-代码/3.5使用核技巧在高维空间发现分离超平面.py)

  当gamma分别去0.2和100时，得到结果如下

  ![Figure_3-7](./pics/Figure_3-7.png)

  ![Figure_3-8](./pics/Figure_3-8.png)

  图2就过拟合了，对未知数据有一个较高的泛化误差

### 决策树

- 最大化信息增益

  - 决策树基本理念

    基于训练数据集的特征，决策树通过一系列的问题来推断样本的类标

    算法：从树根开始，基于最大信息增益(IG,information gain)的特征来对数据进行划分。

    解决过拟合问题：对树进行剪枝来限定树的最大深度。

  - 目标函数：对信息增益最大化
    $$
    IG(D_p,f)=I(D_p)-\Sigma_{j=1}^{m}\frac{N_j}{N_p}I(D_j)
    $$
    信息增益：父节点不纯度 与 所有子节点不纯度总和 之差。

    子节点的不纯度越低：信息增益越大，这样越好。

    ​	$D_p$:父节点

    ​	$$D_j$$：第j个子节点

    ​	$$N_p$$：父节点中样本的数量	

    ​	$$N_j$$：第j个子节点中样本的数量

    ​	$$f$$：要进行划分的特征

    ​	$$I$$：不纯度衡量标准

  - 不纯度衡量标准

    - 熵$$I_H$$(entropy)
      $$
      I_H(D)=-\Sigma _{i=1}^cp(i|D)log_2p(i|D)
      $$
      ​	$$p(i|D)$$：特定节点D中，属于类别c的样本占节点D中样本总数的比例zuidazuida

      ​	当所有样本都属于同一类别，熵为0；

      ​	当样本以相同的比例分属于不同的类，熵最大。

      ​	所以熵的准则是使得互信息最大化。

    - 基尼系数$$I_G$$(gini index)
      $$
      I_G(D)=1-\Sigma _{i=1}^cp(i|D)^2
      $$
      基尼系数可以理解为降低误分类可能性的标准

    - 误分类率$$I_E$$(classification error)
      $$
      I_E=1-max\{p(i|D)\}
      $$
      对于剪枝很有用。

    我们希望：不纯度越低越好，纯度就高，说明样本分离的好，这样目标函数IG就很大。也就说明从父节点到子节点，不纯度变化大，分的有效果。

- 构建决策树

  代码见：[3.6构建决策树](./Python机器学习-代码/3.6构建决策树.py)

  结果：

  ![Figure_3-9](./pics/Figure_3-9.png)

  使用GraphViz程序可以进行可视化处理，得到结果：

  ![tree](./pics/tree.png)

- 通过随机森林将弱分类器集成为强分类器

  随机森林：多棵决策树的集成

  步骤：

  1. 使用bootstrap抽样方法随机选择n个样本用于训练
  2. 使用步骤1的样本构造一棵决策树：不重复地随机选择d个特征
  3. 重复步骤1和2过程很多次
  4. 汇总每棵决策树的类标进行多数投票

  代码见：[3.6通过随机森林将弱分类器集成为强分类器.py](./Python机器学习-代码/3.6通过随机森林将弱分类器集成为强分类器.py)

  结果：

  ![Figure_3-10](./pics/Figure_3-10.png)

### k-近邻算法(KNN)

- 闵可夫斯基距离
  $$
  d(x^{(i)},x^{(j)})=p\sqrt{\Sigma_k|x_k^{(i)}x_k^{(j)}|^2}
  $$
  该距离是对欧几里得距离及曼哈顿距离的一种泛化。

  p=1:曼哈顿距离

  p=2:欧几里得距离



# 第四章  数据预处理-构建好的训练数据集

### 缺失数据的处理

- 删除存在缺失值的特征

  使用df.dropna()

- 填充缺失数据

  Impute类可以实现均值插补

- 数据转换常用的两个方法

  fit方法：对数据集里的参数进行识别，并构建相应的数据补齐模型

  transform方法：用刚构建的模型对相应参数的缺失值进行补齐。

代码见：[4.1处理缺失数据](./Python机器学习-代码/4.1处理缺失数据.py)

### 处理类别数据

- 数据的分类

  - 数值型数据
  - 类别数据
    - 标称特征：如衣服的颜色(红,黄,蓝)
    - 有序特征：如衣服的尺寸(XK>L>M)

- 独热编码

  创建一个新的虚拟特征，虚拟特征的每一列各代表标称数据的一个值

  代码见：[4.2处理类别数据](./Python机器学习-代码/4.2处理类别数据.py)

### 将特征的值缩放到相同的区间

- 特征缩放

  - 归一化(normalization)

    将特征的值缩放到区间[0,1]
    $$
    x_{norm}^{(i)}=\frac{x^{(i)}-x_{min}}{x_{max}-x_{min}}
    $$

  - 标准化(standardization)

    将特征值的均值设为0，方差为1.特征列变为标准正态分布。
    $$
    x_{std}^{(i)}=\frac{x^{(i)}-\mu _x}{\sigma _x}
    $$
    式中变量是均值和标准差。

  代码见：[4.3葡萄酒数据集.py](./Python机器学习-代码/4.3葡萄酒数据集.py)

### 选择有意义的特征

- 解决过拟合的问题的两种方法
  - 正则化引入罚项：对小的权重做出激励
  - 特征选择降维

- 使用L1正则化实现数据稀疏化
  $$
  L1 : ||w||_1=\Sigma_{j=1}^m|w_j|
  $$
  L1:权重绝对值的和

  L2:权重的平方和。其思想是使得代价函数与罚项之和最小

  L1可生成稀疏的特征向量，大多数权值为0.当权值向0收缩时，降低了模型对训练数据的依赖程度。

  代价函数边界和L1边界更有可能相交在坐标轴上，从而使得模型更加稀疏。

  代码见：[4.4使用L1正则化满足数据稀疏化.py](./Python机器学习-代码/4.4使用L1正则化满足数据稀疏化.py)

  结果：

  ![Figure_4-1](./pics/Figure_4-1.png)

  当$$c<10^{-1}$$时，正则化较强，13个特征权重都趋于0。

   C是正则化参数$$\lambda$$的倒数

- 序列特征选择算法

  - 特征选择：选出原始特征(d维)的子集(k维)

    思想：提出不相关特征或噪声，选出最相关的特征子集。

    **SBS序列向后选择算法**(Sequential backward selection)

    思想：依次从特征集合中删除一些特征，指导新的子空间包含指定数量的特征

    ​	每一步特征被删除后，引起的模型性能损失最小。

    ​	所以要最小化标准衡量函数J

    步骤：

    1. 初始化k=d
    2. 定义$$x^{-}$$: $$x^{-}=argmax[J(X_k-x)]$$
    3. 删除$$x^{-}$$: $$X_{k-1}=X_{k}-x^-$$ ,  $$k=k-1$$
    4. 如果k等于目标特征数目，停止

    代码见：[4.5 SBS序列向后特征选择算法.py](./Python机器学习-代码/4.5 SBS序列向后特征选择算法.py)

    结果：

    ![Figure_4-2](./pics/Figure_4-2.png)

    在特征值是5到10的时候，算法准确率100%。

  - 特征提取：对现有的特征信息进行推演，构造一个新的特征子空间

    下一章介绍

### 通过随机森林判定特征的重要性

通过森林中所有决策树得到的平均不纯度衰减来度量特征的重要性，而不必考虑数据是否线性可分。

无需对树的模型做标准化或归一化处理。

代码见：[4.6通过随机森林判定特征的重要性.py](./Python机器学习-代码/4.6通过随机森林判定特征的重要性.py)

结果：

![Figure_4-3](./pics/Figure_4-3.png)

重要性经过归一化处理，和为1.



# 第五章 通过降维压缩数据

### 无监督数据降维技术-主成分分析(PCA)

PCA目标：在高维数据中找到最大方差的方向，并将数据映射到一个维度不大于原始数据的新的子空间上。

PCA步骤：

1. 对原始d维数据集进行标准化处理
2. 构造样本的协方差矩阵
3. 计算协方差矩阵的特征值和相应的特征向量
4. 选择与前k个最大特征值对应的特征向量
5. 通过前k个特征向量构建映射矩阵W
6. 通过映射矩阵W将d维的输入数据集X转换到新的k维特征子空间

注意：PCA是一种无监督学习，我们可以忽略类标信息

- 总体方差和贡献方差

  - 协方差

    1. 沿主对角线对称。
    2. 两个特征的协方差为正，说明她们同时增减。
    3. 协方差的特征向量代表主成分(最大方差方向)
    4. 设一个协方差矩阵为A，有向量v满足$Av=\lambda v$，则v是A的特征向量，$\lambda$是特征值(标量)
    5. 特征值$\lambda_j$的方差贡献率：该特征值与所有特征值总和的比值

  - 代码见：[5.1总体方差与贡献方差.py](./Python机器学习-代码/5.1总体方差与贡献方差.py)

    结果：

    ![Figure_5-1](./pics/Figure_5-1.png)

    可以看出前两个主成分占总体方差的近60%

- 特征转换

  求出映射矩阵W，由$X^{'}=xW$得到新特征的子空间

  代码见：[5.2构造映射矩阵进行特征转换.py](./Python机器学习-代码/5.2构造映射矩阵进行特征转换.py)

  结果：

  ![Figure_5-2](./pics/Figure_5-2.png)

- 使用scikit-learn进行主成分分析

  使用`from sklearn.decomposition import PCA`，再用逻辑斯谛回归分类，绘图部分使用`plot_decision_regions()`函数

  代码见：[5.3使用scikit-learn进行主成分分析.py](./Python机器学习-代码/5.3使用scikit-learn进行主成分分析.py)

  结果：

  ![Figure](./pics/Figure_5-3.png)

### 通过线性判别分析(LDA)压缩无监督数据

LDA：对于不适用于正则化的模型，它可以降低因维度灾难带来的过拟合。

概念：Linear Discriminant Analysis,发现可以最优化分类的特征子空间。

假设：1.数据呈正态分布 2.各类别的数据具有相同的协方差矩阵 3.样本的特征相互独立

LDA步骤：

       	1. 对d维数据进行标准化处理
        	2. 对每个类别，计算d维的均值向量
         	3. 构造类间的散布矩阵$S_B$，以及类内的散布矩阵$S_W$
         	4. 计算矩阵$S_W^{-1}S_B$的特征值和特征向量
         	5. 选取前k个特征值所对应的特征向量，构造d*k维的转换矩阵$W$
         	6. 使用W将样本映射到新的特征子空间

- 计算散布矩阵

  > 散布矩阵的大小由特征维数d决定，是一个为d×d 的半正定矩阵。
  >
  > 关系：散布矩阵=类内离散度矩阵=类内离差阵=协方差矩阵×（n-1）

  均值向量$m_i$存储了类别i中样本的特征均值$\mu_m$:
  $$
  m_i=\frac{1}{n_i}\Sigma_{x \in D_i}^cx_m \ \ \ \ （一共有3个类别对应3个向量：i=1,2,3）
  $$
  各类别i的散布矩阵$S_i$:
  $$
  S_i=\Sigma_{x \in D_i}^c(x-m_i)(x-m_i)^T
  $$
  累加$S_i$得到类内散布矩阵$S_W$:
  $$
  S_W=\Sigma_{i=1}^cS_i
  $$
  协方差矩阵$A$可以看做是归一化的散布矩阵：
  $$
  A=\frac{1}{N_i}S_w=\frac{1}{N_i}(x-m_i)(x-m_i)^T
  $$
  计算类间散布矩阵$S_B$:
  $$
  S_B=\Sigma_{i=1}^cN_i(m_i-m)(m_i-m)^T
  $$

- 在新特征子空间上选取线性判别算法

  1. 计算出矩阵$S_W^{-1}S_B$的广义特征值，发现只有前两项很大于零

     结果：

     ![Figure](./pics/Figure_5-4.png)

  2. 叠加前两个判别能力最强的特征向量列，构建转换矩阵$W$

- 将样本映射到新的特征空间
  $$
  X^{'}=XW
  $$
  代码见：[5.4通过线性判别分析压缩无监督数据.py](./Python机器学习-代码/5.4通过线性判别分析压缩无监督数据.py)

  结果：

  ![Figure](./pics/Figure_5-5.png)

- 使用scikit-learn进行LDA分析

  使用的API：`from sklearn.discriminant_analysis import LinearDiscriminantAnalysis`

  代码见：[5.5使用scikit-learn进行LDA分析.py](./Python机器学习-代码/5.5使用scikit-learn进行LDA分析.py)

  结果：

  ![Figure](./pics/Figure_5-6.png)

### 使用核主成分分析进行非线性映射

- 核函数和核技巧

  思路：通过非线性映射，将数据转换到一个高维空间，然后在此空间使用标准PCA将其映射到另外一个低维空间，再通过线性分类器对样本进行划分。

  核技巧：在原始特征空间中计算两个高维特征空间中向量的相似度。

  **使用核技巧之后，学习是隐式地在特征空间进行的，不需要显式地定义特征空间和映射函数**

  **核函数是二元函数，输入是变换之前的两个向量，其输出与两个向量变换之后的内积相等**
  $$
  K(x_1,x_2)==\phi(x_1)*\phi(x_2)
  $$
  径向基函数(RBF)：
  $$
  k(x,y)=exp(-\frac{|x-y|^2}{2\sigma^2})\ \ \ \ \ \ (分母可去掉)
  $$
  运算后的结果：
  $$
  K(x,y)=\Sigma_{i=0}^{\infty}\frac{c}{\sigma^{2i}2!}(y^Tx)^i
  $$
  因此，RBF Kernel 是所有多项式核函数的线性组合。其实到这里就已经可以看出RBF所对应的特征映射函数就是由多项式核函数所对应的特征映射函数组合而成。

  步骤：

  1. 采用某一核函数后，可计算核矩阵$K$。如果有n个训练样本，则得到n*n维的对称核矩阵。
  2. 定义矩阵$L_n=\frac{1}{n}*ones(n)$，使核矩阵$K$更聚集：

  $$
  K^{'}=K-L_nK-KL_n+L_nKL_n
  $$

  3. 将聚集后的核矩阵的特征值按降序排列，选择前k个特征值所对应的特征向量。

- 使用Python实现核主成分分析

  代码见：[5.6使用python实现核主成分分析.py](./Python机器学习-代码/5.6使用python实现核主成分分析.py)

  输入数据：

  ![Figure](./pics/Figure_5-7.png)

  结果：

  ![Figure](./pics/Figure_5-8.png)

  左图是特征向量的值(100*2)，右图是第一列特征向量的值(值在PC1上)

- 映射新的数据点

  核矩阵的特征向量$\alpha$和特征值$\lambda$满足：$K\alpha=\lambda \alpha$

  我们需要计算训练集和新样本$x^{'}$之间的相似度(RBF核)：
  $$
  \phi(x^{'})^Tv=\Sigma_i\alpha^{(i)}\phi(x^{'})^T\phi(x^{(i)}) =\Sigma_i\alpha^{(i)}k(x^{'},x^{(i)})^T
  $$
  $v$是主成分轴，等式左边将新的样本映射到主成分轴（但不用具体计算）

  代码见：[5.7使用核PCA映射新的数据点.py](./Python机器学习-代码/5.7使用核PCA映射新的数据点.py)

  结果：

  ![Figure](./pics/Figure_5-9.png)

- 使用scikit-learn中的核主成分分析

  代码见：[5.8使用scikit-learn中的核主成分分析.py](./Python机器学习-代码/5.8使用scikit-learn中的核主成分分析.py)

  结果：

  ![Figure](./pics/Figure_5-10.png)



# 第六章 模型评估与参数调优实战

### 基于流水线的工作流

- 加载乳腺癌数据集

  `df = pd.read_csv('wdbc.data',header=None) #[569 rows x 32 columns]`

- 在流水线中集成数据转换及评估操作

  scikit-learn中的Pipline类：可以拟合出包含任意多个处理步骤的模型，病将模型用于新数据的预测。

  代码中，流水线包含：

  1. 数据缩放：StandardScaler标准化处理
  2. 数据转换：PCA主成分分析
  3. 评估器：LogisRegression分类器

代码见：

[6.1加载威斯康星乳腺癌数据集.py](./Python机器学习-代码/6.1加载威斯康星乳腺癌数据集.py)

### 使用k折交叉验证评估模型性能

- holdout交叉验证

  将数据分成三部分：训练数据集，验证数据集，测试数据集

  1. 训练：用于不同模型的拟合
  2. 验证：模型在验证数据集的性能表现作为模型选择的标准
  3. 测试：在训练和模型选择阶段都不曾使用，只做最终性能评估

  优点：评估模型应用于新数据上能够获得较小偏差

  缺点：评价的结果会随样本的不同而发生变化

- k-fold交叉验证

  将训练数据集分为k个，k-1个用于训练，1个用于测试。此过程重复k次，得到k个评价，再算出平均性能。

  找到模型泛化最好的超参值后，在全部训练上重新训练模型，再用独立的测试做出最终评价。

代码见：

[6.2使用k折交叉验证评估模型性能.py](./Python机器学习-代码/6.2使用k折交叉验证评估模型性能.py)

### 通过学习及验证曲线来调试算法

- 使用学习曲线判定偏差和方差问题

  1. 高偏差：准确率不够，不能很好拟合数据。
  2. 高方差：训练准确度和验证准确度之间有很大差距。

  代码见：[6.3使用学习曲线判定偏差与方差问题.py](./Python机器学习-代码/6.3使用学习曲线判定偏差与方差问题.py)

  结果：

  ![Figure](./pics/Figure_6-1.png)

- 通过验证曲线来判定过拟合与欠拟合

  学习曲线：样本大小 - 训练/测试准确率

  验证曲线：模型参数 - 训练/测试准确率

  代码见：[6.3 通过验证曲线来判定过拟合与欠拟合.py](./Python机器学习-代码/6.3 通过验证曲线来判定过拟合与欠拟合.py)

  结果：

  ![Figure](./pics/Figure_6-2.png)

  由图可得：最优点在C=0.1附近

### 使用网络搜索调优机器学习模型

参数类型：

1. 通过训练数据学习得到的参数
2. 超参：调优参数，需要单独进行优化的参数

- 使用网络搜索调优超参

  通过对超参列表进行暴力穷举搜索，并计算评估每个组合对模型性能的影响，以获得参数的最优组合。

- 通过嵌套交叉验证选择算法

  该方法的优点：估计的真实误差和在测试集上得到的结果几乎没有差距。

  外部循环（训练优化参数）：数据分为训练块和测试块

  内部循环（参数调优）：基于训练块使用k折交叉验证

代码见：[6.4使用网络搜索调优模型.py](./Python机器学习-代码/6.4使用网络搜索调优模型.py)

### 了解不同的性能评价指标

衡量模型性能的指标：准确率 precision，召回率 recall，F1分数 F1-score

- 读取混淆矩阵

  confusion matrix：四部分预测结果（预测类别-实际类别）

  代码见：[6.5读取混淆矩阵.py](./Python机器学习-代码/6.5读取混淆矩阵.py)

  结果：

  ![Figure](./pics/Figure_6-3.png)

- 优化分类模型的准确率和召回率

  | TP   | FN   |
  | ---- | ---- |
  | FP   | TN   |

  准确率PRE：$PRE=\frac{TP}{TP+FP}$

  召回率REC：$REC=\frac{TP}{TP+FN}$

  F1分数：$F1=2\frac{PRE*REC}{PRE+REC}$

- 绘制ROC曲线

  ROC: receiver operator characteristic. 受试者工作特征曲线

  AUC: area under the curve. ROC线下区域

  其对角线是随机猜测时的性能，如果在线下，说明性能比随机猜测还要差。

  两个变量可以通过移动分类器的分类阈值来计算。

  函数：真正率TPR - 假正率FPR

  $FPR=\frac{FP}{FP+TN}$

  $FTPR=\frac{TP}{TP+FN}$

  代码见：[6.5绘制ROC曲线.py](./Python机器学习-代码/6.5绘制ROC曲线.py)

  结果：

  ![Figure](./pics/Figure_6-4.png)

- 多类别分类(OvA)的评价标准

  - 微均值：

    当等同看待每个实例或每次预测时，微均值有用。

    通过系统的真正、真负、假正、假负来计算：
    $$
    PRE_{micro}=\frac{TP_1+...+TP_k}{TP_1+...+TP_K+FP_1+FP_k}
    $$
    ​

  - 宏均值：

    当等同看待每个类别，将其用于评估分类器针对最频繁类标的整体性能。

    仅计算不同系统的平均分值：
    $$
    PRE_{macro}=\frac{PRE_1+...+PRE_k}{k}
    $$
    当样本分布不均衡时，各类别以类内实例的数量作为评分的权值，这样比较有效。

    ​


# 第七章 集成学习-组合不同的模型

### 集成学习

集成方法(ensemble method)：将不同的分类器组合成为一个元分类器，有更好的泛化能力。

多数投票(majority voting)：将大多数分类器预测的结果作为最终类标。

将成员分类器集成后的出错概率可表示为二项分布的概率密度函数：
$$
P(y\ge k)=\sum_k^n\binom{n}{k}\epsilon^k(1-\epsilon)^{n-1}=\epsilon_{ensemble}
$$
$\epsilon$：每个成员分类器都有相同的出错率

代码见：[7.1集成分类器出错概率的概率密度函数.py](./Python机器学习-代码/7.1集成分类器出错概率的概率密度函数.py)

结果：

![Figure](./pics/Figure_7-1.png)

由图得，当成员分类器的出错率小于50%时，集成分类器出错率低于单个分类器。

### 实现一个简单的多数投票分类器

1.当单个分类器权重相等：

$\hat{y}=mode\{C_1(x),C_2(x),...C_m(x\}$

2.m个分类器，当权重不等时：
$$
\hat{y}=\arg\max_i\sum_{j=1}^{m}w_j\chi_A(C_j(x)=i)
$$
$\hat{y}$：集成分类器的预测类标

$w_j$：成员分类器$C_j$对应的权重

$\chi_A$：特征函数$[C_j(x)=i\in A]$

$A$：类标的集合

3.修改版本：
$$
\hat{y}=\arg \max_i\sum_{j=1}^mw_jp_{ij}
$$
$p_{ij}$：第j个分类器预测样本类标为i个概率。

代码见：[7.2实现一个简单的多数投票分类器.py](./Python机器学习-代码/7.2实现一个简单的多数投票分类器.py)

结果：

> Accuracy: 0.92 (+/- 0.20) [Logistic Regression]
>
> Accuracy: 0.92 (+/- 0.15) [Decision Tree]
>
> Accuracy: 0.93 (+/- 0.10) [KNN]
>
> Accuracy: 0.97 (+/- 0.10) [Majority Voting]

### 评估和调优集成分类器

代码见：[7.3评估与调优集成分类器 .py](./Python机器学习-代码/7.3评估与调优集成分类器 .py)

结果：

![Figure](./pics/Figure_7-2.png)![Figure](./pics/Figure_7-3.png)

### 通过bootstrap样本构建集成分类器

bootstrap抽样：有放回的抽样。

bagging循环：每轮踩道的抽样都用于$c_j$的训练。

优点：可以提高不稳定模型的准确率，并且降低过拟合的程度。

可以降低模型方差，但是对降低模型偏差的作用不大。

代码见：[7.4通过bootstrap样本构建集成分类器.py](./Python机器学习-代码/7.4通过bootstrap样本构建集成分类器.py)

结果：

![Figure](./pics/Figure_7-4.png)

### 通过自适应boosting提高弱学习机的性能

AdaBoost：Adaptive Boosting

弱学习机：性能仅稍好于随机猜测

- boosting步骤：

  1. 从训练集D中无放回抽取一个子集$d_1$，训练弱学习机$C_1$
  2. 从训练集D中无放回抽取一个子集$d_2$，再从$C_1$中误分类样本50%加入训练集，训练弱学习机$C_2$
  3. 抽取$C_1$和$C_2$分类结果不一致的样本生成训练样本集$d_3$，训练弱学习机$C_3$
  4. 通过多数投票组合三个弱学习机

  优点：可同时降低偏差和方差。

- AdaBoost步骤：

  1. 为权重向量w赋值，所有值相等，和为1
  2. 在共m轮boosting中，对第$j$门有如下操作
  3. 训练一个加权的弱学习机：$C_j=train(X,y,w)$
  4. 预测样本类标：$\hat{y}=predict(C_j,y)$
  5. 计算权重错误率$\epsilon=w\cdot(\hat{y}==y)$  #y取值0或1
  6. 计算相关系数：$\alpha_j=0.5log\frac{1-\epsilon}{\epsilon}$
  7. 更新权重：$w:=w\times exp(-\alpha_j\times \hat{y}\times y)$
  8. 归一化权重：$w:=w/\sum_i w_i$
  9. 完成最终预测：$\hat{y}=(\sum_{j=1}^m(\alpha_j\times predict(C_j,X))>0)$


代码见：[7.5训练一个AdaBoost集成分类器 .py](./Python机器学习-代码/7.5训练一个AdaBoost集成分类器.py)

结果：

![Figure](./pics/Figure_7-5.png)

# 第八章 使用机器学习进行情感分析

NLP(natural language processing)：自然语言处理

情感分析(sentiment analysis)是NLP中的一个分支

### 获取电影评论数据集

代码见：[8.1获取IMDb电影评论数据集 .py](./Python机器学习-代码/8.1获取IMDb电影评论数据集.py)

### 词袋模型简介

词袋模型(bag-of-words model)：将文本以数值特征向量的形式来表示

1. 在整个文档集上为每个词汇创建了唯一的标记
2. 为每个文档构建一个特征向量，其中包含每个单词在此文档中出现的次数

每个文档出现的单词数量是整个词袋中单词总量的子集，所以特征向量中大多数元素为零。

- 1.将单词转换为特征向量

- 2.通过词频-逆文档频率计算单词关联度

  解决的问题：一个单词出现在多个文档中的话一般不具备辨识度和有用信息，要弱化其频率的影响。

  1. 原始词频(raw term frequency)：$tf(t,d)$ - 词汇t在文档d中出现的次数

  2. 逆文档频率(inverse document frequency)：

    $idf(t,d)=log\frac{n_d}{1+df(d,t)}$

    其中$n_d$是文档的总数，$df(d,t)$是包含词汇t的文档d的数量

  3. 词频-逆文档频率：$\text{tf-idf}(t,d)=tf(t,d)\times idf(t,d)$

  注：scikit-learn中实现用的公式与上述略有不同，并最后做了归一化

- 3.清洗文本数据

  使用正则表达式去掉不需要的符号等信息。

- 4.标记文档(tokenize)

  通过文档的空白字符将其拆分为单独的单词

  词干提取(word stemming)：提取单词原形

  词形还原(lemmatization)：获得语法上正确的单词标准形式

  停用词移除(stop-word removal)：如去掉is, and, has等

以上四步代码见：[8.2词袋模型.py](./Python机器学习-代码/8.2词袋模型.py)

### 训练用于文档分类的逻辑斯谛回归模型

代码见：[8.3训练用于文档分类的逻辑斯谛回归模型 .py](./Python机器学习-代码/8.3训练用于文档分类的逻辑斯谛回归模型.py)

### 在线算法与外存学习

代码见：[8.4在线算法与外存学习 .py](./Python机器学习-代码/8.4在线算法与外存学习.py)



# 第九章 在Web应用中嵌入机器学习模型

### 序列化通过scikit-learn拟合的模型

在Python对象与字节码之间进行转换，可以保存分类器当前状态： `import pickle `

代码见：[9.1序列化模型 .py](./Python机器学习-代码/9.1序列化模型.py)

### 使用SQLite数据库存储数据

### 使用Flask开发Web应用

### 将电影分类器嵌入Web应用

### 在公共服务器上部署Web应用

以上具体代码直接在github上clone了。

# 第十章 使用回归分析预测连续型目标变量

### 简单线性回归模型初探

目标：通过模型来描述某一特征（解释变量x）与连续输出（目标变量y）之间的关系。求解样本点的最佳拟合线。

预测的误差：回归线与样本点之间的垂直连线（偏移offset / 残差residual）

### 波士顿房屋数据集

相关系数矩阵 = 将数据标准化后得到的协方差矩阵

相关系数矩阵用来衡量两两特征间的线性依赖关系。

其包含皮尔逊积矩相关系数：
$$
r=\frac{\sum_{i=1}^n[(x^{(i)}-\mu_x)(y^{(i)}-\mu_y)]}{\sqrt{(x^{(i)}-\mu_x)^2}\sqrt{(y^{(i)}-\mu_y)^2}}=\frac{\sigma_{xy}}{\sigma_x\sigma_y}
$$
$\sigma_{xy}$: 特征x和y之间的协方差

$\sigma_x,\sigma_y$: 两个特征的标准差

代码见：[10.2波士顿房屋数据集 .py](./Python机器学习-代码/10.2波士顿房屋数据集.py)

结果：

![Figure](./pics/Figure_10-1.png)

![Figure](./pics/Figure_10-2.png)

### 基于最小二乘法构建线性回归模型

- 通过梯度下降计算回归参数

  最小二乘法：OLS，Ordinary Least Squares

  OLS线性回归：无单位阶跃的Adaline

  OLS代价函数：

  $J(w)=\frac{1}{2}\sum_{i=1}^n(y^{(i)}-\hat{y}^{(i)})^2$

  $\hat{y}=w^Tx$：预测值

  代码见：[10.3通过梯度下降计算回归参数.py](./Python机器学习-代码/10.3通过梯度下降计算回归参数.py)

  结果：

  ![Figure](./pics/Figure_10-3.png)![Figure](./pics/Figure_10-4.png)

- 使用scikit-learn估计回归模型的系数

  ​

### 使用RANSAC拟合高鲁棒性回归模型

### 线性回归模型性能的评估

### 回归中的正则化方法

### 线性回归模型的曲线化-多项式回归

- 房屋数据集中的非线性关系建模
- 使用随机森林处理非线性关系