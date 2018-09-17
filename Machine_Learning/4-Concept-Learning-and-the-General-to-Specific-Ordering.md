---
title: 4 Concept Learning and the General-to-Specific Ordering
date: 2018-08-25 00:04:43
category: Machine_Learning
---
<font size=6>概念学习和一般到特殊序
<!--more-->

---
<font size=5>概念学习
<font size=3>从前面我们看到，机器学习的过程就是归纳的过程，也就是从特殊样例归纳出一般概念。人类也经常找出事物中的一般规律。每个概念可以被认为是一个对象或事件合集，它是从更大的集合中选取的子集或是这个大集合中定义的布尔函数。比如鸟类的概念就包含于动物的概念当中。

概念学习 : 概率学习是指从有关某个布尔代数的输入输出训练样例中推断出该布尔代数。

接下来我们举一个Aldo进行水上运动的日子的例子。

![Machine_Learning_Table_2.1_Positive_and_negative_training_examples_for_the_target_concept_EnjoySport](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/Machine_Learning_Table_2.1_Positive_and_negative_training_examples_for_the_target_concept_EnjoySport.png)
我们用属性EnjoySport来表示这一天是否进行水上运动。也就是基于某天的属性来预测属性EnjoySport的值。我们使用属性的合取式来表示假设，每个假设为6个约束的向量，这些约束指定了属性Sky，AirTemp，Humidity，Wind，Water和Forest的值。每个属性可以取值为 : 
- 由$"?"$表示本属性任意可接受的值
- 明确指定的属性值
- 由"$\emptyset$"表示不接受任何值

如$<?,Cold,High,?,?,?>$，$<?,?,?,?,?,?>$，$<\emptyset,\emptyset,\emptyset,\emptyset,\emptyset,\emptyset>$。综上，这个概念学习的任务需要学习出使EnjoySport=yes的日子。

一般来说，概念学习任务可以被描述为 : 实例的集合、实例集合上的目标函数、候选假设的集合、训练样例这四个集合的集合。同样我们使用上面的例子来表达概念学习 : 
- 已知 : 
    - 实例集$X$ : 所有可能的日子，每个日子由其属性描述 : 
        - Sky (Sunny, Cloudy, Rainy)
        - AirTemp (Warm, Cold)
        - Humidity (Normal, High)
        - Wind (Strong, Weak)
        - Water (Warm, Cool)
        - Forecast (Same, Change)
    - 假设集$H$ : 每个假设被描述为6个属性的值约束的合取
    - 目标概念$c$ : EnjoySport (yes (1), no (0))
    - 训练集$D$ : 训练集中的样例来自于$X$中的一个实例$x$，以及目标概念值$c(x)$。若$c(x)=1$，这个实例为正例，或称为概念成员。若$c(x)=0$，这个实例称为反例，或称为非概念成员。
- 求解 : 
    - $H$中的一假设$h$，使得对于$X$中的$x$，$h(x)=c(x)$

综上，我们可以了解到机器学习的任务就是在整个实例集合$X$上找到与目标概念$c$相同的假设$h$。并且这个空间$X$包含了$3 \times 2 \times 2 \times 2 \times 2 \times 2=96$种实例。包含$5 \times 4 \times 4 \times 4 \times 4 \times 4=5120$种语法不同的假设。但是包含$\emptyset$的假设的空实例集合，将所有实例都划为反例。所以，语义不同的假设只有$1+4 \times 3 \times 3 \times 3 \times 3 \times 3=973$个。
<br/>

<font size=5>概念学习即为搜索
<font size=3>概念学习可以看作为一个搜索过程，范围是假设所表示的整个空间。搜索的目标也是去寻找能最好拟合训练样例的假设。更为自然的是，对于学习算法的研究就是考察对假设空间搜索的策略，特别是能够有效地搜索巨大的假设空间。
<br/>

<font size=5>假设的一般到特殊序
<font size=3>在许多的概念学习算法中，搜索假设空间的方法依赖一种结构 : 假设的一般到特殊序。利用这种结构我们可以在无限的假设空间中进行搜索，而不需要明确地列举出所有的假设。

为了说明这样一种结构，现在假设有这两个假设 : 
$h_1=<?,Warm,?,Strong,?.?>$,$h_2=<?,?,?,?,Strong,?>$。我们可以看到$h_2$比$h_1$的约束更加少，也就是说被$h_1$划为正类的样例，也能被$h_2$划为正类，或者说$h_2$比$h_1$更一般。

定义 : 令$h_j$和$h_k$都是定义在X上的布尔函数。我们称$h_j$比$h_k$更一般或相同，记作$h_j \geq_g h_k$
$$(\forall x \in X)[h_k(x)=1 \rightarrow h_j(x)=1]$$

