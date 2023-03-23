# Knowledge 

我们如何让人工智能具有逻辑性，让AI能够通过已有的 Knowledge 通过逻辑判断得到新的 Knowledge，这将是我们这一节讨论的问题

在这略过一些离散数学关于逻辑的基本知识，这些知识应该是你在离散数学课堂上应该已经学到的

not

and

or

implication

biconditional

你应该知道上面的五个是指的是什么逻辑联结词

 ## model

我们引入 model 这个概念，model 是指我们对于所有的逻辑变元的一个可能取值。 这是一种真实世界的可能的一种情况，是逻辑空间的一个点。 由于每一个命题变元的取值都可能是 True 或者 False，所以我们在一个问题的逻辑空间中，一共有$2^n$种 model。

## Knowledge Base

knowledge base 是指我们设定的知识库，我们告诉机器，我们有些命题是正确的（对应我们的命题变元和各种逻辑联结词连接形成的命题）：这些规则实际上就是一系列的我们认为是真的命题，构成了 knowledge base。我们期望由这些命题，看是否能够得到某些命题的确切值。 这个过程我们叫做推理（inference），具体而言，这是指the process of  deriving new sentences from old ones

我们想要做到的就是询问 $KB \vDash \alpha ?$ ：也就是我们想知道从我们已有的 Knowledge Base 是否能推出 $\alpha$  这样的结论。

### Model Checking

一个比较显然的做法就是，我们考虑枚举每一个 Model，看所有满足 Knowledge Base 的 Model 是否同样满足 $\alpha$ 。这是一个简单朴素的做法，这样的缺点也很明显，我们需要花费很大的成本去枚举，尤其是有很多命题变元作为无关变量时，会有大量无意义枚举，这样的效率很低

通过这个做法我们可以发现，实际上我们想做的就是对一个命题的检验，这个命题把所有前提 and 起来，然后蕴含我们的结论，我们要判断的便是这个命题的真伪

关于这个的具体代码实现思路，无论是你使用状态压缩枚举，还是一般的递归实现，都是相当简单的，但是我还是建议仔细阅读一下 Python 代码，去理解 Python 应该是怎样的

当我们了解到这一点时，我们就可以解决很多问题了，不光是这节课开头时的哈利波特问题，以及后面的通过 Knowledge 推断命题变元的问题，所谓的Knowledge Engineering 也就是为了进行这个过程

我们考虑仔细的考虑一个例子：Mastermind

### Matsermind

