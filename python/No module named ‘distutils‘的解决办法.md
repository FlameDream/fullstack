# ModuleNotFoundError: No module named ‘distutils‘的解决办法

最近在前端开发过程中，npm install发现一个ModuleNotFoundError: No module named ‘distutils‘的问题。经过查看发现Python环境没有“distutils”的情况，在Python低版本的时候并没有这种情况。（Python开发过程中，使用distutils同样也会遇到这样的问题）

解决方案：

```python

pip install setuptools
```

“setuptools”是一个处理Python软件包的工具包，它依赖于 distutils。安装 setuptools可以间接解决没有“distutils”的问题.(根据需要是否全局安装或者是项目安装)


