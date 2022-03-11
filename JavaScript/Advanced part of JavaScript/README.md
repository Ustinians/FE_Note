# JS高级
## 基础总结深入
### 数据类型
1. 分类
    * 基本(值)类型
        - String 任意字符串
        - Number 任意数字
        - Bollean true/false
        - undefined
        - null
    * 对象(引用)类型
        - Object 任意对象
        - Function(一种特别的对象[可以执行])
        - Array(一种特别的对象[数值下标,内部数据是有序的])
2. 判断
* typedef
* instance
* ===
3. 相关问题
* 实例:实例对象
* 类型:类型对象
- undefined 与 null 的区别?
undefined 代表定义但是未赋值
null 代表定义并赋值了,只是值为null
- 什么时候给变量赋值为null
初始赋值为null,表示将要赋值为对象
1. 初始先赋值为null,再赋值为对象
````js
var b = null;
b = ['Loking',12];
````
2. 赋值为对象,最后用null置空,释放空间
让对象成为垃圾对象,被垃圾回收器回收
````js
b = ['Loking',12];
var b = null;
````
3. 严格区分变量类型和数据类型
* 变量类型
    - 基本类型
    - 对象类型
* 数据类型(变量内存值的类型)
    - 基本类型: 保存的就是的基本类型数据
    - 引用类型: 保存的是地址值
### 数据,变量与内存
1. 什么是数据?
* 存储在内存中,代表特定信息的东西(本质上是010101...(二进制))
* 数据的特点:可传递,可运算
* 一切皆数据
* 内存中所有操作的目标:数据
    - 算术运算
    - 逻辑运算
    - 赋值
    - 运行函数
2. 什么是内存?
* 内存条通电后产生的可存储数据类型的空间(临时的)
* 内存的产生与死亡: 内存条(线路板)==>通电====>产生存储空间==>存储数据==>处理数据==>断电==>内存空间和结构都消失
* 每个变量都对应着一块小内存,变量值就是内存中保存的数据
* 一块小内存产生的2个数据
    - 内部存储的数据
    - 地址值数据
* 内存分类
    - 栈:全局变量/局部变量
    - 堆:对象
- 在下面情况中,obj指向对象的地址,而a=obj,故a也指向对象的地址
````js
var obj = {name:"Tom"};
var a = obj;
````
- "."的作用是读取存储在地址中的数据
````js
console.log(obj.name);
````
3. 什么是变量?
* 可变化的量,由变量名,变量值来查找对应的内存,变量值就是保存的数值数据
* 每个变量都对应着一块小内存,变量名用来查找对应的内存,变量值就是内存中保存的数据
4. 内存,数据,变量三者之间的关系
* 内存是用来存储数据的空间
* 变量是内存的标识
### 对象
````js
var a = ×××
````
* ×××是什么
    - 如果×××是基本数据,保存的就是基本数据
    - 如果×××是对象,保存的就是对象的地址值
    - 如果×××是一个变量,保存的×××的内存内容(可能是基本数据,也可能是地址值)
````js
var m = {name:"Tom"};
var n = m;
m.name = "Jack";
console.log(n.name);//Jack
````
* 关于引用变量赋值问题
    - n个引用变量指向同一个对象
    - 通过一个变量修改对象内部数据,其他所有变量看到的是修改后的数据
    - 两个引用变量指向同一个对象,让其中一个引用对象指向另一个对象,另一个引用对象仍指向前一个对象
````js
var obj1 = {name:"Fris",age:19};
var obj2 = obj1;
obj1 = {name:"Loking",age:20};
console.log(obj1.name,obj1.age,obj2.name,obj2.age);
````
* 局部变量,执行后会被当作垃圾对象回收
* 形参只在函数作用域内有效
````js
var Q = {name:"Qi"};
function fn(obj){
    obj = {name:"Bai"};
    // 我悟了 
    // obj = Q;
    // obj = {name:"Bai"};
    // 先将实参的值传给形参,再通过形参修改数据
    // 如果修改的是同一个地址内的数据,则会改变
    // 但是obj直接把地址给改了
    // Q并没有改变
}
fn(Q);
console.log(Q.name);
````
* 在JS中调用函数时传递变量参数时,是值传递还是引用传递
    - 给函数定义形参，那么就相当于在函数执行时就会在函数内部生成一个新的变量
    - 理解一:都是值(基本/地址值)传递
    - 理解二:可能是值传递,也可能是引用传递(地址值)
* JS引擎如何管理内存?
    1. 内存生命周期
        - 分配小内存空间,得到它的使用权
        - 存储数据,可以反复进行操作
        - 释放小内存空间
    2. 释放内存
        - 局部变量:函数执行完自动释放
        - 对象:成为垃圾对象==>垃圾回收器回收
