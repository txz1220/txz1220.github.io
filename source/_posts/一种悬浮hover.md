---
title: 一种hover效果
categories:
- 技术
- css
- hover
tags:
- css
- hover
---

### 效果如下

![](/images/hover.gif)


主要运用了不同的动画实现方式，可以学习下。

<!---more-->
### 实现方式如下


```html
/* 定义按钮 */

    .button {
        top:100px;
        margin: 0.2em;
        left: 50%;
        padding: 1em;
        cursor: pointer;
        background: #ececec;
        text-decoration: none;
        color: #666;
    }

    /* 让我们先定义个动画  我们知道定义动画需要先用关键字@keyframes 来定义我们需要用到的动画 
     hover 和 hover-shadow 就是两个动画的名字了 
     0 50% 100% 代表的是过度效果。里面的内容就是变化的内容
     里面的 transform 是另外一种二D动画  其中translateY 代表的是沿着Y轴移动  opacity代表的是透明度 */


    @keyframes hover {
        50% {
            transform: translateY(-3px);
        }
        100% {
            transform: translateY(-6px);
        }
    }

    @keyframes hover-shadow {
        0% {
            transform: translateY(6px);
            opacity: 0.4;
        }
        50% {
            transform: translateY(3px);
            opacity: 1;
        }
        100% {
            transform: translateY(6px);
            opacity: 0.4;
        }
    }

    .hover-shadow {
        display: inline-block;
        position: relative;
        transition-duration: .3s;
        transition-property: transform;
        /* Prevent highlight colour when element is tapped  只适用于ios  不用管它 */
        -webkit-tap-highlight-color: rgba(0, 0, 0, 0);  
        transform: translateZ(0);
        /* 做一点小的阴影效果 */
        box-shadow: 0 0 1px rgba(0, 0, 0, 0);
    }
/* 下面是添加阴影效果，过会用来实现动画的 */

    .hover-shadow:before {
        pointer-events: none;
        position: absolute;
        z-index: -1;
        content: '';
        top: 100%;
        left: 5%;
        height: 10px;
        width: 90%;
        opacity: 0;
        background: radial-gradient(ellipse at center, rgba(0, 0, 0, 0.35) 0%, rgba(0, 0, 0, 0) 80%);
        /* W3C */
        transition-duration: .3s;
        transition-property: transform opacity;
    }
/* 添加效果 */
    .hover-shadow:hover {
        transform: translateY(-6px);
        animation-name: hover;
        animation-duration: 1.5s;
        animation-delay: .3s;
        animation-timing-function: linear;
        animation-iteration-count: infinite;
        animation-direction: alternate;
    }

    .hover-shadow:hover:before {
        opacity: 0.4;
        transform: translateY(6px);
        animation-name: hover-shadow;
        animation-duration: 1.5s;
        animation-delay: 0.3s;
        animation-timing-function: linear;
        animation-iteration-count: infinite;
        animation-direction: alternate;
    }
</style>

<div class="button hover-shadow">
    点击我吧
</div>
```


<完>