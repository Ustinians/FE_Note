# MongoDB
## 安装MongoDB
MongoDB下载网站: https://www.mongodb.com/try/download/community
## 使用MongDB
* 安装Mongoose
```npm
npm install mongoose
```
* 启动mongoDB服务
```npm
net start mpngdb
```
## 数据库连接
使用mongoose提供的connect方法即可连接数据库
```js
mongoose.connect("mongodb://localhost/playground")
    .then(() => console.log("数据库连接成功"))
    .catch(err => console.log("数据库连接失败",err))
```
## 创建数据库
在MongoDB中不需要显式创建数据库,如果正在使用的数据库不存在,MongoDB会自动创建
## 创建集合
创建集合分为两步,一是对集合设定规则,二是创建集合,创建mpngoose.Schema构造函数的实例即可创建集合
```js
// 创建集合
// 1. 设定集合规则
const courseSchema = new mongoose.Schema({
    name: String,
    author: String,
    isPublished: Boolean
});
// 创建集合并应用规则
/**
 * 两个参数:
 * 集合名称
 * 集合规则
 */
const Course = mongoose.model("Course",courseSchema); //courses
```

## MongoDB增删查改的操作

### 创建文档

创建文档实际上就是向集合中插入数据

#### 方法一

分两步: 

1. 创建集合实例
2. 调用实例对象下的save方法将数据保存到数据库中

```js
// 创建集合实例
const course = new Course({
    name: "MongoDB",
    author: "Aure",
    tags: ["node.js","express","mongodb"],
    isPublished: true
});
// 将数据保存到数据库中
course.save();
```

#### 方法二

```js
Course.create({
    name: "JavaScript基础",
    author: "Susu",
    isPublished: true
},(err, doc) => {
    // 错误对象
    console.log(err);
    // 当前插入的文档
    console.log(doc);
})

// 或者

Course.create({
    name: "CSS由浅入深",
    author: "Xinxi",
    isPublished: true
}).then(doc => {
    console.log(doc);
}).catch(err => {
    console.log(err);
})
```

#### mongoDB数据库导入数据

* 找到mongoDB的安装目录

```
mongoimport -d 数据库名称 -c 集合名称 -file 要导入的数据文件
```

找到mongoDB数据库的安装目录,将安装目录下的bin目录放置在环境变量中

### 查询文档

#### find()

```js
// 根据条件查询文档(条件为空则查找所有文档)
// 返回文档集合
Course.find().then(result => console.log(result));

// 根据ID值查找
// 查询_id为'62299e25ac470e945de85b09'的数据
Course.find({_id: '62299e25ac470e945de85b09'}).then(result => console.log(result));
```

#### findOne()

```js
// findOne()返回的是一个对象而不是一个数组,默认返回当前集合中的第一条文档
Course.findOne().then(result => console.log(result)); 

// findOne()按照条件查询
Course.findOne({name: "CSS由浅入深"}).then(result => console.log(result)); 
```

#### 按照条件查询

* 查询年龄大于20且小于40的

  ```js
  // $gt 大于 $lt 小于
  // 匹配大于小于
  // 匹配年龄大于20小于40的
  User.find({age: {$gt: 20, $lt: 40}}).then(result => console.log(result))
  ```

* 查询爱好(数组)中包括'敲代码'的

  ```js
  // $in 包括
  User.find({hobby: {$in: ['敲代码']}}).then(result => console.log(result))
  ```

* 将数据按照年龄升序排序

  ```js
  // 升序
  User.find().sort('age').then(result => console.log(result))
  // 降序
  User.find().sort('-age').then(result => console.log(result))
  ```

* skip(m) 跳过m条数据 limit(n) 只显示n条数据

  ```js
  User.find().skip(2).limit(3).then(result => console.log(result)) // 跳过了第1,2条数据,展示第3-5条数据
  ```

![image-20220310170251662](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220310170251662.png)

### 删除文档

* 删除单个数据并返回

  ```js
  //! 删除文档
  //! 删除单个并返回
  User.findOneAndDelete({}).then(result => console.log(result))
  ```

* 删除指定`_id`的数据

  ```js
  //! 删除指定_id的数据
  // 如果查询条件匹配了多个文档,那么会删除第一个匹配的文档
  User.findByIdAndDelete({_id: '6229b81bd3e1d8e1ce519128'}).then(result => console.log(result))
  ```

