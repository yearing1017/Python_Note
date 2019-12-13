# Python_Note
⏰ 记录不熟悉的、遗忘的Python3知识点

## Python3的格式化输出
- 在Python中，采用的格式化方式和C语言是一致的，用%实现，举例如下：
```python
>>> 'Hello, %s' % 'world'
'Hello, world'
>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
'Hi, Michael, you have $1000000.'
```
- `%`运算符就是用来格式化字符串的。在字符串内部，`%s`表示用字符串替换，`%d`表示用整数替换;
- 有几个`%?`占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个`%?`，括号可以省略。
- 常见的占位符：
> | 占位符 |   替换内容   |
> | :----- | :----------: |
> | %d     |     整数     |
> | %f     |    浮点数    |
> | %s     |    字符串    |
> | %x     | 十六进制整数 |
- 格式化整数和浮点数还可以指定是否补0和整数与小数的位数:
```python
print('%2d-%02d' % (3, 1))
print('%.2f' % 3.1415926)

# 输出,.表示空格
# .3-01
# 3，14
```
- 上面的%2d表示输出的宽度为2，右对齐，所以在3前面加一个空格。
- %02d表示输出的宽度为2，0表示不够宽度用0补齐。
- 如果不太确定应该用什么，%s永远起作用，它会把任何数据类型转换为字符串：
```python
>>> 'Age: %s. Gender: %s' % (25, True)
'Age: 25. Gender: True'
```
- 如果字符串里面的%是一个普通字符，这个时候就需要转义，用%%来表示一个%：
```python
>>> 'growth rate: %d %%' % 7
'growth rate: 7 %'
```
- 另一种格式化字符串的方法是使用字符串的format()方法，它会用传入的参数依次替换字符串内的占位符{0}、{1}:
```python
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
'Hello, 小明, 成绩提升了 17.1%'
```
