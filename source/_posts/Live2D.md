---
title: Live2D
date: 2019-03-28 13:55:05
categories:
tags:
---
## 为Blog添加live2d看板娘

### 下载文件 
到github `branch`**Hexo**下载`Live2D-master`文件
1. 复制`demo.html`中的需要的代码,  
在`blog/themes/next/layout/_layout.swig` 查找`footer-inner`  
将刚刚的复制的代码粘贴在  
`<footer id="footer" class="footer">`的后一行， 
`<div class="footer-inner">`的前一行，如下  
```
<footer id="footer" class="footer">

    <link rel="stylesheet" href="/live2d/css/live2d.css" />
        <div id="landlord">
            <div class="message" style="opacity:0"></div>
            <canvas id="live2d" width="200" height="300" class="live2d"></canvas>
            <div class="hide-button">隐藏</div>
        </div>
        <script type="text/javascript" src="/live2d/js/download.js"></script>
        <script type="text/javascript">
            var message_Path = '/live2d/'
            var home_Path = 'https://lovezhaozhen@github.io/'
        </script>
        <script type="text/javascript" src="/live2d/js/live2d.js"></script>
        <script type="text/javascript" src="/live2d/js/message.js"></script>
        <script type="text/javascript">
            loadlive2d("live2d", "/live2d/model/xiaoMai/13.json");
        </script>

<div class="footer-inner">
```
2. 复制`Live2D-master`文件里的`live2d`文件夹到`blog/themes/next/source/`路径中

**Tips:使用hexo框架时，如果在文章中需要引用 css,js,json等文件，不能放在`_post`文件夹下，否则这些文件也会被发布，在blog中~~莫名出现~~`Untitled`文件。**  
可以将这些文件放在`blog/themes/next/source/`中,此时`hexo generate`会将该所用的主题(Next)的`source/`中的文件生成到`public/`中

3. 修改刚刚复制的代码
```
<canvas id="live2d" width="200" height="300" class="live2d"></canvas> //修改大小
var home_Path = 'https://lovezhaozhen@github.io/'  //这里是博客主页Url
loadlive2d("live2d", "/live2d/model/xiaoMai/13.json");  //这里是要用的model

```
4. 修改`/live2d/css/live2d.css`
```
#landlord {
    user-select: none;
    position: fixed;
    left: 30px;    //与页面左边框的距离
    bottom: 0;     //与页面右边框的距离
    width: 200px;  //width与height应与_layout.swig 
    height: 300px; //中的<canvas  width="200" height="300">相同
    z-index: 10000;
    font-size: 0;
    transition: all .3s ease-in-out;

.message {
    opacity: 0;
    width: 220px; //修改message宽度
    height: auto;
    margin: auto;
    padding: 7px;
    top: -50px;   //与小埋图片的距离
    left: -10px;
}
```

5. 修改`/live2d/model/xiaoMai/13.json`
```
	"layout":
	{
		"width":1.8,     //修改图片大小(宽度)，高度自动适应
		"center_x":-0.0507,  //图片在 canvas中
		"center_y":0.45     //的相对位置
	},
```

6. 修改`blog/themes/next/source/live2d/message.json` 修改点击后出现的message
**Tips:在修改live2d大小、位置时，可以在chrome中右键，Inspect,直接修改合适后再更改配置文件**
