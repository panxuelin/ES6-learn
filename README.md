# ES6 学习
## ES6 编译成 ES5 的方法
这边介绍用 Gulp 配合 Babel 6 来做。如果其他工具配合 Bable 来做，可以见[这里](http://babeljs.io/docs/setup/)

### 安装插件
安装 Gulp 上的 Babel 插件
```
npm install --save-dev gulp-babel
```

安装将 Babel 上将 ES6 转换成 ES5 的插件

```
npm install --save-dev babel-preset-es2015
```

### Gulp 配置
gulpfile.js 的内容，形如
```
var gulp = require("gulp");
var babel = require("gulp-babel");

gulp.task("default", function () {
  return gulp.src("src/**/*.js")
    .pipe(babel())
    .pipe(gulp.dest("dist"));
});
```

如果要生成 Soucemap， 则用 [gulp-sourcemaps](https://github.com/floridoo/gulp-sourcemaps)，形如：
```
var gulp = require("gulp");
var sourcemaps = require("gulp-sourcemaps");
var babel = require("gulp-babel");
var concat = require("gulp-concat");

gulp.task("default", function () {
  return gulp.src("src/**/*.js")
    .pipe(sourcemaps.init())
    .pipe(babel())
    .pipe(concat("all.js"))
    .pipe(sourcemaps.write("."))
    .pipe(gulp.dest("dist"));
});
```

### Babel 配置
在项目跟路径创建文件 `.babelrc`。内容为
```
{
  "presets": ["es2015"]
}
```

### 编译
```
gulp
```

## 资源
* [ECMAScript 6入门](http://es6.ruanyifeng.com/) 阮一峰老师写的。
* [深入浅出 ES6 的中文版](http://www.infoq.com/cn/es6-in-depth/) [原文](https://hacks.mozilla.org/category/es6-in-depth/)。
* [ES6 Katas](http://es6katas.org/) 通过写ES6的代码来学习ES6。修复失败的测试来学习这些知识。

## 工具
* [Babel](http://babeljs.io/) JavaScript 编译器：指定当前代码转换转换成什么代码。例如可以将 ES6 的代码编译成 ES5的。
