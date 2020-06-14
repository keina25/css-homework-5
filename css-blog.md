    ### 一. 简介

* * *

**层叠样式表**(Cascading Style Sheets，缩写为**CSS**）CSS 描述了在屏幕、纸质、音频等其它媒体上的元素应该如何被渲染的问题。
样式定义如何显示HTML元素。

### 二. CSS几个重要概念

* * *

###### (一)文档流Normal Flow
意思：文档中元素流动方向
作用：
从左到右：内联元素：inline元素，span元素，从左到右排满，知道这行被排满后，另起一行；
从上到下：block元素，div元素，从上到下一次排列，而且每一个元素占一行，不会出现并排现象，这里指不额外添加样式情况下。

###### (二)margin合并

###### 哪些情况会出现合并：

1. 父子margin合并：parent与first child和last child的margin合并
2. 兄弟margin合并：child之间也会合并

###### 如何阻止合并：

1. 父子合并用padding/border挡住
2. 父子合并用overflow-hidden挡住
3. 父子合并用display:flex
4. 兄弟合是符合预期
5. 兄弟合并可以用inline-block消除

###### (三)两种盒模型
分别是：
content-box内容盒-内容就是盒子边界
border-box边框盒-边框才是盒子边界
公式：
content-box width=内容宽度
border-box width=内容宽度+padding+border

### 三.CSS布局

* * *

###### (一)固定宽度布局

原理：一般宽度为960/1000/1024px

###### (二)不固定宽度布局

原理：主要靠文档流的原理来布局，手机上适应

###### (三)响应式布局

原理：电脑端宽度固定，手机不固定，也是一个混合式布局

###### (四)Float布局

用法：
在子元素加上float:left或width;
在父元素上加 .clearfix
```
.clearfix:after{
content:'';
display:block;
clear:both;
}
```
###### (五)Flex布局
flex container样式属性：

 让一个元素变成flex容器
```
.container{
display:flex;or inline-flex;
}
```
 改变折行
```
.container{
flex-wrap:nowrap; wrap; wrap-reserve;
}
```
 主轴流动方式
```
.container{
justify-content:flex-start; flex-end;
}
```
 次轴对齐
```
.container{
align-items:stretch; flex-start;
}
```
 多行内容
```
.container{
align-content:flex-start; flex-end;
}
```
flex item样式属性：

1. item上面加order:改变显示顺位
2. item上面加flex-grow：控制自己如何长胖
3. flex-shrink：控制自己如何变瘦
4. flex-basis：控制基准宽度
5. flex-grow:1;/flex-shrink:0/flex-basis:100px; 缩写flex:1 0 100px;(导航一般为0)
6. align-self定制align-items，对齐方式与其他不一样

###### (六)Grid布局
原理：二维布局用grid布局（横竖同时布局），一维布局用flex（横着或竖着布局）
grid container样式属性：
让一个元素变成grid容器
```
.container{
display:grid; inline-grid;
}
```
行和列
```
.container{
grid-template-columns:40px 50px auto 50px 40px;
grid-template-rows:25% 100px auto;
}
```
可以给每条线取名字
```
.container{
grid-template-columns:[first]40px [line2]50px [line3]auto [col4-start]50px [five]40px[end];
grid-template-rows:[row1-start]25% [row1-end]100px [third-line]auto[last-line];
}
```
每条线取名后，就可以让item设置范围
分区grid-template-areas
```
.item-a{
grid-area:header;
}
.item-b{
grid-area:main;
}
.item-c{
grid-area:footer;
}
```
空隙grap
```
.container{
grid-template-columns:100px 50px 100px;
grid-template-rows:80px auto 80px;
grid-column-grap:10px;
grid-rwo-grap:10px;
}
```
### 四.CSS定位

* * *

**CSS定位**：一个div的分层，布局是在屏幕平面上，定位是垂直于屏幕上的。
###### Position属性：

1. static:默认值，但不等于不写；
2. relative:相对定位,用于平移或给absolute做父元素；
3. absolute：绝对定位，用于对话框关闭按钮或鼠标提示；
4. fixed：固定定位，基准是viewpoint(视口)，用于回到顶部按钮或广告;
5. sticky:粘滞定位，适合导航；

### 五.CSS动画

* * *
###### (一)transform

* translate位移
```
  transform:translate(<length-percentage>);
  transform:translateX(<length-percentage>);
  transform:translateY(<length-percentage>);
  transform:translateZ(<length-percentage>);
  transform:translate3d(x,y,z);
```
###### 重点：translate(-50%,-50%)可做绝对定位元素的居中

* scale缩放
```
scaleX(<number>)
scaleY(<number>)
scale(<number>,<number>?)
```
* rotate旋转
```
rotate([<angle>or<zero>])
rotateZ([<angle>or<zero>])
rotateX([<angle>or<zero>])
rotateY([<angle>or<zero>])
rotate3D
```
* skew倾斜
```
skewX([<angle>or<zero>])
skewY([<angle>or<zero>])
skew([<angle>or<zero>],[<angle>or<zero>])
```

###### (二)transition

* * *
作用：已知开头和结尾，自动补充中间帧
语法：transition:属性名 时长 过渡方式 延迟
属性名：自定义；
时长：以s或者ms为单位；
过渡方式：linear;ease;ease-in;ease-out;ease-in-out;cubic-bezier;step-start;step-end;steps具体靠数学函数；
延迟：多久后开始动画，直接以时间为单位；
```
transition: left 200ms linear;
```
###### (三)animation

* * *
作用：可以自由调整动画每一帧
语法：animation:时长；过渡方式；延迟；次数；方向；填充模式；是否暂停；动画名；
时长：s或者ms;
过渡方式：与transition取值一样，如Linear；
次数：3或4，也可以infinite;
方向：reverse;alternate;alternate-reverse;
填充模式：None;forwards;backwards;both;
是否暂停：paused;running;

@keyframes常用语法：
```
@keyframes identifier{
0%{
top:0;left:0;
}
30%{
top:50px;
}
68%,72%{
left:50px;
}
100%{
top:100px;left:100%;
}
}
```
