[TOC]

https://lovenight.github.io/2015/11/10/Hexo-3-1-1-%E9%9D%99%E6%80%81%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E6%8C%87%E5%8D%97/

https://lovenight.github.io/2015/11/17/%E6%8B%96%E6%9B%B3%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0%E5%88%B0%E4%B8%83%E7%89%9B%E7%9A%84%E8%84%9A%E6%9C%AC/


https://blog.csdn.net/lemonxq/article/details/72676005

## 一、前期准备

### Windows上node.js安装

在https://nodejs.org下载node.js
版本v10.13.0

### 安装git
版本2.13.0

下载安装后，注册Github账号并配置Git和SSH公私钥

### GitHub账号

### 安装hexo

版本v3.8.0

在git bash或cmd中执行都可以

执行如下命令安装Hexo：

    npm install -g hexo

也可以指定版本安装：
    
    npm install hexo@3.1.1 -g

可用hexo -v查看版本


## 二、搭建博客


### 1.创建hexo文件夹：
Node和Git都安装好后,首先创建一个文件夹,进入并执行命令hexo init。hexo 会在目标文件夹建立网站所需要的所有文件。

    hexo init

### 2. 安装依赖包： 
    
    npm install

### 3.创建Github Repository   

Repository名字必须是你的Github名.github.io

### 4.部署：

打开博客根目录下的_config.yml文件，末尾添加如下信息。

    deploy:
      type: git
      repository: 上一步的Github仓库地址，项目主页点SSH再复制URL
      branch: master

+ 配置文件的冒号后必须有一个空格。

### 5.然后执行命令：

    hexo generate # 生成静态页面，可以简化为hexo g
    hexo deploy # 部署到Github，可以简化为hexo d

### 6.本地启动

启动本地服务，进行文章预览调试，命令：

    hexo server（hexo s也可以）

开启调试模式

    hexo s --debug    

浏览器输入http://localhost:4000，当你修改了文章或配置文件时，保存文件再刷新浏览器就能看到修改后的效果，非常方便。



如果报错

    Deployer not found:git

运行命令

    npm install hexo-deployer-git --save



## 三、博客内容编辑

### 1.新建文章

    hexo new post "title"  # 生成新文章：\source\_posts\title.md，可省略post

### 2.新建页面

    hexo new page "title"

post、page等可以改成其他layout，可用layout在scaffolds目录下查看。在同目录下创建文件来添加自己的layout，也可以编辑现有的layout，比如post的layout默认是\scaffolds\post.md。

### 3.编辑文章

打开新建的文章`\source\_posts\postName.md`：

    title: HelloWorld！ # 文章页面上的显示名称，可以任意修改，不会出现在URL中
    date: 2015-11-09 15:56:26 # 文章生成时间，一般不改
    categories:   # 文章分类目录，参数可省略
        - 随笔
        - 瞬间
    tags:   # 文章标签，参数可省略
        - hexo
        - blog # 个数不限，单个可直接跟在tags后面
    ---
    这里开始使用markdown格式输入你的正文。

多级分类语法格式：（标签也可以用类似的写法）

    # 第一种
    categories:
      - 一级分类
      - 二级分类
      - etc...

    # 第二种：
    categories: [一级分类, 二级分类]

首页文章预览添加图片：

    photos:
      - http://xxx.com/photo1.jpg
      - http://xxx.com/photo2.jpg

正文中可以使用`<!--more-->`设置文章摘要 如下:

    以上显示在摘要中
    <!--more-->
    以下是余下全文


more 以上内容即是文章摘要，如果设置了主页只显示摘要，则more以下内容点击 `Read More ` 链接打开全文才显示。


### 4.简单命令

hexo现在支持更加简单的命令格式了，比如：

    hexo g == hexo generate # 生成
    hexo d == hexo deploy # 部署 # 可与hexo g合并为 hexo d -g
    hexo s == hexo server # 本地预览
    hexo n == hexo new # 写文章


### 5.插入图片

