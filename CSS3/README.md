# CSS3 模板
* 选择器
* 盒模型
* 背景和边框
* 文字特效
* 2D/3D 转换
* 动画
* 多列布局
* 用户界面
## CSS3 边框
### border-radius 圆角
````html
border-radius: 25px;
````
下列属性可使用border-radius元素
* 填充背景
* 边框
* 填充背景图片
### CSS3 盒阴影
````html
box-shadow: 10px 10px 5px #888888;
````
### CSS3 边界图片
````html
div{
    border: 15px solid transparent;
    width: 250px;
    padding: 10px 20px;
}
<!-- 平铺 -->
#round{
    -webkit-border-image: url(./border-img.png) 30 30 round;
    /* Safari 5 and older */
    -o-border-image: url(./border-img.png) 30 30 round;
    /* Opera */
    border-image: url(./border-img.png) 30 30 round;
}
<!-- 拉伸 -->
#stretch{
    -webkit-border-image: url(./border-img.png) 30 30 stretch;
    /* Safari 5 and older */
    -o-border-image: url(./border-img.png) 30 30 stretch;
    /* Opera */
    border-image: url(./border-img.png) 30 30 stretch;
}
````
## CSS3 背景
### background-image 背景图像
不同的背景图像和图像用逗号隔开，所有的图片中显示在最顶端的为第一张
````html
background-image: url(./img/bk-img-flower.gif),url(./img/bk-img-paper.gif);
<!-- 默认第一张图片在前 -->
background-position: right bottom,left top;
background-repeat: no-repeat,repeat;
padding: 15px;
````
### background-repeat 背景是否重复平铺
* repeat 默认属性，使背景图像在水平和垂直方向上重复
* repeat-x 背景图像在横向上平铺
* repeat-y 背景图像在竖向上平铺
* no-repeat 背景图像不平铺
### background-size 背景图片的大小
指定背景图片的大小
````html
background: url(./img/bk-img-flower.gif);
background-size: 80px 60px;
background-repeat: no-repeat;
padding-top: 40px;
````
伸展背景图像完全填充内容区域
````html
background: url(./img/bk-img-flower.gif);
background-size: 100% 100%;
background-repeat: no-repeat;
````
### backgrounr-origin
指定背景图像的位置区域
content-box,padding-box和border-box区域内可以放置背景图像
* content-box 内容框
* padding-box 
* border-box 边界框
### backgroung-clip 背景图像裁剪
从指定位置开始绘制
* border-box 没有背景裁剪,没有定义
* padding-box 从padding处开始裁剪
* content-box 从内容处开始裁剪
````html
background-clip: padding-box;
````
## CSS3 线性渐变
* 线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向
* 径向渐变（Radial Gradients）- 由它们的中心定义
### background-image 实现渐变
* 从上到下的线性渐变(默认)
````css
background-image: linear-gradient(#e66465,#9198e5);
/* 从上往下渐变 */
````
* 从左到右的线性渐变
````css
background-image: linear-gradient(to right,red,yellow);
/* 从左往右渐变 */
````
* 从左上角到右下角的线性渐变
````css
background-image: linear-gradient(to bottom right,red,yellow);
````
* 带有指定的角度的线性渐变
@import "带有角度的渐变.jpg"
0deg 将创建一个从下到上的渐变，90deg 将创建一个从左到右的渐变
换算公式 90 - x = y 其中 x 为标准角度，y为非标准角度.
- 从上到下
````css
background-image: linear-gradient(0deg,red,yellow);
````
- 从右到左
````css
background-image: linear-gradient(90deg,red,yellow);
````
- 从下到上
````css
background-image: linear-gradient(180deg,red,yellow);
````
- 从左到右
````css
background-image: linear-gradient(-90deg,red,yellow);
````
* 指定渐变位置
````css
background-image: linear-gradient(red 10%, green 85%, blue 90%); 
/* 标准的语法（必须放在最后） */
````
* 添加文本的渐变背景
````css
div{
    text-align:center;
    margin:auto;
    color:#888888;
    font-size:40px;
    font-weight:bold
}
````
* 重复的线性渐变
````css
/*重复*/
background-image: repeating-linear-gradient(red,yellow 10%,green 20%);
````
### 使用透明度(transparent)
为了添加透明度，我们使用 rgba() 函数来定义颜色节点。rgba() 函数中的最后一个参数可以是从 0 到 1 的值，它定义了颜色的透明度：0 表示完全透明，1 表示完全不透明。
````css
background-image: linear-gradient(to right,rgba(255,0,0,0),rgba(255,0,0,1));
````
## CSS3 径向渐变
* 颜色节点均匀分布的径向渐变
````css
background-image: radial-gradient(red,green,blue);
````
* 颜色节点不均匀分布的径向渐变
````css
background-image: radial-gradient(red 5%,green 15%,blue 60%);
````
#### CSS3 径向渐变的形状设置
* 椭圆形 Ellipse(默认)
````css
background-image: radial-gradient(red,yellow,green);
````
* 圆形 Circle
````css
background-image: radial-gradient(circle,red,yellow,green);
````
### 不同尺寸大小关键字的使用
* closest-side
指定径向渐变的半径长度为从圆心到离圆心最近的边的长度(circle)或分别将水平方向渐变中心到最近的边的长度和垂直方向渐变中心到最近的边的长度指定为椭圆的水平半轴和垂直半轴（ellipse)
````css
background-image: radial-gradient(closest-side at 60% 55%,red,yellow,black);
````
* farthest-side
指定径向渐变的半径长度为从圆心到离圆心最远的边的长度(circle)或分别将水方向渐变中心到最远的边的长度和垂直方向渐变中心到最远的边的长度指定为椭的水平半轴和垂直半轴(ellipse)
````css
background-image: radial-gradient(farthest-side at 60% 55%,red,yellow,black);
````
* closest-corner
指定渐变的半径长度为从圆形到离圆心最近的角的长度(circle)或渐变的边缘形状与容器距离渐变中心点最近的一个角相交，且椭圆的宽高比与closest-side的相同
````css
background-image: radial-gradient(closest-corner at 60% 55%,red,yellow,black);
````
* farthest-corner
指定径向渐变的半径长度为从圆心到离圆心最远的角的长度(circle)或渐变的边缘形状与容器距离渐变中心点最远的一个角相交，且椭圆的宽高比与farthest-side的相同
````css
background-image: radial-gradient(farthest-corner at 60% 55%,red,yellow,black);
````
### 重复的径向渐变
repeating-radial-gradient() 函数用于重复径向渐变
````css
background-image: repeating-radial-gradient(red,yellow 10%,green 15%);
````
# CSS3 文本效果
* text-shadow
````css
/* 水平阴影，垂直阴影，模糊的距离，以及阴影的颜色 */
text-shadow: 5px 5px 5px #ff0000;
````
* box-shadow
依次顺序:
1. h-shadow   水平阴影 
2. v-shadow   垂直阴影 
3. blur       模糊
4. spread     阴影尺寸  
5. color       颜色   
6. insect     外阴影转到内阴影 
````css
box-shadow: 10px 10px 5px #888888;
/* 水平阴影，垂直阴影，模糊的距离(这个是重点!!!)，以及阴影的颜色 */
````
(也可以在 ::before 和 ::after 两个伪元素中添加阴影效果)
````css
#boxshadow{
    position: relative;
    box-shadow:1px 2px 4px rgba(0,0,0,0.5);
    padding: 10px;
    background: white;
}
#boxshadow img{
    width: 100%;
    border: 1px solid #8a4419;
    border-style: inset;
}
#boxshadow::after{
    content:'';
    position: absolute;
    z-index: -1;/* hide shadow behind image */
    box-shadow: 0px 15px 15px rgba(0,0,0,0.3);
    width: 70%;
    left: 15%;/* one half of the remaining 30% */
    height: 100%;
    bottom: 0;
}
````
阴影的一个使用特例是卡片效果
1. 文字卡片
````css
        div.card{
            width: 250px;
            box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19);
            text-align: center;
        }
        div.header{
            background-color: #4caf50;
            color: white;
            padding: 10px;
            font-size: 40px;
        }
        div.container{
            padding: 10px;
        }
