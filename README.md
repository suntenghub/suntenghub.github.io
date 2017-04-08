
通过博客平台 [Hexo](https://hexo.io) 编辑发布文档，静态页面托管在 [GitHub Pages](https://pages.github.com)

## GitHub Pages 创建
### 创建代码仓库
GitHub上新建个人网站项目，在页面右上角点击 **+** 加号按钮，点击 **New repository**。

仓库的名称需要按照GitHub个人网站项目的规定来写，**YOUR-GITHUB-USERNAME** 是GitHub用户名

> **YOUR-GITHUB-USERNAME.github.io**

仓库中创建相关web文件后，就可以通过 [http://YOUR-GITHUB-USERNAME.github.io](https://suntenghub.github.io)来访问此页面了。

### 自定义域名
通过配置以后，可以使用自己的域名来访问。

点击我们的个人网站项目设置选项卡，滚动到下面，就会发现一个自定义域名卡片 `Custom domain`
![Custom domain](http://img.blog.csdn.net/20160814135316742)

输入已购买的域名，域名服务配置见[下文](##域名设置)，然后点击保存。
保存完成，会自动在仓库根目录下创建文件 `CNAME`,其中保存配置的域名

```
blog.sunteng.pub
```

## Hexo 的安装与配置

Hexo 是一个简单地、轻量地、基于 [Node](https://nodejs.org/en/) 的一个静态博客框架，先安装 Node 环境及其 NPM 包管理工具

### Hero 安装

Node 安装好后，安装 Hexo，要用全局安装，加-g参数。

``` bash
$ npm install -g hexo
```

### 创建项目

#### hexo初始化
创建一个文件夹，如：Blog，cd到Blog里执行初始化命令：

``` bash
$ hexo init
```
#### 打包生成静态页面
执行如下命令，`／source` 文件夹中的Markdown 和 HTML 文件会被解析并放到 `／public` 文件夹，而其他文件会被拷贝过去

``` bash
$ hexo generate
```
#### 本地启动
启动本地服务，进行文章预览调试，命令：

``` bash
$ hexo server
```
浏览器输入[http://localhost:4000]，可以看到自己的Blog

#### 部署托管页面
部署前需要修改_config.yml文件，来建立与托管平台关联
按以下修改文件中`deploy`部分，注意 **：后面要有空格**

``` bash
deploy:
  type: git
  repository: https://github.com/suntenghub/suntenghub.github.io.git
  branch: master
```
repository为静态页面托管地址，此处设为GitHub Pages项目的仓库
如果部署到git代码仓库，需先安装git部署包

``` bash
$ npm install hexo-deployer-git --save
```
最后执行部署

``` bash
$ hexo clean
$ hexo generate
$ hexo deploy
```
完成后可以在浏览器中直接访问[http://suntenghub.github.io](http://suntenghub.github.io)即可看到部署的blog页面

### 新建文章
Hexo的目录结构

![hexo-file-struct](http://img2.tuicool.com/yIVFfaZ.png)

> * `scaffolds` ：模板文件夹，新建文章时，Hexo 会根据 scaffold 来建立文件。Hexo 有三种默认布局： post 、 page 和 draft ，它们分别对应不同的路径。新建文件的默认布局是 post ，可以在配置文件中更改布局。
> * `source` ：资源文件夹是存放用户资源的地方,用 post 布局生成的文件会被保存到 `source/_post` 文件夹。
> * `themes` ：主题文件夹。Hexo 会根据主题来生成静态页面。`themes/landscape` 默认的皮肤文件夹
> * `_config.yml` ：全局的配置文件，每次更改要重启服务。

以 MarkDown 格式编写新的文章

``` bash
$ hexo new "My New Post" #新建文章
$ hexo new page "pageName" #新建页面
```

## 域名设置
### 域名购买
可以从域名提供商注册购买

* [万网](https://wanwang.aliyun.com)
* [新网](http://www.xinnet.com)
* [GoDaddy](https://sg.godaddy.com/zh/)

### 域名绑定
注册好的域名，需要在域名服务控制台上绑定到服务器上才可访问

* 记录类型“**A**”，绑定服务器IP地址
* 记录类型“**CNAME**”，绑定原服务器域名

无需添加端口号

## 常见问题
### Hexo部署自动删除CNAME
自己的独立域名需要用CNAME连接到github pages，在Hexo部署时会清除github仓库中的`CNAME`文件

将需要上传至github仓库的内容放在Hexo项目根目录的`/source`文件夹，例如CNAME、favicon.ico、images等。打包成静态文件时会自动复制到`/public`文件夹中一同被部署到github仓库


