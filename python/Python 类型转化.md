#Python基础类型转换

在Python中，经常会遇到就出类型的转换，可以使用以下方法将int、字符串和float类型相互转换：

### 1. int转str（字符串）：使用`str()`函数
```python
num = 123
str_num = str(num)
```

### 2. str（字符串）转int：使用`int()`函数
```python
str_num = "123"
num = int(str_num)
```

### 3. int转float：直接使用`float()`函数
```python
num = 123
float_num = float(num)
```

### 4. float转int：使用`int()`函数，但需要注意的是，会直接截断小数部分，而不是四舍五入
```python
float_num = 123.456
int_num = int(float_num)
```

### 5. float转str（字符串）：使用`str()`函数
```python
float_num = 123.456
str_num = str(float_num)
```