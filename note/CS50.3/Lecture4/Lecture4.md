# Learning

机器学习

## supervised learning

有监督的学习

简单来说就是我们给计算机一些成对的数据，希望他找到一个函数，能够从key到value

### classification

一类有监督的问题就是分类问题，分类问题的特点在于结果是离散的

#### nearest-neighbor classification

这个算法很草率，我们用离它最近的点的答案表示这个点的答案

这样我们参考的数据会很少，这使得我们答案准确度很低，很容易收到局部环境的影响

#### k-nearest-neighbor classification

针对上一个算法，我们考虑到仅知道最近的一个点的信息是片面的，所以我们改进成最近的 k 个点，这样可以使得我们的查询更加的整体化，但是同时，我们降低了其的速度。我们很多时候需要用到数据结构去得到最近的 k 个点的信息，这使得算法难度很大，而且这并不能完全解决其片面性，因为我们考虑点的信息时我们只考虑了距离这个要素，并没有考虑其他意义上的关系，如果我们的分类与这种距离上的临近无关，而是与一些更抽象的数学关系有关时，这将不再适用。有一些特殊情况也会使得这个算法在某些数据部分正确率很低。比如当我们的预测对象的成功区域是一个正三角形，但是我们预测三个角周围的数据的时候，很容易因为外面的点的数量比里面点的多，就将里面的点预测为错误区域中的点

#### Linear Regression

我们上述的做法有很大的局限性，一方面意味着我们即便是优化到knn，也无法避免 classification 的正确性在特殊图形的边缘的正确性，另一方面，作为一个机器学习算法，他没有办法精简模型，他需要庞大的数据集作为模型，在查询的时候需要重新对数据集进行数据结构上的维护，这无异是费时费力的

我们现在想要一种方式来找到两个类的一个边界，通过定义边界来避免knn的部分局限性

我们首先讨论 Linear 的二分割，也就是说我们用一个线性的低空间将高空间切分为正反两面，两面分别代表两个类（这样的分割无疑是局限的，首先只能处理二分割，其次将两个类的边界定义成一个线性的低维空间是在大多数情况下不可行的，曲面才是真实世界大多数的表现）

我们用一个方程代表低维空间，这样的空间显然有 n+1 个参数。
$$
w_0+w_1x_1+\dots+w_nx_n=0
$$
我们可以定义，当上面的等号变为大于号时，表示成功区域，小于号时，表示失败区域。我们现在的问题就变成了，如何利用线性回归找到这样的一个低维空间。这是一个很 normal 的数学问题

#### perceptron learning rule

这是其中一种线性回归的方法，这并没有展开讲解

大致意思是通过残差不断迭代得到线性回归平面

#### 总结

上述的问题都是比较偏 hard 的，意思就是说，我们有一个明确的界限，跨过这个界限结论就会有所改变。这对我们边界上的点并不友好，我们对内部的点可以很确切的知道，但是对于边界的点我们并不确定。我们尝试用soft的东西来拟合我们这种不确定性

#### Support Vector Mechine

支持向量机是一种监督学习算法，试图找到最佳超平面进行分类，通过间隔超平面和两类点的距离，使得得到的模型具有泛化能力

SVM可以在高维度上进行分割，使得分割不再只是 Linear 的，能够适应不同的环境

### regression

结果为连续实数的学习过程叫做 regression （回归）

在这里我们将更进一步的讨论，我们如何将机器学习，归结为一种模型的范式，这将与我们上一章的 optimization 相关

具体而言，我们会先得到一个函数作为一个起点，然后定义这个函数的优秀程度，然后尽可能的通过上一章的 optimization 的方法得到一个优秀的解

我们的 loss 函数就是上一章的 cost 函数，都是一个想要尽量小的量，用于描述我们距离目标的远近，也就是我们用于追寻最值的函数

这一部分的思路在李宏毅Lecture1中非常清晰

loss 函数的选择直接决定了我们模型的精度和偏向，loss 函数应该被设计成什么样子才能够使得能公正的表明两个模型哪个才是我们更想要的，才能更加切合我们的使用场景，这是我们需要考虑的

L1 loss 使用绝对值表示 loss