博客中的图片文件可以直接放在source文件夹下，部署时上传到Github仓库中。但是Github项目容量有限，而且主机在国外，访问速度较慢，把图片放在国内的图床上是个更好的选择。使用七牛云存储
    
+ 注册账号，新建空间，我的新空间名是blog，专门用来放置博客上引用的资源。
+ 进入空间后点击「内容管理」，再点击「上传」：
+ 七牛空间没有文件夹的概念，但是允许为文件添加带斜杠/的前缀，用来给资源分类。这里我设置前缀为img/Hexo 3.1.1 静态博客搭建指南/。上传了一张图片：
+ 在右侧可以找到外链，复制地址：
+ Markdown 插入图片的语法为：
```
    ![](图片网址)
```


## 四、配置博客

### 全站配置

**注意：文件中配置项的冒号后面必须加空格，否则报错**

下面有些选项要配置后文的插件才有效，文件中已注明。

+ **整站的配置：博客根目录下的`\_config.yml`文件。**

```
# Hexo Configuration
## Docs: http://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: 岁月如歌 # 站点名
subtitle: 莫厌追欢笑语频，寻思离乱好伤神。闲来屈指从头数，得见清平有几人 # 副标题
description: 自古求真皆寂寞，唯挑心灯伴夜霭
author: loveNight # 作者，在站点左下角可以看到
avatar: /images/avatar.jpg # 头像。Next主题增加的字段
language: zh-Hans # 语言。Next主题增加的字段
timezone:
since: 2015 # 博客建立年份，Next主题增加的字段

# 多说 ShortName
duoshuo_shortname: # xxx.duoshuo.com，xxx即是shortname。

# Social links
social:
  Github: https://github.com/loveNight
  Weibo: http://weibo.com/p/1005051069913250
  Email: mailto:286242151@qq.com
  # zhihu: http://www.zhihu.com/people/your-user-name

# title, chinese available
links_title: 友情链接
# links
links:
  我的CSDN博客: http://blog.csdn.net/kinglearnjava
  我的新浪博客: http://blog.sina.com.cn/u/1069913250


# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://lovenight.github.io/ # 网址
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang  # 国际化文件夹
skip_render:   # 跳过指定文件的渲染

# Writing # 文章布局、写作格式的定义
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0   # 1 为小写， 2 为大写
render_drafts: false  # 显示草稿
post_asset_folder: false  # 启动asset文件夹
relative_link: false # 链接改为与根目录的相对地址
future: true  # 显示未来的文章
highlight:
  enable: true
  line_number: true
  auto_detect: true
  tab_replace:

# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination # 每页显示文章数
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions # 这里配置站点所用主题和插件
## Plugins: http://hexo.io/plugins/
plugins:
baidusitemap: # 需要安装插件 npm install hexo-generator-baidu-sitemap@0.1.1 --save
  path: baidusitemap.xml

# Extensions
## Plugins: http://hexo.io/plugins/
## Themes: http://hexo.io/themes/
theme: next

feed:
  type: atom       #feed 类型 (atom/rss2)
  path: atom.xml   #rss 路径
  limit: 0        #在 rss 中最多生成的文章数(0显示所有)

# 自定义站点内容搜索
# 需要先安装插件：
# npm install hexo-generator-search --save
search:
  path: search.xml
  field: all  # 如只想索引文章，可设置为post


# Deployment # 站点部署到github
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: git@github.com:loveNight/loveNight.github.io.git
  branch: master


# ---------------下面选项需要对应插件的支持---------------
# npm install hexo-generator-index --save
# npm install hexo-generator-archive --save
# npm install hexo-generator-category --save
# npm install hexo-generator-tag --save

index_generator:
  per_page: 10 ##首页默认10篇文章标题 如果值为0不分页

archive_generator:
  per_page: 20 ##归档页面默认20篇文章标题
  yearly: true  ##生成年视图
  monthly: true ##生成月视图

tag_generator:
  per_page: 10 ##标签分类页面默认10篇文章

category_generator:
  per_page: 10 ###分类页面默认10篇文章
```