* 删除多条数据

  ```js
  //! 删除多个文档
  //! 注意: 当deleteMany()中不传参数或者传入空对象,将删除所有的数据
  User.deleteMany({}).then(result => console.log(result))
  ```

### 更新文档

传入两个参数,第一个是要修改的数据的条件,第二个是要修改的值

如果第一个参数传入空对象`{}`,则所有数据都会被修改

```js
User.updateOne({name: "Jack"},{name: "杰克"}).then(result => console.log(result))
```

### Mongoose验证

在创建集合规则时,可以设置当前字段的验证规则,验证失败就则输入插入失败

* require: true 必传字段
* minLength: 字符串最小程度
* maxLength: 字符串最大长度
* min: 数值最小
* max: 数值最大
* enum: ['html','css','js'] 只能熊目录中选择做为值
* trim: true 去除字符串两边的空格
* validate: 自定义验证器
* default: 默认值

### 集合关联

通常不同集合之间的数据事有关系的,例如文章信息和用户信息存储在不同的集合中,但是文章事某个用户发表的,要查询文章的所有信息包括发表作者,就需要用到集合关联

* 使用id对集合进行关联
* 使用populate方法进行关联集合查询

![image-20220310220742887](D:\AFrontEnd\frontEndStudy\MongDB\mongoDB\image-20220310220742887.png)

```js
const Author = mongoose.model("Author", new mongoose.Schema({
    name: {
        type: String,
        require: true
    },
    age: {
        type: Number
    },
    sex: {
        type: String,
        enum: ["male","female"]
    }
}))

const Post = mongoose.model("POST", new mongoose.Schema({
    title:{
        type: String,
        require: true
    },
    desc: {
        type: String
    },
    author: {
        type: mongoose.Schema.Types.ObjectId, 
        ref: "Author",
        required: true
    }
}))
```

创建Post数据时

```js
POST.create({
    title: "故国的春天",
    desc: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Eaque sit voluptates quod officia aliquid eveniet omnis recusandae repudiandae explicabo deleniti tempore sapiente, vitae molestiae natus a dolorum. Nesciunt, similique quia.",
    author: '622abf164b07a4e909cf7345'
}).then(doc => {
    console.log(doc);
}).catch(err => {
    console.log(err);
```

**<font color="red">联合查询</font>**

```js
Post.find()
    .populate("author")
    .then((result) => {
        console.log(result);
    })
```

## 模板引擎

模板引擎是第三方模块

让开发者已更友好的方式拼接字符串,使项目代码更加清晰,更加易于维护

![image-20220311164752450](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220311164752450.png)

### art-template模板引擎

1. 在命令行工具中使用`npm install art-template`命令进行下载
2. 使用`const template = require('art-template')`引入模板引擎
3. 告诉模板引擎要拼接的数据和模板在哪里 `const html = template('模板引擎',数据);`

模板引擎代码

```js
// 导入模板引擎模块
const template = require("art-template");

// 将特定模块与特定数据进行拼接
const html = template("./views/index.art",{
    data: {
        name: "Jack",
        age: 20
    }
})
```

模板代码

```html
<div>
    <span>{{data.name}}</span>
    <span>{{data.age}}</span>
</div>
```

* `art-template`同时支持i昂中模板语法: <font color="red">标准语法</font>和<font color="red">原始语法</font>
* 便准语法可以让模板更容易读写,原始语法具有强大的逻辑处理能力

标准语法: `{{ 数据 }}`

原始语法: `<%= 数据 %>`

### 条件判断

在模板中可以根据条件来决定显示哪块HTML代码

![image-20220311215934595](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220311215934595.png)

```html
{{if age > 18}}
    年龄大于18
{{else if age < 15}}
    年龄小于15
{{else}}
    年龄不符合要求
{{/if}}

<% if(age > 18) { %> 
    年龄大于18 
<% } else if(age < 15) { %> 
    年龄小于15
<% } else { %> 
    年龄不符合要求 
<% } %>

```

### 循环

* 标准语法: `{{each 数据}} {{/each}}`
* 原始语法: `<% for() {% > <% } %>`

![image-20220311221120732](D:\AFrontEnd\frontEndStudy\MongDB\mongoDB\image-20220311221120732.png)

```html
// 数据循环
// 标准语法
<ul>
    {{each users}}
        <li>
            {{$value.name}}
            {{$value.age}}
            {{$value.sex}}
        </li>
    {{/each}}
</ul>
// 原始语法
<ul>
    <% for(var i = 0;i < users.length;i++) { %>
        <li>
            <%=users[i].name %>
            <%=users[i].age %>
            <%=users[i].sex %>
        </li>
    <% } %>
</ul>
```

