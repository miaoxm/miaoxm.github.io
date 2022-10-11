## 写在最前

> 关于docsify的使用
>
> 会了markdown的语法之后，其实就掌握了大多数的使用。这个我的个人拙见。也可能并不是“我以为就是我以为的”。
>
> 剩下的就是docsify的的一些规定写法。既然用人家的，就遵守人家的约定。即：约定大约配置。

## 关于跳转

> 关于封面的Getting Started的跳转

在封面文件`_coverpage.md`中，关于`Getting Started`的跳转，有下面几种实现：

- 跳转到指定文档

  > 跳转到根目录下的home.md文档
  >
  > `[Getting Started](/home)`
  >
  > 跳转到其他目录下的home.md文档
  >
  > `[Getting Started](/test/home)`

- 跳转到默认(`README.md`)文档

  > `[Getting Started](#About)`
  >
  > 这表示跳转到根目录下的`README.md`文档下的`About`标题
  >
  > 或者这样直接跳转到默认文档下
  >
  > `[Getting Startedd](/README)`

## 关于侧边栏目录定义

目录定义

> `* <p>入门</p>` # 该行表示第一级目录，并且不设置任何跳转，就是原原本本的文字
>
> `** [快速开始](/zh-cn/quickstart)` # 该行表示第二级目录，设置跳转为`zh-cn`目录下的`quickstart.md`文档

官方文档中的`源文档`中是这样定义的

> `- Getting started`
>
> ​	`- [Quick start](quickstart.md)`
>
> ​	`- [Writing more pages](more-pages.md)`
>
> ​	`- [Custom navbar](custom-navbar.md)` 
>
> ​	`- [Cover page](cover.md)`
>
> 使用的是markdown的语法