1. 什么是对象?
    * 多个数据的封装体
    * 用来保存多个数据的容器
    * 一个对象代表现实中的一个事物
2. 为什么要用对象?
    * 统一管理多个数据
3. 对象的组成
    * 属性:属性名(字符串)和属性值(任意)组成
    * 方法(一种特殊的属性):属性值是函数
4. 如何访问对象内部数据?
    * .属性名:编码简单
    *['属性名']:编码复杂
5. 什么时候必须用['属性名']的方式?
    * 属性名包含特殊字符
    * 变量名不确定
````js
var p = {
    name:"Fris",
    age:19,
    setName:function(name){
        this.name = name;
    },
    setAge:function(age){
        this.age = age;
    }
};
````
### 函数
1. 什么是函数
    * 实现特定功能的n条语句的封装体
    * 只有函数是可以执行的,其他类型的数据都不能执行
2. 为什么要用函数
    * 提高代码复用
    * 便于阅读交流
3. 如何定义函数
    * 函数声明
````js
function fn1(){
    console.log('fn1');
}
````
    * 表达式
````js
var fn2 = function(){
    console.log('fn2');
}
````
    * 区别:var 声明的会在浏览器加载页面前 就加载好
    * var声明会在浏览器加载之前就提升到当前作用域的最顶上
    * 函数声明 整体会被提升到当前作用域顶部，函数表达式，也会提升到顶部，但是只有变量名提升
4. 如何调用(执行)函数
    * test():直接调用
    * obj.test():通过对象调用
    * new test():new 调用
    * test.call/apply(obj):临时让test成为obj的方法进行调用
````js
function fn1(){// 函数声明
    console.log('fn1');
}
var fn2 = function(){// 表达式
    console.log('fn2');
}
var obj = {};
function test2(){
    this.abc = 'QiBai';
}
// obj.test2();
// 不能直接调用,根本就没有
// 可以让一个函数成为指定任意对象的方法进行调用
test2.call(obj);
console.log(obj.abc);
````
### 回调函数
1. 什么函数才是回调函数
    * 你定义的
    * 你没有调
    * 但最终它执行了
2. 常见的回调函数
    * DOM事件回调函数
    * 定时器回调函数
    * ajax请求回调函数
    * 生命周期回调函数
### 定时器
* 超时定时器(延时)
* 循环定时器(定时)
    - setTimeout
## 函数高级
## 面向对象高级
## 线程机制与事件机制
# IIFE
## 理解
* 全称:Immediately-Invoked Function Expression
* 匿名函数自调用
````js
(function(){
    console.log("________");
})();
````
````js
(function(){
    var a = 1;
    function test(){
        console.log(++a);
    }
    window.$ = function(){ //向外暴露一个全局函数
        return{
            test:test,
            // 一个名叫test的属性存了上面的test函数
        }
    }
})();
````
* $是一个函数
* $执行后返回一个对象
* 以(),[],开头必须加分号,要不就报错
## 作用
* 隐藏实现
* 不会污染外部(全局)命名空间
* 防止污染或占用全局变量
* 用它来编码JS模块
# this
## this是什么
* 任何函数本质上都是通过某个对象来调用的,如果没有直接指定就是window
* 所有函数内部都有一个变量this
* 它的值是调用函数的当前对象
## 如何确定this的值
* 直接调用函数，函数中的this永远指向window对象
* 通过方法的形式调用函数，函数中的this指向调用方法的对象
* 通过构造函数的形式调用函数，函数中的this指向新创建的那个对象
* test():window
* p.test():p
* new test():新创建的对象
* p.call(obj):obj
1. 以函数的形式调用时，this是window
2. call( )或apply() 通过第一个实参来指定函数中this
3. 以方法的形式调用时，this就是调用方法的对象
4. 以构造函数的形式调用时，this就是新创建的对象
5. 箭头函数中的this，是定义时所在的对象，而不是使用时的对象
* Vue、React、Angular三大主流前端框架
![](2021-04-29-10-40-04.png)

![](2021-04-29-10-41-21.png)
# 函数的prototype
1. 函数的prototype属性(图)
* 每个函数都有一个prototype属性,它默认指向一个Object空对象(即称为:原型对象)
* 原型对象中有一个属性constructor,它指向函数对象
2. 给原型对象添加属性(一般都是方法)
* 作用:函数所有实例对象自动拥有原型链中的属性(方法)
![](2021-04-29-11-43-51.png)
# 显式原型和隐式原型
1. 每个函数function都有一个prototype,即显式原型(属性)
2. 每个实例对象都有一个__proto__,可称为隐式原型(属性)
3. 对象的隐式原型的值为其对应构造函数的显示原型的值
4. 内存结构
5. 总结:
    * 函数的prototype属性:在定义函数时自动添加的,默认值是一个空Object对象
    * 对象的__proto__属性:创建对象时自动添加的,默认值为构造函数的prototype属性值
    * 程序员能直接操作显示原型,但不能直接操作隐式原型(ES6之前)
