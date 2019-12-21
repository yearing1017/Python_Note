# 💡 Numpy 相关知识

## 1.有关`np.argmin/argmax`在axis维度上的认识

- 先看一段有关argmin的代码：
```python
import numpy as np
a = np.random.randint(24, size=[4,2,3,3])

print("a本身为:")
print(a)

a_argmin = np.argmin(a, axis=1)
print("argmin: axis=1")
print(a_argmin)

print("加上None:")
print(a_argmin[:,None,:,:])
```

- 输出结果
```python
a本身为:
[[[[ 3 14  4]
   [ 5 23 12]
   [ 0 22 20]]

  [[12 17 10]
   [ 1 15  1]
   [ 2 18  7]]]


 [[[19  6  5]
   [ 9 22  7]
   [ 4  8 11]]

  [[10  8 12]
   [21  7  4]
   [17 21  8]]]


 [[[ 5 22  0]
   [ 0 13 13]
   [14  5 13]]

  [[11 18  4]
   [ 0 10  7]
   [22  0  9]]]


 [[[15 21  2]
   [13 20 12]
   [14  3  7]]

  [[12 23 22]
   [11  1 21]
   [11 20 14]]]]
argmin: axis=1
[[[0 0 0]
  [1 1 1]
  [0 1 1]]

 [[1 0 0]
  [0 1 1]
  [0 0 1]]

 [[0 1 0]
  [0 1 1]
  [0 1 1]]

 [[1 0 0]
  [1 1 0]
  [1 0 0]]]
加上None:
[[[[0 0 0]
   [1 1 1]
   [0 1 1]]]


 [[[1 0 0]
   [0 1 1]
   [0 0 1]]]


 [[[0 1 0]
   [0 1 1]
   [0 1 1]]]


 [[[1 0 0]
   [1 1 0]
   [1 0 0]]]]
[Finished in 0.2s]
```
- a本身是一个numpy的多维数组，shape:[4, 2, 3, 3]

- 理解：4代表第0维，其中输出a的结果首尾有4个`[`或`]`就代表该维度的数值

- 理解：2代表第1维，其中每3个`[`或`]`的中间就有两块数据，如下：
```python
[[[19  6  5]
   [ 9 22  7]
   [ 4  8 11]]

  [[10  8 12]
   [21  7  4]
   [17 21  8]]]
```
- 理解：3代表第2维和第3维，shape的最后两个数字表示行列。即每两个`[`或`]`包起来的数据：
```python
  [[10  8 12]
   [21  7  4]
   [17 21  8]]
```
- `np.argmin`表示在某维度上比较大小，取最小的下标组成，返回array，shape为原ndarray去掉axis维度后的shape[4, 3, 3]

- 在上面的例子中，axis=1表示第1维，即在每两个3x3的矩阵上下比较大小

- `np.argmax`同理，即取较大的下标返回。

- 在shape中加None，相当于加了一个新的维度，但是没有新的数值插入，仅仅多了表示维度的`[`和`]`

## 2. Numpy对ndarry的一些操作

- 看代码：
```python
# 仿照列表排序
A = np.arange(14,2,-1).reshape((3,4)) # -1表示反向递减一个步长
print(A)
# 输出
[[14 13 12 11]
 [10  9  8  7]
 [ 6  5  4  3]]
 
print(np.sort(A))
# 输出
[[11 12 13 14]
 [ 7  8  9 10]
 [ 3  4  5  6]]
 
# 矩阵转置，或print(A.T)
print(np.transpose(A))
# 输出
[[14 10  6]
 [13  9  5]
 [12  8  4]
 [11  7  3]]
 
# clip函数
print(np.clip(A,5,9))
# 输出
[[9 9 9 9]
 [9 9 8 7]
 [6 5 5 5]]
'''
clip(Array,Array_min,Array_max)

将Array_min<X<Array_max X表示矩阵A中的数，如果满足上述关系，则原数不变。

否则，如果X<Array_min，则将矩阵中X变为Array_min;

如果X>Array_max，则将矩阵中X变为Array_max.
'''
```

## 3. Numpy的索引和切片
- 看代码：
```python
import numpy as np
A = np.arange(3,15)
B = A.reshape(3,4)
print(B)
# B
[[ 3  4  5  6]
 [ 7  8  9 10]
 [11 12 13 14]]
 
print(B[2])
# B[2]
[11 12 13 14]

print(B[0][2]) #B[0][2]和B[0,2]等价，打印都是5

# list切片操作
print(B[1,1:3]) # [8 9] 1:3表示1-2不包含3


for row in B:
    print(row)
# 输出
[3 4 5 6]
[ 7  8  9 10]
[11 12 13 14]

# 如果要打印列，则进行转置即可
for column in B.T:
    print(column)
# 输出
[ 3  7 11]
[ 4  8 12]
[ 5  9 13]
[ 6 10 14]

# 多维转一维
A = np.arange(3,15).reshape((3,4))
# print(A)
print(A.flatten())
# flat是一个迭代器，本身是一个object属性
[ 3  4  5  6  7  8  9 10 11 12 13 14]
```
- 一些常见的切片如下图所示，每种颜色对应结果：
![numpy](https://github.com/yearing1017/Python_Numpy_Pandas_Note/blob/master/images/qiepian.jpg)
