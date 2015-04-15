# 004-使用Yeoman为你的应用创建脚手架.md

对于“脚手架”这个词我们已经见过好多次了，但你可能还不太理解它的真正意思。在Yeoman里面，
脚手架意味着可以根据你的配置来为你的web应用创建文件。

在这个步骤里，你将会看到Yeoman如何以一种快速的方式来为AngularJS应用创建文件，
这里将包括类似于SASS及Twitter Bootstrap的一些第三方库。

## 创建项目文件夹

创建一个**mytodo**文件夹，这在以后也将会用到

```
$ mkdir mytodo && cd mytodo
```


我们通过构造器创建的项目文件也将会放在这个文件夹里

> 这里需要特别说明的是，AngularJS构造器将会根据你创建的文件夹动态的为应用创建命名空间。例如，
>**mytodo**意味着程序就是这样`angular.module('mytodoApp', [])`。
>所以要在确定不再对文件夹名**mytodo**做任何修改时再执行下一步。


## 通过Yeoman提供的菜单使用构造器

再次运行`yo`来查看你的构造器

```
$ yo
```

如果你已经安装了一些构造器，那么你就可以直接使用他们了。按上下方向键使**Run the Angular generator**高亮，
然后按回车键开始安装。

![yo命令截图](http://yeoman.io/assets/img/codelab/image_7.2c2a.png)

> 直接使用构造器
>
> 随着你对`yo`越来越熟悉，你可以直接通过交互式菜单创建构造器，比如`$ yo angular`

## 配置你的构造器

在初始化开发环境的时候，一些构造器会提供一些配置项来选择公共的开发库，从而自由定制你的应用。

AngularJS构造器提供了是否使用[SASS](http://sass-lang.com/)及[Twitter Bootstrap](http://getbootstrap.com/)的可选项，
在这个教程里，我们暂不使用SASS，但使用Bootstrap。输入`y`或`n`来进行选择。

![配置项截图](http://yeoman.io/assets/img/codelab/image_8.5a17.png)

下一步，将会提示你需要安装哪些Angular模块。

![angular模块选择截图](http://yeoman.io/assets/img/codelab/image_9.1f31.png)

Angular模块会以独立的js文件的形式提供有用的功能。例如，ngResource模块(angular-resource.js)会提供与RESTFUL服务的支持。
这些模块可以使用空格来决定是否选中并安装。

我们这里选择默然安装(也即是所有的模块都要保持选中状态)

然后按下回车，见证奇迹的时刻到了!

![angular构造器安装过程](http://yeoman.io/assets/img/codelab/image_10.5219.png)

Yeoman将会自动为你的应用创建脚手架、抓取依赖关系并将会为你的工作流提供一些有用的Grunt任务。
下一步我们将会在下一篇里面进行。