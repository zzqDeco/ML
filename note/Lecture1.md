# Regression

## What's Machine Learning ?

Looking for Function

我们需要去拟合得到很多不同的函数（映射）

接收各种信息，得到我们想要的

* 如果我们得到的是一个 scalar ，这样的过程叫做 regression 
* 如果我们得到的是一个从多个选项中找出的一个选项，这样的过程叫做 classification
* 如果我们得到的是一个有结构的text或者image等一系列的内容，那我们把这个过程叫做 Structured Learning

## Different Kinds of Machine Learning

### Supervised Learning

通过大量的资料训练，让机器得到一个范式，可以根据已有信息推测出未知信息的结果。

### Self-supervised Learning

#### Pre-train

Develop general purpose knowledge

我们期待机器通过 Pre-train ，得到通用的本领，可以适用于普遍目标

用大量的 unlabeled images 去对其进行训练，提高效率（用 unlabeled images 去训练有很强的特殊性，后续会具体讲解）

### 