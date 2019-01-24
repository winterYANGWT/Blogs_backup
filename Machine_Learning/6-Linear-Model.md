---
title: 6 Linear Model
date: 2018-09-25 14:53:28
category: Machine_Learning
---
<font size=6>线性模型
<!--more-->

---
<font size=5>线性模型的基本形式
<font size=3>给定一个由$d$个属性描述的实例$x=(x_1;x_2;...;x_d)$。线性模型的目标就是学习一个由属性线性组合来进行预测函数
$$f(x)=\omega^Tx+b,\omega=(\omega_1;\omega_2;...;\omega_d)$$
只要学得$\omega$和$b$之后，模型就已经确定下来。可以看出，线性模型形式简单，但是在机器学习的领域中有着重要的地位。许多功能强大的非线性模型可以在线性模型的基础上通过引入层级结构或高维映射得到。而且$\omega$直观描述了各属性对预测结果的影响，线性模型具有很好的解释性。假设线性模型在学得$f(x)$后,每一个属性的权重代表着不同属性对于结果的贡献度。
<br/>

<font size=5>线性回归
<font size=3>线性回归在给定含有$m$个样本的数据集上使用线性模型来尽可能准确地预测输出。线性回归的模型是
$$f(x_i)={\hat{\omega}}^T X,f(y)\simeq y$$
$$X=\left[
\begin{matrix}
x_{11} & x_{21} & \cdots & x_{m1}\\
x_{12} & x_{22} & \cdots & x_{m2}\\
\vdots & \vdots & \ddots & \vdots\\
x_{1d} & x_{2d} & \cdots & x_{md}\\
1 & 1 & \cdots & 1\\
\end{matrix}
\right]
$$
$$y=\left[
\begin{matrix}
y_1 & y_2 & \cdots & y_m\\
\end{matrix}
\right]
$$
$${\hat{\omega}}=\left[
\begin{matrix}
\omega_1 \\
\omega_2 \\
\vdots \\ 
\omega_d \\
b\\
\end{matrix}
\right]
$$
确定线性回归模型里的参数${\hat{\omega}}$来使得$f(X)$与$y$之间的差别减小。我们使用均方误差作为线性回归的性能度量,也就是
$${\hat{\omega}}^*=\arg\min_{\hat{\omega}} E_{\hat{\omega}}$$
$$=\arg\min_{\hat{\omega}} (y-{\hat{\omega}}^T X)^T(y-{\hat{\omega}}^T X)$$
基于均方误差最小化来进行模型求解的方法称为最小二乘法，最小二乘法的思想就是找到一条直线使所有样本到直线上的欧式距离最小。将$E_{\hat{\omega}}$对${\hat{\omega}}$进行求导,并让
$$\frac{\partial E_{\hat{\omega}}}{\partial {\hat{\omega}}}=2({\hat{\omega}}^T X-y)X^T$$
等于0就可以得到${\hat{\omega}}$的最优闭式解 : 
$$\hat{\omega}^{*T}=yX^T(XX^T)^{-1}$$
但是在现实任务中$XX^T$往往不是满秩矩阵，可能会有多个闭式解，选择哪一个解由学习算法的归纳偏好决定，最常见的方法就是引入正则化项。
<br/>

<font size=5>逻辑回归
<font size=3>
<br/>

<font size=5>线性判别分析
<font size=3>