````
2. 图片卡片
````css
        div.polaroid{
            /* 为撒第一次运行就不起作用 */
            width: 250px;
            box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19);
            text-align: center;
        }
````
* text-overflow
CSS3文本溢出属性指定应向用户如何显示溢出内容
````css
        div.test{
            white-space: nowrap;
            width: 12em;
            overflow: hidden;
            border: 1px solid #000000;
        }
        style="text-overflow: ellipsis;"
        /* 超出部分变成省略号 */
        style="text-overflow: clip;"
        /* 超出部分不显示 */
        style="text-overflow: '>>';"
        /* 只在 Firefox 浏览器下有效,自定义字符串 */
````
* word-wrap
CSS3的换行
如果某个单词太长，不适合在一个区域内，它扩展到外面
CSS3中，自动换行属性允许您强制文本换行 - 即使这意味着分裂它中间的一个字
````css
word-wrap: break-word;
````
* word-break
CSS3 单词拆分换行
CSS3 单词拆分换行属性指定换行规则
word-break 属性不兼容 Opera
1. normal	使用浏览器默认的换行规则
2. keep-all 只能在半角空格或连字符处换行
3. break-all 允许在单词内换行
````css
/* 	只能在半角空格或连字符处换行 */
word-break: keep-all;
/* 允许在单词内换行 */
word-break: break-all;
````
# CSS3 新文本属性
* hanging-punctuation	规定标点字符是否位于线框之外。
1. none	不在文本整行的开头还是结尾的行框之外放置标签符号。
2. first	标点附着在首行开始边缘之外。
3. last	标点附着在首行结尾边缘之外。
4. allow-end
5. force-end

* punctuation-trim	规定是否对标点字符进行修剪。
1. none	请勿修剪打开或关闭标点符号
2. start	在每一行的开头放置开头标点符号
3. end	在每一行的末尾修剪结束标点符号
4. allow-end	如果另有不适合之前的理由，修剪每行末尾的结束标点符号。
5. adjacent	若以前相邻字符修剪开口punctuation是一个全形开口，中间或结束标点符号，或表意文字空间。修剪结束标点.

* text-align-last	设置如何对齐最后一行或紧挨着强制换行符之前的行。
1. auto	默认值。最后一行被调整，并向左对齐。	
2. left	最后一行向左对齐。
3. right	最后一行向右对齐。	
4. center	最后一行居中对齐。	
5. justify	最后一行被调整为两端对齐。	
6. start	最后一行在行开头对齐（如果 text-direction 是从左到右，则向左对齐；如果 text-direction 是从右到左，则向右对齐）。
7. end	最后一行在行末尾对齐（如果 text-direction 是从左到右，则向右对齐；如果 text-direction 是从右到左，则向左对齐）。	
8. initial	设置该属性为它的默认值。请参阅 initial。	
9. inherit	从父元素继承该属性。请参阅 inherit。

* text-emphasis	向元素的文本应用重点标记以及重点标记的前景色。
1. text-emphasis-style	向元素的文本应用重点标记。
2. text-emphasis-color	定义重点标记的前景色。