![](2021-04-29-12-09-15.png)

![](2021-04-29-12-20-42.png)

# 原型链
1. 原型链
    * 访问一个对象的属性时,先在自身属性中查找,找到并返回
    * 如果没有,再沿着__proto__这条链向上查找,找到返回
    * 如果最终没有找到,返回undefined
- 别名:隐式原型链
- 作用:查找对象的属性(方法)
- 实例对象才有隐式原型属性
- 实例对象的隐式原型 = 构造对象的显示原型
2. 构造函数/原型/实体对象的关系
3. 构造函数/原型/实体对象的关系(2)
* 普通对象的原型是空Object对象
![](2021-04-29-16-27-52.png)
乾坤巽震坎艮离兑
![](2021-04-29-21-06-55.png)
## 补充
1. 函数的显示原型指向的对象默认是空Object实例对象(但是Object不满足)
2. 所有函数都是Function的实例(包括Function本身),Function是它自身的实例
3. Object的原型对象是原型链的尽头
4. 读取对象的属性值时,会自动到原型链中查找
5. 设置对象的属性值时,不会查找原型链,如果当前对象中没有此属性,直接添加此属性并设置其值
6. 方法一般定义在原型中,属性一般通过构造函数定义在对象本身上
* 原型链相当于继承
* 不会查找原型链
* 读先从自身找，找不到再往原型链找，写是直接写在对象上
* Prototype是共享的方法不是内部的方法。用prototype的好处是，共享数据
![](2021-04-29-22-13-38.png)
* 每个对象都有自己的属性,但是修改时(?)不影响构造对象的显示原型链,只会影响自身(?)
````js
function Fn(){

}
Fn.prototype.a = 'xxx';
var fn1 = new Fn();
console.log(fn1.a,fn1);
var fn2 = new Fn();
fn2.a = 'yyy';
console.log(fn1.a,fn2.a,fn2);//给自己添加一个a属性
function Person(name,age){
    this.name = name;
    this.age = age;
}
Person.prototype.setName = function(name){
    this.name = name;
}
var p1 = new Person('Tom',12);
p1.setName('Bob');
console.log(p1);
var p2 = new Person('Jack',17);
p2.setName('Dba');
console.log(p1.name,p1.age);
console.log(p1.__proto__ === p2.__proto__);//true
````
## instanceof 
* 判断左边对象是不是右边对象的实例
* 表达式: A instanceof B
* 如果B函数的显式原型对象在A对象的原型链上,返回true,否则返回false
* Function是通过new自己产生的实例
* 所有函数（包括构造函数）都是Function的实例
* 所有函数的原型对象默认都是Object的实例(Object除外)
* 原型对象也是对象，是Object的实例对象
* object()是一个构造函数，从对象的角度看是个函数对象，所有的函数对象，都是最抽象的函数对象Function的实例。而函数对象Functionc也是对象，也是最一般的Object对象的实例。
![](2021-04-29-22-24-11.png)

![](2021-04-29-22-30-59.png)
![](2021-04-29-22-31-08.png)
# 原型_面试题
![](2021-04-30-16-04-17.png)
* A的原型对象被改变了 不是那个空的对象了
* 两个值指向同一个对象的地址，但后一个对象改变地址不会影响上一个对象地址
* 这个新赋值算开辟了另一个堆的地址空间，改变了地址了
````js
var A = function(){

}
A.prototype.n = 1;
var b = new A;
A.prototype = {
    n:2,
    m:3,
}
var c = new A;
console.log(b.n,b.m,c.n,c.m);
````
# 变量提升与函数提升
1. 变量声明提升
    * 通过var定义(声明)的变量,在定义语句之前就可以访问到
    * 值:undefined
2. 函数声明提升
    * 通过function声明的函数,在之前就可以直接调用
    * 通过var定义的函数在之前不能直接调用
    * 值:函数定义(对象)
3. 问题:变量提升和函数提升是如何产生的?
* 面试题:输出:undefined
    - 由于就近原则,函数先在自身内部寻找a
    - 相当于定义了a,即var a
    - 但是并没有为a赋值,所以此时a为undefined
