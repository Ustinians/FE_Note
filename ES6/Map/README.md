# JavaScript的Map数据类型

## Map数据类型产生背景

ES6更新版本

1. ES6是一个非常重要的JavaScript版本
2. 在ES6版本中,对于JavaScript的语法缺陷做了补充和修改
3. 提出了很多重要的语法结构: `Class`类 , 箭头函数 , `Map` , `Set`数据类型 , 方法函数等...
4. ES6版本的更新 , 让JavaScript从弱类型的计算机语言进化成了半强类型的计算机语言

## Map类型简介

1. Map是一个<font color="red">类似于对象</font>的数据类型
2. 与常规对象和Array不同的是 , 它是"键控集合"
3. 它的行为有稍许不同,并且在特定的上下文中使用 , 它可以提供相当大的性能优势

**对象**

* 存储数据都是<font color="red">键值对</font>类型(`key : value`)

## Map的工作形式

Map更像是<font color="red">以空间为代价</font>，换取<font color="red">速度上的提升</font>。那么对于空间和速度的衡量，必然存在一个阈值。在数据量比较少时，相比与速度的提升，其牺牲的空间代价更大，此时显然是不适合使用Map；当数据量足够大时，此时空间的代价影响更小。所以，看开发者如何衡量两者之间的关系，选择最优解。

## Map基本语法

`new Map()`

## Map的使用

1. 构造函数形式 —— 在声明的同时赋值

   参数必须是<font color="red">二维数组</font>的形式

   * 键名: Map单元数据的键名
   * 键值: Map单元数据的数值

   ```js
   const map = new Map([键名1,数值1],[键名2,数值2]); // 语法格式
   const map = new Map(['name':'Jack'],['age':18]); // 案例展示
   ```

2. 构造函数声明之后再赋值

   书写方式: <font color="red">Map对象.set(键名,数值)</font>

   ```js
   const map = new Map(); // 声明构造函数
   map.set(name,'张三'); // 赋值
   ```

## 获取Map数据类型中的数据

语法形式: <font color="red">Map数据类型.get('键名')</font>

```js
const map = new Map(['name':'Jack'],['age':18]);
console.log(m.get('name')); // 获取Map数据并打印在控制台
// 打印出'Jack'
```

## 删除Map数据类型中指定的键名

语法形式: 语法形式：<font color="red">Map数据类型.delete('键名')</font>

```js
const map = new Map(['name':'Jack'],['age':18]);
map.delete('name');
console.log(map); 
// 输出 Map(1) {'age' => 18}
```

## 清除Map数据类型中,所有的键名和数据

语法形式: 语法形式：<font color="red">Map数据类型.clear()</font>

```js
const map = new Map(['name':'Jack'],['age':18]);
map.clear();
console.log(map); 
// 输出 Map(0) {}
```

## 判断是否是Map的成员

语法形式：<font color="red">Map数据类型.has('键名')</font>

```js
const map = new Map(['name':'Jack'],['age':18]);
console.log(map.has('name')); // true
console.log(map.has('sex')); // false
```

## 循环遍历

使用forEach()语法,进行循环遍历

```js
const map = new Map(['name':'Jack'],['age':18]);
map.forEach(function(item,key){
    console.log(item,key)
})
// Jack name
18 'age'
```



















