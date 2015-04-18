# 007-开始编写我们的AngularJS应用程序

在浏览器里看到的文件都可以在**app**文件夹里找到。本节中的操作都是假定你在app文件夹里编辑文件为基础的。
如果你对接下来所要做的没有把握的话，可以参考[完整的代码](http://yeoman.io/codelab.html#source-files)。

## 创建一个新模板来显示todo list

打开**views/main.html**

为了从一个干净的文件开始，我们需要删除main.html里面的所有内容，让后创建一个`div`，添加`container`类。

现在main.html的内容如下所示：

```
<div class="container">
</div>
```

打开**scripts/controllers/mian.js**

编辑Angular控制器样板，把`awesomeThings`列表替换为`todos`列表：

```
'use scrict';

angular.module('mytodoApp')
    .controller('MainCtrl', function ( $scope ) {
        $scope.todos = ['Item 1', 'Item 2', 'Item 3'];
    });
```

然后编辑我们的view(main.html)，使todos列表以html的input标签显示出来：

```
<div class="container">
    <h2>My todos</h2>
    <p class="form-group" ng-repeat="todo in todos">
        <input type="text" ng-model="todo" class="form-control">
    </p>
</div>
```
段落标签里面的[`ng-repeat`](https://docs.angularjs.org/api/ng/directive/ngRepeat)属性是一个Angular[指令](https://docs.angularjs.org/guide/directive)，它的作用是把集合中的每一项实例化成模板。


在这里，设想被添加`ng-repeat`属性的段落标签及其内容被变成了虚拟的橡皮图章，然后在todos数组里面遍历每一项，
最后Angular将会印出实例化后的HTML标签。


[`ng-model`](https://docs.angularjs.org/api/ng/directive/ngModel)属性是Angular的另外一个指令，
它将和`input`、`select`、`textarea`配合工作，并且通常会创建一个[双向数据绑定](https://docs.angularjs.org/guide/databinding)，
在我们的例子里，它将作用于每一个通过`ng-repeat`循环出来的`input`中的value属性。

让我们看一下`ng-repeat`和`ng-model`在浏览器里的表现。保存后，我们的应用看起来应该是这样：

![todo效果图](http://yeoman.io/assets/img/codelab/image_15.cb9d.png)

待续...








