---
layout: post
title:  "在github上搭建jekyll要点"
date:   2016-06-02 10:50:35 +0800
categories: jekyll update
---

使用jekyll将markdown文件生成静态的html文件，并使用主题有序的进行布局，形成最终的博客页面。

特点

基于ruby
使用Markdown书写文章
无需数据库
可以使用GitHub Pages发布
安装Ruby环境

由于我的是在windows的操作，所以这里用rubyinstaller——http://rubyinstaller.org/downloads/，linux和mac的朋友就直接官网的ruby。

我使用的版本：rubyinstaller-2.2.3-x64.exe(17.1M)。安装很简单，这里不多描述，但要注意安装的路径。这里我的是D:\Ruby22。安装目录中不要有空格或中文，可能会引发未知的错误。

安装过程中若没有添加到环境变量，需要设置下环境变量：
windows下在计算机属性->系统高级设置->环境变量，PATH中追加：
D:\Ruby22\bin\;。注意不是覆盖！

命令行下输入ruby -v 检测是否安装成功：

D:\Ruby22>ruby -v
ruby 2.2.3p173 (2015-08-18 revision 51636) [x64-mingw32]
出现版本号就说明安装成功了，接下来就要安装jekyll。

安装jekyll

使用gem install jekyll命令安装jekyll。会安装在D:\Ruby22\lib\ruby\gems\2.0.0\gems\目录下，并把相应的依赖文件一同安装下来。

安装错误，提示：

