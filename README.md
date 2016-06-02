# liuxingroom.github.io
来访问我的博客吧
通过搭建自己的静态博客使我熟悉了一些ruby的操作
另外在这个过程中值得注意的是 安装jekyll的操作，因为国外的镜像文件容易获取，即使获取到了在以后的运行中也会出现bug，
所以建议大家用淘宝的镜像文件连接 https://ruby.taobao.org 其实这个连接也不怎么好原本我想用Octopress来制作静态博客但是由于环境搭建的
时候执行了gem install hundler 和hundler install 操作是总是报错，原因是得用http://ruby.taobao.org 该链接下的镜像文件 而淘宝又停止了
该链接下的镜像文件的使用所以真的好坑
总结一下操作
1. ruby -v  //查看ruby的版本，如果出现表示ruby已经安装
2. ruby dk.rb init //在Devkit目录下执行
3. ruby dk.rb install //在DevKit目录下执行
4. gem install jekyll //jieyll安装  gem uninstall jekyll  //jekyll卸载
5. jekyll new myblog  //在DevKit目录下创建博客
6. jekyll serve --watch  //不加--watch则不会检测文件夹内的变化，即修改后需要重新启动jekyll(其实相当于将博客发布到服务器上)
7. http://localhost:4000 //然后就可以通过该链接访问到博客
8. jekyll build --trace  //在博客文件夹下输入该命令就可以将所有文章文件根据其模板进行编译，生成结果，放在根目录下的_site中
博客目录分析：
生成的目录结构如下：
1、文件夹_layouts：用于存放模板的文件夹，里面有两个模板，default.html和post.html
2、文件夹_posts：用于存放博客文章的文件夹
3、文件夹css：存放博客所用css的文件夹
4、_site：jekyll自动生成的目录，为静态的页面
5、_coinfig.yml：jekyll的配置文件，里面可以定义相当多的配置参数，具体配置参数可以参照其官网
注意：将博客发布到github上：是将_site文件夹下的所有文件push到github上，且该仓库的的名字为  github账号名.github.io
