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

### Knowledge Base

knowledge base 是指我们设定的知识库，我们告诉机器，我们有些命题是正确的（对应我们的命题变元和各种逻辑联结词连接形成的命题）：这些规则实际上就是一系列的我们认为是真的命题，构成了 knowledge base。我们期望由这些命题，看是否能够得到某些命题的确切值。 这个过程我们叫做推理（inference），具体而言，这是指the process of  deriving new sentences from old ones

我们想要做到的就是询问 $KB \vDash \alpha ?$ ：也就是我们想知道从我们已有的 Knowledge Base 是否能推出 $\alpha$  这样的结论。

## Model Checking

一个比较显然的做法就是，我们考虑枚举每一个 Model，看所有满足 Knowledge Base 的 Model 是否同样满足 $\alpha$ 。这是一个简单朴素的做法，这样的缺点也很明显，我们需要花费很大的成本去枚举，尤其是有很多命题变元作为无关变量时，会有大量无意义枚举，这样的效率很低

通过这个做法我们可以发现，实际上我们想做的就是对一个命题的检验，这个命题把所有前提 and 起来，然后蕴含我们的结论，我们要判断的便是这个命题的真伪

关于这个的具体代码实现思路，无论是你使用状态压缩枚举，还是一般的递归实现，都是相当简单的，但是我还是建议仔细阅读一下 Python 代码，去理解 Python 应该是怎样的

当我们了解到这一点时，我们就可以解决很多问题了，不光是这节课开头时的哈利波特问题，以及后面的通过 Knowledge 推断命题变元的问题，所谓的Knowledge Engineering 也就是为了进行这个过程

我们考虑仔细的考虑一个例子：Mastermind

### Matsermind

Mastermind 是这样一个问题：我们有 n 个不同颜色的球，他们从前到后排成一列，现在给出一个可能的排列方式，并反馈有几个位置是把球放对了的，推理出正确的摆放方式

对于 Knowledge 的处理，我们可以将其转化为枚举所有可能的对于情况，然后全部 or 起来，然后再整体 add，得到整个 Knowledge Base。然后用相同的方式去得到 answer

当我们的 n 为4时，我们就会发现效率已经极低了：我们不仅要处理一个极为冗长的knowledge信息，还要枚举每个变元的状态，这无疑是一个巨大的工作量

 ## Inference Rules

回忆离散数学，我们有大量的规则用于处理命题的等价转化，同时我们想要把这个机械化的用于机器，让机器进行这样的演化提高效率。因此我们有需要接触 Inference Rules（其实这部分大致和你在离散数学学到的是一致的，不知道为什么这样的课程总是热衷于把一些东西讲一半让你可以快速使用）

你应该自己知道下面这些对应什么：

* Modus Ponens
* And Elimination
* Double Negation Elimination
* Implication Elimination
* Biconditional Elimination
* De Morgan's Law
* Distributive Property

## Theorem Proving

正如上次课讲到的，我们搜索贯穿 everywhere，在 Proving 当中，我们也可以引入搜索。

我们把我们本来知道的 Knowledge Base 当作 initial state，然后将我们刚刚学过的 Inference Rules 作为各种 actions，各种结果就是我们想要证明的。如果我们想要更好的处理，根据我们学习的内容可以通过定义各种的启发式函数，优化搜索效率。由于这是上节课的简单拓展，就不展开了

## Resolution

我们考虑从另一个角度切入，来考虑这个问题。从离散数学的角度，我们都知道如何用反证法来将一个难以推理的问题。（推理是相当麻烦的，因为它不太符合一定的范式，这使得我们的搜素有效性会比较低）

当我们由反证法来考虑的时候，这个问题变为我们证明一个命题是恒假的。在这里我们引入一个概念叫做解析（Resolution）

具体而言，解析是指：

$(P \lor Q) \land (\lnot P \lor R) \Rightarrow Q \lor R$

特别地，当 $Q$ 和 $R$ 都为 $0$ 的时候：

$P \land \lnot P \Leftrightarrow 0$

所以我们就想要尽量的得到合取范式，然后用解析的方式去证明整体的命题永假

解析可以使得命题中的命题变元减少，当其最简单的时候，若为0，那么得证，否则得否

我们的重心变为想要将找到一种将命题变为合取范式的有效方法，这很简单，我们只需要一层一层剥离：

* 先取消$\Leftrightarrow$
* 再取消$\Rightarrow$
* 再通过分配率变为合取范式

## First-Order Logic

我们将要接触一种完全不同于命题逻辑的逻辑系统：First-Order Logic

实际上就是谓词逻辑