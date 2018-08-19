# Rust 程序设计语言（第二版） 简体中文版

[![Build Status](https://travis-ci.org/KaiserY/trpl-zh-cn.svg?branch=master)](https://travis-ci.org/KaiserY/trpl-zh-cn)

## 状态

还在施工中。大部分章节已经可以阅读。具体状态请参见官方 [projects](https://github.com/rust-lang/book/projects/1)，`Frozen` 之后的内容应该较为稳定。

每章翻译开头都带有官方链接和 commit hash，若发现与官方不一致，欢迎 Issue 或 PR :)

## 静态页面构建与文档撰写

![image](/vuepress_page.png)

### 构建

你可以将本mdbook构建成一系列静态html页面。这里我们采用[vuepress](https://vuepress.vuejs.org/zh/)打包出静态网页。在这之前，你需要安装[Nodejs](https://nodejs.org/zh-cn/)。

全局安装vuepress

``` bash
npm i -g vuepress 
```

cd到项目目录，然后开始构建。构建好的静态文档会出现在"./src/.vuepress/dist"中

```bash
vuepress build ./src
```

### 文档撰写

vuepress会启动一个本地服务器，并在浏览器对你保存的文档进行实时热更新。

```bash
vuepress dev ./src
```

## 社区资源

- Rust语言中文社区：[https://rust.cc/](https://rust.cc/)
- Rust 中文 Wiki：[https://wiki.rust-china.org/](https://wiki.rust-china.org/)
- Rust编程语言社区主群：303838735
- Rust 水群：253849562

## GitBook

本翻译主要采用 [mdBook](https://github.com/rust-lang-nursery/mdBook) 格式。同时支持 [GitBook](https://github.com/GitbookIO/gitbook)，但会缺失部分功能，如一些代码没有语法高亮。

本翻译加速查看站点[上海站点http://rustdoc.saigao.fun](http://rustdoc.saigao.fun)

[GitBook.com](https://www.gitbook.com/) 地址：[https://www.gitbook.com/book/kaisery/trpl-zh-cn/details](https://www.gitbook.com/book/kaisery/trpl-zh-cn/details)








## RCS
```
4.1
“Data Types” 部分涉及到的数据类型都是储存在栈上的并且当离开作用域时被移出栈，不过我们需要寻找一个储存在堆上的数据来探索 Rust 是如何知道该在何时清理数据的。

13.1
当闭包从环境中捕获一个值，闭包会在闭包体中储存这个值以供使用。这会使用内存并产生额外的开销，当执行不会捕获环境的更通用的代码场景中我们不希望有这些开销。因为函数从未允许捕获环境，定义和使用函数也就从不会有这些额外开销。

闭包可以通过三种方式捕获其环境，他们直接对应函数的三种获取参数的方式：获取所有权，可变借用和不可变借用。这三种捕获值的方式被编码为如下三个 Fn trait：

FnOnce 消费从周围作用域捕获的变量，闭包周围的作用域被称为其 环境，environment。为了消费捕获到的变量，闭包必须获取其所有权并在定义闭包时将其移动进闭包。其名称的 Once 部分代表了闭包不能多次获取相同变量的所有权的事实，所以它只能被调用一次。
FnMut 获取可变的借用值所以可以改变其环境
Fn 从其环境获取不可变的借用值
当创建一个闭包时，Rust 根据其如何使用环境中变量来推断我们希望如何引用环境。由于所有闭包都可以被调用至少一次，所以所有闭包都实现了 FnOnce 。那些并没有移动被捕获变量的所有权到闭包内的闭包也实现了 FnMut ，而不需要对被捕获的变量进行可变访问的闭包则也实现了 Fn 。 在示例 13-12 中，equal_to_x 闭包不可变的借用了 x（所以 equal_to_x 具有 Fn trait），因为闭包体只需要读取 x 的值。

如果你希望强制闭包获取其使用的环境值的所有权，可以在参数列表前使用 move 关键字。这个技巧在将闭包传递给新线程以便将数据移动到新线程中时最为实用。

15.2
这里使用 &m 调用 hello 函数，其为 MyBox<String> 值的引用。因为示例 15-12 中在 MyBox<T> 上实现了 Deref trait，Rust 可以通过 deref 调用将 &MyBox<String> 变为 &String。标准库中提供了 String 上的 Deref 实现，其会返回字符串 slice，这可以在 Deref 的 API 文档中看到。Rust 再次调用 deref 将 &String 变为 &str，这就符合 hello 函数的定义了。




```
