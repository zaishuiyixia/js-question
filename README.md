# javascript学习笔记
<br/><br/>

#### 1、![image](https://github.com/zaishuiyixia/js-question/raw/master/image/tostring.png),图片中toString.call(str)结果为什么不是"1,2,4"呢？
<br/>

语法：object.toString()

返回值：toString()函数的返回值为String类型。返回当前对象的字符串形式。

JavaScript的许多内置对象都重写了该函数，以实现更适合自身的功能需要。
![image](https://github.com/zaishuiyixia/js-question/raw/master/image/img1.png)
又因为：
![image](https://github.com/zaishuiyixia/js-question/raw/master/image/img2.png)
所以调用的是对象的toString方法。

#### 2、以下代码执行结果是什么
```
var t = function() {
    var n = 99;
    var t2 = function() {
    	n++
    	console.log(n)
    }
    return t2;
};

var a1 = t();
var a2 = t();

a1(); // 100
a1(); // 101

a2(); // 100
a2(); // 101
```
n 的值都是从 99 开始，执行 一次a1() 的时候，值会加一，再执行一次，值再加一，但是 n 在 a1() 和 a2() 并不是公用的(a1不等于a2)。可以理解为：同一个函数形成的多个闭包的值都是相互独立的。

#### 3、以下代码的执行结果是什么
```
var nAdd;
var t = function() {
    var n = 99;
    nAdd = function() {
    	 n++;
    }
    var t2 = function() {
    	console.log(n)
    }
    return t2;
};

var a1 = t();
var a2 = t();

nAdd();

a1(); //99
a2(); //100
```
当执行 var a1 = t()的时候，变量 nAdd 被赋值为一个函数 ，这个函数是function (){n++}，我们命名这个匿名函数为 fn1 吧。接着执行 var a = t()的时候，变量 nAdd 又被重写了，这个函数跟以前的函数长得一模一样，也是function (){n++}，但是这已经是一个新的函数了，我们就命名为 fn2 吧。

所以当执行 nAdd 函数，我们执行的是其实是 fn2，而不是 fn1，我们更改的是 a2 形成的闭包里的 n 的值，并没有更改 a1 形成的闭包里的 n 的值。所以 a1() 的结果为 99 ，a2()的结果为 100。

#### 4、以下代码的执行结果是什么？
```
var value = 1;

var foo = {
  value: 2,
  bar: function () {
    return this.value;
  }
}

//示例1
console.log(foo.bar()); // 2
//示例2
console.log((foo.bar)()); // 2
//示例3
console.log((foo.bar = foo.bar)()); // 1
//示例4
console.log((false || foo.bar)()); // 1
//示例5
console.log((foo.bar, foo.bar)()); // 1
```
 (foo.bar)() 是作为对象调用，this指向foo。(false || foo.bar)()，有赋值操作就是函数调用，this指向window。赋值表达式、逗号表达式、还有 || 这类的运算符（！！！运算符），如果和函数一起使用，返回值是目标函数的引用，所以说是foo.bar 已经不再是foo.bar，简单可以看成是bar就好了。
 
 #### 5、一下运算的结果是什么
 ```
 1 + 'a' // "1a"
false + 'a' // "falsea"
'3' + 4 + 5 // "345"
3 + 4 + '5' // "75"

如果一个运算子是字符串，另一个运算子是非字符串，这时非字符串会转成字符串，再连接在一起。
 ```
 
 ```
 1 - '2' // -1
1 * '2' // 2
1 / '2' // 0.5

除了加法运算符，其他算术运算符（比如减法、除法和乘法）的规则是：所有运算子一律转为数值，再进行相应的数学运算。上面代码中，减法、除法和乘法运算符，都是将字符串自动转为数值，然后再运算。
 ```
 
 ```
 var obj = { p: 1 };
obj + 2 // "[object Object]2"

var obj = { p: 1 };
var a = [1,2,3];
obj + a // "[object Object]1,2,3"
 ```
 如果运算子是对象，必须先转成原始类型的值，然后再相加。上面代码中，对象obj转成原始类型的值是[object Object]，再加2就得到了上面的结果。