* text-justify	规定当 text-align 设置为 "justify" 时所使用的对齐方法。
1. auto	浏览器决定齐行算法。
2. none	禁用齐行。
3. inter-word	增加/减少单词间的间隔。
4. inter-ideograph	用表意文本来排齐内容。
5. inter-cluster	只对不包含内部单词间隔的内容（比如亚洲语系）进行排齐。
6. distribute	类似报纸版面，除了在东亚语系中最后一行是不齐行的。
7. kashida	通过拉伸字符来排齐内容。

* text-outline	规定文本的轮廓。
1. thickness	必需。轮廓的粗细。
2. blur	   可选。轮廓的模糊半径。
3. color	必需。轮廓的颜色。参阅 CSS 颜色值 。

* text-overflow	规定当文本溢出包含元素时发生的事情。
* text-shadow	向文本添加阴影。
* text-wrap	  规定文本的换行规则。
* word-break	规定非中日韩文本的换行规则。
* word-wrap	允许对长的不可分割的单词进行分割并换行到下一行。

# CSS3 字体
## @font-face
! Internet Explorer 9 只支持 .eot 格式的字体
* 字体
````css
        @font-face{
            font-family: myFirstFont;
            /* 名字 */
            src: url(./font/云梦深深深几许（非商用）.ttf);
            /* 字体样式 */
        }
        div{
            font-family: myFirstFont;;
        }
````
* 加粗
````css
        @font-face{
            font-family: myFirstFont;
            src: url(./font/方正鲁迅简体.TTF);
        }
        div{
            font-family: myFirstFont;
            font-weight: bold;
        }
````
## font-stretch
可选。定义如何拉伸字体。默认是 "normal"。
* normal
* condensed
* ultra-condensed
* extra-condensed
* semi-condensed
* expanded
* semi-expanded
* extra-expanded
* ultra-expanded
## font-style
可选。定义字体的样式。默认是 "normal"。
* normal
* italic(倾斜)
* oblique(倾斜)
## unicode-range
* unicode-range	
可选。定义字体支持的 UNICODE 字符范围。默认是 "U+0-10FFFF"。
# CSS3 2D转换 transform

* translate()
translate值（50px，100px）是从左边元素移动50个像素，并从顶部移动100像素 
````css
transform: translate(50px,100px);
/* 向右平移50px,向下平移100px */
````

* rotate()
rotate()方法，在一个给定度数顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。
````css
transform: rotate(30deg);
````

* scale()
div 元素的宽度是原始大小的两倍，高度是原始大小的三倍。
````css
transform: scale(2,3);
````

* skew()
包含两个参数值，分别表示X轴和Y轴倾斜的角度，如果第二个参数为空，则默认为0，参数为负表示向相反方向倾斜。
1. skewX(<angle>);表示只在X轴(水平方向)倾斜。
2. skewY(<angle>);表示只在Y轴(垂直方向)倾斜。
````css
transform: skew(30deg,20deg);
/* skew(30deg,20deg) 元素在X轴和Y轴上倾斜20度30度。 */
````

* matrix()
matrix()方法和2D变换方法合并成一个。
matrix 方法有六个参数，包含旋转，缩放，移动（平移）和倾斜功能。
````css
transform: matrix(0.886,0.5,-0.5,0.886,0,0);
````
## CSS3 transform-origin 属性
````css
        #div1{
            position: relative;
            height: 200px;
            width: 200px;
            margin: 100px;
            padding: 10px;
            border: 1px solid black;;
        }
        #div2{
            padding: 50px;
            position: absolute;
            border: 1px solid black;
            background-color: red;
            transform: rotate(45deg);
            transform-origin: 20% 40%;
        }
````
1. x-axis	定义视图被置于 X 轴的何处。
* left
* center
* right
* length
* %
2. y-axis	定义视图被置于 Y 轴的何处。
* top
* center
* bottom
* length
* %
3. z-axis	定义视图被置于 Z 轴的何处。
* length
## 2D 转换方法
* matrix(n,n,n,n,n,n)	定义 2D 转换，使用六个值的矩阵。
* translate(x,y)	定义 2D 转换，沿着 X 和 Y 轴移动元素。
* translateX(n)	定义 2D 转换，沿着 X 轴移动元素。
* translateY(n)	定义 2D 转换，沿着 Y 轴移动元素。
* scale(x,y)	定义 2D 缩放转换，改变元素的宽度和高度。
* scaleX(n)	定义 2D 缩放转换，改变元素的宽度。
* scaleY(n)	定义 2D 缩放转换，改变元素的高度。
* rotate(angle)	定义 2D 旋转，在参数中规定角度。
* skew(x-angle,y-angle)	定义 2D 倾斜转换，沿着 X 和 Y 轴。
* skewX(angle)	定义 2D 倾斜转换，沿着 X 轴。
* skewY(angle)	定义 2D 倾斜转换，沿着 Y 轴。
# CSS3 3D转换
* rotateX()
围绕其在一个给定度数X轴旋转的元素
````css
transform: rotateX(120deg);
````
* rotateY()
围绕其在一个给定度数Y轴旋转的元素
````css
transform: rotateY(130deg);
````
## transform-style 
让转换的子元素保留3D转换
* flat	表示所有子元素在2D平面呈现。
* preserve-3d	表示所有子元素在3D空间中呈现。
````css
transform: rotateY(60deg);
transform-style: preserve-3d;
````
## perspective	规定 3D 元素的透视效果
````css
perspective: 150;
-webkit-perspective:150; /* Safari and Chrome */
/* 就类似纸片在那个平面上平移 */
/* 自己调调试试看吧 */
````
## perspective-origin
````css
perspective-origin: 10% 10%;
-webkit-perspective: 150px; /* Safari and Chrome */
-webkit-perspective-origin: 10% 10%; /* Safari and Chrome */
/* emm..绕着那个轴,想怎么动都行,只要还在那条直线上 */
````
### 语法
#### perspective-origin: x-axis y-axis;
1. x-axis
* left
* center
* right
* length
* %
2. y-axis
* top
* center
* bottom
* length
* %
# CSS3 过渡
* transition
````css
        div{
            width: 100px;
            height: 100px;
            background: red;
            transition: width 2s;
            -webkit-transition: width 2s;
        }
        div:hover{
            width: 300px;
        }