### 更换主题

默认主题太丑，换成`NexT`主题。

next 安装文档
http://theme-next.iissnan.com/getting-started.html

+ 安装：在博客根目录下执行`git clone https://github.com/iissnan/hexo-theme-next.git themes/next`
+ 启用：修改博客根目录下的`_config.yml`配置文件中的`theme`属性，将其设置为`next`。
+ 更新：在`themes/next`目录下执行`git pull`。（暂时不需要）
+ `\themes\next\_config.yml`修改主题配置。


我的_config.yml文件：

```
# ---------------------------------------------------------------
# Site Information Settings
# ---------------------------------------------------------------

# Place your favicon.ico to /source directory.
favicon: /favicon.ico

# Set default keywords (Use a comma to separate)
keywords: "loveNight, Android, Python, 神锋"

# Set rss to false to disable feed link.
# Leave rss as empty to use site's feed link.
# Set rss to specific value if you have burned your feed already.
rss:

# Specify the date when the site was setup
#since: 2015


# ---------------------------------------------------------------
# Menu Settings
# ---------------------------------------------------------------

# When running hexo in a subdirectory (e.g. domain.tld/blog)
# Remove leading slashes ( "/archives" -> "archives" )
menu:
  home: /
  archives: /archives
  categories: /categories
  tags: /tags
  Android: /Android
  Python: /Python
  API: /API
  Notes: /Notes
  Links: /Links
  About: /About

  #commonweal: /404.html


# Enable/Disable menu icons.
# Icon Mapping:
#   Map a menu item to a specific FontAwesome icon name.
#   Key is the name of menu item and value is the name of FontAwsome icon.
#   When an question mask icon presenting up means that the item has no mapping icon.
menu_icons:
  enable: true
  # Icon Mapping.
  home: home
  about: user
  categories: th
  tags: tags
  archives: archive
  commonweal: heartbeat




# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------

# Schemes
scheme: Mist




# ---------------------------------------------------------------
# Sidebar Settings
# ---------------------------------------------------------------

# Sidebar, available value:
#  - post    expand on posts automatically. Default.
#  - always  expand for all pages automatically
#  - hide    expand only when click on the sidebar toggle icon.
#  - remove  Totally remove sidebar including sidebar toggle icon.
sidebar: always
# sidebar: post
#sidebar: hide
#sidebar: remove


# Social links
# social:
  #GitHub:
  #Others:

# Social Icons
social_icons:
  enable: true
  # Icon Mappings
  GitHub: github
  Twitter: twitter
  Weibo: weibo


# Sidebar Avatar
#avatar:


# Social links
# social:
  #GitHub:
  #Others:


# TOC in the Sidebar
toc:
  enable: true

  # Automatically add list number to toc.
  number: true


# Creative Commons 4.0 International License.
# http://creativecommons.org/
# Available: by | by-nc | by-nc-nd | by-nc-sa | by-nd | by-sa | zero
#creative_commons: by-nc-sa
#creative_commons:




# ---------------------------------------------------------------
# Misc Theme Settings
# ---------------------------------------------------------------

# Custom Logo.
# !!Only available for Default Scheme currently.
# Options:
#   enabled: [true/false] - Replace with specific image
#   image: url-of-image   - Images's url
custom_logo:
  enabled: false
  image:


# Code Highlight theme
# Available value:
#    normal | night | night eighties | night blue | night bright
# https://github.com/chriskempson/tomorrow-theme
highlight_theme: night blue

# `阅读全文` 按钮跳转之后是否自动滚动页面到设置 `<!-- more -->` 的地方。
scroll_to_more: true

# 是否为侧边栏文章的目录自动添加索引，默认开启。设置为 `false` 关闭。
toc_list_number: true

# Automatically Excerpt
auto_excerpt:
  enable: false
  length: 150

# Use Lato font
use_font_lato: true



# ---------------------------------------------------------------
# Third Party Services Settings
# ---------------------------------------------------------------

# MathJax Support # 数学公式，要使用就设置为True
mathjax:


# Swiftype Search API Key
swiftype_key:

# Baidu Analytics ID
#baidu_analytics:


# 多说热评文章 true 或者 false
# duoshuo_hotartical: true

# Disqus
#disqus_shortname:

# Share
jiathis: true

# Share
# duoshuo_share: true

# Google Webmaster tools verification setting
# See: https://www.google.com/webmasters/
#google_site_verification:


# Google Analytics
#google_analytics:


# Make duoshuo show UA
# user_id must NOT be null when admin_enable is true!
# you can visit http://dev.duoshuo.com get duoshuo user id.
duoshuo_info:
  ua_enable: true
  admin_enable: false
  user_id: 0
  #admin_nickname: ROOT


# Facebook SDK Support.
# https://github.com/iissnan/hexo-theme-next/pull/410
facebook_sdk:
  enable: false
  app_id:       #<app_id>
  fb_admin:     #<user_id>
  like_button:  #true
  webmaster:    #true









#! ---------------------------------------------------------------
#! DO NOT EDIT THE FOLLOWING SETTINGS
#! UNLESS YOU KNOW WHAT YOU ARE DOING
#! ---------------------------------------------------------------

# Motion
use_motion: true

# Fancybox
fancybox: true

# Static files
vendors: vendors
css: css
js: js
images: images

# Theme version
version: 0.4.5.2

```


