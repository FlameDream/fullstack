文章目录
一、使用pymysql连接MySQL数据库
二、使用ORM操作MySQL数据库
1.认识ORM
2.演示
一、使用pymysql连接MySQL数据库
安装三方包：pip install pymysql

演示:

连接数据库
创建游标
定义sql语句
执行sql语句
关闭连接
import pymysql

cursorclass=pymysql.cursors.DictCursor # 可以使查询出的单条数据数据为字典形式，多条数据为列表套字典

# 1.连接数据库
db = pymysql.connect(host='localhost', user='root', password='', 
        database='school',cursorclass=pymysql.cursors.DictCursor)
        
# 2.创建游标对象
cursor = db.cursor()

# 3.定义SQL语句
sql = 'insert into students(id,name) values(101,"钟无艳")' # 添加数据

# 4.执行SQL语句
cursor.execute(sql)

# 5.获取结果，涉及改变数据库需要提交
print(cursor.fetchone())  # 只获取一个数据，并且还是个生成器
print(cursor.fetchall())  # 会获取所有数据
db.commit()  # 提交，执行了改变数据库的操作，必须提交才会生效，查询可以不加

# 6.断开连接
cursor.close()
db.close()

封装一下

import pymysql


class MyDB:
    def __init__(self, h='localhost', u='root', p=None, db=None):
        """连接数据库和定义游标"""
        self.db = pymysql.connect(host=h, user=u, password=p, database=db,
                                  cursorclass=pymysql.cursors.DictCursor)
        self.cursor = self.db.cursor()
        
    #-----------------------------------------------------------②操作
         # 
    def select(self, sql):
        """查询操作"""
        self.cursor.execute(sql)  # 执行sql语句
        return self.cursor.fetchall()  # 会获取所有数据

        
    def change(self, sql):
        """增删改操作"""
        self.cursor.execute(sql)
        self.db.commit()  # 提交数据
        print('操作成功！')
        return self.cursor.rowcount #获取操作的行数
        
    def __del__(self):
        """自动关闭连接"""
        self.cursor.close()
        self.db.close()


if __name__ == '__main__':
    my = MyDB(db='school')
    sql = input('请输入SQl语句：')
    print(my.select(sql))


二、使用ORM操作MySQL数据库
1.认识ORM
ORM，全称Object Relational Mapping，意为对象关系映射。

ORM是一个操作数据库的框架
ORM会将python代码翻译成对应数据库的sql语句
ORM会将每张表映射为一个类，并将表中的字段映射成对象的属性。
优点：使用方便：我们在使用ORM时，可以不关心用的是什么数据库，只专心关心业务逻辑。即使开发人员不会sql语句，也能与数据库进行交互。

缺点：ORM生成的sql语句，不是最优的sql语句，执行效率会比较低。

python中有一个ORM，即sqlalchemy，仿照的是Django框架的ORM。
flask中有一个ORM插件：flask-sqlalchemy

2.演示
Python安装三方包：pip install sqlalchemy

导包
创建连接
声明一个基类
创建类–数据模型
操作
import sqlalchemy
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker # 类似于 pymysql中的游标


# 1.创建连接
"""
数据库类型+数据库操作的包:// 用户名:密码@主机地址/你要操作的数据库
mysql://scott:tiger@hostname/dbname
"""
db = sqlalchemy.create_engine('mysql://root:@localhost/sqlorm')

# 2.创建基类
base = declarative_base(db)

# 3.创建类 必须继承基类  创建模型
class User(base):
    # 表名
    __tablename__='user'
    id = sqlalchemy.Column(sqlalchemy.Integer,primary_key=True)
    name = sqlalchemy.Column(sqlalchemy.String(32)) # varchar()
    age = sqlalchemy.Column(sqlalchemy.Integer)

class Userinfo(base):
    __tablename__='userinfo'
    id = sqlalchemy.Column(sqlalchemy.Integer,primary_key=True)
    phone = sqlalchemy.Column(sqlalchemy.String(20))

class Shop(base):
    __tablename__='shop'
    id = sqlalchemy.Column(sqlalchemy.Integer,primary_key=True)
    name = sqlalchemy.Column(sqlalchemy.String(32))


if __name__ == '__main__':
    # 执行数据库迁移 创建表 
    # 注意：创建表只会映射一次，创建成功则不会再映射
    base.metadata.create_all(db)

    # 绑定一个实例
    # s = sessionmaker(bind=db)
    # # 创建回话对象  类似于游标
    # session = s()

    # 添加
    # user = User(name='hello',age=16)
    # session.add(user)
    # session.commit()
    # session.add_all([
    #     User(name='world',age=1),
    #     User(name='python',age=28),
    #     User(name='PHP', age=30),
    # ])
    # session.commit()
    # 查询
    # 查询所有的数据 返回一个列表
    # res = session.query(User).all()
    # for i in res:
    #     print(i.name,i.age)
    # 通过主键查询一条数据 返回一个对象
    # res = session.query(User).get(1)
    # print(res.name,res.age)
    # 条件查询 返回的是一个列表
    # res = session.query(User).filter_by(name='hello').all()
    # print(res)
    # res = session.query(User).filter(User.name=='hello').all()
    # print(res)
    # 修改数据
    # res = session.query(User).get(1)
    # print(res.name)
    # res.name='HELLO'
    # session.commit()
    # 删除数据
    # res = session.query(User).get(1)
    # session.delete(res)
    # session.commit()
————————————————
版权声明：本文为CSDN博主「张烫麻辣亮。」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_40558166/article/details/100109288