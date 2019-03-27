---
title: 博客配置
date: 2019-03-21 13:47:44
categories: 
- 博客搭建
tags: [blog]
---

## 使用NexT主题
- 进入themes目录
`git clone https://github.com/theme-next/hexo-theme-next.git next/`
- 设置主题
打开配置文件_config.yml
找到theme修改为：
`themes: next`
<!-- more-->

## Hexo同步部署上传
* 在github上新建一个`branch`**Hexo**
* 在blog根目录安装插件`npm install hexo-git-backup --save`
* 在根目录下`_config.yml`文件结尾添加
```
# 同步部署
backup:
  type: git
  repository:
    github: git@github.com:loveZhaoZhen/loveZhaoZhen.github.io.git,Hexo
```
* 进行同步部署 `hexo b(backup)`  
Tips:
>Update
>if you install with --save, you must remove firstly when you update it.
>`$ npm remove hexo-git-backup`
>`$ npm install hexo-git-backup --save`

>You may get some troubles by your computer' permission。
>just do `sudo hexo b`


## 配置Next主题 
[Next官方配置文档](http://theme-next.iissnan.com/theme-settings.html)  

### 配置`/themes/next/_config.yml`文件

#### 修改网站底部信息
```
footer:
    since: 2019（建站时间）
    copyright:
    powered: false (不显示hexo授权图片)
    theme: （不显示网站Next主题信息）
        enable: false
```

#### 菜单栏menu
```
menu:
  home: / || home
  #about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
```
#### 主题风格
```
# Schemes
#scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini 
```
这里选择`Pisces`

#### 个人社交信息
```
social:
  E-Mail: https://love.zhaozhen@gmail.com || envelope  (tip:前面必须加上网络协议)
```

#### 网站头像
`avatar:`

#### 网站动画效果
```
motion:
  enable: true
  async: true
```
选择一个动画效果，不止有如下选择，但只能同时选择一个
```
canvas_nest: true
three_waves: false
canvas_lines: false
canvas_sphere: false
```
需要**Download**js文件
进入next主题目录中*source/lib* direcotry
`git clone https://github.com/theme-next/theme-next-canvas-nest canvas-nest`
**Update**
```
cd themes/next/source/lib/canvas-nest
git pull
```
#### 复制代码按钮
```
codeblock:
  border_radius:
  copy_button:
    enable: false
    show_result: false
```
#### 站内搜索
* 安装站内搜索插件  
  在blog根目录下
`npm install hexo-generator-searchdb --save`  
<br>
* 在blog根目录`_config.yml`中添加
```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```
* 在`/themes/next/_config.yml`中搜索`local_search`并做如下修改
```
local_search:
  enable: true
  trigger: auto
  top_n_per_article: 1
  unescape: true
```

#### 打赏功能
在`themes/next/_config.yml`中搜索`reward`
支持微信(wechatpay)，支付宝(alipay)，比特币(bitcoin)


### 用LeanCloud增加Blog文章访问量功能
-　注册leancloud [Leancloud官网](https://leancloud.cn/)
- 进入控制台，创建应用（名称随意，可以更改）
- 点击应用右上角的齿轮图标（设置） -->存储 -->创建class (此处`class name 必须是` `Counter`)，权限可设为所有用户
- 在安全中心添加Web安全域名, 如`https://lovezhaozhen.github.io/`
- 找到 应用key 复制AppID 与 AppKey
- 打开`next`的配置文件`themes/next/_config.yml`
    找到
    ```
    leancloud_visitors:
        enable: true
        app_id: 
        app_key: 
        security: true
        betterPerformance: false
    ```
    对应填上刚复制的AppID 与 AppKey
- 打开blog配置文件`_config.yml`
        在最后添加如下代码
    ```
    leancloud_counter_security:
        enable_sync: true
        app_id: lMLdjNReIMxWXUbCfFcApNGb-gzGzoHsz
        app_key: GUCncs6ewY1f8yfwy92yNQ0J
        username: <<username>> 
        password: <<password>>
    ```
- 安装`hexo-leancloud-counter-security`插件  
    在blog文件**根目录**下输入  
        `npm install hexo-leancloud-counter-security --save`  
        相同路径下输入  
        `hexo lc-counter register username password`(username password 随便输，不需要是leancloud的用户名密码)
- 打开blog配置文件`_config.yml`  
    - 将之前添加的 `<<username>>和<<password>>`替换为 刚设置的用户名密码(密码是纯数字需要加上双引号（表明是字符串），此用户名和密码将在hexo部署时使用。
    - 在deploy下增加`type:              leancloud_counter_security_sync`  
        如下
        ```
        deploy:
        - type: git
        repo: git@github.com:loveZhaoZhen/loveZhaoZhen.github.io.git
        branch: master
        - type: leancloud_counter_security_sync
        ```
- 进一步设置权限  
    进入[leancloud网站](https://leancloud.cn/)
    设置class *Counter*的权限，将*add_fields*,*create*,*delete*权限都设为指定用户(在**用户**中输入之前设置的*username*之后点击添加即可)

可在浏览器点击右键点击**Inspect**查看是否有bug
[另附详转载细配置教程](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/LEANCLOUD-COUNTER-SECURITY.md)（内含leancloud权限详细配置）

### 为博客增加评论功能
这里选择livere
[详见官网](http://theme-next.iissnan.com/third-party-services.html#comment-system)

### DaoVoice 在线联系
首先注册[daovoice](http://dashboard.daovoice.io)账号,邀请码是`0f81ff2f`，注册完成后会得到一个 app_id 
打开`/themes/next/layout/_partials/head.swig`在文件末尾写入
```
{% if theme.daovoice %}
  <script>
  (function(i,s,o,g,r,a,m){i["DaoVoiceObject"]=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;a.charset="utf-8";m.parentNode.insertBefore(a,m)})(window,document,"script",('https:' == document.location.protocol ? 'https:' : 'http:') + "//widget.daovoice.io/widget/0f81ff2f.js","daovoice")
  daovoice('init', {
      app_id: "{{theme.daovoice_app_id}}"
    });
  daovoice('update');
  </script>
{% endif %}
```
打开主题配置文件`themes/next/_config.yml`，在最后写下如下代码：
```
# Online contact 
daovoice: true
daovoice_app_id: 填入你的app_id

```
# Online contact 
daovoice: true
daovoice_app_id: 这里填你的刚才获得的 app_id


### 在每篇文章末尾加上结束标志
* 在`\themes\next\layout\_macro` 中新建 `passage-end-tag.swig` 文件,并添加以下内容：
```
<div>
    {% if not is_index %}
        <div style="text-align:center;color: #ccc;font-size:20px;">-------------本文结束-------------</div>
    {% endif %}
</div>
```
* 打开`\themes\next\layout\_macro\post.swig`文件，在`<div class="post-body></div>` 之后， `<div class="post-footer></div>`之前添加如下代码
```
<div>
  {% if not is_index %}
    {% include 'passage-end-tag.swig' %}
  {% endif %}
</div>
```
* 最后打开主题配置文件（/themes/next/_config.yml),在末尾添加：
```
# 文章末尾添加“本文结束”标记
passage_end_tag:
  enabled: true
```
### 自定义样式
如:
* 代码块自定义样式
* 主页文章添加阴影效果
* 文章目录默认展开
打开`\themes\next\source\css\_custom\custom.styl`,加入：(自己看需求修改定义)
```
// Custom styles.
code {
    color: #ff7600;
    background: #fbf7f8;
    margin: 2px;
}
// 大代码块的自定义样式
.highlight, pre {
    margin: 5px 0;
    padding: 5px;
    border-radius: 3px;
}
.highlight, code, pre {
    border: 1px solid #d6d6d6;
}

// 主页文章添加阴影效果
 .post {
   margin-top: 60px;
   margin-bottom: 60px;
   padding: 25px;
   -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
   -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
  }

// 文章目录默认展开
.post-toc .nav .nav-child { display: block; }
// 目录字体大小调整
.post-toc ol {  
  font-size : 16px;     
}  
```


### 在右上角或者左上角实现fork me on github
* 打开链接选择样式，复制该样式代码
[样式1](http://tholman.com/github-corners/)
[样式2](https://github.blog/2008-12-19-github-ribbons/)
* 然后粘贴刚才复制的代码到`themes/next/layout/_layout.swig`文件中(放在`<div class="headband"></div>`的下面)
* 把href改为你的github地址
如下
```
  <div class="{{ container_class }} {% block page_class %}{% endblock %}">
    <div class="headband"></div>

  <a href="https://github.com/loveZhaoZhen" (修改此处)
  class="github-corner" aria-label="View source on GitHub">
  ......
  .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>

    <header id="header" class="header" itemscope itemtype="http://schema.org/WPHeader">
      <div class="header-inner">{% include '_partials/header/index.swig' %}</div>
    </header>
```


### [参考文章](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)