L2 loss 使用平方表示 loss

### overfitting

在数据中我们始终不能避免有离群点以及噪点的出现。如何我们的模型在训练集中的正确率极高，可能会导致我们的模型并没有抓住数据的抽象信息，只是停留在表面层次，会在测试集上表现很差。这样的情况是我们不希望的，ai的目的是实现预测效果的优秀，而不是在原始训练集自娱自乐。这是我们需要考虑到的

其中一个想法是，我们将模型的复杂度也归纳成一种 loss，与我们传统的距离目标的 loss 进行一个综合，这使得当我们的模型是以一种很僵硬的复杂度很高的方式拟合函数的时候，即便其拟合效果很好，我们也不认为这是一个优秀的模型，因为这样的模型很容易 overfitting。我们定义 $cost(h)=loss(h)+\lambda complexity(h)$，用这样的东西代替我们单纯的 loss，让我们更有可能得到更抽象的拟合。$\lambda$越大，意味着我们对于模型复杂性的要求越严格

上面的这个过程叫做正则化，正则化的本质就是对可能的 overfitting 进行惩罚

### holdout cross-validation

我们将已有的数据划分为training set和test set，training set用于训练模型，找到一个合适的模型，而test set用于验证模型在未知数据上的表现

### k-fold cross-validation

我们尝试把数据进行k划分，每次取出其中一个划分作为test set，其他的作为training set，将k个模型的平均值作为结果，避免 overfitting

## reinforcement learning

我们在面对一系列选择的问题时，有时候我们只关心一系列选择的结果尽量好，但是过程极其复杂，我们就需要reinforcement learning

比如我们想要设计一个alphago，我们需要对其每一个step进行奖励惩罚

同样的情况也适用于我们想要开发一个直立行走的虚拟机器人

对于 reinforcement learning，我们有两个要素：agent和environment

agent是我们对情况作出决断的ai，environment是agent可以作出操作的空间，在训练进行过程中，agent有一个对应的state，每次在environment中作出一个操作，我们都会对其进行评估，基于奖励或者惩罚

更简单的来讲，environment每时每刻给agent提供其所在状态和上一次操作的奖励，agent每时每刻在众多的可行操作中选择一个进行操作，并告诉environment下一个时间点空间应该如何变化

### Markov Decision Process

Markov Decision Process 确切地告诉我们一个操作之后，状态如何改变，得到的反馈是怎样的

具体而言，我们需要知道初始状态，初始状态下可以采取的操作，采取某个操作后状态的转移，或者状态的概率转移，对于状态转移的惩罚或奖励

### Q-learning

Q-learning的目的是找到一个函数$$Q(s,a)$$，表示针对现在的情况s下，我作出a这个操作，预期未来得到的奖励或者惩罚是多少

一开始我们将这样的函数全设为0，然后根据我们的随机游走，对这个函数进行更新

具体而言，我们通过这样的方式来更新我们的Q函数：
$$
Q(s,a)\leftarrow Q(s,a)+\alpha(\text{new value}-\text{old value})
$$
其中$\alpha$代表的是学习率，表示我们对新的结果的接受程度

$\alpha$代表的是0-1中的一个值

更具体的解释来说
$$
Q(s,a)\leftarrow Q(s,a)+\alpha((r+\max{Q(s',a')})-Q(s,a))
$$

#### Greedy Decision-Making

在操作时我选择最高期望值的选项，会使得我们并不能对未知领域进行探索，我们需要一些随机性

#### $\epsilon-greedy$

有$\epsilon$的概率随机游走，有$1-\epsilon$的概率进行最优游走

随机操作是非常有效的消除这种意义上的overfitting的方式，这点需要非常注意

与退火类似，我们依然可以选择在训练初期放大随机游走的尺度（概率），在训练的后期缩小这个尺度，使得结果趋于稳定

#### example

Nim游戏

## unsupervised learning

无监督学习

没有label，对于目标不好区分

### clustering

聚类，将一些点分类为相似的簇

#### k-means clustering

基于中心的分簇，不断转移中心，$k-means$的缺点非常明显，他不一定在数学意义上能够收敛，或者收敛效果很差