````js
var a = 3;
function fn(){
    // var a;
    console.log(a);
    var a = 4;
}
fn();
console.log(b); // undefined 变量提升
fn2(); // 可调用 函数提升
fn3(); // 不能 变量提升
var b;
function fn2(){
    console.log('fn2()');
}
var fn3 = function(){
    console.log('fn3()');
}
````
# 执行上下文
1. 代码分类(位置)
    * 全局代码
    * 函数(局部)代码
2. 全局执行上下文
    * 在执行全局代码前将window确定为全局执行上下文
    * 对全局数据进行预处理
        - var定义的全局变量==>undefined,添加为window属性
        - function声明是全局函数==>赋值(fun),添加为window的方法
        - this==>赋值(window)
    - 开始执行全局代码
3. 函数执行上下文
    * 在调用函数时,准备执行函数体之前,创建对应的函数执行上下文对象(虚拟的,存在于栈中)
    * 函数创建是在堆里，执行是在桟里 
    * 对全局变量进行预处理
        - 形参变量==>赋值(实参)==>添加为执行上下文的属性
        - arguments==>赋值(实参列表),添加为执行上下文的属性
        - var定义的局部变量==>undefined,添加为执行上下文的属性
        - function声明的函数==>赋值(fun),添加为执行上下文的方法
        - this==>赋值(调用函数的对象)
    * 开始执行函数体代码
# 执行上下文栈
1. 在全局代码执行前,JS引擎就会创建一个栈来存储管理所有的执行上下文对象
2. 在全局执行上下文(window)确定后,将其添加到栈中(压栈)
3. 在函数执行上下文创建后,将其添加到栈中(压栈)
4. 在当前函数执行完之后,将栈顶的对象移除(出栈)
5. 当所有的代码执行完后,栈中只剩下window
![](2021-05-01-14-42-21.png)
![](2021-05-01-14-42-38.png)
* 执行上下文对象
    - windows
    - foo(x+b);
    - bar(10);
````js
var a = 10;
var bar = function(x){
    var b = 5;
    foo(x+b);
}
var foo = function(y){
    var c = 5;
    console.log(a+c+y);
}
bar(10);
````
# 面试题
* 依次输出什么?
* 整个过程中产生了几个执行上下文?
1. 先执行变量提升,再执行函数提升
````js
function a(){};
var a;
console.log(typeof a);
// function
````
2. 
````js
if(!(b in window)){
    var b = 1;
}
console.log(b);
// undefined
````
3. 
````js
var c = 1;
function c(c){
    console.log(c);
}
c(2);
// c is not a function
````
````js
var c;
function c(c){
    console.log(c);
}
c = 1;
c(2);
// c is not a function
````
# 作用域与作用域链
1. 理解
    * 就是一块"地盘",一个代码段所在的区域
    * 它是静态的(相对于上下文对象),在编写代码时就确定了
2. 分类
    * 全局作用域
    * 函数作用域
    * 没有块作用域(ES6有了)
3. 作用
    * 隔离变量,不同作用域下同名变量不会有冲突
* 没有块作用域
````js
if(true){
    var c = 3;
}
console.log(c);
````
* 执行上下文函数对象时N+1原则
* N: 调用提示函数
````js 
var a = 10,b = 20;
function fn(x){
    var a = 100,c = 300;
    console.log('fn()',a,b,c,x);
    function bar(x){
        var a = 1000,d = 400;
        console.log('bar()',a,b,c,d,x)
    }
    bar(100);
    bar(200);
}
fn(10);
````
![](2021-05-01-17-05-36.png)
# 全局作用域与执行上下文
1. 区别1
    * 全局作用域之外,每个函数都会创建自己的作用域,作用域在函数定义时就已经确定了,而不是在函数调用时(?)
    * 全局执行上下文环境是在全局作用域确定后,JS代码马上执行之前创建
    * 函数执行上下文环境是在调用函数时,函数体代码执行之前创建
2. 区别2
    * 作用于是静态的,只要函数定义好了就一直存在,且不会变化
    * 执行上下文环境是动态的,调用函数创建,函数调用结束时上下文环境就会被自动释放
3. 联系
    * 执行上下文环境(对象)是从属于所在的作用域
    ![](2021-05-01-17-31-33.png)
    ![](2021-05-01-17-32-29.png)
    * 全局上下文环境==>全局作用域
    * 函数上下文环境==>对应的函数使用域
