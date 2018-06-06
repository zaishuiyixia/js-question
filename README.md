# javascript学习笔记

#### 1、![image](https://github.com/zaishuiyixia/js-question/raw/master/image/tostring.png),图片中toString.call(str)结果为什么不是"1,2,4"呢？

语法：object.toString()

返回值：toString()函数的返回值为String类型。返回当前对象的字符串形式。

JavaScript的许多内置对象都重写了该函数，以实现更适合自身的功能需要。
![image](https://github.com/zaishuiyixia/js-question/raw/master/image/img1.png)
又因为：
![image](https://github.com/zaishuiyixia/js-question/raw/master/image/img2.png)
所以调用的是对象的toString方法。
