# pyodbc使用详解

pyodbc是用于调用ODBC数据库接口而封装的python模块，可以方便地连接和操作数据库。

首先，需要安装pyodbc，可以使用pip进行安装：


```shell
pip install pyodbc
```
连接数据库可以通过指定Driver和DSN，也可以通过配置文件。

连接DB的代码如下：


```python
# 指定Driver连接
connection = pyodbc.connect('Driver={ODBC Driver 13 for SQL Server};Server=XXX;database=XXX;uid=XXX;pwd=XXX')
# 通过DSN连接(需要先配置)
connection = pyodbc.connect('DSN=MSSQL-ABC;Server=XXX;database=XXX;uid=XXX;pwd=XXX')
```
其中，XXX需要替换为实际的服务器名、数据库名、用户名和密码。

常用操作主要是通过游标（cursor）进行操作，创建游标的代码如下：


```python
cursor = connection.cursor()
```
下面是一些常用操作：

1. select：查询数据


```python
cursor.execute("SELECT * FROM dbo.RecognisePhoto WHERE RecogStatus=0 AND Cate=2")
```
注意：select必须为第一条语句，一次执行不能同时返回多个select结果集；不能使用commit()。
2. update、insert及delete：需要持久化的操作，可以多条一起执行，然后提交事务。


```python
cursor.execute('UPDATE RecognisePhoto SET RecogStatus=0 WHERE RecogStatus=-1')
cursor.execute('UPDATE RecognisePhoto SET RecogStatus=-1 WHERE RecogStatus=0 AND Cate=2')
connection.commit() # 必须提交事务否则会产生事务锁
```
3. 既带select又带需要持久化操作的如update的语句，不能放在同一个执行里，可分多个execute或采用存储过程。
4. 遍历结果：通过游标捉个遍历。


```python
row = cursor.fetchone() while row: print (str(row[0]) + " " + str(row[1])) row = cursor.fetchone()
```
5. 批量执行：使用executemany可以批量插入数据。


```python
sql = 'INSERT INTO 表名 VALUES(%s,%s,%s)' #不管什么类型,统一使用%s作为占位符
param = ((username1, salt1, pwd1), (username2, salt2, pwd2), (username3, salt3, pwd3)) #对应的param是一个tuple或者list
n=cursor.executemany(sql,param)
```