````
````css
        div{
            width: 100px;
            height: 100px;
            background: red;
            -webkit-transition: width 2s,height 2s,-webkit-transform 2s;
            /* For Safari 3.1 to 6.0 */
            transition: width 2s,height 2s,-webkit-transform 2s;
        }
        div:hover{
            width: 200px;
            height: 200px;
            -webkit-transform: rotateX(180deg);/* Chrome, Safari, Opera */
            transform: rotate(180deg);
        }
````
## 过渡属性
* transition	简写属性，用于在一个属性中设置四个过渡属性。	
transition 属性设置元素当过渡效果，四个简写属性为:
1. transition-property
2. transition-duration
3. transition-timing-function
4. transition-delay
* transition-property	规定应用过渡的 CSS 属性的名称。	
````css
/* 就是把整体分开了 */
/* 就好像background和backgroung-color */
transition-property: width;
transition-duration: 2s;
-webkit-transition-property: width; /* Safari */
-webkit-transition-duration: 2s; /* Safari */
````
* transition-duration	定义过渡效果花费的时间。默认是 0。	
* transition-timing-function	规定过渡效果的时间曲线。默认是 "ease"。
这个好高级!!!
1. linear	规定以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）。
2. ease	规定慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier(0.25,0.1,0.25,1)）。
3. ease-in	规定以慢速开始的过渡效果（等于 cubic-bezier(0.42,0,1,1)）。
4. ease-out	规定以慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)）。
5. ease-in-out	规定以慢速开始和结束的过渡效果（等于 cubic-bezier(0.42,0,0.58,1)）。
6. cubic-bezier(n,n,n,n)	在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。
* transition-delay	规定过渡效果何时开始。默认是 0。
# CSS3 动画
## CSS3 @keyframes 规则
当在 @keyframes 创建动画，把它绑定到一个选择器，否则动画不会有任何效果。
指定至少这两个CSS3的动画属性绑定向一个选择器:
* 规定动画的名称
* 规定动画的时长
````css
        div{
            width: 100px;
            height: 100px;
            background: red;
            animation: myfirst 5s;
            /* 规定动画时间 */
            -webkit-animation: myfirst 5s;
        }
        /* 绑定绑定!!! */
        @keyframes myfirst{
            form{background: red;}
            to{background: yellow;}
            /* 制作动画 */
        }
        @-webkit-keyframes myfirst{
            form{background: red;}
            to{background: yellow;}
        }
````
动画是使元素从一种样式逐渐变化为另一种样式的效果,可以改变任意多的样式任意多的次数。
请用百分比来规定变化发生的时间，或用关键词 "from" 和 "to"，等同于 0% 和 100%。
0% 是动画的开始，100% 是动画的完成。
为了得到最佳的浏览器支持，应该始终定义 0% 和 100% 选择器。
当动画完成时，会变回初始的样式。
````css
        div{
            width: 100px;
            height: 100px;
            background: red;
            position: relative;
            animation: myfirst 5s;
            /* 动画名称 动画时间 */
            -webkit-animation: myfirst 5s;
        }
        @keyframes myfirst{
            /* 动画效果 */
            0% {background: red;left: 0px;top: 0px;}
            25% {background: yellow;left: 200px;top: 0px;}
            50% {background: blue;left: 200px;top: 200px;}
            75% {background: green;left: 0px;top: 200px;}
            100% {background: red;left: 0px;top: 0px;}
        }
        @-webkit-keyframes myfirst{
            0% {background: red;left: 0px;top: 0px;}
            25% {background: yellow;left: 200px;top: 0px;}
            50% {background: blue;left: 200px;top: 200px;}
            75% {background: green;left: 0px;top: 200px;}
            100% {background: red;left: 0px;top: 0px;}
        }
````
@import "./img/css动画.png";
* animation-iteration-count控制播放次数
````html
animation-iteration-count: value;
````
1. value = n 一个数字,定义应该播放多少次动画
2. value = infinite 指定动画应该播放无限次(永远)
````css
        div{
            width: 100px;
            height: 100px;
            background: red;
            position: relative;
            animation: mymove 3s;
            animation-iteration-count: 3;
            /* Safari and Chrome */
	        -webkit-animation:mymove 3s;
	        -webkit-animation-iteration-count:3;
        }
        @keyframes mymove{
            form {top:0px}
            to {top:200px}
        }
        @-webkit-keyframes mymove{
            form {top:0px}
            to {top:200px}
        }
````
* animation-direction
animation-direction: normal|reverse|alternate|alternate-reverse|initial|inherit;
1. normal	默认值。动画按正常播放。	
2. reverse	动画反向播放。	
3. alternate	动画在奇数次（1、3、5...）正向播放，在偶数次（2、4、6...）反向播放。	
4. alternate-reverse	动画在奇数次（1、3、5...）反向播放，在偶数次（2、4、6...）正向播放。	
initial	设置该属性为它的默认值。请参阅 initial。	
inherit	从父元素继承该属性。请参阅 inherit。
````css
        div{
            width: 100px;
            height: 100px;
            background: red;
            position: relative;
            animation: myfirst 5s infinite;
            /* 无限循环 */
            animation-duration: alternate;
            /* 逆向 */
            /* Safari 和 Chrome */
	        -webkit-animation:myfirst 5s infinite;
	        -webkit-animation-direction:alternate;
        }
        @keyframes myfirst{
            0% {background: red;left: 0px;top: 0px;}
            25% {background: yellow;left: 200px;top: 0px;}
            50% {background: blue;left: 200px;top: 200px;}
            75% {background: green;left: 0px;top: 200px;}
            100% {background: red;left: 0px;top: 0px;}
        }
        @-webkit-keyframes myfirst{
            0% {background: red;left: 0px;top: 0px;}
            25% {background: yellow;left: 200px;top: 0px;}
            50% {background: blue;left: 200px;top: 200px;}
            75% {background: green;left: 0px;top: 200px;}
            100% {background: red;left: 0px;top: 0px;}
        }
