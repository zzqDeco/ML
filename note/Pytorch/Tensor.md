# PyTorch Tensor

PyTorch提供了多种方法来创建张量。以下是一些常见的创建张量的方式：

## 创建未初始化的张量

```python
# 创建一个未初始化的5x3张量
x = torch.empty(5, 3)
```

## 创建零张量

```python
# 创建一个5x3的零张量
x = torch.zeros(5, 3, dtype=torch.long)
```

## 创建单位张量

```python
# 创建一个5x5的单位张量（对角线上的元素为1，其他为0）
x = torch.eye(5)
```

## 创建随机初始化的张量

```python
# 创建一个5x3的随机初始化张量
x = torch.rand(5, 3)
```

## 从已有数据创建张量

```python
# 从一个已有的list创建张量
x = torch.tensor([5.5, 3])

# 从一个已有的NumPy数组创建张量
import numpy as np
np_array = np.array([5.5, 3])
x = torch.from_numpy(np_array)
```

## 创建等差数列张量

```python
# 创建一个从0到10的等差数列张量，共有5个元素
x = torch.linspace(0, 10, steps=5)
```

## 创建具有相同大小的张量

```python
# 创建一个和x大小相同的零张量
x = torch.zeros_like(x)

# 创建一个和x大小相同，随机初始化的张量
x = torch.rand_like(x, dtype=torch.float)  # 注意重写dtype!
```

## 创建指定形状的张量

```python
# 创建一个形状为5x3的张量，元素都是1
x = torch.ones(5, 3)

# 创建一个形状为5x3的张量，元素都是0
x = torch.zeros(5, 3)

# 创建一个形状为5x3的张量，元素由正态分布随机生成
x = torch.randn(5, 3)
```

## 创建满足特定分布的张量

```python
# 创建一个形状为5x3的张量，元素为从均匀分布中抽取的随机数
x = torch.rand(5, 3)

# 创建一个形状为5x3的张量，元素为从标准正态分布中抽取的随机数
x = torch.randn(5, 3)

# 创建一个形状为5x3的张量，元素为从0到1的均匀分布中抽取的随机整数
x = torch.randint(0, 2, (5, 3))
```

### 点对点操作（Element-wise Operations）

- 加法：`torch.add`
- 减法：`torch.sub`
- 乘法：`torch.mul`
- 除法：`torch.div`
- 幂运算：`torch.pow`

```python
x = torch.tensor([1, 2, 3])
y = torch.tensor([4, 5, 6])
torch.add(x, y)  # 等价于 x + y
torch.sub(x, y)  # 等价于 x - y
torch.mul(x, y)  # 等价于 x * y
torch.div(x, y)  # 等价于 x / y
torch.pow(x, 2)  # 等价于 x**2
```

### 归约操作（Reduction Operations）

- 求和：`torch.sum`
- 均值：`torch.mean`
- 最大值：`torch.max`
- 最小值：`torch.min`
- 乘积：`torch.prod`

```python
x = torch.tensor([1, 2, 3])
torch.sum(x)
torch.mean(x.float())  # mean需要浮点数输入
torch.max(x)
torch.min(x)
torch.prod(x)
```

### 比较操作（Comparison Operations）

- 最大值：`torch.max`
- 最小值：`torch.min`
- 等于：`torch.eq`

```python
x = torch.tensor([1, 2, 3])
y = torch.tensor([3, 2, 1])
torch.max(x, y)
torch.min(x, y)
torch.eq(x, y)
```

### 矩阵操作（Matrix Operations）

- 矩阵乘法：`torch.mm` 或 `@` 操作符
- 矩阵向量乘法：`torch.mv`
- 点积：`torch.dot`
- 外积：`torch.outer`

```python
x = torch.tensor([[1, 2], [3, 4]])
y = torch.tensor([[5, 6], [7, 8]])
torch.mm(x, y)  # 或者 x @ y
v = torch.tensor([1, 2])
torch.mv(x, v)
torch.dot(v, v)
torch.outer(v, v)
```

### 变形操作（Manipulation Operations）

- 重塑：`torch.reshape` 或 `tensor.view`
- 转置：`torch.transpose`
- 连接：`torch.cat`
- 分割：`torch.chunk`
- 增加维度：`torch.unsqueeze`
- 减少维度：`torch.squeeze`

```python
x = torch.tensor([[1, 2], [3, 4]])
x.reshape(4, 1)
torch.transpose(x, 0, 1)
torch.cat((x, x), dim=0)
torch.chunk(x, chunks=2, dim=0)
torch.unsqueeze(x, 0)
torch.squeeze(torch.unsqueeze(x, 0))
```

### 其他操作

- 梯度操作：`torch.autograd`
- 填充：`torch.fill_`
- 剪裁：`torch.clamp`
- 排序：`torch.sort`

```python
x = torch.tensor([1.0, 2.0, 3.0], requires_grad=True)
y = x * x
y.backward(torch.tensor([1.0, 1.0, 1.0]))
x.grad  # 梯度
x.fill_(5)
torch.clamp(x, min=0, max=10)
torch.sort(x)
```

这些操作是构建复杂数学表达式的基础，并在机器学习和深度学习模型中广泛使用。