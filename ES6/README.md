# ES6(ECMA Script)
* 兼容性问题(https://kangax.github.io/compat-table/es6/)
## let变量声明及声明特性
* let声明变量的特性
    1. 变量不能重复声明
    ````js
    let b = 100;
    let b = 200;
    // ERROR
    ````
    2. 块及作用域,只在代码块内有效
    3. 不存在变量提升(不允许在变量声明前使用变量)
    4. 不影响作用域链
    ````js
    {
        let shcool = "尚硅谷";
        function fn2(){
            console.log(shcool);
        }
        fn2();
    }
    ````
### let经典实例
1. 使用var时
````js
for(var i = 0;i < items.length;i++){
    items[i].onclick = function(){
        // 修改当前元素的背景颜色
        // this指的是window中的 items[i]
        this.style.background = "pink";
    }
}
````
2. 使用let时
````js
for(let i = 0;i < items.length;i++){
    items[i].onclick = function(){
        // 修改当前元素的背景颜色
        items[i].style.background = "pink";
    }
}
````
## const声明常量
* 值不能修改的量称为常量
1. 一定要赋初始值
2. 一般常量使用大写(潜规则)
3. 常量的值不能修改
4. 块级作用域(let也是)
5. 对于数组和对象的修改,不算做对常量的修改,不会报错(地址未改变)
## 变量的解构赋值
* ES6允许按照一定的模式从数组和对象中提取值,对变量进行赋值
1. 数组的解构
````js
const F4 = ['Qi','Bai','Mei','He'];
let [Q,B,M,H] = F4;// 用var也可以
console.log(Q);
console.log(B);
console.log(M);
console.log(H); 
````
2. 对象的解构
````js
const Xuan = {
    name:'Qi',
    age:19,
    wu:function(){
        console.log("Modao")
    }
};
let {name,age,wu} = Xuan;
console.log(name);
console.log(age);
console.log(wu);
wu();
````
## 模板字符串
* ES6引入新的声明字符串的方式 `` '' ""
1. 声明
````js
let str = `我是一个字符串`;
console.log(str,typeof str);
````
2. 内容中可以直接出现换行符
````js
let str = `1
            2
            3
            4
            5`;
console.log(str);
````
3. 可以直接进行变量拼接
    - 固定格式 ${}
````js
let love = "JavaScript";
let out = `${love}是我最喜欢的语言×`;
console.log(out);
````
## 对象的简化写法
* ES6允许在大括号里面,直接写入变量和函数,作为对象的属性和方法,这样的书写更加简洁
````js
let name = "尚硅谷";
let change = function(){
    console.log("我们可以改变你!");
}
const SCHOOL = {
    name,
    change,
    // improve:function(){
    //     console.log("我们可以提高你的技能");
    // }
    improve(){
        console.log("我们可以提高你的技能");
    }
}
console.log(SCHOOL);
````
## 箭头函数及声明特点
* arguments像数组(并不是真的数组,是一个Arguments对象)一样,有length属性,可以代表传给函数的参数的个数
* ES6允许使用[箭头](=>)定义函数
````js
let fn = (a,b) => {
    return a+b;
}
let result = fn(1,2);
console.log(result);
````
1. this是静态的,始终指向函数声明时所在作用于下this的值
````js
function getName1(){
    console.log(this.name);
}
let getName2 = () => {
    console.log(this.name);
}
// 设置window对象的name属性
window.name = "尚硅谷";
const school = {
    name:"AtGuigu",
}
// 直接调用
getName1();// 尚硅谷
getName2();// 尚硅谷
// call方法调用
// 可以改变函数内部this的值
getName1.call(school);// AtGuigu
getName2.call(school);// 尚硅谷
````
2. 不能作为构造函数实例化对象
````js
let Person = (name,age) => {
    this.name = name;
    this.age = age;
}
let me = new Person("Qi",19);
console.log(me);// 报错
````
3. 箭头函数里不能使用arguments变量
````js
let fn = () => {
    console.log(arguments);
}
fn(1,2,3);
````
4. 箭头函数的简写
    - 当形参有且只有一个时,可以省略小括号()
    ````js
    let add = n => {
        return n+n;
    }
    console.log(add(9));
    ````
    - 当代码体只有一条语句时,可以省略花括号{},此时return必须省略,而且语句的执行结果就是函数的返回值
    ````js
    let pow = n => n*n;
    console.log(pow(9));
    ````
### 箭头函数的实践及场景应用
* 箭头函数适合与this无关的回调,如定时器,数组的方法调用
* 不适合与this有关的回调,如DOM的事件回调,对象的方法
1. 需求1 点击div 2s 后颜色变成[粉色]
````js
let ad = document.getElementById("ad");
ad.addEventListener("click",function(){
    // 把外层函数作用域下的this进行保存
    // let _this = this;
    // 添加定时器
    setTimeout(() => {
        // 修改背景颜色
        // console.log(this);
        // 箭头函数的this指向的是声明时所在作用域下的this.指向ad
        this.style.background = 'pink';
    },2000);
});
````
2. 需求2 从数组中返回偶数的元素
    - 它用于把Array的某些元素过滤掉，然后返回剩下的元素
    - 和map()类似，Array的filter()也接收一个函数。和map()不同的是，filter()把传入的函数依次作用于每个元素，然后根据返回值是true还是false决定保留还是丢弃该元素。
    * JS常规方法
    ````js
    const arr = [1,6,9,10,25,8];
    const result = arr.filter(function(item){
        if(item % 2 === 0){
            return true;
        }
        else{
            return false;
        }
    });
    console.log(result);
    ````
    * 箭头函数方法
    ````js
    const arr = [1,6,9,10,25,8];
    const result = arr.filter(item => {
        if(item % 2 === 0){
            return true;
        }
        else{
            return false;
        }
    });
    console.log(result);
    ````
    * 箭头函数简略方法
    ````js
    const arr = [1,6,9,10,25,8];
    const result = arr.filter(item => item % 2 === 0);
    console.log(result);
    ````
## 函数参数的默认值设置
* ES6允许给函数参数赋值初始值
1. 形参的初始值,具有默认值的参数,一般位置要靠后(潜规则)
````js
function add(a,b,c=10){
    return a+b+c;
}
let result = add(1,2);
console.log(result);
````
2. 可以与解构赋值结合使用
````js
console.log(result);
function connect({host="127.0.0.1",username,password,port}){
    console.log(host);
    console.log(username);
    console.log(password);
    console.log(port);
}
connect({
    // host:"localhost",
    username:"ruuy",
    password:"root",
    port:3306
});
````
## rest参数
* ES6引入rest参数,用于获取函数的实参,用来代替arguments
1. ES5获取实参的方式
    - 返回的是一个对象
````js
function date(){
    console.log(arguments);
}
date("学习","去学习","快去学习","滚去学习啊!");
````
2. rest参数
* 以数组方式返回,具有数组的性质
* 如 filter some every map
* rest参数必须要放到参数的最后,放到前面会报错
````js
function date(...args){
    console.log(args);
}
date("学习","去学习","快去学习","滚去学习啊!");
````

````js
function fn(a,b,...args){
    console.log(a);
    console.log(b);
    console.log(args);
}
fn(1,2,3,4,5,6);
// a 1
// b 2
// args [3,4,5,6]
````
## 拓展运算符的介绍
* [...] 拓展运算符能将数组转换为逗号分隔的【参数序列】
````js
// 声明一个数组
const Xuan = ["Qi","Bai","Mei"];
// => "Qi","Bai","Mei"
// 声明一个函数
function fn(){
    console.log(arguments);
}
fn(...Xuan);
````
### 拓展运算符的应用
1. 数组的合并
    - ES5
    ````js
    const Xuan = ["Qi","Bai"];
    const Wu = ["Mei","Qing","Chi"];
    const Xuanwu = Xuan.concat(Wu);
    console.log(Xuanwu);
    ````
    - 拓展运算符
    ````js
    const Xuan = ["Qi","Bai"];
    const Wu = ["Mei","Qing","Chi"];
    const Xuanwu = [...Xuan,...Wu];
    console.log(Xuanwu);
    ````
2. 数组的克隆
````js
const Wu = ['W','D','Q'];
const Xuan = [...Wu];
console.log(Xuan);
````
3. 将伪数组转换成真正的数组
````js
const divs = document.querySelectorAll('div');
const divArr = [...divs];
console.log(divs);
console.log(divArr);
````
## Symbol的介绍与创建
* 前言:ES5中对象的属性名都是字符串,容易造成重名,污染环境
* Symbol:
    - 概念:ES6中的添加了一种原始数据类型Symbol(已有的原始数据类型:String,Number,Boolean,Null,Undefined,Object,Function)
    - 特点
        1. Symbol属性对应的值是唯一的,解决命名冲突问题
        2. Symbol值不能与其他数据进行计算.包括同字符串拼串
        3. for in(枚举对象属性),for of遍历时不会遍历Symbol属性
    - 使用:
        1. 调用Symbol函数得到symbol值
            ````js
            let symbol = Symbol();
            let object = {};
            obj[symbol] = 'hello';
            ````
        2. 传参标识
            ````js
            let symbol = Symbol('one');
            let symbol2 = Symbol('two');
            console.log(symbol);// Symbol('one')
            console.log(symbol2);// Symbol('two')
            ````
        3. 内置Symbol值
            - 除了定义自己使用的Symbol值外,ES6还提供了11个内置的Symbol值,指向语言内部使用的方法
            - Symbol.iterator属性,指向该对象的默认遍历器方法
* typedef检测数据类型,返回值有7种,String,Number,Booiean,Undefined,Symbol,Odject,Function
````js
let obj = {
    name:"Qi",
    age:19
}
obj[Symbol.iterator] = function(){

}
console.log(obj);
````
![](2021-05-19-17-04-47.png)
* 不能与其他数据进行运算
* 运算或者对比都会被报错
* 自己和自己运算也不行
````js
let s = Symbol();
console.log(s,typeof s);
let s2 = Symbol("尚硅谷");
let s3 = Symbol("尚硅谷");
let s4 = Symbol.for("尚硅谷");
let s5 = Symbol.for("尚硅谷");
console.log(s2 === s3);//false
console.log(s4 === s5);//true
let result = s + 100;// ERROR
let result = s + s;// ERROR
````
### 对象添加Symbol类型的属性
* 向对象中添加方法 up down
    1. 方法一
    ````js
    let game = {
        name:"Qi",
        age:19,
        up:function(){
            console.log("我可以改变形状");
        },
        down:function(){
            console.log("我可以快速下降");
        }
    }
    // 声明一个对象
    let methods = {
        up: Symbol(),
        down: Symbol()
    };
    game[methods.up] = function(){
        console.log("我可以改变形状");
    }
    game[methods.down] = function(){
        console.log("我可以快速下降");
    }
    console.log(game);
    ````
    2. 方法二
    ````js
    let You = {
        name:"滚去学习",
        [Symbol('say')]:function(){
            console.log("你给我闭嘴");
        },
        [Symbol('Qi')]:function(){
            console.log("球球了讲原理啊!!!");
        }
    }
    ````
### iterator接口基本实现
* 概念:iterator是一种接口机制,为各种不同的数据类型提供统一的访问机制
* 作用:
    1. 为各种数据结构,提供一个统一的,简便的访问接口
    2. 使得数据结构的成员能够按某种次序排列
    3. ES6创造了一种新的遍历命令for...of循环,Iterator接口主要提供for...of消费
* 工作原理
    - 创建一个指针对象(遍历器对象),指向数据结构的起始位置
    - 第一次调用next方法,指针自动指向数据结构的第一个成员
    - 接下来不断调用next方法,指针会一直往后移动,直到指向最后一个成员
    - 每次调用next方法返回的是一个包含value和done的对象,{value:当前成员的值,done:布尔值}
        * value表示当前成员的值,done对应的布尔值表示当前的数据的结构是否遍历结束
        * 当遍历结束的时候返回的value值是undefined,done值为false
    原生具备iterator接口的数据(可用for...of遍历)
    1. Array
    2. arguments
    3. set容器
    4. map容器
    5. String
### Symbol的内置属性
![](2021-05-19-21-49-12.png)
![](2021-05-20-10-10-38.png)
![](2021-05-20-10-11-25.png)
### 迭代器
![](2021-05-20-10-26-07.png)
![](2021-05-20-10-32-23.png)
````js
// 声明一个数组
const xiyou = ['唐曾','孙悟空','猪八戒','沙和尚'];
// 使用for...of遍历
// 输出键值
for(let v of xiyou){
    console.log(v);
}
// 输出键名
for(let v in xiyou){
    console.log(v);
}
console.log(xiyou);
let iterator = xiyou[Symbol.iterator]();
console.log(iterator);
// 调用对象的next方法
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
// 最后一次值为undefined,done为true
// 说明遍历已经完成
console.log(iterator.next());
````
### 迭代器的应用
````js
// 自定义遍历数据
const banji = {
    name:"Study",
    stus:[
        'Xuexi',
        'xuexixuexi',
        'kuaixuexi',
        'knight'
    ],
    [Symbol.iterator](){
        // 索引变量
        let index = 0;
        // 声明一个变量作为保存
        // 咋觉得像是人工实现了呢
        // 也可以直接使用箭头函数
        let _this = this;
        return {
            // 直接自己写了一个函数?!
            // 合理
            next:function(){
                if(index < _this.stus.length){
                    const result = {value:_this.stus[index],done:false};
                    // 下标自增
                    index++;
                    return result;
                }else{
                    return {value:undefined,done:true};
                }
            }
        };
    }
}
for(let v of banji){
    console.log(v);
}
````
## 生成器函数声明与调用
* 生成器其实是一个特殊的函数
* 异步编程 纯回调函数 node fs ajax mongodb
* yield 算作是函数代码的分隔符
* 必须调next方法才能执行
````js
// 生成器其实是一个特殊的函数
// 异步编程 纯回调函数 node fs ajax mongodb
// yield 算作是函数代码的分隔符
function *gen(){
    // console.log("hello generator");
    // console.log(111);
    yield '滚去学习';
    // console.log(222);
    yield '快去学习';
    // console.log(333);
    yield '学习学习学习';
    // console.log(444);
}
let iterator = gen();
// console.log(iterator);
// 必须调next方法才能执行
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
for(let v of gen()){
    console.log(v);
}
````
## 生成器函数的参数传递
* next方法可以传入实参
* 将作为上一个语句的整体返回结果
````js
function * gen(arg){
    console.log(arg);
    let one = yield 111;
    console.log(one);
    yield 222;
    yield 333;
}
// 执行获取迭代器对象
let iterator = gen('AAA');
// next方法可以传入实参
console.log(iterator.next());
// 将作为上一个语句的整体返回结果
console.log(iterator.next('BBB'));
console.log(iterator.next());
console.log(iterator.next());
````
## 生成器函数实例
### 实例一
* 异步编程 文件操作 网络操作(ajax request) 数据库操作
* 1s后控制台输出111,2s后控制台输出222,3s后控制台输出333
* 生成器函数在异步编程里的表现
1. 回调地狱(无限缩进)
````js
// 回调地狱
setTimeout(()=>{
    console.log(111);
    setTimeout(()=>{
        console.log(222);
        setTimeout(()=>{
            console.log(333);
        },3000)
    },2000)
},1000)
````
2. 异步函数
````js
function one(){
    setTimeout(()=>{
        console.log(111);
        iterator.next();
    },1000);
}
function two(){
    setTimeout(()=>{
        console.log(222);
        iterator.next();
    },2000);
}
function three(){
    setTimeout(()=>{
        console.log(333);
        iterator.next();
    },3000);
}
function * gen(){
    yield one();
    yield two();
    yield three();
}
let iterator = gen();
iterator.next();
````
### 实例二
* 模拟获取 用户数据 订单数据 商品数据
````js
// 模拟获取 用户数据 订单数据 商品数据
function getUsers(){
    setTimeout(()=>{
        let data = '用户数据';
        // 调用next方法并将数据传入
        iterator.next(data);
    },1000);
}
function getOrders(){
    setTimeout(()=>{
        let data = '订单数据';
        iterator.next(data);
    },1000);
}
function getGoods(){
    setTimeout(()=>{
        let data = '商品数据';
        iterator.next(data);
    },1000);
}
function * gen(){
    let user = yield getUsers();
    console.log(user);
    let orders = yield getOrders();
    console.log(orders);
    let goods = yield getGoods();
    console.log(goods);
}
// 调用生成器函数
let iterator = gen();
iterator.next();
````
## Promise
![](2021-05-20-13-17-06.png)
````js
// 实例化Promise对象
const p = new Promise(function(resolve,reject){
setTimeout(function(){
    // 成功
    let data = '数据库中的用户数据';
    // resolve
    resolve(data);
    // 失败
    let err = '数据读取失败';
    reject(err);
},1000)
});
// 调用promise对象的then方法
p.then(function(value){
console.log(value);
},function(reason){
console.log(reason);
});
````
### Promise封装读取文件
````js
// 1. 引入fs模块
const fs = require('fs');
// 2. 调用方法读取文件
fs.readFile('./淋雪.md',(err,data)=>{
// 如果失败,则抛出错误
if(err) throw err;
// 如果没有出错,则输出内容
console.log(data,toString);
})
// 3. 使用Promise封装
const p = new Promise(function(resolve,reject){
fs.readFile('./淋雪.md',(err,data)=>{
    // 判断如果失败
    if(err) reject(err);
    // 如果成功
    resolve(data);
})
})
p.then(function(value){
console.log(value.toString());
},function(reason){
console.log("读取失败!");
})
````
### Promise封装AJAX请求
````js
// 接口地址：https://api.apiopen.top/getJoke
const p = new Promise((resolve,reject) => {
    // 1. 创建对象
    const xhr = new XMLHttpRequest();
    // 2.初始化
    xhr.open("GET","https://api.apiopen.top/getJoke");
    // 3. 发送
    xhr.send();
    // 4. 绑定事件，处理响应结果
    xhr.onreadystatechange = function(){
        // 判断
        if(xhr.readyState === 4){
            // 判断响应状态码 200-299
            if(xhr.status >= 200 && xhr.status < 300){
                resolve(xhr.response);
            }else{
                reject(xhr.status);
            }
        }
    }
});
p.then(function(value){
    console.log(value);
},function(reason){
    console.log(reason);
});
````
### Promise.prototype.then方法
````js
const p = new Promise((resolve,reject)=>{
    setTimeout(()=>{
        resolve('用户数据');
    },1000)
})
````
* 调用then方法
* then方法的返回结果是Promise对象
* 对象状态有回调函数的执行结果决定
````js
const result = p.then(value=>{
    console.log(value);
    // 1. 非promise类型的属性
    return 123;

    // 2.是promise对象
    return new Promise((resolve,reject)=>{
        // resolve('OK');
        reject("ERROR");
    });

    // 3. 抛出错误
    // throw new ERROR("出错了!");
    throw '出错了!';
},reason=>{
    console.warn(reason);
});
console.log(result);
````

````js
// 链式调用
p.then(value=>{
    
},reason=>{

});
console.log(result);
````
### Promise实践练习-多个文件内容读取
````js
// 引入fs模块
// 1. 回调地狱法
const fs = require("fs");
const { resolve } = require("path/posix");
fs.readFile('./淋雪.md',(err,data1)=>{
    fs.readFile('./人生七十古来稀.md',(err,data2)=>{
        fs.readFile('./九万字.md',(err,data3)=>{
            let result = data1 + '\r\n' + data2 + '\r\n' + data3;
            console.log(result);
        });
    });
});
// 2. Promise实现
const p = new Promise((resolve,reject)=>{
    fs.readFile("./人生七十古来稀.md",(err,data)=>{
        resolve(data);
    });
});
p.then(value=>{
    // console.log(value.toString());
    return new Promise((resolve,reject)=>{
        fs.readFile("./淋雪.md",(err,data)=>{
            resolve([value,data]);
        });
    });
}).then(value=>{
    return new Promise((resolve,reject)=>{
        fs.readFile("./九万字.md",(err,data)=>{
            // 压入
            value.push(data);
            resolve(value);
        });
    });
}).then(value=>{
    console.log(value.join('\r\n'));
});
````
### Promise对象catch方法
````js
const p = new Promise((resolve,reject)=>{
    setTimeout(()=>{
        // 设置 p 对象的状态为失败,并设置失败的值
        reject("Painu helvettiin.");
    },1000);
});
p.then(function(value){},function(reason){
    console.error(reason);
});
p.catch(function(reason){
    // console.warn(reason);
    console.log(reason);
});
````
## 集合介绍与API
![](2021-05-20-21-07-35.png)
* 可以使用for...of...遍历
1. size
    - 输出集合元素的个数
    - s2.size();
2. add
    - 向集合中添加新元素
    - s2.add('xxx');
3. delete
    - 删除集合中已有元素
    - s2.delete('xxx');
4. clear
    - 清空集合
    - s2.clear();
````js
// 声明一个set
let s = new Set();
let s2 = new Set(['吃饭','睡觉','学习','画画','学习']);
console.log(s,typeof s);
s2.add('去死');
s2.delete('吃饭');
// 会自动去重
/*
    * 元素的个数 size
    * 添加新的元素 add
    * 删除元素 delete
    * 检测元素 has
    * 清空集合
    */ 
// 存在返回true
console.log(s2.has('画画'));
// s2.clear();
console.log(s2.size);
console.log(s2);
for(let v of s2){
    console.log(v);
}
````
### 集合实践
1. 数组去重
````js
let arr = [1,2,3,4,5,4,3,2,1];
let result = [...new Set(arr)];
// ... 用来展开arr
console.log(result);
````
2. 求交集
````js
let arr = [1,2,3,4,5,4,3,2,1];
let arr2 = [4,5,6,5,6];
// 1. 详写
// let result = [...new Set(arr)].filter(item => {
//     let s2 = new Set(arr2);
//     if(s2.has(item)){
//         return true;
//     }else{
//         return false;
//     }
// });
// 2. 简略方法
let result = [...new Set(arr)].filter(item => new Set(arr2).has(item));
console.log(result);
````
3. 求并集
````js
let arr = [1,2,3,4,5,4,3,2,1];
let arr2 = [4,5,6,5,6];
let union = [...new Set([...arr,...arr2])];
console.log(union);
````
4. 求差集
````js
let arr = [1,2,3,4,5,4,3,2,1];
let arr2 = [4,5,6,5,6];
// A-B,A里面有,B里面没有
let diff = [...new Set(arr)].filter(item => !(new Set(arr2).has(item)));
console.log(diff);
````
## Map的介绍与API
* 键值对的集合
* 各种类型的值(包括对象)都可以当作键
![](2021-05-21-15-49-16.png)
1. 声明Map
````js
let m = new Map();
````
2. 添加元素
````js
m.set('name','尚硅谷');
m.set('change',function(){
    console.log('我们可以改变你');
});
let key = {
    school:'AtGuigu',
}
m.set(key,['北京','上海','深圳']);
console.log(m);
````
3. 获取元素个数
````js
console.log(m.size);
````
4. 删除元素
````js
m.delete('name');
````
5. 获取元素
````js
console.log(m.get('change'));
// 找到就输出
// 没找到就输出undefined
````
6. 清空元素
````js
m.clear();
````
7. 遍历元素
````js
for(let v of m){
    console.log(v);
}
````
## class介绍与初体验
![](2021-05-21-16-08-47.png)
![](2021-05-21-16-11-53.png)
![](2021-05-21-16-12-21.png)
1. ES5 用构造函数实例化一个对象
````js
function Phone(brand,price){
    this.brand = brand;
    this.price = price;
}
// 添加方法
// 通过原型对象来添加
Phone.prototype.call = function(){
    console.log("我可以打电话");
}
let Huawei = new Phone('华为',5999);
Huawei.call();
console.log(Huawei);
````
2. class实现
````js
class Phone{
    // 构造方法,名字不能修改
    constructor(brand,price){
        this.brand = brand;
        this.price = price;
    }
    // 方法必须使用该语法
    // 不能使用ES5的对象完整性是
    call(){
        console.log('我可以打电话');
    }
}
let onePhone = new Phone("1+",1999);
console.log(onePhone);
onePhone.call();
````
### class静态成员
1. ES5
    * 实例对象和函数对象的属性是不通的
````js
// 实例对象和函数对象的属性是不通的
function Phone(){

}
// 下面两个属于函数对象并不属于实例对象 静态成员
// 属于类,不属于实例对象
Phone.name = '手机';
Phone.change = function(){
    console.log("我可以改变世界");
}
Phone.prototype.size = '5.5inch';
let nolia = new Phone();
console.log(nolia.name);// undefined
// nolia.change();// ERROR
console.log(nolia.size);// 5.5inch
````
2. class 静态属性
````js
class Phone{
    // 静态属性
    static name = "手机";
    static change(){
        console.log("我可以改变世界");
    }
}
let vivo = new Phone();
console.log(vivo.name);// undefined
console.log(Phone.name);// 手机
````
## ES5构造函数继承
* 使用ES5构造函数实现==继承==
````js
// 手机
function Phone(brand,price){
    this.brand = brand;
    this.price = price;
}
Phone.prototype.call = function(){
    console.log("我可以打电话");
}
// 声明智能手机
function SmartPhone(brand,price,color,size){
    Phone.call(this,brand,price);
    this.color = color;
    this.size = size;
}
// 设置子集构造函数类型
SmartPhone.prototype = new Phone;
SmartPhone.prototype.constructor = SmartPhone;
// 声明子类的方法
SmartPhone.prototype.photo = function(){
    console.log("我可以拍照");
}
SmartPhone.prototype.playGame = function(){
    console.log("我可以玩游戏");
}
const oppo = new SmartPhone('OPPO',3999,'蓝色','5.5inch');
console.log(oppo);
````
## class的类继承
````js
class Phone{
    constructor(brand,price){
        this.brand = brand;
        this.price = price;
    }
    // 父类的成员属性
    call(){
        console.log("我可以打电话");
    }
}
class SmartPhone extends Phone{
    // 构造方法
    constructor(brand,price,color,size){
        super(brand,price);//Phone.call(this,brand,price);
        this.color = color;
        this.size = size;
    }
    photo(){
        console.log("我可以拍照");
    }
    playGame(){
        console.log("我可以玩游戏");
    }
}
const oppo = new SmartPhone('OPPO',3999,'蓝色','5.5inch');
console.log(oppo);
````
## 子类对父类方法的重写
* 子类不能直接调用父类的同名方法
````js
class Phone{
    constructor(brand,price){
        this.brand = brand;
        this.price = price;
    }
    // 父类的成员属性
    call(){
        console.log("我可以打电话");
    }
}
class SmartPhone extends Phone{
    // 构造方法
    constructor(brand,price,color,size){
        super(brand,price);//Phone.call(this,brand,price);
        this.color = color;
        this.size = size;
    }
    photo(){
        console.log("我可以拍照");
    }
    playGame(){
        console.log("我可以玩游戏");
    }
    call(){
        console.log("我可以进行视频通话");
    }
}
const oppo = new SmartPhone('OPPO',3999,'蓝色','5.5inch');
console.log(oppo);
oppo.call();//我可以进行视频通话
````
## class中的get和set设置
````js
// get 和 set
class Phone{
    get price(){
        console.log("价格属性被读取了");
        return 'iloveyou';
    }
    // 必须有一个参数
    set price(newVal){
        console.log("价格属性被修改了");
    }
}
let s = new Phone();
// console.log(s.price);//iloveyou
s.price = 'Free';// 触发方法
// ???????
````
## ES6的数值拓展
1. Number.EPSILON 是 JavaScript 表示的最小精度
    - EPSILON属性的值接近2.22044060492503130808472633361816E-16
````js
function equal(a,b){
    if(Math.abs(a-b) < Number.EPSILON){
        return true;
    }else{
        return false;
    }
}
console.log(0.1+0.2 === 0.3);
console.log(equal(0.1+0.2,0.3));
````
![](2021-06-06-21-51-13.png)
2. 二进制和八进制
````js
let b = 0b1010;// 二进制
let o = 0o777;// 八进制
let d = 100;
let x = 0xff;// 十六进制
console.log(b);
console.log(o);
console.log(x);
````
3. Number.isFinite 检测一个数值是否为有限数
````js
console.log(Number.isFinite(100));//true
console.log(Number.isFinite(100/0));//false
````
4. Number.isNaN 检测一个数值是否为NaN
````js
console.log(Number.isNaN(123));//false
````
5. Number.parseInt Number.parseFloat字符串转整数
````js
console.log(Number.parseInt('516266BNAJ44557'));//516266
console.log(Number.parseFloat('5.21849AD4488'));//5.21849
````
6. Number.isInteger 判断一个数是否为整数
````js
console.log(Number.isInteger(5));//true
console.log(Number.isInteger(2.5));//false
````
7. Math.trunc 将数字的小数部分抹掉
````js
console.log(Math.trunc(3.5));//3
````
8. sign 判断一个数到底为正数 负数 还是零
````js
console.log(Math.sign(100));//1
console.log(Math.sign(0));//0
console.log(Math.sign(-200));//-1
````
## ES6的对象方法拓展
1. Object.is 判断两个值是否完全相等
````js
// 与 === 作用大致相同
console.log(Object.is(120,120));//true
console.log(Object.is(120,121));//false
console.log(Object.is(NaN,NaN));//true,
console.log(NaN === NaN);//false NaN和任何数作比较都不相等
````
2. Object.assign 对象的合并
    - 如果两个对象有相同的元素,后面的会覆盖前面的
````js
const config1 = {
    host:'localhost',
    port:3306,
    name:'root',
    pass:'root',
    test:'test'
};
const config2 = {
    host:'https://baidu.com',
    port:33060,
    name:'AtGuigu.com',
    pass:'love'
}
// 后面的会覆盖前面的
console.log(Object.assign(config1,config2));
</script>
````
3. Object.setPrototypeOf 设置原型对象 Object.getPrototypeOf 
````js
const school = {
    name:"尚硅谷",
}
const cities = {
    xiaoqu:["北京","上海","深圳"],
}
// 添加到原型对象中
Object.setPrototypeOf(school,cities);
console.log(Object.getPrototypeOf(school));
console.log(school);
````
## 模块化介绍,优势以及产品
![](2021-05-22-12-18-10.png)
![](2021-05-22-12-19-38.png)
## 浏览器使用ES6模块化引入模块
* 引入的语法
>    - **type = =="module"==**
>    - **==import * as ___ from "___.js"==**
````js
<scrip type="module">
    // 引入m1.js模块内容        
    // 这个语法...
    import * as m1 from "./m1.js";
    console.log(m1);
</scrip>
````
````js
export let school = "尚硅谷";
export function teach(){
    console.log("我们可以交给你开发技能");
}
````
## ES6模块暴露数据语法汇总
1. 分别暴露
````js
// 分别暴露
export let school = "尚硅谷";
export function teach(){
    console.log("我们可以交给你开发技能");
}
````
2. 统一暴露
````js
// 统一暴露
let school = '尚硅谷';
function findJob(){
    console.log("我们可以帮助你找工作");
}
export {school,findJob};
````
3. 默认暴露
    - 想要使用里面的属性和方法的话,就必须多加一层default
````js
// 默认暴露
export default{
    school:'AtGuigu',
    change:function(){
        console.log("我们可以改变你");
    }
}
````
4. 引入
````js
<script type="module">
    // 引入m1.js模块内容
    import * as m1 from "./m1.js";
    console.log(m1);
    import * as m2 from "./m2.js";
    console.log(m2);
    // 引入m3.js
    // 想要使用里面的属性和方法的话,就必须多加一层default
    import * as m3 from "./m3.js";
    console.log(m3);
    m2.findJob();
    m3.default.change();
</script>
````
## ES6 引入模块数据语法汇总
1. 通用的导入方式
````js
<script type="module">
    // 引入m1.js模块内容
    import * as m1 from "./m1.js";
    console.log(m1);
    import * as m2 from "./m2.js";
    console.log(m2);
    // 引入m3.js
    // 想要使用里面的属性和方法的话,就必须多加一层default
    import * as m3 from "./m3.js";
    console.log(m3);
    m2.findJob();
    // ???
    m3.default.change();
</script>
````
2. 解构赋值形式
````js
import {school,teach} from "./m1.js";
// 为了防止重名,使用别名
import {school as guigu,findJob} from "./m2.js";
// 默认暴露
import {default as m3} from "./m3.js";
console.log(school);
console.log(teach);
console.log(guigu);
console.log(m3);
````
3. 简便形式
    - 只能针对默认暴露
````js
import m3 from "./m3.js";
console.log(m3);
console.log(m3.school);
m3.change();
````
## 浏览器使用ES6模块化2
* 很少这样做
* 兼容性不支持
````js
<script src="./app.js" type="module"></script>
````
* app.js
````js
// 模块引入
import * as m1 from "./m1.js";
import * as m2 from "./m2.js";
import * as m3 from "./m3.js";
console.log(m1);
console.log(m2);
console.log(m3);
````
## babel对ES6模块化代码转换
!!!
## ES6模块化引入NPM包
!!!
## ES7新特性
![](2021-05-22-14-35-19.png)
1. includes 判断一个元素是否在数组内
    - 和indexOf相似,不同的是indexOf返回的是下标,不存在则返回-1
    - includes返回的是true或者false
````js
// includes
const mingzhu = ['西游记','红楼梦','水浒传','三国演义'];
// 判断
console.log(mingzhu.includes('西游记'));
console.log(mingzhu.includes('金瓶梅'));
console.log(mingzhu.indexOf('西游记'));
````
2. ** 
    - 和 Math.pow() 相似
````js
console.log(2 ** 10);//1024
console.log(Math.pow(2,10));//1024
````
## ES8-async函数
![](2021-05-22-14-46-10.png)
1. async函数的返回值为promise对象
2. promise对象的结果由async函数执行的返回值决定
* 如果返回的结果**不是一个Promise类型的对象**,则函数的返回结果就是一个**成功的Promise对象**
* 如果是**抛出错误**,则返回的结果是一个**失败的Promise**
* 如果返回结果是一个Promise对象
    - 如果是一个成功的Promise,则结果也是一个成功的Promise
    - 反之则返回一个失败的Promise
````js
// async函数
async function fn(){
    // 返回一个字符串
    // return '尚硅谷';
    // 返回的结果不是一个Promise类型的对象,则函数的返回结果就是一个成功的Promise对象
    // return;//undefined
    // 抛出错误 返回的结果是一个失败的Promise
    // throw new Error("出错了!");
    // 返回结果如果是一个Promise对象
    // 如果是一个成功的Promise,则结果也是一个成功的Promise
    // 反之则返回一个失败的Promise
    return new Promise((resolve,reject)=>{
        // resolve('成功的数据');
        reject("失败的数据");
    });
}
const result = fn();
// console.log(result);
// 调用then方法
result.then(value=>{
    console.log(value);
},reason=>{
    console.warn(reason);
});
````
## ES8-await表达式
![](2021-05-22-15-03-26.png)
1. await必须放在async函数中
2. await右侧的表达式一般为promise对象
3. await返回的是promise成功的值
4. await的promise失败了,就会抛出异常,需要通过try...catch捕获处理
````js
// 创建Promise对象
const p = new Promise((resolve,reject)=>{
    // resolve("成功的值!");
    reject("失败数据");
})
// await必须放在async函数中
async function main(){
    try{
        let result = await p;
        // 
        console.log(result);
    }catch(e){
        console.log(e);
    }
}
// 调用函数
main();
````
## ES8-async与await结合读取文件内容
* 结合Node.js
````js
//  1. 引入fs模块
const { rejects } = require("assert/strict");
const fs = require("fs");
const { resolve } = require("path/posix");
function RenSheng(){
    return new Promise((resolve,reject)=>{
        fs.readFile("./人生七十古来稀.md",(err,data)=>{
            // 如果失败
            if(err) reject(err);
            // 如果成功
            resolve(data);
        })
    })
}
function Linxue(){
    return new Promise((resolve,reject)=>{
        fs.readFile("./淋雪.md",(err,data)=>{
            // 如果失败
            if(err) reject(err);
            // 如果成功
            resolve(data);
        })
    })
}
function Jiuwanzi(){
    return new Promise((resolve,reject)=>{
        fs.readFile("./九万字.md.md",(err,data)=>{
            // 如果失败
            if(err) reject(err);
            // 如果成功
            resolve(data);
        })
    })
}
// 声明一个async函数
async function main(){
    let Ren = await RenSheng();
    let Xue = await Linxue();
    let Jiu = await Jiuwanzi();
    console.log(Ren.toString());
    console.log(Xue.toString());
    console.log(Jiu.toString());
}
main();
````
## async与await结合发送Ajax请求
````js
// 发送AJAX请求,返回结果是一个Promise对象
function sendAjax(url){

    return new Promise((resolve,reject)=>{
        // 1. 创建对象
        const x = new XMLHttpRequest();
        // 2. 初始化
        x.open('GET',url);
        // 3. 发送
        x.send();
        // 4. 事件绑定
        x.onreadystatechange = function(){
            if(x.readyState == 4){
                if(x.status >= 200 && x.status < 300){
                    // 成功了
                    resolve(x.response);
                }else{
                    reject(x.status);
                }
            }
        }
    });
        
}
````
1. promise then方法 测试
````js
// promise then方法 测试
sendAjax("https://api.apiopen.top/getJoke").then(value=>{
    console.log(value);
},result=>{});
````
2. async与await测试
````js
// async与await测试
async function main(){
    let result = await sendAjax("https://api.apiopen.top/getJoke");
    console.log(result);
}
main();
````
## ES8对象方法拓展
````js
const school = {
    name:"尚硅谷",
    cities:["北京","上海","深圳"],
    xueke:["前端","Java","大数据","运维"],
};
// 获取对象所有的键
console.log(Object.keys(school));
// 获取对象所有的值
console.log(Object.values(school));
// entries
console.log(Object.entries(school));
// 可以用来创建Map
const m = new Map(Object.entries(school));
console.log(m);
console.log(m.get("cities"));

// console.log(Object.getOwnPropertyDescriptor(school));
// 对象属性的描述对象
console.log(Object.getOwnPropertyDescriptor(school));
const obj = Object.create(null,{
    name:{
        // 设置值
        value:'尚硅谷',
        // 属性特性
        writable:true,// 可修改的
        configurable:true,// 可删除的
        enumerable:true//可枚举
    }
});
````
## ES9拓展运算符与test参数
* rest参数与spread拓展运算符在ES6中已经引入，不过ES6中知识针对于**数组**
* 在ES9中为**对象**提供了像数组一样的rest参数和拓展运算符
````js
function connect({host,port,...user}){
    console.log(host);
    console.log(port);
    console.log(user);
}
connect({
    host: '127.0.0.1',
    port:3306,
    username:'root',
    password:'root'
});
````

````js
const skillOne = {
    q:'天音波',
    w:'金钟罩'
}
// ...skillOne => q:'天音波',w:'金钟罩'
````
* 对象的合并
````js
const skillOne = {
    q:'天音波'
}
const skillTwo = {
    w:'金钟罩'
}
const skillThree = {
    e:'天雷破'
}
const skillFour = {
    r: '猛龙摆尾'
}
// 对象的合并
const Maneseng = {...skillOne,...skillTwo,...skillThree,...skillFour};
console.log(Maneseng);
````
## ES9正则拓展-命名捕获分组
1. 未分组时 groups:undefined
![](2021-05-22-17-14-14.png)
````js
// 声明一个字符串
let str = '<a href="https//www.atguigu.com">尚硅谷</a>';
// 提取 url 与 标签文本
const reg = /<a href="(.*)">(.*)<\/a>/;
// 执行
const result = reg.exec(str);
console.log(result);
console.log(result[1]);
console.log(result[2]);
````
2. 分组后
![](2021-05-22-17-20-30.png)
````js
let str = '<a href="https//www.atguigu.com">尚硅谷</a>';
const reg = /<a href="(?<url>.*)">(?<text>.*)<\/a>/;
const result = reg.exec(str);
console.log(result);
console.log(result.groups.url);
console.log(result.groups.text);
````
## ES9正则拓展-反向断言
1. 正向断言
````js
// 声明字符串
let str = 'JS3127907我快疯了555啊啊啊';
// 正向断言
// \d 匹配数字0-9
const reg = /\d+(?=啊)/;
const result = reg.exec(str);
````
2. 反向断言
````js
// 声明字符串
let str = 'JS3127907我快疯了555啊啊啊';
// 反向断言
const reg = /(?<=了)\d+/;
result = reg.exec(str);
console.log(result);
````
## ES9正则拓展-dotAll模式
!!!
## ES10 对象拓展方法Object.fromEntries
* 将二维数组或者Map转化成对象
1. 二维数组
    - 只取前两个值,后面的忽略
````js
const result = Object.fromEntries([
    ['name','尚硅谷'],
    ['xueke','Java,大数据,前端','再添一个'],
    // 如果像这样再添一个的话,会被自动忽略,只取前两个
]);
console.log(result);
````
![](2021-05-24-21-41-01.png)
2. Map
````js
const m = new Map();
m.set('name','AtGuigu');
const result = Object.fromEntries(m);
console.log(result);
````
![](2021-05-24-21-41-32.png)
3. Object.entries ES8 可以将一个对象转化成数组
````js
// Object.entries ES8 可以将一个对象转化成数组
const arr = Object.entries({
    name:'尚硅谷',
    xueke:'Java',
});
console.log(arr);
````
![](2021-05-24-21-43-45.png)
## ES10 字符串方法拓展 trimStart trimEnd
* ES5 trim 清除字符串两端的空白字符
* trimStart清除字符串左边空白
* trimEnd清除字符串右边空白
````js
// ES5 trim 清除字符串两端的空白字符
// trimStart清除字符串左边空白
// trimEnd清除字符串右边空白
let str = '   iloveyou   ';
console.log(str);
console.log(str.trim());
console.log(str.trimStart());
console.log(str.trimEnd());
````
![](2021-05-24-21-55-44.png)
## ES10 数组方法拓展 flat与flatMap
* flat 降低数组维度,将多维数组转化为低维数组
* 参数为深度,是一个数字,参数n表示深度为n层
* 如三维数组转化成一维数组,深度为2
````js
// flat 降低数组维度
// 将多维数组转化为低维数组
// const arr = [1,2,3,4,[5,6]];
const arr = [1,2,3,4,[5,6,[7,8,9]]];
// 参数为深度 是一个数字
// n 表示 n层
// 如三维数组转化成一维数组，深度为2
console.log(arr.flat(2));
````
* flatMap将执行map时产生的多维数组降维
````js
// flatMap
const arr = [1,2,3,4];
// const result = arr.map(item => [item*10]);//二维数组
// [[10],[20],[30],[40]]
const result = arr.flatMap(item => [item*10]);//转化成一维数组
// [10,20,30,40]
````
## ES10 Symbol.prototype.description
* 可以得到传入的字符串
````js
// 创建 Symbol
let s = Symbol('尚硅谷');
console.log(s.description);// 可以得到传入的字符串
````
## ES11 私有属性
* 私有属性前面要加'#',并且只能在类的内部使用
````js
class Person{
    // 公有属性
    name;
    // 私有属性
    #age;
    #weight;
    // 构造方法
    constructor(name,age,weight){
        this.name = name;
        // 私有属性要写全
        this.#age = age;
        this.#weight = weight;
    }
    intro(){
        console.log(this.name);
        console.log(this.#age);
        console.log(this.#weight);
    }
}
// 实例化
const girl = new Person('晓红',18,'45kg');
console.log(girl);
// console.log(girl.name);
// console.log(girl.#age);// ERROR 不能在类的外部使用
girl.intro();
````
## ES11 Promise.allSettled方法
1. allSettled方法
    * 接收一个Promise数组,返回结果也是一个Promise对象
    * 但是返回结果永远是成功的状态
    * 而且成功的值是里面每一个Promise的状态和结果
    * 成功的值是一个数组,数组的每一个元素是一个对象
2. All方法
    * 只有所有Promise对象都是成功时返回结果才是成功的
    * 只要有一个是失败的,最终结果就是失败的
    * 失败的值就是数组里面出错的Promise对象失败的值
````js
// 接收一个Promise数组,返回结果也是一个Promise对象
// 但是返回结果永远是成功的状态
// 而且成功的值是里面每一个Promise的状态和结果

// 声明两个Promise对象
const p1 = new Promise((reslove,reject)=>{
    setTimeout(()=>{
        reslove('商品数据 - 1');
    },1000);
});
const p2 = new Promise((reslove,reject)=>{
    setTimeout(()=>{
        // reslove('商品数据 - 2');
        reject('出错了!');
    },1000)
});
// 调用allSettled方法
// const result = Promise.allSettled([p1,p2]);
// 成功的值是一个数组,数组的每一个元素是一个对象
// console.log(result);

// all方法
// 只有所有Promise对象都是成功时返回结果才是成功的
// 只要有一个是失败的,最终结果就是失败的
// 失败的值就是数组里面出错的Promise对象失败的值
const res = Promise.all([p1,p2]);
console.log(res);
````
## ES11 String.prototype.matchAll方法
* 用于数据的批量提取
````js
let str = `
<ul>
    <li>
        <a>肖生客的救赎</a>
        <p>上映时间:1994-09-10</p>
    </li>
    <li>
        <a>阿甘正传</a>
        <p>上映时间:1994-07-06</p>
    </li>
</ul>`;
// 声明正则
const reg = /<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/sg;
// 调用方法
// 用于数据的批量提取
const result = str.matchAll(reg);
// console.log(result);
// for(let v of result){
//     console.log(v);
// }
const arr  = [...result];
console.log(arr);
````
## ES11 可选链操作符
````js
//  ?.
// 当应对对象类型的参数时使用
function main(config){
    // 如果没有的话报错
    // const dbHost = config && config.db && config.db.host;
    // 如果没有的话undefined
    const dbHost = config?.db?.host; 
    console.log(dbHost);
}
main({
    db:{
        host:'192.168.1.100',
        username:'root'
    },
    cache:{
        host:'192.168.1.200',
        username:'admin'
    }
});
````
## 动态 import
````js
// import * as m1 from './hello.js';
// 获取元素
const btn = document.getElementById("btn");
btn.onclick = function(){
    import('./hello.js').then(module => {
        // 用的时候再导入
        // console.log(module);
        module.hello();
    })
}
````
## ES11 BigInt类型
* 大整型 用来进行更大的数值运算
* 表达方式 在整数后面加上n
* 不能与正常整数进行运算
````js
// 大整型 用来进行更大的数值运算
// 表达方式 在整数后面加上n
// let n = 521n;
// console.log(n,typeof n);

// 函数
let n = 123;
// 可以将整数转化成大整数
console.log(BigInt(n));

// 主要用于更大数值的运算
// 最大安全整数
let max = Number.MAX_SAFE_INTEGER;
console.log(max);// 9007199254740991
console.log(max+1);// 9007199254740992
// 不能表示更大的运算结果
console.log(max+2);// 9007199254740992

// 不能与正常整数进行运算
console.log(BigInt(max));
console.log(BigInt(max) + BigInt(1));
console.log(BigInt(max) + BigInt(2));
````
## ES11 绝对全局对象globalThis
* 无论执行环境是什么,始终指向全局对象
````js
// 无论执行环境是什么,始终指向全局对象
console.log(globalThis);
````

