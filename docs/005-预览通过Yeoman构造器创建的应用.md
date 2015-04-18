# 005-预览通过Yeoman构造器创建的应用

打开你的**mytodo**文件夹看一下实际搭建的项目，看起来像这样：

![文件结构预览](http://yeoman.io/assets/img/codelab/image_11.820e.png)

在mytodo文件夹里，主要有这些：

**app**：我们的web应用的根目录

+ **index.html**：我们Angular应用的基础html文件

+ **404.html**，**favicon.ico**以及**robots.txt**：通用的项目文件，现在你不需要自己创建了

+ **scripts**：我们自己的JS文件

    + **app.js**：Angular应用的主要代码

    + **controllers**：Angular控制器

+ **styles**：一些css文件

+ **views**：用于放置Angular模板

**bower_components**，**bower.json**：我们的JS依赖以及应用依赖，通过Bower安装

**Gruntfile.js**，**package.json**以及**node_modules**：Grunt配置文件(Gruntfile.js)、依赖声明文件(package.json)以及安装后的依赖包(node_modules)

**test**：搭建了测试运行器以及我们项目的单元测试，包括了我们控制器的样板测试