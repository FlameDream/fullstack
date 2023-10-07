# Python String JSON相互转换

在Python中，字符串和JSON的相互转换通常使用json模块。这个模块提供了一个简单的方式来编码和解码JSON数据。


## 一、字符串转JSON

```python
import json  
  
# 假设你有一个字符串  
string_data = '{"name": "John", "age": 30, "city": "New York"}'  
  
# 使用json.loads方法将字符串转换为JSON  
json_data = json.loads(string_data)  
  
print(json_data)

#输出 ：{"name": "John", "age": 30, "city": "New York"}
# print(json_data['name'])会输出John。

```

**注意：**

如果你的字符串不是有效的JSON格式，json.loads()将会抛出一个json.JSONDecodeError异常。所以在使用json.loads()之前，要确保你的字符串是有效的JSON格式。



## 二、JSON转字符串

如果你有一个JSON对象，并希望将其转换为字符串，你可以使用json.dumps()函数。

```python
import json  
  
# 示例JSON对象  
json_data = {'name': 'John', 'age': 30, 'city': 'New York'}  
  
# 使用json.dumps将JSON对象转换为字符串  
string_data = json.dumps(json_data)  
  
print(string_data)

#上面的代码会输出：
#{"name": "John", "age": 30, "city": "New York"}'

```

**注意：**
json.dumps()函数还可以接受一些额外的参数，如indent，用于美化输出的JSON字符串。例如：

python
string_data = json.dumps(json_data, indent=4)
