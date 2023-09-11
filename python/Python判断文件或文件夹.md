## Python判断文件或文件夹

在Python开发过程中，经常会用到判断某个文件或文件夹是否存在，遍历文件夹等操作。在数据处理、文件操作等应用场景中尤其常见。



## 方法一： 使用os模块中path模块

os模块是Python中对操作系统进行调用的接口，其中的path模块提供了一些用于处理文件或者目录路径的函数。path模块中的path.isfile()和path.isdir()函数，用于分别判断指定路径是否为文件或者文件夹。（path模块中存在一个path.exists()，用于判断文件或者文件夹是否存在）


以下是一个示例代码：

```python

import os

file_path = './data/xxxx.txt'
folder_path = './data'

# 判断文件是否存在
if os.path.isfile(file_path):
    print('文件存在！')
else:
    print('文件不存在！')

# 判断文件夹是否存在
if os.path.isdir(folder_path):
    print('文件夹存在！')
else:
    print('文件夹不存在！'

```

在上述代码中，我们使用os.path.isfile()和os.path.isdir()函数分别判断文件data/example.txt和文件夹data是否存在，并输出结果。


## 方法二：使用[pathlib](https://pypi.org/project/pathlib/)模块

Python第三方平台的介绍[pathlib](https://pypi.org/project/pathlib/) https://pypi.org/project/pathlib/模块，Python 3.4版本及以上版本中，提供了pathlib模块。但是在其他低版本中也可以安装使用（建议使用Python 3.2或更高版本，但pathlib也可用于Python 2.7和2.6。）

通过pathlib模块，可以使用Path.is_file()和Path.is_dir()方法分别判断指定路径是否为文件或文件夹


以下是一个示例代码：

```python

from pathlib import Path

file_path = Path('./data/xxxx.txt')
folder_path = Path('./data')

# 判断是否是文件
if file_path.is_file():
    print('是文件！')
else:
    print('不是文件！')

# 判断是否是文件夹
if folder_path.is_dir():
    print('是文件夹！')
else:
    print('不是文件夹！')

```


以上就是Python中判断文件或文件夹是否存


## 扩展

在数据处理、文件操作等我也也会经常用到对文件夹遍历

其中也是存在两种方法


**方法一：os模块中的**

```python
import os

os.listdir("./xxxx/")

```
**方法一：pathlib模块中的**

```python
from pathlib import pathlib
Path("./xxxx/").iterdir()
```





