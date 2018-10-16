---
title: "搭建个人hugo网站"
date: 2018-10-10T17:11:55+08:00
draft: false

---
>**准备工作**

>>1. 前往[hugo二进制文件下载](https://github.com/gohugoio/hugo/releases  "Optional Title Here")
下载对应的hugo二进制文件（hugo或者hugo.exe） 
 本人在windows下安装的hugo_0.24.1_Windows-64bit.zip
 
>>2. 解压到指定文件夹，将hugo.exe所在的目录的路径配置到环境变量path中

>>3. 配置完成之后，使用cmd或者其它命令行操作工具，输入hugo version查看是否有版本信息
<center>
 ![hugo版本](/createHogo/hugo-v.png "hugo版本")
</center>

>**创建博客**

>>1. 选择一个目录，使用命令行工具输入hugo new site blog，创建名文件夹名为 blog的网站：
<center>
![创建网站](/createHogo/create-site.jpg)
<center/>

>>目录说明

    |- archetypes ：存放default.md，头文件格式

    |- content ：content目录存放博客文章（.markdown/.md文件）

    |- data ：存放自定义模版，导入的toml文件（或json，yaml）

    |- layouts ：layouts目录存放的是网站的模板文件

    |- static ：static目录存放js/css/img等静态资源

    |- config.toml ：config.toml是网站的配置文件



>>2. 使用hugo new about.md和hugo new blog/first.md 创建两个文章文件,他们分别存放在content和content/blog目录下
<center>
![创建文章](/createHogo/create-md.jpg)
</center>

>>3. 创建完成之后，需要下载主题来渲染显示网站，前往[皮肤网站](https://themes.gohugo.io)选择自己喜欢的主题皮肤，以AllinOne为例

>>>1. 进入到theme目录下，将主题clone下来
   <center>
   ![主题](/createHogo/theme.jpg)
   <center>
   根据主题说明，将themes\AllinOne\exampleSite的config.toml拷贝到根目录下，覆盖该目录的config.toml文件

>>>2. 使用hugo server --theme=AllinOne --buildDrafts --watch 启动，它会默认监听1313端口，如果被占用会分配别的端口
--theme表示使用什么皮肤渲染你的网站，--watch则是会监听你的修改自动刷新浏览器
<center>
![启动](/createHogo/startHogu.jpg)
</center>
网站截图
<center>
![主页](/createHogo/home.jpg)
</center>

>>>3. 修改根目录下的config.toml文件，指定访问地址
<center>
![修改config](/createHogo/configToml.jpg)
</center>
此时点击blog和about按钮就可以看见文章了
<center>
![blog](/createHogo/blog.jpg)
</center>

>**部署到GitHub**

>>1. 在github中创建一个仓库，取名为 你的用户名.github.io

>>2. 切到根目录 输入 hugo --theme=你的主题 --baseUrl="http://你的用户名.github.io/" 别掉了最后那个斜杠/,否则样式会出不来
（注意，以上命令并不会生成草稿页面，如果未生成任何文章，请去掉文章头部的 draft=true 再重新生成。）

>>3. 所有静态页面都会生成到 public 目录，将pubilc目录里所有文件 push 到刚创建的Repository的 master 分支（官方文档说明）
  ````
  $ cd public
  $ git init
  $ git remote add origin https://github.com/coderzh/coderzh.github.io.git
  $ git add -A
  $ git commit -m "first commit"
  $ git push -u origin master
  ````
>>4. 最后访问 https://xxx.github.io ,https://后面的是你刚创建的那个仓库名字
效果如下
