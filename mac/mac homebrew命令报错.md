在使用Mac 的brew命令安装git时,出现以下报错:



/usr/local/Homebrew/Library/Homebrew/macos_version.rb:4:in `require': /usr/local/Homebrew/Library/Homebrew/version.rb:497: syntax error, unexpected <<, expecting end (SyntaxError)
<<<<<<< Updated upstream
^~
/usr/local/Homebrew/Library/Homebrew/version.rb:500: syntax error, unexpected ===, expecting end
=======
^~~
/usr/local/Homebrew/Library/Homebrew/version.rb:506: syntax error, unexpected >>, expecting end
>>>>>>> Stashed changes
^~
/usr/local/Homebrew/Library/Homebrew/version.rb:514: dynamic constant assignment
  HEAD_VERSION_REGEX = /\AHEAD(?:-(?<commit>.*))?...
  ^~~~~~~~~~~~~~~~~~
/usr/local/Homebrew/Library/Homebrew/version.rb:763: dynamic constant assignment
  NULL = Version.new("NULL").tap { ...
  ^~~~
/usr/local/Homebrew/Library/Homebrew/version.rb:764: syntax error, unexpected end-of-input, expecting end
	from /usr/local/Homebrew/Library/Homebrew/macos_version.rb:4:in `<top (required)>'
	from /usr/local/Homebrew/Library/Homebrew/global.rb:80:in `require'
	from /usr/local/Homebrew/Library/Homebrew/global.rb:80:in `<top (required)>'
	from /usr/local/Homebrew/Library/Homebrew/brew.rb:18:in `require_relative'
	from /usr/local/Homebrew/Library/Homebrew/brew.rb:18:in `<main>'



/usr/local/Homebrew/Library/Homebrew/version.rb:368:in `initialize': Version........

通过百度搜索,有以下两个解决方法:

1.升级brew 版本

brew update-reset
2.快捷打开version.rb这个文件的所在路径并编辑，/usr/local/Homebrew/Library/Homebrew/version.rb，把系统版本写死

在尝试过以上两种方法都失败的情况下,想起自己的Mac升级过,升级成macOS Monterey 12.0.1版本,于是将brew重新卸载重装,这里卸载参考了以下博文
————————————————
版权声明：本文为CSDN博主「cyh_90」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/cyh_90/article/details/124986707