* 定义了n个函数,就有n+1个作用域,其中1是指全局作用域
* 不管创建多少个同一个函数执行上下文他的作用域是已经确定的了
![](2021-05-02-10-02-46.png)
* 先看当前作用域,没有的话一层层向上找(就近原则)
* 有this找原型链，没有this找作用域链
````js 
var a = 2;
function fn1(){
    var b = 3;
    function fn2(){
        var c = 4;
        console.log(c);
        console.log(b);
        console.log(a);
        console.log(d);
    }
    fn2();
}
fn1();
````
# 作用域_面试题
1. 面试题一
    * 输出x = 10
    * 因为传的是地址值,相当于从内部调用外部函数
    * 作用域从一开始就已经确定好了,不会再发生变化
![](2021-05-02-10-15-28.png)

![](2021-05-02-10-19-00.png)

![](2021-05-02-10-21-21.png)
````js 
var x = 10;
function fn(){
    console.log(x);
}
function show(f){
    var x = 20;
    f();
}
show(fn);
````
2. 面试题二
    * 只有两个东西能形成作用域.一个是全局,一个是函数.函数外面没包函数,那就直接看到全局作用域.
    * fn2是obj的变量（属性），值为函数的地址值，但它不存在于函数作用域中，相当于var fun = function(){...}，可以通过fun()来调用函数，但不能通过function来访问fun
````js 
var fn = function(){
    console.log(fn);
}
fn();
var obj = {
    fn2:function(){
        console.log(this.fn2);
    }
}
obj.fn2();
````
# 循环遍历加监听
1. 需求:点击某个按钮,提示点击的是第n个按钮
2. 点击事件是回调函数,当循环结束之后才会执行
* 为每个对象添加一个属性
````js 
for(var i = 0;i < btns.length;i++){
    var obj = btns[i];
    obj.index = i;
    // 为每一个对象绑定一个属性
    obj.onclick = function(){
        alert("这是第 "+(this.index+1)+" 个按钮");
    }
}
````
* 立即执行函数（匿名函数自调用)IIFE
* 利用到了闭包
![](2021-05-02-11-29-32.png)
````js 
for(var i = 0;i < btns.length;i++){
    (function(i){// 第一个i，局部
        var obj = btns[i];// 局部
        obj.onclick = function(){
            alert("这是第 "+(this.index+1)+" 个按钮");
        }
    })(i)
    // 第二个i，全局
}
````
# 闭包理解
* 闭包就是创建一个函数，然后在函数里面调用外层函数的一个变量，然后在全局变量中再提取这个变量
* 接js是在全局变量里面的变量，可以在函数中调用，但是函数中的变量不能在全局变量中调用
* 闭包的作用就是把函数里面的变量可以在全局变量中调用
1. 如何产生闭包?
    - 当一个嵌套的内部(子)函数引用了嵌套的外部(父)函数的变量(函数)时，就产生了闭包
2. 闭包到底是什么?
    - 使用Chrome调试查看
    - 理解一：闭包是嵌套的内部函数(绝大部分人)
    - 理解二：包含被引用变量(函数)的对象(极少数人)
    - 注意:闭包存在于嵌套的内部函数
3. 产生闭包的条件?
    - 函数嵌套
    - 内部函数引用了外部函数的数据(变量/函数)
* 执行函数定义就会产生闭包(不用调用内部函数)
# 常见的闭包
- 存储在closure对象里的数据会常驻内存，我们需要产生closoure对象，就是闭包的规则
1. 将函数作为另一个函数的返回值
    * 产生了两个闭包(创建时产生)
````js 
function fn1(){
    var a = 2;
    function fn2(){
        a++;
        console.log(a);
    }
    return fn2;
}
var f = fn1();
f(); //输出3
f(); //输出4
````
2. 将函数作为实参传递给另一个函数调用
    * 定时器只是调用函数，不是定义函数对象,所以time不能够产生闭包
````js 
function showDelay(msg,time){
    setTimeout(function(){
        alert(msg);
    },time);
}
showDelay("柒白是真的!!!",1000);
````
# 闭包的作用
- 使用函数内部的变量在函数执行完之后,仍然存活在内存中(延长了局部变量的生命周期)
- 让函数外部可以操作(读写)到函数内部的数据(变量/函数)
问题:
1. 函数执行完之后,函数内部声明的局部变量是否还存在?
    * 一般是不存在
    * 存在于闭包中的变量才可能存在
2. 在函数外部能直接访问函数内部的局部变量吗?
    * 不能
    * 但是我们可以通过闭包的方式让外部操作它