````
# CSS3 多列属性
### CSS3 创建多列
* column-count
column-count 属性指定了需要分割的列数
````css
.newspaper{
    -moz-column-count: 3;
    -webkit-column-count: 3;
    column-count: 3;
}
````
### CSS3 指定列间隙
* column-gap
column-gap 属性指定了列与列间的间隙
````css
        .newspaper{
            -moz-column-count: 3;
            -webkit-column-count: 3;
            column-count: 3;
            -moz-column-gap: 40px;
            -webkit-column-gap: 40px;
            column-gap: 40px;
        }
````
### CSS3 列边框
* column-rule-style
column-rule-style 属性指定了列与列间的边框样式
````css
column-rule-style: dotted;
````
* column-rule-width
column-rule-width 属性指定了两列的边框厚度
````css
column-count: 3;
column-gap: 40px;
column-rule-style: outset;
column-rule-width: 1px;
/* 但是超出column-gap规定的宽度后就会覆盖文字了 */
````
* column-rule-color
column-rule-color 属性指定了两列的边框颜色
````css
            column-count: 3;
            column-gap: 40px;
            column-rule-style: outset;
            column-rule-color: #ff0000;
````
* column-rule
column-rule 属性是 column-rule-* 所有属性的简写
````css
        .newspaper{
            column-count: 3;
            column-gap: 40px;
            column-rule: 4px outset #ff00ff;
            
        }
````
* column-span
指定某元素跨越多少列
1. 1	元素应跨越一列
2. all	该元素应该跨越所有列
````css
        .newspaper{
            column-count: 3;

        }
        h2{
            column-span: all;
        }
````
* column-width
column-width 属性指定了列的宽度
````css
.newspaper{
    column-width: 100px;
}
````
# CSS3 用户界面
## CSS3 调整尺寸(Resizing)
* resize
resize属性指定一个元素是否应该由用户去调整大小。
这个 div 元素由用户调整大小???
* none	用户无法调整元素的尺寸。
* both	用户可调整元素的高度和宽度。
* horizontal	用户可调整元素的宽度。
* vertical	用户可调整元素的高度。
````css
        div{
            border: 2px solid;
            padding: 10px 40px;
            width: 300px;
            resize: both;
            overflow: auto;
        }
````

## box-sizing
box-sizing 属性允许您以确切的方式定义适应某个区域的具体内容
````css
        div.container{
            width: 30em;
            border: 1em solid;
        }
        div.box{
            box-sizing: border-box;
            width: 50%;
            border: 1em solid red;
            float: left;
        }
````
## CSS3 外形修饰（outline-offset ）
outline-offset 属性对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓
outline-offset: length|inherit
* length	轮廓与边框边缘的距离。
* inherit	规定应从父元素继承 outline-offset 属性的值。
````css
div{
    margin: 20px;
    width: 150px;
    padding: 10px;
    height: 70px;
    border: 2px solid black;
    /* 外轮廓 */
    outline: 2px solid red;
    outline-offset: 15px;
}

* 轮廓不占用空间
* 轮廓可能是非矩形
## CSS3 appearance 属性
````css
div{
    appearance: button;
}   
````
* normal	正常呈现元素
* icon	作为一个小图片的呈现元素
* window	作为一个视口呈现元素
* button	作为一个按钮，呈现元素
* menu	作为一个用户选项设定呈现元素选择
* field	作为一个输入字段呈现元素
## CSS3 icon 属性
将图像元素设置为图标化的等价物
````css
img
{
content:icon;
icon:url(imgicon.png);
}
/* 不是很懂,试验失败 */
````
````css
<link rel="stylesheet" href="./iconfont/iconfont.css">
<i class="iconfont icon-xianxingshanzi"></i>
````
## CSS3 nav-down 属性
规定在使用方向键时向何处导航
# CSS 图片
## 圆角图片
````css
img{
    border-radius: 8px;
}
````
## 椭圆形照片
````css
img{
    border-radius: 50%;
}
````
## 缩略图
````css
        a{
            display: inline-block;
            border: 1px solid #ddd;
            border-radius: 4px;
            padding: 5px;
            transition: 0.3px;
        }
        a:hover{
            box-shadow: 0 0 2px 1px rgda(0,140,186,0.5);
        }
````
## 响应式图片
响应式图片会自动适配各种尺寸的屏幕。
实例中，你可以通过重置浏览器大小查看效果
````css
img{
    max-width: 100%;
    /* 设置最大宽度 */
    height: auto;
}
````
## 图片文本
如何定位图片文本
````css
        .container{
            position: relative;
        }
        .topleft{
            position: absolute;
            top: 8px;
            left: 16px;
            font-size: 18px;
        }
        img{
            width: 100%;
            height: auto;
            opacity: 0.3;
            /* 设置不透明度 */
            /* 越小越透明 */
        }
        <div class="container">
            <img src="./img/trolltunga.jpg" alt="" width="1000"     height="300">
            <div class="topleft">
                左上角
            </div>
        </div>
