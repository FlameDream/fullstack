# onclick事件跳转到指定URL
一、如果本页面显示，可以直接用location,方法如下：

1、οnclick="javascript:window.location.href='url '"

2、οnclick="location='url '"

3、οnclick="window.location.href='url '"

 

二、如果页面中有frame可以在location前面添加

top.mainframe.frames['right_frame'] .location