# 闭包的生命周期
1. 产生:在嵌套内部函数定义执行完时就产生了(不是在调用)
2. 死亡:在嵌套的函数对象成为垃圾时
* 函数提升
````js 
function fn1(){
    // 此时闭包就已经产生了(函数提升,内部函数对象已经创建了)
    var a = 2;
    function fn2(){
        a++;
        console.log(a);
    }
    return fn2;
}
var f = fn1();// !
f(); //输出3
f(); //输出4 
f = null; // 闭包死亡(包含闭包的函数对象成为垃圾对象)
````
* 变量赋值
````js 
function fn1(){
    var a = 2;
    fn2 = function(){
    // 此时闭包产生(函数提升,内部函数对象已经创建了)
        a++;
        console.log(a);
    }
    return fn2;
}
var f = fn1();// !
f(); //输出3
f(); //输出4 
f = null; // 闭包死亡(包含闭包的函数对象成为垃圾对象)
````
# 闭包应用_自定义JS模板
* 具有特定功能的JS文件
* 将所有的的数据和功能都封装到一个函数内部(私有的)
* 只想外包暴露一个包含n个方法的对象或函数
* 模板的使用者,只需要通过模板暴露的对象调用方法来实现对应的功能
1. 
````js 
function myModule(){
    // 私有的数据
    var msg = "qibai";
    function doSomething(){
        console.log('doSomething()' + msg.toUpperCase());
        // 输出字符串的全部大写
    }
    function doOtherthing(){
        // 输出字符串的全部小写
        console.log('doOtherthing()' + msg.toLowerCase());
    }
    return {
        doSomething:doSomething,
        doOtherthing:doOtherthing
    };
}
````
2. 
````js 
// 匿名函数自调用
(function(){
    // 私有的数据
    var msg = "qibai";
    function doSomething(){
        console.log('doSomething()' + msg.toUpperCase());
        // 输出字符串的全部大写
    }
    function doOtherthing(){
        // 输出字符串的全部小写
        console.log('doOtherthing()' + msg.toLowerCase());
    }   
    window.myModule2 = {
        doSomething:doSomething,
        doOtherthing:doOtherthing
    } 
})()
````
3. 
````js 
// 匿名函数自调用
(function(w){
    // 私有的数据
    var msg = "qibai";
    function doSomething(){
        console.log('doSomething()' + msg.toUpperCase());
        // 输出字符串的全部大写
    }
    function doOtherthing(){
        // 输出字符串的全部小写
        console.log('doOtherthing()' + msg.toLowerCase());
    }   
    w.myModule2 = {
        doSomething:doSomething,
        doOtherthing:doOtherthing
    } 
})(window)
````
# 闭包的缺点及解决
1. 缺点
    * 函数执行之后,函数内的局部变量没有释放,占用内存时间会变长
    * 容易造成内存泄露
2. 解决
    * 能不用闭包就不用闭包
    * 及时释放
# 内存溢出与内存泄露
1. 内存溢出
    * 一种程序运行出现的错误
    * 当程序运行需要的内存超过了剩余的内存时,就抛出出内存溢出的错误
2. 内存泄漏
    * 占用的没有及时释放
    * 内存泄漏积累多了就容易导致内存溢出
    * 常见的内存泄漏
        - 意外的全局变量
        ````js 
        // 直接赋值相当于全局变量
        function fn(){
            a = 3;
            console.log(a);
        }
        fn();
        // a所占用的内存并没有释放
        ````
        - 没有及时清理的计时器或回调函数
        ````js 
        var timer = setInterval(function(){
            console.log("______");
        },1000);
        // clearInterval(timer);   
        ````
        - 闭包
        ````js 
        function fn1(){
            var a = 3;
            function fn2(){
                console.log(++a);
            }
            return fn2;
        }
        var f = fn1();
        f();
        // f = null;
        ````
# 闭包_面试题
* 闭包形成条件
    - 函数嵌套
    - 内部函数引用外部函数变量
1. 面试题一
    * 返回 The Window
    * 没有形成闭包
    * this 指的是 window
````js 
var name = "The Window";
var object = {
    name:"My Object",
    getNameFunc:function(){
        return function(){
            return this.name;
        };
    }
};
alert(object.getNameFunc()());
// My Window
````
2. 面试题二
    * 返回 My Object
    * that 指向 object2,形成闭包
````js 
var name2 = "The Window";
var object2 = {
    name2:"My Object",
    getNameFunc:function(){
        var that = this;
        return function(){
            return that.name2;
        };
    }
};
alert(object2.getNameFunc()());
// My Object
````
3. 面试题三
````js 
function fun(n,o){
    console.log(o);
    return{
        fun:function(m){
            return fun(m,n);
        }
    };
}
var a = fun(0); a.fun(1); a.fun(2); a.fun(3);
// undefined 0 0 0
var b = fun(0).fun(1).fun(2).fun(3);
// undefined 0 1 2
var c = fun(0).fun(1); c.fun(2); c.fun(3);
// undefined 0 1 1
````
# 对象创建模式
1. 方法一:Object构建函数模式
    * 套路:先创建空的Object对象,在动态添加属性/方法
    * 适用场景:起始时不确定对象内部数据
    * 问题:语句太多