或者一种严格的更一般的表示方法。

定义 : 令$h_j$和$h_k$都是定义在$X$上的布尔函数。我们称$h_j$比$h_k$更一般，记作$h_j >_g h_k$
$$(\forall x \in X)[(h_k(x)=1 \rightarrow h_j(x)=1) \wedge (h_j(x)=1 \nrightarrow h_k(x)=1) ]$$

这个结构正如下图所展示
![Machine_Learning_Figure_2.1_Instances_hypotheses_and_the_more-general-than_relation](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/Machine_Learning_Figure_2.1_Instances_hypotheses_and_the_more-general-than_relation.png)
<br/>

<font size=5>FIND-S : 寻找极大特殊假设
<font size=3>使用前面的假设一般到特殊序的结构，FIND-S从$H$中的最特殊假设开始，再在该假设覆盖正例失败时将其一般化。下为该算法的伪代码 : 
```nohighlight
input : X,H
FIND-S(X,H) : 
    h=<∅,∅,∅,∅,∅,∅>                        /*将h初始化为H中最为特殊的假设*/
    for positive training instance x in X : /*对于X中的每一个正例x*/
        for constraint a in h :             /*对于h中的每一个约束a*/
            if a is satisfied by x          /*如果约束满足x*/
            then do nothing                 /*就什么都不做，否则将a替换为更为一般的约束*/
            else replace a in h by the next general constraint that is satisifed by x
        end
    end
output : h
```

FIND-S算法沿着偏序链，从最特殊的假设逐渐转移到较一般的假设。在每一步的搜索中，假设只是在为了覆盖新的正例时被一般化。每一步的假设都是在那一点上与训练样例的最特殊的假设。

这个算法的特点就在于对属性约束的合取式描述的假设空间，该算法保证输出为$H$中最特殊的。如果训练数据都是正确的，最终的假设也会与所有的反例一致。然而这个算法也存在一些缺点 : 
- 学习过程是否收敛到正确的目标概念，虽然FIND-S能够找到于训练数据一致的假设，但是这个假设可能不是目标概念本身，可能还有其他假设。
- 使用最特殊的假设。在多个与训练数据一致的假设，FIND-S使用最特殊的，但是为什么不选择最一般的，或介于其中的假设?
- 训练数据出现错误或噪声会导致训练数据不相互一致。FIND-S算法忽略了所有反例，对于这种不一致的训练样例会严重破坏算法的正确性。
- 如果有多个极大特殊假设，FIND-S算法需要得到扩展使得算法能够允许在选择一般化的过程中进行路径回溯，以容纳目标假设位于偏序结构的另一分支的可能性。
<br/>

<font size=5>Candidate-Elimination : 候选消除算法
<font size=3>概念学习的另一途径就是候选消除算法。候选消除算法能够输出所有与训练样例一致的假设，这与FIND-S只能给出其中一个假设有着不同之处。候选消除算法也使用了一般到特殊序，所以无需列出所有假设集中的所有成员。同样，对于有噪声的数据，候选消除算法的性能会比较差。

为了描述这个算法需要引入的定义

定义 : 一个假设$h$与训练样例$D$一致，当且仅当对于$D$中的每一个样例$< x,c(x)>$,都有
$$Consistent(h,D)=(\forall <x,c(x)> \in D) h(x)=c(x)$$

候选消除算法能表示与训练样例一致的所有假设,在假设空间中这一子集称为关于假设空间$H$个训练样例$D$的变形空间,它包含了目标概念的所有合理的变型。
定义 : 关于假设空间$H$个训练样例$D$的变形空间,记为$VS_{H,D}$，是$H$中与训练样例$D$一致的所有假设构成的子集。
$$VS_{H,D}=\{h \in H|Consistent(h,D)\}$$

在介绍候选消除算法前先介绍一个简单的算法 : 列表后消除算法。这个算法列出假设集的所有成员，去除与样例不一致的假设，留下与训练数据一致的假设，下面是这个算法的伪代码 : 
```nonhighlight
input : H,D
Cadidate-Elimination(H,D) :
    VersionSpace=H                              /*将变形空间初始化为H*/
    for every training example <x,c(x)> in D :  /*对于D中的每一个样例*/
        for every hyperthesis h in H :          /*从变形空间中移除所有与样例不一致的假设*/
            if h(x)!=c(x)
            then H=H-h
        end
    end
output : VersionSpace
```

理论上，只要假设集$H$是有限的，就可以使用列表后消除算法。这一算法能够得到与所有样例一致的假设。但是，当样例集很大的时候会造成很大的开销，是不现实的。

