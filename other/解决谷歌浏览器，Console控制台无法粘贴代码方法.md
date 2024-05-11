# 解决谷歌浏览器，Console控制台无法粘贴代码方法

在使用浏览器调试过程中，会使用到Console控制台复制粘贴的功能。但是会出现无法粘贴的问题。


网上搜了一些方法：1.使用右键选择粘贴  2.Settings -> Experiments -> Filter 输入 Past，取消勾选 Show warning about Self-XSS when pasting

这两种方法在最新的浏览器中并不能使用


可以根据浏览器的提示：

Warning: Don’t paste code into the DevTools Console that you don’t understand or haven’t reviewed yourself. This could allow attackers to steal your identity or take control of your computer. Please type ‘allow pasting’ below and hit Enter to allow pasting.
2main.js:183 

在console中手动输入 “allow pasting”。就可以粘贴了