````js 
var p = new Object();
p.name = 'Tom';
p.age = 12;
p.setName = function(name){
    this.name = name;
}
// 测试
p.setName('Jack');
console.log(p.name,p.age);
````
2. 方法二:对象字面量模式
    * 套路:适用{}创建对象,同时指定属性/方法
    * 适用场景:起始时对象内部的数据是确定的
    * 问题:如果创建多个对象,有重复代码
````js 
var p = {
    name:'Tom',
    age:12,
    setName:function(name){
        this.name = name;
    }
};
p.setName('Jack');
console.log(p.name,p.age);
````
3. 方法三:工厂模式
    * 套路:通过工厂函数动态创建对象并返回
    * 适用场景:需要创建多个对象
    * 问题:对象没有一个具体的类型,都是Object类型
````js 
function createPerson(name,age){
    var obj = {
        name:name,
        age:age,
        setName:function(name){
            this.name = name;
        }
    };
    return obj;
}
var p1 = createPerson('Tom',12);
var p2 = createPerson('Fris',19);
console.log(p1.name,p1.age);
console.log(p2.name,p2.age);
````
4. 方式四:自定义构造函数模式
    * 套路:自定义构造函数,通过new创建对象
    * 适用场景:需要创建多个类型确定的对象
    * 问题:每个对象都有相同的类型,浪费内存
````js 
function Person(name,age){
    this.name = name;
    this.age = age;
    this.setName = function(name){
        this.name = name;
    }
}
var p1 = new Person('Tom',12);
var p2 = new Person('Jack',23);
p1.setName("Jack");
console.log(p1.name,p1.age);
function Student(name,price){
    this.name = name;
    this.price = price;
}
var s = new Student('Fris',19);
console.log(s.name,s.price);
console.log(p1,p2);
````
5. 构造函数+原型的组合模式
    * 套路:自定义构造函数.属性在函数中初始化,方法添加到原型上
    * 适用场景:需要创建多个类型确定的对象
````js 
function Person(name,age){
    this.name = name;
    this.age = age;
}
Person.prototype.setName = function(name){
    this.name = name;
}
var p1 = new Person('Loking',20);
var p2 = new Person('Fris',19);
console.log(p1,p2);
````
# 原型链继承
1. 套路
    1. 定义父类型构造函数
    2. 给父类型的原型添加方法
    3. 定义子类型的构造函数
    4. 创建父类型的对象赋值给子类型的原型
    5. 将子类型原型的构造属性设置为子类型
    6. 给子类型原型添加方法
    7. 创建子类型的对象:可以调用父类型的方法
2. 关键
    1. 子类型的原型为父类性的一个实例对象 
![](2021-05-04-15-40-45.png)
![](2021-05-04-15-42-48.png)
![](2021-05-04-15-43-19.png)
````js 
// 父类型
function Supper(){
    this.supProp = "Supper property";
}
Supper.prototype.showSupperProp = function(){
    console.log(this.supProp);
}
// 子类型
function Sub(){
    this.subProp = "Sup property";
}
Sub.prototype = new Supper();
Sub.prototype.showSubProp = function(){
    console.log(this.subProp);
}
var sub = new Sub();
sub.showSupperProp();
// sub.toString();
sub.showSubProp();
````
# 组合继承
## 借用构造函数继承
1. 套路
    1. 定义父类型构造函数
    2. 定义子类型构造函数
    3. 在子类型构造函数中调用父类型构造
2. 关键
    1. 在子类型构造函数中通用call()调用父类型构造函数
````js 
function Person(name,age){
    this.name = name;
    this.age = age;
}
Person.prototype.setName = function(name){
    this.name = name;
}
function Student(name,age,price){
    Person.call(this,name,age);// 为了得到属性
    // 相当于this.Person(name,age)
    // this.name = name;
    // this.age = age;
    this.price = price;
}
Student.prototype = new Person();// 为了能看到父类型的方法
Student.prototype.setPrice = function(price){// 修正constructor属性
    this.price = price;
}
var s = new Student('Tom',20,14000);
s.setName('Bob');
s.setPrice(25000);
console.log(s.name,s.age,s.price);
````
# 闭包_终极面试题
````js 
function fun(n,o){
    console.log(o);
    return{
        // 闭包
        fun:function(m){
            return fun(m,n);
        }
    }
}
var a = fun(0);//fun(0,undefined)
a.fun(1);//fun(1,0)
a.fun(2);//fun(2,0)
a.fun(3);//fun(3,0)
// undefined 0 0 0
var b = fun(0).fun(1).fun(2).fun(3); 
//fun(0,undefined) fun(1,0) fun(2,1) fun(3,2)
//undefined 0 1 2
var c = fun(0).fun(1);
// fun(0,undefined) fun(1,0)
c.fun(2);// fun(2,1)
c.fun(3);// fun(3,1)
// undefined 0 1 1
````
# 进程与线程
* 进程
    - 程序的第一次执行,它占有一片独有的内存空间
    - 可以通过windows任务管理器查看进程
