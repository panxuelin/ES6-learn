# ES6 编译成 ES5 的方法
这边介绍用 [Gulp](http://gulpjs.com/) 配合 [Babel 6](http://babeljs.io/) 来做。如果用其他工具配合 Babel 来做，可以见[这里](http://babeljs.io/docs/setup/)。

不知道 Gulp 是什么？请先查看[Gulp 入门指南](https://github.com/nimojs/gulp-book)。

## 安装依赖
安装 Gulp 上 Babel 的插件
```
npm install --save-dev gulp-babel
```

安装 Babel 上将 ES6 转换成 ES5 的插件

```
npm install --save-dev babel-preset-es2015
```

## Gulp 配置
gulpfile.js 的内容，形如
```
var gulp = require("gulp");
var babel = require("gulp-babel");

gulp.task("default", function () {
  return gulp.src("src/**/*.js")// ES6 源码存放的路径
    .pipe(babel())
    .pipe(gulp.dest("dist")); //转换成 ES5 存放的路径
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

## Babel 配置
在项目跟路径创建文件 `.babelrc`。内容为
```
{
  "presets": ["es2015"]
}
```

## 转换
命令行中执行
```
gulp
```