使用偏序结构后，就不同列出所有的假设。变形空间也可以使用更简介的表示方法 : 将变形空间表示为极大一般和极大特殊的成员。这些成员形成了一般和特殊边界的集合。下图为EnjoySport概念学习问题的变形空间。FIND-S所找到的假设就是极大特殊的假设。其余还有5个假设。
![Machine_Learning_Figure_2.7_The_final_version_space_for_the_EnjoySport_concept_learning_problem](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/Machine_Learning_Figure_2.3_The_final_version_space_for_the_EnjoySport_concept_learning_problem.png)
变形空间使用两个集合就可以表示，分别是极大一般成员$G$，极大特殊成员$S$。这两个集合的定义如下 : 

定义 : 关于假设空间$H$和训练数据$D$的一般边界$G$，是在$H$中与$D$相一致的极大一般成员的集合。
$$G \equiv \{g \in H|Consistent(g,D) \land (\lnot \exists g' \in H)[(g'>_gg) \land Consistent(g',D)]\}$$

定义 : 关于假设空间$H$和训练数据$D$的特殊边界$S$，是在$H$中与$D$相一致的极大特殊成员的集合。
$$G \equiv \{s \in H|Consistent(s,D) \land (\lnot \exists s' \in H)[(s'>_gs) \land Consistent(s',D)]\}$$

现在，变形空间的组成为$G$，$S$，$G$和$S$之间偏序结构所规定的假设。

定理 : 令$X$为任意的实例集合，$H$为$X$上定义的布尔假设集合。令$c$ : $X \rightarrow \{0,1\}$为$X$上定义的任一目标概念，并令$D$为任意训练样例的集合$\{< c,c(x)>\}$.对所有的$X,H,c,D$以及良好定义的$S$和$G$ :
$$VS_{H,D}=\{h \in H|(\exists s \in S)(\exists g \in G)(g \geq_{g} h \geq_{g} s)\}$$

有了以上的定义后，我们来正式介绍候选消除算法。该算法先将$S$初始化为最特殊的假设，$G$初始化为最一般的假设。在处理训练样例时，将$S$和$G$边界集合分别一般化和特殊化。处理完后就得到与所有样例一致的集合。下面是该算法的伪代码。
```nonhighlight
input: H,D
G=[<?,?,?,?,?,?>]
S=[<∅,∅,∅,∅,∅,∅>]
for every training example <x,c(x)> in D :
    if <x,c(x)> is positive example
        for maximally genaral hyperthesis g in G : 
            if g(x)!=c(x)
                G=G-g
        end
        for maximally specific hyperthesis s in S :
            if s(x)!=c(x)
                S=S-s
                for every minimally generalization h of s : 
                    if h(x)==c(x) and some member of G is more general than h
                        S=S+h
                end
                Remove from S any hypothesis that is more general than another hypothesis in S
        end
    if <x,c(x)> is negative example
        for maximally specific hyperthesis s in S : 
            if s(x)!=c(x)
                S=S-s
        end
        for maximally general hyperthesis g in G :
            if g(x)!=c(x)
                G=G-g
                for every minimally specialization h of g : 
                    if h(x)==c(x) and some member of S is more specific than h
                        G=G+h
                end
                Remove from G any hypothesis that is more specific than another hypothesis in G
        end
end
output : G,S
```

从这个算法可以看出，正例使得特殊边界$S$变得一般化，反例使得一般边界$G$特殊化。且要注意的是，$S$边界说明了前面所有的正例，任何比$S$一般的假设都要能够覆盖$S$中的假设。而$G$边界说明了前面所有的反例，任何比$G$特殊的假设都要被$G$中的假设所覆盖。

候选消除算法能够收敛到目标概念需要两个要求 : (1) 训练样例中没有错误，(2) H中要确实包含描述目标概念的假设。如果不满足要求，在足够多的训练样例下，变形空间会变成一个空集。

假如我们的机器能够自己获取样例而非认为提供，那么应该选择什么样的样例呢？答案就是那些具有疑惑性的样例，也就是在变形空间中的一部分假设划为正例，另一类的假设划为反例。这种方法又叫做查询。最好的查询是每一次能够减少变形空间中的一部分假设。

在学习的过程中，真正的目标还未完全学习到，这种学习又叫不完全学习。但是就在这种情况下也能够进行一定置信度的分类。这种分类为以下规则所决定 : 
1. 实例满足S中所有的假设，被划分为正例
2. 实例不满足G中所有的假设，被划为反例
3. 实例满足变形空间中的一部分假设，不满足另一部分假设。且两部分假设数量相近，无法被划分
4. 实例满足变形空间中的一部分假设，不满足另一部分假设。但某部分假设数量比另一部分多，可以被由多数假设来决定，还可以加上置信度比例来表明投票的倾向。若所有假设有着相同的先验概率，正例投票占比可以看作实例为正例的可能性。
