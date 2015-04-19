# 008-使用Bower安装应用所需要的包

![http://yeoman.io/assets/img/yeoman-005.caff.png](http://yeoman.io/assets/img/yeoman-005.caff.png)

让我们给todo列表添加一些规则使它们可以排序。因此我们将要使用Bower安装[AngularUI Sortable模块](https://github.com/angular-ui/ui-sortable)，
这是AngularJS的指令之一。

## 列出当前已经安装的包

我们可以通过在项目根目录里面执行如下命令来检查我们已经安装了哪些包：

```
$ bower list
```

![http://yeoman.io/assets/img/codelab/image_22.3761.png](http://yeoman.io/assets/img/codelab/image_22.3761.png)

你应该可以看到已经安装的包有`angular-cookie`、`angular-resources`、`angular-route`等。还记得这是在我们在安装构造器时选择的吗？

## 搜索包

为了验证AngularUI包是否可用，使用Bower搜索`angular-ui-sortable`:

```
$ bower search angular-ui-sortable
```

出现了有关`angular-ui-sortable`的一条结果，同时还提示我们安装[jQuery UI](http://jqueryui.com/)，
我们已经安装过jQuery了，下面我们只需要安装jQuery UI，包名叫做jquery-ui。

## 安装包

使用Bower安装`angular-ui-sortable`和`jquery-ui`：

```
$ bower install --save angular-ui-sortable
```

```
$ bower install --save jquery-ui
```

`--save`参数可以更新bower.json的依赖项，把angular-ui-sortable及jquery-ui写进去，
这样就不用手动更新bower.json文件了。

> 一次需要安装多个Bower包时，可以执行类似下面的这条命令：
```
$ bower install --save angular-ui-sortable jquery-ui
```

![http://yeoman.io/assets/img/codelab/image_24.71c1.png](http://yeoman.io/assets/img/codelab/image_24.71c1.png)

## 确认安装成功

打开**bower_components**文件夹看看有什么变化。你将会看到在里面出现了`jquery-ui`和`angualr-ui-sortable`文件夹。

![http://yeoman.io/assets/img/codelab/image_25.8256.png](http://yeoman.io/assets/img/codelab/image_25.8256.png)

## 使todos列表可以调整排序

引入了新的安装依赖，我们必须在index.html文件里添加相应的依赖文件。你可能需要手动地添加angualr-ui-sortable模块和jquery-ui模块的脚本文件，
不过这些Yeoman都可以帮你自动完成。

通过`Ctrl+C`组合键退出你的命令行进程。

然后再次运行`grunt serve`。

你将会看到index.html文件下面的脚本块里面自动添加了`jquery-ui/ui/jquery-ui.js`和`angular-ui-sortable/sortable.js`：

```
<!-- build:js scripts/vendor.js -->
<!-- bower:js -->
<script src="bower_components/jquery/dist/jquery.js"></script>
<script src="bower_components/angular/angular.js"></script>
<script src="bower_components/bootstrap/dist/js/bootstrap.js"></script>
<script src="bower_components/angular-resource/angular-resource.js"></script>
<script src="bower_components/angular-cookies/angular-cookies.js"></script>
<script src="bower_components/angular-sanitize/angular-sanitize.js"></script>
<script src="bower_components/angular-animate/angular-animate.js"></script>
<script src="bower_components/angular-touch/angular-touch.js"></script>
<script src="bower_components/angular-route/angular-route.js"></script>
<script src="bower_components/jquery-ui/jquery-ui.js"></script>
<script src="bower_components/angular-ui-sortable/sortable.js"></script>
<!-- endbower -->
<!-- endbuild -->
```

为了使用Sortable模块，我们必须把它添加到app.js的模块定义里面，它现在看起来像这样：

```
angular
  .module('mytodoApp', [
    'ngAnimate',
    'ngCookies',
    'ngResource',
    'ngRoute',
    'ngSanitize',
    'ngTouch'
  ])
```

在`ngTouch`后面添加上`ui.sortable`依赖：

```
angular
  .module('mytodoApp', [
    'ngAnimate',
    'ngCookies',
    'ngResource',
    'ngRoute',
    'ngSanitize',
    'ngTouch',
    'ui.sortable'
  ])
```

最后，我们在包含`ng-repeat`的段落外面添加一个div，并且加上`ui-sortable`指令：

```
<!-- Todos list -->
<div ui-sortable ng-model="todos">
    <p class="input-group" ng-repeat="todo in todos">
```

然后我们在段落标签里添加css样式，以方便我们移动todo列表：

```
<p class="input-group" ng-repeat="todo in todos" style="padding:5px 10px; cursor: move;">
```

完整的代码如下：

```
<!-- Todos list -->
<div ui-sortable ng-model="todos">
    <p class="input-group" ng-repeat="todo in todos" style="padding:5px 10px; cursor: move;">
        <input type="text" ng-model="todo" class="form-control">
        <span class="input-group-btn">
            <button class="btn btn-danger" ng-click="removeTodo($index)" aria-label="Remove">X</button>
        </span>
    </p>
</div>
```

回到浏览器，我们就可以对todo列表调整顺序了：

![http://yeoman.io/assets/img/codelab/image_26.8645.png](http://yeoman.io/assets/img/codelab/image_26.8645.png)
![http://yeoman.io/assets/img/codelab/image_27.cdcd.png](http://yeoman.io/assets/img/codelab/image_27.cdcd.png)

回过来想想，我们使用Yeoman很快就创建了一个高大上的应用。现在你是否想到用另外一种方式去做前端开发呢？

