````
## 图片滤镜
CSS filter 属性用为元素添加可视效果 (例如：模糊与饱和度)
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        img{
            width: 33%;
            height: auto;
            float: left;
            max-width: 235px;
        }
        .blur{filter: blur(4px);}/* 模糊?给图像设置高斯模糊 */
        .brightness{filter: brightness(250%);}/* 提高亮度?给图片应用一种线性乘法，使其看起来更亮或更暗 */
        .contrast{filter: contrast(180%);}/* 调整图像的对比度 */
        .grayscale{filter: grayscale(100%);}/* 将图像转换为灰度图像 */
        .huerotate{filter: hue-rotate(180deg);}/* 给图像应用色相旋转 */
        .invert{filter: invert(100%);}/*  反转输入图像 */
        .opacity{filter: opacity(50%);}/* 给图像应用色相旋转 */
        .saturate{filter: saturate(7);}/* 转换图像饱和度 */
        .sepia{filter: sepia(100%);}/* 将图像转换为深褐色 */
        .shadow{filter: drop-shadow(8px 8px 10px green);}/* 给图像设置一个阴影效果,加了阴影? */
    </style>
</head>
<body>
    <img src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="blur" src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="brightness" src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="contrast" src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="grayscale" src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="huerotate" src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="invert" src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="opacity" src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="saturate" src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="sepia" src="./img/pineapple.jpg" alt="" width="300" height="300">
    <img class="shadow" src="./img/pineapple.jpg" alt="" width="300" height="300">
</body>
</html>
````
## 图片 Modal(模态)
后期结合js做
# CSS3 框大小
使用这种方式如果想要获得较小的那个框且包含内边距，就不得不考虑到边框和内边距的宽度。
## 使用 CSS3 box-sizing 属性
CSS3 box-sizing 属性在一个元素的 width 和 height 中包含 padding(内边距) 和 border(边框)。
如果在元素上设置了 box-sizing: border-box; 则 padding(内边距) 和 border(边框) 也包含在 width 和 height 中
````css
        width: 300px;
            height: 100px;
            border: 1px solid blue;
            box-sizing: border-box;
        }
        .div2{
            width: 300px;
            height: 100px;
            padding: 50px;
            border: 1px solid red;
            box-sizing: border-box;
        }
````
CSS中*{}代表的是所有HTML的doc元素标签
如:
1. <div></div>
2. <p><span></span><p>
那么*{}  代表的就是body div p span标签元素
通配符样式,一般用于公共样式的书写,会全局定义。
# CSS3 弹性盒子(Flex Box)
## display: flex; 
弹性布局
## CSS3 弹性盒子内容
弹性盒子由弹性容器(Flex container)和弹性子元素(Flex item)组成。
弹性容器通过设置 display 属性的值为 flex 或 inline-flex将其定义为弹性容器。
弹性容器内包含了一个或多个弹性子元素。
注意： 弹性容器外及弹性子元素内是正常渲染的。弹性盒子只定义了弹性子元素如何在弹性容器内布局。
弹性子元素通常在弹性盒子内一行显示。默认情况每个容器只有一行。
以下元素展示了弹性子元素在一行内显示，从左到右
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
如果我们设置 direction 属性为 rtl (right-to-left),弹性子元素的排列方式也会改变，页面布局也跟着改变
````css
        body{
            direction: rtl;
        }
        .flex-container{
            display: -webkit-flex;
            display: flex;
            /* 弹性布局 */
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
## flex-direction 属性指定了弹性子元素在父容器中的位置。
语法 : flex-direction: row | row-reverse | column | column-reverse
* row：横向从左到右排列（左对齐），默认的排列方式。
* row-reverse：反转横向排列（右对齐，从后往前排，最后一项排在最前面。
````css
            /* 弹性布局 */
            display: -webkit-flex;
            display: flex;
            -wedkit-flex-direction: row-reverse;
            flex-direction: row-reverse;
````
* column：纵向排列。
````css
display: -webkit-flex;
display: flex;
-wedkit-flex-direction: column;
flex-direction: column;
````
* column-reverse：反转纵向排列，从后往前排，最后一项排在最上面。
````css
display: -webkit-flex;
display: flex;
-wedkit-flex-direction: column;
flex-direction: column;
````
## justify-content 属性
内容对齐（justify-content）属性应用在弹性容器上，把弹性项沿着弹性容器的主轴线（main axis）对齐。
justify-content 语法如下：
justify-content: flex-start | flex-end | center | space-between | space-around
* flex-start：
弹性项目向行头紧挨着填充。这个是默认值。第一个弹性项的main-start外边距边线被放置在该行的main-start边线，而后续弹性项依次平齐摆放。

* flex-end：
弹性项目向行尾紧挨着填充。第一个弹性项的main-end外边距边线被放置在该行的* main-end边线，而后续弹性项依次平齐摆放。
* center：
弹性项目居中紧挨着填充。（如果剩余的自由空间是负的，则弹性项目将在两个方向上同时溢出）。
* space-between：
弹性项目平均分布在该行上。如果剩余空间为负或者只有一个弹性项，则该值等同于* flex-start。否则，第1个弹性项的外边距和行的main-start边线对齐，而最后1个弹性项的外边距和行的main-end边线对齐，然后剩余的弹性项分布在该行上，相邻项目的间隔相等。
* space-around：
弹性项目平均分布在该行上，两边留有一半的间隔空间。如果剩余空间为负或者只有一个弹性项，则该值等同于center。否则，弹性项目沿该行分布，且彼此间隔相等（比如是20px），同时首尾两边和弹性容器之间留有一半的间隔（1/2*20px=10px）。

效果图展示:

@import "./img/2259AD60-BD56-4865-8E35-472CEABF88B2.jpg";
### 以下都是从左往右排列
1. flex-end
````css
            .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-justify-content: flex-end;
            justify-content: flex-end;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
2. center
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-justify-content: center;
            justify-content: center;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
3. space-between
贴着边的
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-justify-content: space-between;
            justify-content: space-between;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
4. space-around
挤在中间的
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-justify-content: space-around;
            justify-content: space-around;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
## align-items 属性
align-items 设置或检索弹性盒子元素在侧轴（纵轴）方向上的对齐方式
### 语法
align-items: flex-start | flex-end | center | baseline | stretch
* stretch(默认值)
如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-align-items: stretch;
            align-items: stretch;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            margin: 10px;
        }
