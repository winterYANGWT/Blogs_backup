---
title: 5 Decision Tree
date: 2018-09-02 14:37:05
category: Machine_Learning
---
<font size=6>决策树
<!--more-->

---
<font size=5>决策树算法
<font size=3>决策树是一种逼近离散值目标的方法，从名字可以看出，这种模型使用树型结构来进行决策。这种结构也能表示为多个if-then规则。
![Machine_Learning_FIGURE_3.1_A_decision_tree](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/Machine_Learning_FIGURE_3.1_A_decision_tree.png)

决策树的每个节点指定了对实例的某个属性的测试，这个节点的后续分支对于该属性的可能取值。分类实例的方法就是从树的根节点开始测试节点的属性，按照给定实例的属性值进行向下移动，直到分类完成。决策树代表实例属性值约束的合取的析取式。从树根到树叶的每一条路径对于属性值的合取，所以决策树就是这些合取的析取。所以上面的决策树对应这个的表达式 : 
$$(Outlook=Sunny \land Hunmidity=Normal)$$
$$\lor (Outlook=Overcast)$$ 
$$\lor (Outlook=Rain \land Wind=Weak)$$

决策树适合解决具有以下特征的问题 : 
- 实例具有一系列固定的属性和值，在最简单的决策树问题中，每一个属性取少数离散的值。在一些扩展的算法中，可以接受具有连续值的属性。
- 输出值为离散的，一些扩展算法中允许输出连续值的函数。
- 需要析取的描述。
- 训练数据可以包含错误，决策树对于错误有良好的健壮性。
- 训练数据可以包含缺少属性值的实例

下面是决策树生成算法
```nonhighlight
input : D,A
Decision_Tree(D,A):
    root=new node
    if all examples in D belong to a category C
    then root is labeled as C
    else if A==∅ or all samples in D have the same value in A
    then the root is lableed as the category with the largest number of D
    else choose the best attribution a*
    for every value v in a*:
        branch= new node
        D_v=the set of the samples whose value in a* is v
        if D_v==∅
        then branch is labeled as the category with the largest number of D
        else branch=Decision_Tree(D_v,A\{a*})
output : Decision Tree
```

决策树的生成算法是一个递归算法，这个递归会在三种情况下返回 : 
- 当前节点包含的样本属于同一个类别，无需划分。
- 属性集为空，或者样本在所有属性上取值相同，无法划分。
- 当前节点的样本集合为空，不能划分。
<br/>

<font size=5>最优属性划分选择
<font size=3>从决策树的生成算法来看，其中至关重要的一步就是选择最优属性。一个划分标准就是纯度，也就是决策树的分支节点所包含的的样本尽可能属于同一类别。有三种常用的指标，对应了三种不同的算法。

- 信息增益。
    定义 : 假设当前样本集合$D$中第$k$类样本所占的比例为$p_k$ ($k=1,2,\cdots,|Y|$)，则$D$的信息熵定义为
    $$Ent(D)=-\sum_{k=1}^{|Y|} p_k \log_2{p_k}$$

    信息熵越小，则样本集合的纯度越高。在信息论中，熵的另一种解释就是 : 熵确定了要编码集合$D$中的任意成员 (以均匀的概率随机抽出的一个成员) 的分类所需要的最少二进制位数。举个例子,在二分类问题中，正反例各占一半，从上的公式可以得到信息熵为1，编码这两类需要1位二进制编码。当只有正例时，信息熵为0，也就是无需编码。如果正例占比0.8，信息熵位0.217，对应的编码方法就是对正例较短的编码，对反例进行较长的编码，平均每条编码为0.217位。信息增益就是假设使用某一属性进行划分后对纯度的提升。

    定义 : 假定离散属性$a$有$V$个可能的取值$\{a_1,a_2,\cdots,a_V\}$,第$v$个分支节点包含了$D$中所有在属性$a$上取值为$a_v$的样本，记为$D_v$。使用$a$进行划分的信息增益为
    $$Gain(D,a)=Ent(D)-\sum_{v=1}^V{\frac{|D_v|}{|D|}Ent(D_v)}$$

    一般而言，信息增益越大，意味着使用这种属性来进行划分对样本集合带来的纯度提升就越大。带来信息增益最大的划分属性就是最优的划分属性。ID3决策树算法就是使用信息增益为准则来选择划分属性。
- 增益率。
    信息增益准则有一个缺点，就是会对可取值数目值较多的属性有所偏好，当可取值较多，样本会被分散到不同的属性值上。从表面上看纯度大幅提高，但是这样的树不具有泛化能力。为了解决这个问题，使用增益率来选择最优划分属性。
    $$Gain\_ratio=\frac{Gain(D,a)}{IV(a)}$$
    $$IV(a)=-\sum_{v=1}^V{\frac{|D_v|}{|D|}\log_2{\frac{|D_v|}{|D|}}}$$

    $IV(a)$被称为属性$a$的固有值，当$a$的可取值越多，$IV(a)$的值通常会越大。CS4.5算法使用增益率来找到最优划分属性。但是，使用增益率准则可能会对那些可取值数目较少的属性有所偏好。所以CS4.5算法不直接使用增益率，而是先从属性中找出信息增益高于平均水平的属性，再从中选择增益率最高的。
- 基尼指数
    CART决策树使用基尼指数来选择划分属性。数据集$D$的纯度用下面的公式来进行度量。
    $$Gini(D)=\sum_{k=1}^{|Y|}{\sum_{k' \neq k}{p_k p_{k'}}}$$
    $$=1-\sum_{k=1}^{|Y|}{p_k^2}$$

    这个公式直观来看，反应了从数据集中抽取两个样本，其类别不一致的概率。因此，基尼指数越小，数据集的纯度越高。使用属性$a$划分数据集后的基尼指数为
    $$Gini\_index(D,a)=\sum_{v=1}^{|Y|}{\frac{|D_v|}{|D|}Gini(D_v)}$$
    
    我们选择使划分后基尼指数最小的属性来划分数据集。
<br/>

<font size=5>剪枝算法
<font size=3>为了避免决策树过拟合现象，可以使用剪枝算法来主动去掉一些分支。剪枝算法有预剪枝和后剪枝两种。预剪枝算法是指再决策树生成的过程中，对每个节点划分前进行估计，如果节点划分不能带来泛化性能的提升，就停止划分并将该节点设为叶节点。后剪枝则是先生成一棵完整的决策树，然后自底向上对非叶节点进行考察，若将该节点更换为叶节点能够带来泛化性能的提升，就使用叶节点替换该子树。预剪枝使决策树的许多分支都没有展开，降低了过拟合风险和训练时间。但是，有些分支当前划分不能提高泛化性能甚至有所降低，却有可能在后续划分提高泛化性能。禁止一些分支的展开，带来了欠拟合的风险。后剪枝却不会有这种风险，泛化性能也一般优于预剪枝。但是，后剪枝在决策树生成后进行，且对所有节点进行考察，增加了时间开销。

<font size=5>缺失值处理
<font size=3>