### 个性化设置

先按照 [NexT 使用文档](http://theme-next.iissnan.com/ "NexT 使用文档") 设置一下，其中的内容下面不再赘述。


### sitemap 插件

谷歌与百度的站点地图，前者适用于其他搜索引擎，用来手动提交以增加收录


安装：

    npm install hexo-generator-sitemap@1 --save
    npm install hexo-generator-baidu-sitemap@0.1.1 --save

_config.yml添加代码：

    baidusitemap:
      path: baidusitemap.xml

谷歌的sitemap.xml不需要写到配置文件中，自动生效。

在主页后面加/baidusitemap.xml可以看到baidusitemap（谷歌同理），将该网址它提交给百度搜索：百度站长平台，贴吧账号无法在这里使用。

不过由于Github禁止了百度爬虫，百度无法抓取其中的URL,除非把博客托管到其他平台上。


### 添加新 Page

用如下命令添加新page

    hexo new page "Android"
    hexo new page "Python"
    hexo new page "API"

然后在主题配置文件`\themes\next\_config.yml`添加：

    menu:
      home: /
      categories: /categories
      archives: /archives
      tags: /tags
      Android: /Android  # 加在这里
      Python: /Python
      API: /API

打开`\themes\next\languages\zh-Hans.yml`，这是简体中文的配置文件，如果你的博客用的是其他语言，请打开对应的文件。

    menu:
      home: 首页
      archives: 归档
      categories: 分类
      tags: 标签
      about: 关于
      search: 搜索
      commonweal: 公益404
      android: Android
      python: Python
      api: API

注意这里第一列必须全为小写

### 自动弹出侧栏的BUG

配置文件里写着：

    # Sidebar, available value:
    #  - post    expand on posts automatically. Default.
    #  - always  expand for all pages automatically
    #  - hide    expand only when click on the sidebar toggle icon.
    #  - remove  Totally remove sidebar including sidebar toggle icon.

但是当设置成`always`时，侧栏在文章页却不会自动弹出。在别的页面都能正常。

在`\themes\next\layout/_scripts/pages/post-details.swig`文件里看到这段代码
    

    // Expand sidebar on post detail page by default, when post has a toc.
    motionMiddleWares.sidebar = function () {
      var $tocContent = $('.post-toc-content');
      if (CONFIG.sidebar === 'post') {
        if ($tocContent.length > 0 && $tocContent.html().trim().length > 0) {
          displaySidebar();
        }
      }
    };

虽然没学过JS，但是看注释和 if 语句，都是仅在sidebar参数为post时才会自动展开，坑爹呢。在if里加上always判断，即可，修改后如下：  

    // Expand sidebar on post detail page by default, when post has a toc.
        motionMiddleWares.sidebar = function () {
          var $tocContent = $('.post-toc-content');
          if (CONFIG.sidebar === 'post' || CONFIG.sidebar === 'always') {
            if ($tocContent.length > 0 && $tocContent.html().trim().length > 0) {
              displaySidebar();
            }
          }
        };

### 使Page也自动弹出侧栏

上一步中只有主页和文章页才会弹侧栏，自己添加的Page却不会。打开`\themes\next\layout\page.swig`，找到底部的

```
    {% block sidebar %}
        {{ sidebar_template.render(false) }}
    {% endblock %}
```

把`false`改成`true`。这时不管有没有目录，都会弹出侧栏。需要让它根据目录的度来决定是否弹出，继续修改，结果如下：
```
    {% block sidebar %}
        {{ sidebar_template.render(true) }}
    {% endblock %}
```

```
    {% block script_extra %}
      {% include '_scripts/pages/post-details.swig' %}
    {% endblock %}
```

直接使用与文章页（post-details）相同的侧栏设置。

### 修改页面宽度

现在一般都用宽屏显示器，博客页面两侧留白太多，调整一下宽度。
打开`\themes\next\source\css\_common\components\post\post-expand.styl`文件，找到

    @media (max-width: 767px)

改为

    @media (max-width: 1080px)

打开`\themes\next\source\css\ _variables\base.styl`文件，找到

    $main-desktop                   = 960px
    $main-desktop-large             = 1200px
    $content-desktop                = 700px

修改`$main-desktop`和`$content-desktop`的数值：

    $main-desktop                   = 1080px
    $main-desktop-large             = 1200px
    $content-desktop                = 810px

Next.Mist主题的文章宽度至此改完了。如果你用的是Next.Pisces，还需要继续修改。
打开`\themes\next\source\css\_schemes\Pisces\_layout.styl`文件，将第4行的`width`改为`1080px`，修改后如下：

    .header {
      position: relative;
      margin: 0 auto;
      width: 1080px;

### 修改字体大小

打开`\themes\next\source\css\ _variables\base.styl`文件，将`$font-size-base`改成`16px`：

    $font-size-base           = 16px

### 修改网页配色

#### 添加自定义颜色

继续修改上一步中的`\themes\next\source\css\ _variables\base.styl`文件，找到文件开头的`colors for use across theme`，加入自定义颜色：

```
// Colors
// colors for use across theme.
// --------------------------------------------------
$whitesmoke   = #f5f5f5
$gainsboro    = #eee
$gray-lighter = #ddd
$grey-light   = #ccc
$grey         = #bbb
$grey-dark    = #999
$grey-dim     = #666
$black-light  = #555
$black-dim    = #333
$black-deep   = #222
$red          = #ff2a2a
$blue-bright  = #87daff
$blue         = #0684bd
$blue-deep    = #262a30
$orange       = #fc6423
// 下面是我自定义的颜色
$my-link-blue = #0593d3  //链接颜色
$my-link-hover-blue = #0477ab  //鼠标悬停后颜色
$my-code-foreground = #dd0055  // 用``围出的代码块字体颜色
$my-code-background = #eee  // 用``围出的代码块背景颜色

```


#### 修改超链接颜色

改掉这几行：

    // Global link color.
    $link-color                   = $my-link-blue
    $link-hover-color             = $my-link-hover-blue
    $link-decoration-color        = $gray-lighter
    $link-decoration-hover-color  = $my-link-hover-blue


#### 修改小型代码块颜色

修改`$code-background`和`$code-foreground`的值：

    // Code & Code Blocks
    // 用``围出的代码块
    // --------------------------------------------------
    $code-font-family               = $font-family-monospace
    $code-font-size                 = 15px
    $code-background                = $my-code-background
    $code-foreground                = $my-code-foreground
    $code-border-radius             = 4px

### 替换字体库网址

使用中发现网站打开速度巨慢，一开始以为是Github的原因，但是本地调试时也要一分钟才能打开。使用Chrome抓包发现：

在`\themes\next`目录执行命令
    
    grep 'css?family' -r ./

可以找到罪魁祸首就在`\themes\next\layout\_partials\head.swig`文件中：

```
{% if theme.use_font_lato %}
  {% if config.language === 'zh-Hans' %}
    <link href='//fonts.lug.ustc.edu.cn/css?family=Lato:300,400,700,400italic&subset=latin,latin-ext' rel='stylesheet' type='text/css'>
  {% else %}
    <link href='//fonts.googleapis.com/css?family=Lato:300,400,700,400italic&subset=latin,latin-ext' rel='stylesheet' type='text/css'>
  {% endif %}
{% endif %}
```


作者的原意是想让语言设置为简体的用户都连接到中国科技大学的免费字体库，其他用户链接到Google，没想到这个链接挂了。使用[Ping检测工具](http://ping.chinaz.com/)可以看到`fonts.googleapis.com`被解析到了北京的服务器，速度相当快，所以我们直接使用Google的字体库就可以了：

    {% if theme.use_font_lato %}
        <link href='//fonts.googleapis.com/css?family=Lato:300,400,700,400italic&subset=latin,latin-ext' rel='stylesheet' type='text/css'>
    {% endif %}

### 修改底栏

先准备一些代码。[站长统计](https://www.umeng.com/)，注册并获取统计代码：

```
&nbsp;&nbsp;|&nbsp;&nbsp;
<script type="text/javascript">
  var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");
  document.write(xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' type='text/javascript'%3E%3C/script%3E"));
</script>
```

百度和Google网站地图，上面已经安装了，这是插入到底栏的代码：

    &nbsp;&nbsp;|&nbsp;&nbsp;<span><a href="/sitemap.xml">Google网站地图</a></span>
    &nbsp;&nbsp;|&nbsp;&nbsp;<span><a href="/baidusitemap.xml">百度网站地图<


[不蒜子](http://ibruce.info/2015/04/04/busuanzi/)统计代码：

    &nbsp;&nbsp;|&nbsp;&nbsp;本页点击 <span id="busuanzi_value_page_pv"></span> 次
    &nbsp;&nbsp;|&nbsp;&nbsp;本站总点击 <span id="busuanzi_value_site_pv"></span> 次
    &nbsp;&nbsp;|&nbsp;&nbsp;您是第 <span id="busuanzi_value_site_uv"></span> 位访客

    <script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">
    </script>


百度自动推送代码，在页面被访问时，页面URL将立即被推送给百度，可以增加百度收录：

    <script>
    (function(){
        var bp = document.createElement('script');
        bp.src = '//push.zhanzhang.baidu.com/push.js';
        var s = document.getElementsByTagName("script")[0];
        s.parentNode.insertBefore(bp, s);
    })();
    </script>


下面把这些代码全加入模板中，打开`\themes\next\layout\_partials\footer.swig`，修改后的完整文件内容为：

```
<div class="copyright" >
  {% set current = date(Date.now(), "YYYY") %}
  &copy; {% if theme.since and theme.since != current %} {{ theme.since }} - {% endif %}
  <span itemprop="copyrightYear">{{ current }}</span>
  <span class="with-love">
    <i class="icon-next-heart fa fa-heart"></i>
  </span>
  <span class="author" itemprop="copyrightHolder">{{ config.author }}

  &nbsp;&nbsp;|&nbsp;&nbsp;
  <script type="text/javascript">
    var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");
    document.write(xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' type='text/javascript'%3E%3C/script%3E"));
  </script>

  &nbsp;&nbsp;|&nbsp;&nbsp;<span><a href="/sitemap.xml">Google网站地图</a></span>
  &nbsp;&nbsp;|&nbsp;&nbsp;<span><a href="/baidusitemap.xml">百度网站地图</a></span>

  </span>
</div>

<div class="powered-by">
  {{ __('footer.powered', '<a class="theme-link" href="http://hexo.io">Hexo</a>') }}
</div>

<div class="theme-info">
  {{ __('footer.theme') }} -
  <a class="theme-link" href="https://github.com/iissnan/hexo-theme-next">
    NexT{% if theme.scheme %}.{{ theme.scheme }}{% endif %}
  </a>
</div>


&nbsp;&nbsp;|&nbsp;&nbsp;本站总点击 <span id="busuanzi_value_site_pv"></span> 次
&nbsp;&nbsp;|&nbsp;&nbsp;您是第 <span id="busuanzi_value_site_uv"></span> 位访客

<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">
</script>

<script>
(function(){
    var bp = document.createElement('script');
    bp.src = '//push.zhanzhang.baidu.com/push.js';
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(bp, s);
})();
</script>

{% block footer %}{% endblock %}
```

注意把上面的xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx换成你自己的站长统计代码

### 标题下添加「阅读量」


上一节中有一段JS代码：

    <script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js">
    </script>

现在要添加的阅读量统计也依赖这段代码，上面已经将它添加到页面中，这里可以直接调用它。

打开`/themes/next/layout/_macro/post.swig`，找到标签`<div class="post-meta"></div>`，在该标签内部合适的位置添加：

    {% if not is_index %}
      <span id="busuanzi_container_page_pv">&nbsp;&nbsp;|&nbsp;&nbsp;阅读量 <span id="busuanzi_value_page_pv"></span> 次</span>
    {% endif %}


### SEO优化

更改首页标题格式为「关键词-网站名称 - 网站描述」。打开`\themes\next\layout\index.swig`文件，找到这行代码：
    
    {% block title %} {{ config.title }} {% endblock %}

把它改成：    

    {% block title %}
      {{ theme.keywords }} - {{ config.title }} - {{ theme.description }}
    {% endblock %}

### 项目主页添加README

Github上博客的仓库主页空荡荡的，没有README。如果把README.md放入source文件夹，`hexo g`生成时会被解析成html文件，放到public文件夹，生成时又会自动删除。

解决方法很简单，在source目录下新建文件`README.mdown`，在里面写README即可。`hexo g`会把它复制到public文件夹，且不会被解析成html


## 五、Git相关

### 多PC同步

需要在公司和家里电脑上写博客，打包拷来拷去太麻烦。我使用Coding.net的免费私有仓库来同步hexo文件夹。

+ 1.删除根目录和\theme\next\下的.git文件夹。

+ 2.修改根目录下的.gitignore文件为：

    /.deploy_git
    /public

其实第一行留不留都一样，它是hexo默认的git配置文件夹，里面也有一个`.git`，使`/.deploy_git`里的文件无法被提交。`public`是每次`hexo g`新生成的静态博客文件，不需要同步。


### pull失败：Filename too long

在`git bash`里面，输入

    git config --global core.longpaths true

### 关闭换行符警告

部署时会出现如下警告

    warning: LF will be replaced by CRLF

LF为换行符，CR为回车符。Windows结束一行用CRLF，Mac和Linux用LF。Git默认在你提交时自动地把行结束符CRLF转换成LF，而在签出代码时把LF转换成CRLF。

要关闭警告，执行如下命令：

    git config --global core.autocrlf false

上述命令中：

    false表示取消自动转换功能。适合纯Windows
    true表示提交代码时把CRLF转换成LF，签出时LF转换成CRLF。适合多平台协作
    input表示提交时把CRLF转换成LF，签出时不转换。适合纯Linux或Mac

#### 补充：
Git还提供了一个换行符检查功能core.safecrlf，可以在提交时检查文件是否混用了不同风格的换行符。可以用同样的命令更改设置。
选项如下：

    false - 不做任何检查
    warn - 在提交时检查并警告
    true - 在提交时检查，如果发现混用则拒绝提交

建议使用最严格的 true 选项


## 六、博客部署的message

`\node_modules\hexo-deployer-git\lib\deployer.js`文件末尾找到这一句：
  
    Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }}.

改得个性化一点：  

    这个勤奋的家伙又更新了: {{ now(\'YYYY-MM-DD HH:mm:ss\') }}.