ERROR:  While executing gem ... (Gem::RemoteFetcher::FetchError)
Errno::ECONNABORTED: An established connection was aborted by the software in your host machine. - SSL_connect (https://api.rubygems.org/specs.4.8.gz)
解决：
FetchError 明显是连接错误，使用国内的镜像源即可。
gem source -a https://ruby.taobao.org换个源，再安装。

或者直接改源配置文件：
在用户主目录下，Linux 是 ~，Windows 是 C:\Users\USERNAME （也可能是 Administrator 或 ProgramData） 下面有一个 .gemrc文件（若没有手动新建），写入下面内容试试：

:sources:
- https://ruby.taobao.org
:update_sources: true
然后重新gem install jekyll：

Fetching: ffi-1.9.10-x64-mingw32.gem (100%)
Successfully installed ffi-1.9.10-x64-mingw32
Fetching: rb-inotify-0.9.5.gem (100%)
Successfully installed rb-inotify-0.9.5
Fetching: rb-fsevent-0.9.7.gem (100%)
Successfully installed rb-fsevent-0.9.7
Fetching: listen-3.0.5.gem (100%)
Successfully installed listen-3.0.5
Fetching: jekyll-watch-1.3.0.gem (100%)
Successfully installed jekyll-watch-1.3.0
Fetching: sass-3.4.20.gem (100%)
Successfully installed sass-3.4.20
Fetching: jekyll-sass-converter-1.4.0.gem (100%)
Successfully installed jekyll-sass-converter-1.4.0
Fetching: rouge-1.10.1.gem (100%)
Successfully installed rouge-1.10.1
Fetching: colorator-0.1.gem (100%)
Successfully installed colorator-0.1
Fetching: safe_yaml-1.0.4.gem (100%)
Successfully installed safe_yaml-1.0.4
Fetching: mercenary-0.3.5.gem (100%)
Successfully installed mercenary-0.3.5
Fetching: kramdown-1.9.0.gem (100%)
Successfully installed kramdown-1.9.0
Fetching: liquid-3.0.6.gem (100%)
Successfully installed liquid-3.0.6
Fetching: jekyll-3.0.1.gem (100%)
Successfully installed jekyll-3.0.1
Parsing documentation for ffi-1.9.10-x64-mingw32
Installing ri documentation for ffi-1.9.10-x64-mingw32
Parsing documentation for rb-inotify-0.9.5
Installing ri documentation for rb-inotify-0.9.5
Parsing documentation for rb-fsevent-0.9.7
Installing ri documentation for rb-fsevent-0.9.7
Parsing documentation for listen-3.0.5
Installing ri documentation for listen-3.0.5
Parsing documentation for jekyll-watch-1.3.0
Installing ri documentation for jekyll-watch-1.3.0
Parsing documentation for sass-3.4.20
Installing ri documentation for sass-3.4.20
Parsing documentation for jekyll-sass-converter-1.4.0
Installing ri documentation for jekyll-sass-converter-1.4.0
Parsing documentation for rouge-1.10.1
Installing ri documentation for rouge-1.10.1
Parsing documentation for colorator-0.1
Installing ri documentation for colorator-0.1
Parsing documentation for safe_yaml-1.0.4
Installing ri documentation for safe_yaml-1.0.4
Parsing documentation for mercenary-0.3.5
Installing ri documentation for mercenary-0.3.5
Parsing documentation for kramdown-1.9.0
Installing ri documentation for kramdown-1.9.0
Parsing documentation for liquid-3.0.6
Installing ri documentation for liquid-3.0.6
Parsing documentation for jekyll-3.0.1
Installing ri documentation for jekyll-3.0.1
Done installing documentation for ffi, rb-inotify, rb-fsevent, listen, jekyll-watch, sass, jekyll-sass-converter, rouge, colorator, safe_yaml, mercenary, kramdown, liquid, jekyll after 23 seconds
14 gems installed
如果需要安装指定版本，可以使用

gem install jekyll -v 3.0.1
检测是否安装成功：

$ jekyll -v
jekyll 3.0.1
ok!

如需卸载使用：

 gem uninstall jekyll
新建博客

执行jekyll new xxx会在当前的目录下创建一个xxx的目录，里面就是网站的所有文件了：

jekyll new myblog
之后我们在生成的博客文件夹内执行jekyll serve --watch（不加--watch则不会检测文件夹内的变化，即修改后需要重新启动jekyll），即可以通过http://localhost:4000看到默认的页面。

cd myblog
jekyll serve --watch
发布文章

jekyll的所有文章都放在_posts目录下，分类的话暂时没涉及到，有兴趣的朋友可以先去看看。只需要在此目录内新建一个文件，后缀名为markdown即可。
我们新建一个文件，名为：first-post.markdown，内容如下：

---  
layout: post  
title: "First post"  
date: 2016-1-2 21:55:48
categories: mypost  
---  
  
>> Here is my first jekyll post  
  
+ Just for test  
* Just for Test  

I'm trying to write some code 
注意，此文件上的日期跟实际页面显示的日期没关系，页面的日期由内容中的date来决定。至于其他值，肯定也有相应的用处，大家有兴趣就慢慢研究。

就这样，我们的第一篇文章也创建完成了。

jekyll目录结构分析

生成的目录结构如下：
1、文件夹_layouts：用于存放模板的文件夹，里面有两个模板，default.html和post.html
2、文件夹_posts：用于存放博客文章的文件夹
3、文件夹css：存放博客所用css的文件夹
4、_site：jekyll自动生成的目录，为静态的页面
5、_coinfig.yml：jekyll的配置文件，里面可以定义相当多的配置参数，具体配置参数可以参照其官网

根据实际需要，可能还需要创建如下文件或文件夹：
1、 _includes:用于存放一些固定的HTML代码段，文件为.html格式，可以在模板中通过liquid标签引入，常用来在各个模板中复用如 导航条、标签栏、侧边栏 之类的在每个页面上都一样不变的内容，需要注意的是，这个代码段也可以是未被编译的，也就是说也可以使用liquid标签放在这些代码段中
2、 image和js等自定义文件夹：用来存放一些需要的资源文件，如图片或者javascript文件，可以任意命名
3、 CNAME文件：用来在github上做域名绑定的，将在后面介绍
4、 favicon.ico：网站的小图标

更换主题

更换主题比较简单，直接将主题文件作为一个应用即可。没有专门的主题目录。也就是说下载了主题，相当于已经jekyll new my-awesome-site了。jekyll主题站：http://jekyllthemes.org/。这里列出部分主题：

1、Huxpro/huxpro.github.io
https://github.com/Huxpro/huxpro.github.io
2、Phlow/feeling-responsive
https://github.com/Phlow/feeling-responsive

可能出现的问题
1、提示分页错误

 Deprecation: You appear to have pagination turned on, but you haven't included the `jekyll-paginate` gemguration file.
解决：只需要在_config.yml里面加一句: gems: [jekyll-paginate]就ok了。

permalink: pretty
gems: [jekyll-paginate]
paginate: 10
提交至github pages

新建xx.github.io仓库，将_site下文件提交至仓库。原理是在本地，jekyll将markdown转化成html静态文件。

注意：仓库名必须是  你的github用户.github.id    提交时只需要将_site目录下的文件提交上去就行

命令概览

gem install jekyll #使用ruby的gem安装器安装jekyll
gem uninstall jekyll #卸载jekyll
jekyll new my-awesome-site #新建应用
jekyll serve #启动应用(需进入应用目录)
jekyll serve --watch #启动应用
调试

在博客文件夹下，在命令行中输入jekyll build --trace就可以将所有文章文件根据其模板进行编译，生成结果，放在根目录下的_site中，
参考

1、Jekyll • 简单的博客、静态网站工具
http://jekyll.bootcss.com/
2、jekyll博客搭建 - 编程人生 - ITeye技术网站
http://cxshun.iteye.com/blog/1924153
3、jekyll安装与应用 - BeginMan - 博客园
http://www.cnblogs.com/BeginMan/p/3549241.html
4、使用Jekyll在Github上搭建个人博客（博客编写） - 说学逗唱 - SegmentFault
http://segmentfault.com/a/1190000000406013
5、使用 GitHub, Jekyll 打造自己的免费独立博客
http://www.360doc.com/content/14/0415/07/13232598_369075184.shtml