### 子模版

使用子模版可以将网页公共区块(头部,底部)抽离到单独的文件中

* 标准语法: `{{include '模板'}}`
* 原始语法: `<%include('模板') %>`

![image-20220312145024853](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220312145024853.png)

```html
{{ include './common/header.art' }}
<% include("./common/header.art") %>
<div> {{ msg }} </div>
<% include("./common/footer.art") %>
{{ include './common/footer.art' }}
```

### 模板继承

使用模板继承可以将网站HTML骨架抽离到单独的文件中,其他页面模板可以集成骨架文件

![image-20220312145415523](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220312145415523.png)

![image-20220312145651850](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220312145651850.png)

```html
// layout.art
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    {{block 'link'}} {{/block}}
</head>
<body>
    {{block 'content'}} {{/block}}
</body>
</html>
```

```html
// index.art
{{extend './common/layout.art'}}

{{block 'content'}}
<p>{{msg}}</p>
{{/block}}

{{block 'link'}}
<link href="/main.css" />
{{/block}}
```

### 模板配置

1. 向模板中导入变量`template.defaults.imports.变量名 = 变量值`
2. 设置模板根目录`template.defaults.root = 模板目录`
3. 设置模板默认后缀`template.defaults.extname = '.art'`

## 中间件

中间件就是一堆方法,可以接受客户端发送过来的请求,可以对请求做出响应,也可以将请求继续交给下一个中间件处理

![image-20220312165045631](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220312165045631.png)

中间件主要由两部分构成,<font color="red">中间件方法</font>以及<font color="red">请求处理函数</font>

中间件方法由`Express`提供,负责拦截请求,请求处理函数由开发人员提供,负责处理请求

```js
app.get("请求路径","处理函数"); // 接受并处理get请求
app.post("请求路径","处理函数"); // 接受并处理post请求
```

可以针对同一个请求设置多个中间件,对一个请求进行多次处理

默认情况下,请求从上到下依次匹配中间件,一但匹配成功,终止匹配

```js
app.get("/request",(req,res,next) => {
    req.name = "Jack";
})
app.get("/requext",(req,res) => {
    res.send(req.name);
})
```

`app.use`匹配所有的请求方式,可以直接传入请求处理函数,代表接受所有的请求

```js
app.use((req,res,next) => {
    console.log(req.url);
    next();
})
```

### 中间件应用

1. 路由保护,客户端在访问需要登录的页面的时候,也已先使用中间件判断用户的登录状态,用户如果未登录,则拦截登录请求,直接响应,禁止用户进入需要登陆的页面

   ```js
   app.use("/admin",(req,res,next) => {
       // 用户没有登录
       let isLogin = false;
       if(isLogin){
           next();
       }
       else{
           res.send("您还没有登录,不能访问/admin页面")
       }
   })
   ```

2. 网页维护公告,早所有路由的最上面定义接受所有请求的中间件,直接为客户端作出相应,网页正在维护中...

   ```js
   app.use((req,res,next) => {
       res.send("网站正在维护中...");
   })
   ```

3. 自定义404页面

   ```js
   //! 当前访问的页面是不存在的
   app.use((req,res,next) => {
       res.status(404).send("您访问的页面不存在...")
   })
   ```

### 错误处理中间件

在程序执行的过程中,不可避免的会出现一些无法预料的错误,比如文件读取失败,数据库连接失败等...

错误处理中间件是一个集中处理错误的地方

```js
app.use((err,req,res,next) => {
    req.status(500).send("服务器发生未知错误");
})
```

当程序出现错误时,调用next()方法,并且将错误信息通过参数的方式传递给next()方法,即可触发错误处理中间件

```js
app.get("/",(req,res,next) => {
    fs.readFile("/code/day/index.html",(err,data) => {
        if(err){
            next(err);
        }
    })
})
```

### 捕获错误

在node.js中,异步API的错误信息都是通过回调函数获取的,支持`Promise`对象的异步API发生错误可以通过catch方法捕获

`try catch`可以捕获异步函数以及其他同步代码在执行过程中发生的错误,但是不能捕获其他类型的API发生的错误

```js
app.get("/",async (req,res,next) => {
    try {
        await User.find({name: "Jack"});
    }catch(err){
        next(err)
    }
})
```























