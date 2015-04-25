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