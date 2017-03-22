# JS-closure 关于js闭包
## 1.闭包的定义<br/>  
* 当一个函数可以记住并访问所在的作用域（全局作用域除外），并在定义该函数的作用域之外执行时，该函数就称之为一个闭包。
* 简单的说，假设函数A在函数B的内部进行定义了，并在函数B的作用域之外执行（不管是上层作用域，下层作用域，还是其他作用域），那么A就是一个闭包。
## 2.通过例子理解闭包
```
var fn=null;
function foo(){
  var a=2;
  function innerFoo(){
    console.log(a);
  }
  fn=innerFoo;  //将innerFoo的引用，赋值给全局变量中的fn
}
function bar(){
  fn(); //此处保留的innerFoo的引用
}
foo();  //foo()执行完毕之后，按照常理，其执行环境生命周期会结束，所占内存会被垃圾收集器释放。
但是通过fn=innerFoo,函数innerFoo的引用被保留了下来，复制给了全局变量fn。
bar();  //此处控制台输出2。 函数fn在函数bar内部执行时，依然可以访问这个被保留下来的变量对象，所以此刻仍然可以访问到变量a的值。
//这样，我们称fn为闭包
```<br/>
* 通过调试断点来看执行过程
* 先进入var fn=null;
* 之后调用函数foo()
* 进入foo()内部 var a=2;
* fn=innerFoo;
* 调用bar()
* 进入bar(),调用fn()
* 进入innerFoo(),console.log(a)
* 输出2
## 3.闭包的应用场景
### 3.1延迟函数setTimeout
```
function fn(){
  console.log('this is test');
}
var timer=setTimeout(fn,1000);
console.log(timer);
```
