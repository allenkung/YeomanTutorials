# 009-使用Karma和Jasmine来进行测试

[Karma](http://karma-runner.github.io/)是一个JavaScript测试框架。Angular构造器自带了两个测试框架，
分别为[ngScenario](https://code.angularjs.org/1.2.16/docs/guide/e2e-testing)和[Jasmine](http://jasmine.github.io/)。


## 运行单元测试

我们回到命令行并用`Ctrl+C`结束Grunt server进程。在Gruntfile.js配置文件里面，
已经有了grunt任务来运行测试。可以通过下面命令运行：

```
$ grunt test
```

当你运行`grunt test`的时候，命令行里面会出现一些警告，不要担心，目前报错的原因有两个，
下面让我们修复它。

## 更新Karma配置

首先，我们需要检查Karma的配置，确定新安装的Bower依赖是否更新进去。

打开**karma.conf.js**，现在`files`数组看起来像这样：

```
files: [
    // bower:js
    'bower_components/jquery/dist/jquery.js',
    'bower_components/angular/angular.js',
    'bower_components/bootstrap/dist/js/bootstrap.js',
    'bower_components/angular-animate/angular-animate.js',
    'bower_components/angular-cookies/angular-cookies.js',
    'bower_components/angular-resource/angular-resource.js',
    'bower_components/angular-route/angular-route.js',
    'bower_components/angular-sanitize/angular-sanitize.js',
    'bower_components/angular-touch/angular-touch.js',
    'bower_components/jquery-ui/jquery-ui.js',
    'bower_components/angular-ui-sortable/sortable.js',
    'bower_components/angular-mocks/angular-mocks.js',
    // endbower
    'app/scripts/**/*.js',
    'test/mock/**/*.js',
    'test/spec/**/*.js'
],
```

Bower已经读取了新添加的依赖`bowercomponents/jquery-ui/jquery-ui.js`和`bowercomponents/angular-touch/angular-touch.js`
并且自动把它们添加到了karma.conf.js文件里面。

## 更新单元测试

你将会在**test**文件夹里找到单元测试脚手架，然后打开**test/spec/controllers/main.js**文件，
这是Angular的MainCtrl控制器的单元测试，我们需要做一下修改。

文件里边的内容还是涉及到`awesomeThings`的，因此我们把下面这些删掉：

```
it('should attach a list of awesomeThings to the scope', function () {
    expect(scope.awesomeThings.length).toBe(3);
});
```

然后写入下面的内容：

```
it('should have no items to start', function () {
    expect(scope.todos.length).toBe(0);
});
```

打开**scripts/controllers/main.js**文件，去掉我们早些时候在`$scope.todos`声明里面添加的的3项：

```
$scope.todos = [];
```

重新运行`grunt test`，现在我们可以看到测试通过了：

![http://yeoman.io/assets/img/codelab/image_33.2ea1.png](http://yeoman.io/assets/img/codelab/image_33.2ea1.png)

## 添加更多的单元测试

上面的测试仅仅覆盖了应用的一部分功能，下面我们再添加更多的测试来测试增加和删除列表项：

```
it('should add items to the list', function () {
    scope.todo = 'Test 1';
    scope.addTodo();
    expect(scope.todos.length).toBe(1);
});

it('should add then remove an item from the list', function () {
    scope.todo = 'Test 1';
    scope.addTodo();
    scope.removeTodo(0);
    expect(scope.todos.length).toBe(0);
});
```

现在你的MainCtrl测试脚本(test/spec/controllers/main.js)整体看起来像这样：

```
'use strict';

describe('Controller: MainCtrl', function () {

  // load the controller's module
  beforeEach(module('mytodoApp'));

  var MainCtrl,
    scope;

  // Initialize the controller and a mock scope
  beforeEach(inject(function ($controller, $rootScope) {
    scope = $rootScope.$new();
    MainCtrl = $controller('MainCtrl', {
      $scope: scope
    });
  }));

  it('should have no items to start', function () {
    expect(scope.todos.length).toBe(0);
  });

  it('should add items to the list', function () {
    scope.todo = 'Test 1';
    scope.addTodo();
    expect(scope.todos.length).toBe(1);
  });

  it('should add then remove an item from the list', function () {
    scope.todo = 'Test 1';
    scope.addTodo();
    scope.removeTodo(0);
    expect(scope.todos.length).toBe(0);
  });

});
```

重新运行测试命令，我们将会看到4个测试被执行并且全部通过：

![http://yeoman.io/assets/img/codelab/image_34.b030.png](http://yeoman.io/assets/img/codelab/image_34.b030.png)

太不可思议了!

当更多的开发者加入你的团队时你的应用将会越来越复杂，因此编写单元测试可以很方便的捕获错误。
Yeoman的脚手架特性使编写单元测试更加的容易，因此没有理由自己不编写测试。