````
* flex-start：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-align-items: flex-start;
            align-items: flex-start;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            margin: 10px;
        }
````
* flex-end：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-align-items: flex-end;
            align-items: flex-end;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            margin: 10px;
        }
````
* center：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-align-items: center;
            align-items: center;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            margin: 10px;
        }
````
* baseline：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-align-items: baseline;
            align-items: baseline;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            margin: 10px;
        }
````
## flex-wrap 属性
flex-wrap 属性用于指定弹性盒子的子元素换行方式。
### 语法
flex-wrap: nowrap|wrap|wrap-reverse|initial|inherit;
* nowrap - 默认， 弹性容器为单行。该情况下弹性子项可能会溢出容器。
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-flex-wrap: nowrap;
            flex-wrap: nowrap;
            width: 300px;
            height: 250px;
            background-color: lightgrey;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
* wrap - 弹性容器为多行。该情况下弹性子项溢出的部分会被放置到新行，子项内部会发生断行
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -weblit-flex-wrap: wrap;
            flex-wrap: wrap;
            width: 300px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
* wrap-reverse -反转 wrap 排列。* 
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -weblit-flex-wrap: wrap-reverse;
            flex-wrap: wrap-reverse;
            width: 300px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
## align-content 属性
align-content 属性用于修改 flex-wrap 属性的行为。类似于 align-items, 但它不是设置弹性子元素的对齐，而是设置各个行的对齐。
### 语法
align-content: flex-start | flex-end | center | space-between | space-around | stretch
* stretch - 默认。各行将会伸展以占用剩余的空间。

* flex-start - 各行向弹性盒容器的起始位置堆叠。

* flex-end - 各行向弹性盒容器的结束位置堆叠。

* center -各行向弹性盒容器的中间位置堆叠。
````css
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-flex-wrap: wrap;
            flex-wrap: wrap;
            -webkit-align-content: center;
            align-content: center;
            width: 300px;
            height: 300px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
````
* space-between -各行在弹性盒容器中平均分布。

* space-around - 各行在弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半。

## 弹性子元素属性
### 排序
### 语法
order: 
#### <integer>：用整数值来定义排列顺序，数值小的排在前面。可以为负值。
order 属性设置弹性容器内弹性子元素的属性:
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .flex-container{
            display: -webkit-flex;
            display: flex;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 100px;
            height: 100px;
            margin: 10px;
        }
        .first{
            -webkit-order: -1;
            order: -1;
        }
    </style>
</head>
<body>
    <div class="flex-container">
        <div class="flex-item">flex item 1</div>
        <div class="flex-item first">flex item 2</div>
        <div class="flex-item">flex item 3</div>
    </div>
</body>
</html>
````
### 对齐
设置"margin"值为"auto"值，自动获取弹性容器中剩余的空间。所以设置垂直方向margin值为"auto"，可以使弹性子元素在弹性容器的两上轴方向都完全居中。
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .flex-container{
            display: -webkit-flex;
            display: flex;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 75px;
            height: 75px;
            margin: 10px;
        }
        .flex-item:first-child{
            margin-right: auto;
        }
    </style>
</head>
<body>
    <div class="flex-container">
        <div class="flex-item">flex item 1</div>
        <div class="flex-item">flex item 2</div>
        <div class="flex-item">flex item 3</div>
    </div>
</body>
</html>
````
### 完美的居中
以下实例将完美解决我们平时碰到的居中问题。
使用弹性盒子，居中变的很简单，只需要设置 margin: auto; 可以使得弹性子元素在两上轴方向上完全居中:
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .flex-container{
            display: -webkit-flex;
            display: flex;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 75px;
            height: 75px;
            margin: auto;
        }
    </style>
</head>
<body>
    <div class="flex-container">
        <div class="flex-item">Lorem, ipsum.</div>
    </div>
</body>
</html>
````
## align-self
align-self 属性用于设置弹性元素自身在侧轴（纵轴）方向上的对齐方式。
### 语法
align-self: auto | flex-start | flex-end | center | baseline | stretch
各个值解析:
* auto：如果'align-self'的值为'auto'，则其计算值为元素的父元素的'align-items'值，如果其没有父元素，则计算值为'stretch'。
* flex-start：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
* flex-end：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
* center：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
* baseline：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
* stretch：如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .flex-container{
            display: -webkit-flex;
            display: flex;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            width: 60px;
            min-height: 100px;
            margin: 10px;
        }
        .item1{
            align-self: flex-start;
        }
        .item2{
            align-self: flex-end;
        }
        .item3{
            align-self: center;
        }
        .item4{
            align-self: baseline;
        }
        .item5{
            align-self: stretch;
        }
    </style>
</head>
<body>
    <div class="flex-container">
        <div class="flex-item item1">flex-start</div>
        <div class="flex-item item2">flex-end</div>
        <div class="flex-item item3">center</div>
        <div class="flex-item item4">baseline</div>
        <div class="flex-item item5">stretch</div>
    </div>
