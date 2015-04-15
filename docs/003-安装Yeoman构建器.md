# 003-安装Yeoman构造器

在传统的前端开发工作流中，你需要花费很多时间为你的web应用搭建模板代码，下载各种依赖，
并且还要手动的创建文件夹结构。现在Yeoman可以把我们从中解脱出来了，那么我们就为AngularJS项目安装一个构造器吧。

## 安装AngularJS构造器

你可以通过[npm](https://www.npmjs.com/)命令安装Yeoman构造器，现在已经有超过1000+个构造器可供使用，它们很多都是由开源社区写的。

安装[generator-angular](https://www.npmjs.com/package/generator-angular)的命令如下：

```
$ npm install --global generator-angular@0.9.2
```

然后就开始安装构造器所需要的Node模块了。`@0.9.2`意思是使用指定版本的构造器。

> 出错了?
> 如果遇到权限问题时，可以使用sudo来安装，像这样：
> ```$ sudo npm install --global generator-angular@0.9.2```

安装完成后，可以通过Yeoman提供的交互式菜单搜索构造器，运行`yo`命令然后选择`Install a generator`来搜索已经发布的构造器。

![菜单图](http://yeoman.io/assets/img/codelab/image_4.168c.png)