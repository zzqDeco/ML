

# Uncertainty

## Probability

我们来研究一下概率论的数学基础

我们用这样的一些希腊数字（如$\omega$）来代表事件

那么我们对应这样的一个事件在一般世界的发生概率就表示为$P(\omega)$

接下来，我们有一些关于概率的基础公理：

1. 任何事件的概率范围都在 0-1 之间
2. $\sum\limits_{\omega \in \Omega}P(\omega) =1$

### unconditional probability

无条件概率就是指在考虑两个事件同时发生的概率时，认为两个事件的概率满足不相互依赖，不相互依赖意味着$P(A)=P(A|B)$（这也同时意味着$P(B)=P(B|A)$），更特殊的，如果存在两个事件集合，如果这两个集合中的事件都是互斥的，且都满足$\sum\limits_{\omega \in \Omega}P(\omega) =1$，又同时满足如果从两个集合随便各选择一个事件，这两个事件不相互依赖，那么$P(AB)=P(A) \times P(B),A\in \Omega_1,B \in \Omega_2$。更具体的，如果这之中存在某种数值的和的关联（尤其是独立重复的某些 game，一个明显的例子就是丢两次骰子，将骰子的分数和当作对应要讨论的事件的时候），意味着这是一个卷积（如果你不了解卷积是什么，那你现在也不用了解）

### conditional probability

单纯考虑 unconditional 的问题是没有太大意义的，因为真实世界的概率关系是相当复杂的，有很多事件的相互作用并不是均匀的，

我们有$P(A|B)=P(AB)/P(B)$（虽然我们刚刚早已使用这个东西，但我还是写一下这个公式）

我们遇到的很多有意义的问题都是 conditional probability：我们在知道今天下雨的情况下想要知道明天下雨的

我们很容易从高中知识可以知道：

$P(a|b)=\frac{P(a \land b)}{P(b)}$

这样的公式告诉我们一种得到条件概率的方式，同时我们可以得到这样的东西：

Bayes' rule
$$
P(b|a)=\frac{P(b)\ P(a|b)}{P(a)}
$$


### random variable

拥有一些可能值的一个变量，变量被限定在一定范围之内

并且他们的每一种取值都有一定的对应概率

这如同上一章讲到的谓词逻辑，这将基于概率一个更抽象的体现，我们不再聚焦于事件，而是对象

通过定义 random variable，我们进一步有了概率分布概率分布更一般的告诉我们事物总有这样的一个性质，对于一个对象的某个行为，总有一个时间点有一样是会出现的

### probability distribution

概率分布是指在给定空间中变量出现不同情况的概率

概率分布的一个固有性质是无论你在哪一个空间考虑概率总和都是1

### independence

一个重要的关于概率的想法就是independence，就是说在给定空间上一个变量的情况并不会对另一个变量的概率分布产生影响

$P(B)=P(B|A)$

上述式子表现了我们independence是指的什么

显然，下面的式子也是成立的

$P(A\wedge B)=P(A)P(B)$

### Bayes' Rule

$P(a)P(b|a)=P(b)P(a|b)$

$P(b|a)=\frac{P(a|b)P(b)}{P(a)}$

这意味着我们在知道一个条件概率大情况下很容易知道另一个

我们只需要选择计算两个条件概率中比较容易的那一个，就可以得到both

这是Bayes' Rule的基本用法

### some rule

#### Negation

$P(\neg a)=1-P(a)$

#### Inclusion-Exclusion

$P(a\vee b)=P(a)+P(b)-P(a\wedge b)$

#### Marginalization

$P(a)=P(a\wedge b)+P(a\wedge(\neg b))$

这东西可拓展到b的概率分布空间上

### Bayesian network

data structure that represents the dependencies among random variables

从上面的rules中我们可以发现，变量与变量之间有复杂的离散的关联关系，我们用Bayesian network就可以捕获到变量与变量之间的复杂关系

这个网络是一个有向图，每一个点代表一个变量，每条边代表两个变量之间的相互作用，一般认为起点是重点的原因，我们需要知道在起点成立的情况下终点成立的概率，然后在这个DAG上从头开始进行松弛，得到最终的结果

### Inference and Approximate Inference

通过完全搜索，或者随机游走的形式，进行推理

### Markov assumption

#### Markov chain

Markov假设是指相同地位的一系列变量有前后线性变换形式的概率关系，在这种情况下，我们可以通过线性变换得到一些关于概率的信息

