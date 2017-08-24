## 前言

> this是js种非常复杂的机制之一，是一个非常特殊的关键字，被自动定义在所有函数的作用域中。

## 1.1 为什么要使用this

> this到底用在哪里？是否真的值得我们花费很多时间去学习它？接下来我们先搞清楚它**到底用在哪里**


``` javascript
function identify () {
  return this.name.toUpperCase()
}

function speak () {
  let greeting = `Hello, i'm ${identify.call(this)}`
  console.log(greeting)
}

let me = {
  name: 'Kyle'
}

let you = {
  name: 'Reader'
}

identify.call( me ); // KYLE
identify.call( you ); // READER
speak.call( me ); // Hello, 我是 KYLE
speak.call( you ); // Hello, 我是 READER

```
这段代码可以在不同的上下文对象（me和you）中使用identify和speak函数。不用针对每个对象编写不同版本的函数。

当然为了实现同样的效果，完全可以在两个函数中显示地传入上下文。


``` javascript
function identify (context) {
  return context.name.toUpperCase()
}

function speak (context) {
  let greeting = "Hello, I'm " + identify( context )console.log( greeting )
}

identify( you ) // READER
speak( me ) //hello, 我是 KYLE

```

但是this提供了一种更加优雅的方式来隐士传递一个对象的引用，因此**可以将api设计得更加简洁并且易用。**

