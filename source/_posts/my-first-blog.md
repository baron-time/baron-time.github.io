---
title: 自己手写的一个jQuery轮播图+滚动导航楼层效果+点击返回顶部
date: 2019-09-05 11:54:59
tags:
cover: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=864532528,2344832028&fm=26&gp=0.jpg
highlight_copy: true
---
这是我博客的第一天从此以后我自己成长学到的内容将全部放到此地方 欢迎大家访问！

## jQuery轮播图+滚动导航楼层效果+点击返回顶部

### html部分

``` html部分(只有body内)
<ul id="nav">
    <li data-in="go1" class="blue">1</li>
    <li data-in="go2">2</li>
    <li data-in="go3">3</li>
    <li data-in="go4">4</li>
    <li data-in="go5">5</li>
    <li data-in="go6">6</li>
    <li data-in="go7">7</li>
    <li data-in="go8">8</li>
    <li data-in="go9">9</li>
    <li data-in="go10">10</li>
</ul>
<div class="btn">
    <button class="left fl">←</button>
    <button class="right fr">→</button>
</div>
<ul id="list">
    <li id="go1">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
        <div>7</div>
        <div>8</div>
        <div>9</div>
        <div>10</div>
    </li>
    <li id="go2">2</li>
    <li id="go3">3</li>
    <li id="go4">4</li>
    <li id="go5">5</li>
    <li id="go6">6</li>
    <li id="go7">7</li>
    <li id="go8">8</li>
    <li id="go9">9</li>
    <li id="go10">10</li>
    <li class="undfand"> </li>
</ul>

<div class="top">返回顶部</div>
```

### css部分

``` css部分
 * {
	margin:0;
	padding:0;
}
#nav {
	position:fixed;
	left:30px;
	top:10px;
}
#nav li {
	width:50px;
	height:30px;
	font:bold 20px/30px simhei;
	text-align:center;
	list-style-type:none;
	background:#333;
	color:#fff;
	margin:10px 0;
	cursor:pointer;
}
#list {
	width:470px;
	overflow:hidden;
	margin-left:200px;
}
#list li {
	width:470px;
	height:300px;
	text-align:center;
	font:bold 100px/300px simhei;
	list-style-type:none;
	background:yellow;
	color:blue;
	/* margin:50px 200px;
	*/
            margin-bottom:50px;
}
.blue {
	background-color:blue !important;
	color:#fff !important;
}
.undfand {
	background-color:#fff !important;
}
.top {
	position:fixed;
	right:0;
	bottom:0;
	width:50px;
	height:50px;
	background-color:pink;
	cursor:pointer;
}
#list #go1 {
	position:relative;
	height:300px;
}
#go1 div {
	float:left;
	width:470px;
	height:100%;
	background-color:orange;
	margin-right:10px;
}
.btn {
	position:absolute;
	width:546px;
	height:50px;
	top:130px;
	left:160px;
}
.btn button {
	width:30px;
	height:40px;
}
.fl {
	float:left;
}
.fr {
	float:right;
}
```

### js部分

``` js部分
 var len = $('#go1 div').length
 // 动态计算轮播图的宽度
 $(document).ready(function() {
     $('#list #go1').css({
         'width': len * 480
     })
 })
 // 轮播图的右按钮点击
 var i = 0;
 $('.right').on('click', function() {
     i++;
     var j = 480 * i;
     $('#go1').stop().animate({
         'right': j
     })
     if (i >= len) {
         $('#go1').stop().css({
             'right': 0
         });
         i = 0;
     }
 })
 // 轮播图的左按钮点击
 $('.left').on('click', function() {
     i--;
     var j = 480 * i + 'px';
     $('#go1').stop().animate({
         'right': j
     })
     if (i < 0) {
         $('#go1').stop().css({
             'right': 480 * (len - 1)
         });
         i = len;
     }
 })
 // 点击导航滚动到对应位置
 $('#nav').on('click', 'li', function(e) {
     var target = e.target;
     var id = $(target).data("in");
     $('html,body').stop().animate({
         scrollTop: $('#' + id).offset().top
     }, 800);
 });
 // 滚动到某个位置导航某个背景颜色变化
 $(document).scroll(function() {
     var scroH = $(document).scrollTop(); //滚动高度
     var viewH = $(window).height(); //可见高度 
     var contentH = $(document).height(); //内容高度
     var li = $('#nav li');
     if (scroH >= 50) {
         li.eq(0).addClass('blue').siblings().removeClass('blue')
     }
     if (scroH >= 400 - 200) {
         li.eq(1).addClass('blue').siblings().removeClass('blue')
     }
     if (scroH >= 749 - 200) {
         li.eq(2).addClass('blue').siblings().removeClass('blue')
     }
     if (scroH >= 1100 - 200) {
         li.eq(3).addClass('blue').siblings().removeClass('blue')
     }
     if (scroH >= 1450 - 200) {
         li.eq(4).addClass('blue').siblings().removeClass('blue')
     }
     if (scroH >= 1800 - 200) {
         li.eq(5).addClass('blue').siblings().removeClass('blue')
     }
     if (scroH >= 2150 - 200) {
         li.eq(6).addClass('blue').siblings().removeClass('blue')
     }
     if (scroH >= 2500 - 200) {
         li.eq(7).addClass('blue').siblings().removeClass('blue')
     }
     if (scroH >= 2850 - 200) {
         li.eq(8).addClass('blue').siblings().removeClass('blue')
     }
     if (scroH >= 3200 - 200) {
         li.eq(9).addClass('blue').siblings().removeClass('blue')
     }
 });
 // 点击到达顶部
 $('.top').on('click', function() {
     $('html,body').stop().animate({
         scrollTop: 0
     }, 800);
 })
```
## 效果图(点击左侧导航可以到对应的位置和轮播图)
![](/img/lti.gif)
页面刚进去轮播图父盒子的宽度就已经计算出来了 所以宽度是动态的 因为咱们在日常工作总轮播图是后台数据遍历出来的 所以宽度是动态算出来的  左导航方法比较笨不过很容易看懂  代码都很简单新手看四五分钟就懂了
# 此代码需要jq2.2.0以上版本才可以运行