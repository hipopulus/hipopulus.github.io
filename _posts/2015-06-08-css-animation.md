---
layout: post
category: "动画"
title: "CSS Animation"
tags: ["CSS", "Animation"]
---

###这是一个简单的CSS动画，你也可以在[封面][frontCover]看到：###
============================
* 页面载入时，图标从下至上移动并渐渐显示
* 鼠标悬停在图标上时，图标放大

<a id="myGithub" href="https://github.com/soda1015" class="fa fa-github"></a>

****************************

###实现这个动画需要一下技术：###
==============================
1. Web Font（[Font Awesome][fontawesome]-[中文][fontawesomecn]为例）
2. CSS伪元素、伪类
3. CSS过渡（`transition`属性）、CSS动画（`@keyframes`属性、`animation`属性）

****************************

###Web Font###

>   Web Font是通过CSS3的`@font-face`语句引入**在线**的**矢量**图形，它能够支持缩放，减少图片的流量消耗，并且可以重复利用。

以[Font Awesome][fontawesome]为例，下面将一个Github图标显示到网页上：

引入在线CSS文件：

     <link href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css" rel="stylesheet">

将`<a>`标签（也可以是其他标签）的`class`属性设置为某个字体样式，如`fa fa-github`:

     <a id="githubIcon" href="https://github.com/soda1015" class="fa fa-github"></a>

同时为

显示结果如下：

<a id="githubIcon" href="https://github.com/soda1015" class="fa fa-github"></a>

为图标设置一下式样：

    #githubIcon {
        color: inherit;
        text-decoration: none;
        border-radius: 100%;
        border: solid 1px #333;
        display: block;
        font-size: 2.0em;
        height: 2.5em;
        line-height: 2.5em;
        position: relative;
        text-align: center;
        top: 0;
        margin: auto;
        width: 2.5em; }

结果如下：

<a id="githubIcon1" href="https://github.com/soda1015" class="fa fa-github"></a>

###CSS伪元素和伪类###

>   伪元素和伪类实际上是指两种选择器，选择器通过元素的标签名、类名或属性名获得该元素，如果某选择器没有对应的标签名、类名或属性名，而是通过某些特殊状态来获取元素，则该选择器为伪元素或伪类选择器。伪元素或伪类必须跟在某个选择器之后。

`:hover`为伪类中的一种，它选择鼠标当前悬停位置的元素，并设置元素属性，例如，使它放大两倍：

    #githubIcon:hover {
        font-size: 4em;
    }

<a id="githubIcon2" href="https://github.com/soda1015" class="fa fa-github"></a>

###CSS过渡（transition属性）###

刚刚的放大效果有些唐突，我们为图标设置`transition`属性，使之有一个过渡：

    #githubIcon {
        -moz-transition: all 0.2s ease-in-out;
        -webkit-transition: all 0.2s ease-in-out;
        -o-transition: all 0.2s ease-in-out;
        -ms-transition: all 0.2s ease-in-out;
        transition: all 0.2s ease-in-out;
        color: inherit;
        text-decoration: none;
        border-radius: 100%;
        border: solid 1px #333;
        display: block;
        font-size: 2.0em;
        height: 2.5em;
        line-height: 2.5em;
        position: relative;
        text-align: center;
        top: 0;
        margin: auto;
        width: 2.5em; }

<a id="githubIcon3" href="https://github.com/soda1015" class="fa fa-github"></a>

###CSS动画（`@keyframes`属性、`animation`属性）###

接下来，我们来添加一个动画效果：图标由下至上的移动，并逐渐显示

>   为元素添加动画需要两步：1.定义动画；2.设置元素动画属性为定义的动画

定义动画`@keyframes`：

    @keyframes icon-animation {
        0% {
            -moz-transform: translate3d(0,1em,0);
            -webkit-transform: translate3d(0,1em,0);
            -o-transform: translate3d(0,1em,0);
            -ms-transform: translate3d(0,1em,0);
            transform: translate3d(0,1em,0);
            opacity: 0; }
        100% {
            -moz-transform: translate3d(0,0,0);
            -webkit-transform: translate3d(0,0,0);
            -o-transform: translate3d(0,0,0);
            -ms-transform: translate3d(0,0,0);
            transform: translate3d(0,0,0);
            opacity: 1; } }

设置动画属性`animation: icon-animation 1.5s infinite ease-in-out forwards;`：

    #githubIcon {
        -moz-transition: all 0.2s ease-in-out;
        -webkit-transition: all 0.2s ease-in-out;
        -o-transition: all 0.2s ease-in-out;
        -ms-transition: all 0.2s ease-in-out;
        transition: all 0.2s ease-in-out;
        -moz-animation: icon-animation 1.5s infinite ease-in-out forwards;
        -webkit-animation: icon-animation 1.5s infinite ease-in-out forwards;
        -o-animation: icon-animation 1.5s infinite ease-in-out forwards;
        -ms-animation: icon-animation 1.5s infinite ease-in-out forwards;
        animation: icon-animation 1.5s infinite ease-in-out forwards;
        color: inherit;
        text-decoration: none;
        border-radius: 100%;
        border: solid 1px #333;
        display: block;
        font-size: 2.0em;
        height: 2.5em;
        line-height: 2.5em;
        position: relative;
        text-align: center;
        top: 0;
        margin: auto;
        width: 2.5em; }

最后，当鼠标悬停在图标上时，动画暂停`animation-play-state: paused;`：

    #githubIcon:hover {
        font-size: 4em;
        animation-play-state: paused;
        -moz-animation-play-state: paused;
        -webkit-animation-play-state: paused;
        -o-animation-play-state: paused;
        -ms-animation-play-state: paused;
    }


<a id="githubIcon4" href="https://github.com/soda1015" class="fa fa-github"></a>

**********************************

###更多好网站##
<http://www.w3.org/TR/css3-content/>：content属性与伪元素配合使用来生成内容，CSS3为content增加了更多特性。  
<https://cssanimation.rocks/cn/principles/>：动画的十二个原则描述了动画能怎样用于让观众相信自己沉浸在现实世界中。  
<http://www.iconfont.cn>：阿里巴巴UX部门推出的矢量图标管理网站，也是国内首家推广Webfont形式图标的平台  
<https://developer.mozilla.org/zh-CN/docs/Web/SVG>：矢量图文件有不同的格式，可缩放矢量图形（Scalable Vector Graphics，SVG)是其中一种，它本质是xml。

**********************************

[fontawesome]: http://fortawesome.github.io/Font-Awesome/
[fontawesomecn]:http://www.bootcss.com/p/font-awesome/
[frontCover]: http://blog.hipoplar.me/
