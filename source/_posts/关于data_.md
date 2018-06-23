---
title: HTML 中的data_
categories:
- 技术
- html 
tags:
- Html
- data_
---

### 'data-'属性的作用是什么?

下面我们通过一个例子来看看

我们写一个html页面，自定义一个data-chb="header"的属性，希望具备这个属性的div区域背景颜色为黑色，文字为白色，居中显示；不具备data-chb自定义属性的div按照默认方式显示，html代码如下：

```html
<body>   
  <div data-chb="header">   
    <h1>我是使用了data-chb自定义属性的div</h1>   
  </div>   
  <br/>   
  <div>   
    我没有使用data-chb自定义属性，该怎么展现就怎么展现；   
  </div>   
</body>   

```
<!--more-->
要想实现"背景颜色为黑色，文字为白色，居中显示"的显示效果，我们定义如下的css：

```css
<style>   
 .ui_header {   
  background-color: black;   
  text-align: center;   
  color:white;   
  border:1px solid #000;   
}   
</style>   
```


然后我们通过如下js方法实现在页面加载时，动态添加css定义，改变具备data-chb属性的div的显示样式：

```javascript
<script type="text/javascript">   
    window.onload=function(){   
       var elems = document.getElementsByTagName("div");   
       if(elems!=null&&elems.length>0){   
          var length = elems.length;   
          //遍历所有DIV控件   
          for(var i=0;i<length;i++){   
              var elem = elems[i];   
              //获取该控件的自定义属性   
              var customAttr = elem.dataset.chb;   
             //也可以通过如下方式获得自定义属性   
             //var customAttr = elem.dataset["chb"];   
             //如果是我们预先定义好的header值，表示需要处理   
             if(customAttr=="header"){   
                //添加样式   
                elem.setAttribute("class","ui_header");   
             }   
          }   
      }   
  }   
</script>   
```


这样我们就能动态的改变需要控制的div了。