* 线程
    - 是进程的一个独立执行单元
    - 是程序执行的一个完整流程
    - 是CPU的最小的调度单元
![](2021-05-04-16-35-44.png)
1. 进程:程序的一次执行.它占有一片独有的内存空间
2. 线程:CPU的基本调度单位,是程序执行的一个完整流程 
3. 进程与线程
    * 一个进程中一般至少有一个运行的线程:主线程
    * 一个进程中也可以同时运行多个线程,我们会说程序是多线程运行的
    * 一个进程内的数据可以供其中的多个线程直接共享
    * 多个线程之间的数据是不能直接共享的
4. 浏览器运行是单进程还是多进程
    * 有的是单进程
        - FireFox
        - 老版IE
    * 有的是多进程
        - Chrome
        - 新版IE
5. 如何查看浏览器是否是多进程运行呢
6. 相关知识
    * 应用程序必须运行在某个进程的某个线程上
    * 一个进程中至少有一个运行的线程:主线程,进程启动后自动创建
    * 一个进程中也可以同时运行多个线程,我们会说程序是多线程运行的
    * 一个进程内的数据可以供其中的多个线程直接共享
    * 多个进程之间的数据是不能直接共享的
    * 线程池(thread pool):保存多个线程对象的容器,实现线程对象的反复利用
7. 相关问题
    1. 何为多进程与多线程
        - 多进程运行:一应用程序可以同时启动多个实例运行
        - 多线程:在一个线程内,同时有多个线程运行
    2. 比较单线程与多线程
        - 多线程
            * 优点
                能有效提升CPU的利用率
            * 缺点
                创建多线程开销
                线程间切换开销
                思索与状态同步问题
        - 单线程
            * 优点
                顺序编程简单易懂
            * 缺点
                效率低
    3. JS是单线程还是多线程
        - JS是单线程运行的
        - 但适用H5中的Web Workers可以多线程运行
    4. 浏览器运行是单线程还是多线程
        - 都是多线程运行的
    5. 浏览器运行是单进程还是多进程
        - 有的是单进程
            * Firefox
            * 老版IE
        - 有的是多进程
            * Chrome
            * 新版IE
        - 如何查看浏览器是否是多进程运行的呢?
# 浏览器内核
1. 支持浏览器运行的最核心的程序

2. 不同的浏览器可能不一样
    * Chrome,Safari:wedkit
    * Firefox:Gecko
    * IE:Trident
    * 360,搜狗等国内浏览器:Trident + webkit
3. 内核由很多模块组成
    * JS引擎模块:负责JS程序的编译与运行
    * html,css文档解析模块:负责页面文本的解析
    * DOM/CSS模块:负责dom/css在内存中的相关处理
    * 布局和渲染模块:负责页面的布局和效果的绘制(内存中的对象)
    * 定时器模块:负责定时器的管理
    * 事件响应模块:负责事件的管理
    * 网络请求的模块:负责ajax请求
# 定时器引发的思考
1. 定时器真的是定时执行的吗?
    * 定时器并不能保证真正定时执行
    * 一般会稍微延迟一丁点(可以接受),也有可能延长很长时间(不能接受)
2. 定时器回调函数是在分线程执行的吗?
    * 在主线程执行的,JS是单线程
3. 定时器是如何实现的?
    * 事件循环模型
# JS是单线程的
![](2021-05-09-16-01-10.png)
1. 如何证明JS执行时单线程的?
    * setTimeout()的回调函数是在主线程执行的
    * 定时器回调函数只能在运行栈中的代码全部执行完之后才有可能执行
2. 为什么JS要用单线程模式,而不用多线程模式?
    * JavaScript的单线程,与它的用途有关
    * 作为浏览器脚本语言,JavaScript的主要用途是与用户互动,以及操作DOM
    * 这决定了它只能是单线程,否则将会带来很复杂的同步问题
3. 代码的分类
    * 初始化代码
    * 回调代码
4. JS引擎执行代码的基本流程
    * 先初始化代码,包含一些特别的代码
        - 设置定时器
        - 绑定监听
        - 发送ajax请求
    * 后面某个时刻才会执行回调代码
