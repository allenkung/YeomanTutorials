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

现在手动更新`$scope.todos`，为它添加第四项，并保存

```
$scope.todos = ['Item 1', 'Item 2', 'Item 3', 'Item 4'];
```

通过即时刷新，你将会看到新的todo项目出现在列表里。

然后手动删掉第四项再观察列表的变化。

## 增加todo

让我们实现用户可以添加新的todo项到列表里

修改main.html，以前面html代码为基础，在`<h2>`元素和`<p>`元素之间添加'<form>'元素。
修改后的main.html如下所示：

```
<div class="container">
  <h2>My todos</h2>

  <!-- Todos input -->
  <form role="form" ng-submit="addTodo()">
    <div class="row">
      <div class="input-group">
        <input type="text" ng-model="todo" placeholder="What needs to be done?" class="form-control">
        <span class="input-group-btn">
            <input type="submit" class="btn btn-primary" value="Add">
        </span>
      </div>
    </div>
  </form>

  <!-- Todos list -->
    <p class="form-group" ng-repeat="todo in todos">
        <input type="text" ng-model="todo" class="form-control">
    </p>
</div>
```

这次在页面上添加了含有提交按钮的form表单。它使用了Angular的另一个指令[`ng-submit`](https://docs.angularjs.org/api/ng/directive/ngSubmit)，使用它可以进行下一步。
回到你的浏览器，现在界面将会看起来像这样：

![界面上出现了表单及提交按钮](http://yeoman.io/assets/img/codelab/image_16.c919.png)

如果你现在点击**Add**，什么也不会发生，下面让我们去改变它。

`ng-submit`为form表单的onsubmit事件绑定了Angular表达式。即使没有动作属性应用于form表单，它也会阻止浏览器的默认事件。
在我们的例子中增加的Angular表达式就是`addTodo()`。

下面这个`addTodo()`方法实现了向已经存在的todo列表数组里添加新的todo项并清空输入框。

```
$scope.addTodo = function () {
    $scope.todos.push($scope.todo);
    $scope.todo = '';
}
```
编辑main.js文件，向已经定义的`MainCtrl`控制器里面添加`addTodo()`函数。现在你的控制器看起来将会是像这样：

```
'use strict';

angular.module('mytodoApp')
  .controller('MainCtrl', function ($scope) {
    $scope.todos = ['Item 1', 'Item 2', 'Item 3'];
    $scope.addTodo = function () {
        $scope.todos.push($scope.todo);
        $scope.todo = '';
    };
  });
```

> 提示：如果在你的命令行界面里出现了错误信息，这可能是由于[jshint](http://jshint.com/)抛出的缩进警告。
它们只是警告，因此你的todo应用可以继续工作。然而最好还是看一下由jshint抛出的建议，从而改进你的代码，
使它们更加整洁可读。

再次到浏览器里看一下这个应用，在输入框里面输入新的todo项然后点击`Add`，它将会立马出现在todo列表里。

![添加之前](http://yeoman.io/assets/img/codelab/image_17.60e9.png)
![添加之后](http://yeoman.io/assets/img/codelab/image_18.518b.png)

> 提示：如果你多次添加空的内容或者是添加相同的内容的话，你的应用将会意外的停止工作:( 。
这可以作为你的一个有趣的练习，为`addTodo()`函数增加错误检查。

## 删除todo

让我们来为todo增加删除的功能。我们将要在每一项todo旁边增加一个新的删除按钮。

回到view模板(main.html)，直接在已经存在的`ng-repeat`里面添加一个按钮，
并且还要确保input字段和删除按钮美观的在一条线上，把段落标签的class从`form-group`改成`input-group`。

改之前：

```
<!-- Todos list -->
<p class="form-group" ng-repeat="todo in todos">
    <input type="text" ng-model="todo" class="form-control">
</p>
```

改之后：

```
<!-- Todos list -->
<p class="input-group" ng-repeat="todo in todos">
    <input type="text" ng-model="todo" class="form-control">
    <span class="input-group-btn">
        <button class="btn btn-danger" ng-click="removeTodo($index)" aria-label="Remove">X</button>
    </span>
</p>
```

然后看一下浏览器，你的todo应用已经变的高大上了。

![带删除按钮的todo app](http://yeoman.io/assets/img/codelab/image_19.365f.png)

我们来介绍一个新的Angular指令[`ng-click`](https://docs.angularjs.org/api/ng/directive/ngClick)，
`ng-click`允许你指定自定义行为，当一个元素被点击的时候。在这个例子里，我们指定`removeTodo()`，
并给这个函数传入一个`$index`参数。

由于`ng-repeat`指令的作用，参数`$index`将会成为每一个todo项的索引值。
例如，第一个todo项将会有一个索引值0并且`removeTodo()`函数将会传入0。相似的，剩余的todo项也会给`removeTodo()`函数传入相应的索引值。

让我们现在为我们的控制器添加删除todo项的逻辑。接下来的`removeTodo()`函数将会从todo列表里删除一个todo项通过JavaScript的`slice()`方法和传入的`$index`参数。

```
$scope.removeTodo = function ( index ) {
    $scope.todos.slice( index, 1 );
}
```

包含`removeTodo()`方法的新控制器(main.js)如下：

```
'use strict';

angular.module('mytodoApp')
    .controller('MainCtrl', function ($scope) {
        $scope.todos = ['Item 1', 'Item 2', 'Item 3'];
        $scope.addTodo = function () {
            $scope.todos.push($scope.todo);
            $scope.todo = '';
        };
        $scope.removeTodo = function (index) {
            $scope.todos.splice(index, 1);
        };
    });
```
回到浏览器，现在你就可以通过删除按钮删除todo项了，多么奇妙啊！

![删除前](http://yeoman.io/assets/img/codelab/image_20.6896.png)
![删除后](http://yeoman.io/assets/img/codelab/image_21.365f.png)

你可能已经发现了一个问题，现在我们无法存储我们的todo列表，每次刷新页面的时候，todo列表都会变回那些我们在main.js里面写入的默认项。
不要担心，我们将会在《[011-为todos应用添加本地存储功能](docs/011-为todos应用添加本地存储功能)》里面解决这个问题。
在它之前，我们先来看一下如何在[下一步](docs/008-使用Bower安装应用所需要的包.md)里面通过Bower安装依赖包。