</body>
</html>
````
## flex
flex 属性用于指定弹性子元素如何分配空间。
(艹艹不懂...)
### 语法
* flex: auto | initial | none | inherit |  [ flex-grow ] || [flex-shrink ] || [ flex-basis ]
* auto: 计算值为 1 1 auto
* initial: 计算值为 0 1 auto
* none：计算值为 0 0 auto
* inherit：从父元素继承
* [ flex-grow ]：定义弹性盒子元素的扩展比率。
* [ flex-shrink ]：定义弹性盒子元素的收缩比率。
* [ flex-basis ]：定义弹性盒子元素的默认基准值。
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .flex-container{
            display: -webkit-flex;
            display: flex;
            width: 400px;
            height: 250px;
            background-color: lightgray;
        }
        .flex-item{
            background-color: cornflowerblue;
            margin: 10px;
        }
        .item1{
            -webkit-flex: 2;
            flex: 2;
        }
        .item2{
            -webkit-flex: 1;
            flex: 1;
        }
        .item3{
            -webkit-flex: 1;
            flex: 1;
        }
    </style>
</head>
<body>
    <div class="flex-container">
        <div class="flex-item item1">flex item 1</div>
        <div class="flex-item item2">flex item 2</div>
        <div class="flex-item item3">flex item 3</div>
    </div>
</body>
</html>
````
# 使用弹性盒子创建响应式页面
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .flex-container{
            display: -webkit-flex;
            display: flex;
            -webkit-flex-flow: row wrap;
            flex-flow: row wrap;
            font-weight: bold;
            text-align: center;
        }
        .flex-container > * {
            padding: 10px;
            flex: 1 100%;
        }
        .main{
            text-align: left;
            background: cornflowerblue;
        }
        .header{background: coral;}
        .footer{background: lightgreen;}
        .aside1{background: moccasin;}
        .aside2{background: violet;}

        @media all and (min-width: 600px){
            .aside{flex: 1 auto;}
        }
        @media all and (min-width: 800px){
            .main{flex: 3 0px;}
            .aside1{order: 1;}
            .main{order: 2;}
            .aside2{order: 3;}
            .footer{order: 4;}
        }
    </style>
</head>
<body>
    <div class="flex-container">
        <header class="header">头部</header>
        <article class="main">
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis, mollitia deleniti voluptatem quidem tempore nam. Explicabo odit, quod placeat reiciendis animi expedita, quidem, obcaecati temporibus consequuntur quas natus sit dolores.</p>
        </article>
        <aside class="aside aside1">边栏1</aside>
        <aside class="aside aside2">边栏2</aside>
        <footer class="footer">底部</footer>
    </div>
</body>
</html> 
````
# CSS3 多媒体查询
## 多媒体查询语法
多媒体查询由多种媒体组成，可以包含一个或多个表达式，表达式根据条件是否成立返回 true 或 false。
如果指定的多媒体类型匹配设备类型则查询结果返回 true，文档会在匹配的设备上显示指定样式效果。

除非你使用了 not 或 only 操作符，否则所有的样式会适应在所有设备上显示效果。

* not: not是用来排除掉某些特定的设备的，比如 @media not print（非打印设备）。

* only: 用来定某种特别的媒体类型。对于支持Media Queries的移动设备来说，如果存在only关键字，移动设备的Web浏览器会忽略only关键字并直接根据后面的表达式应用样式文件。对于不支持Media Queries的设备但能够读取Media Type类型的Web浏览器，遇到only关键字时会忽略这个样式文件。

* all: 所有设备，这个应该经常看到。

你也可以在不同的媒体上使用不同的样式文件：

````css
<link rel="stylesheet" media="mediatype and|not|only (expressions)" href="print.css">
````
### CSS3 多媒体类型
* all	用于所有多媒体类型设备
* print	用于打印机
* screen	用于电脑屏幕，平板，智能手机等。
* speech	用于屏幕阅读器
### 多媒体查询简单实例
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body{
            background-color: pink;
        }
        @media screen and (max-width:600px){
            body{
                background-color: lightgreen;
            }
        }
    </style>
</head>
<body>
    <h1>重置浏览器窗口查看效果</h1>
    <p>如果媒体的可视窗口宽度小于 600 px,背景颜色将改变</p>
</body>
</html>
````
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .wrapper{overflow: auto;}
        #main{margin-left: 4px;}
        #leftsidebar{float: none;width: auto;}
        #menulist{margin: 0;padding: 0;}
        .menuitem{
            background: #cdf0f6;
            border: 1px solid #d4d4d4;
            border-radius: 4px;
            list-style-type: none;
            margin: 4px;
            padding: 2px;
        }

        @media screen and (min-width: 600px) {
            /* 左边那一栏变窄 */
            #leftsidebar {width: 200px;float: left;}
            /* 移动上去 */
            #main {margin-left: 216px;}
        }
    </style>
</head>
<body>
    <div class="wrapper">
        <div id="leftsidebar">
            <ul id="menulist">
                <li class="menuitem">Menu-item 1</li>
                <li class="menuitem">Menu-item 2</li>
                <li class="menuitem">Menu-item 3</li>
                <li class="menuitem">Menu-item 4</li>
                <li class="menuitem">Menu-item 5</li>
            </ul>
        </div>
        <div id="main">
            <h1>重置浏览器窗口查看效果</h1>
            <p>在屏幕可视窗口尺寸大于 480 像素时将菜单浮动到页面左侧</p>
        </div>
    </div>
    
</body>
</html>
````
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div.example{
            background-color: yellow;
            padding: 20px;
        }
        @media screen and (max-width:600px){
            div.example{
                display: none;
            }
        }
    </style>
</head>
<body>
    <h2>屏幕可视尺寸小于 600 px 时,隐藏以下元素.</h2>
    <div class="example">我是会隐藏的元素</div>
    <p>重置浏览器,查看效果</p>
</body>
</html>
````
快速插入图片:  
1. 先复制图片
2. Ctrl + Alt + V
![media](./img/media01.png)
![](2021-03-11-16-23-34.png)
![](2021-03-11-16-24-09.png)
![](2021-03-11-16-24-39.png)
![](2021-03-11-16-24-52.png)