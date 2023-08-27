# Neural Networks

 生物学发现神经是由神经元处理电信号并相互连接形成的

Artificial Neural Networks实际上是一些函数代替神经元进行抽象的过程

unit是指节点，节点与节点之间通过这些函数相连

现在的问题变成了，我们要以什么形式的函数拟合，我们想要知道每个函数拟合后的具体参数

这当中很大一部分李宏毅讲的很清楚了

后面就是对于loss的梯度下降

Neural Networks中的一种非常常见的降低过拟合的方法是dropout

方式就是取消某些节点的选择权限，避免Neural Networks对某一个节点过度依赖，获取到的信息不够抽象

computer vision

对于实际世界的图像认知

对于图像而言，如果我们单纯把各个像素点用作神经前端，这会导致会忽略图像的一些特征，比如图像中有某一条线，单纯的像素排列很难意识到这一点，所以我们需要一些特征工程

比如 image convolution

图像卷积的作用在于从图像中提取特征，其核心是各式各样的核

即便我们拥有图像卷积这样的技术，我们还是要考虑，对于一个庞大图像，拥有过于庞大的像素阵列，我们需要进行压缩。这样的东西叫做 pool

pool 与 convolution 很相似，但是也有不同的地方，这里不做细致的阐述

实际上 CNN(convolutional neural network)，就是一个使用 pool，convolution，neural network的机器学习算法

convolution 和 pool 与 neural network 能够有效结合的一个重要原因是 convolution 和 pool 实际上相当于是一种人工意义上的抽象特征，而 neural network 是通过 optimization 来进行的抽象特征，人工意义上的抽象特征以人力的方式介入了特征的方向和速度，提高了效率和效果

从某种意义上而言，convolution 和 pool 是一种特殊的 neural network，他们的 node 的关系是相对固定的，同样，如果你愿意你也可以对我们所谓的核进行 optimization

正是如此我们更愿意在 convolution 和 pool 上进行 neural network

我们现在讨论的 neural network 属于 feed-forward  neural network 

这样的 neural network 仅仅在一个方向上传播，因此也比较局限

其中一个点就在于，我们的输入输出都是标准的，我们有固定的神经元用于输入，也有固定的神经元用于输出

与此相对应的有 recurrent neural network，这样的神经网络接受自己的结果作为自己的输入，这样的神经网络适用于你需要得到一系列不确定长度的结果的时候

最典型的例子就是，有关于nlp的东西的时候，如果我们的结果是一个句子，我们就需要一个单词一个单词的输出，每一个单词的输出又是给予上一个（或者许多）单词的语法结构的，我们后一个单词的输出就需要根据前面的进行调整



