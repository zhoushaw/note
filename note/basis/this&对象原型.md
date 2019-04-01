## 一、this关键词


<p class="tip">this是关键词，表示指向的索引位置</p>

很多人对于this最终指向常见的误解是，this是编写时绑定的，通常会将其认为成一下几种情况：


1、认为this指向，foo函数

```javascript
function foo () {
    console.log(this);
}
foo();
```

2、认为this指向，obj对象

```javascript
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

var bar = obj.foo; // 函数引用！

var a = "oops, global"; // `a` 也是一个全局对象的属性

bar(); // "oops, global"
```

### 可以大致分为以下几种情况：

函数调用方式与内部this指针关系
1.直接调用:函数内部this指向全局对象window
2.通过对象使用点来调用:函数内部this指向调用对象
3.触发事件调用函数:函数内部的this指向触发事件的对象
4.以new的方式来调用:函数内部this指向本次函数执行时对应的一个匿名对象（以new的方式创建的函数，函数名的首字母一般以大写字母开始）
构造函数 ，是一种特殊的方法。主要用来在创建对象时初始化对象， 即为对象成员变量赋初始值，总与new运算符一起使用在创建对象的语句中。

5.通过call的方法来间接调用方法:函数内部this指向call方法的第一参数对象
有点:我们可以创建结构相同，但内容不同的对象


### 仅仅是规则

this的最终指向可以将其分为大致四种规则

#### 默认绑定

我们要考察的第一种规则源于函数调用的最常见的情况：独立函数调用

在非`strict mode`模式下，独立函数调用默认指向全局对象window，在`strict mode`模式下默认绑定 来说全局对象是不合法，所以 `this` 将被设置为 `undefined`

```
function foo() {
	console.log( this.a );
}

var a = 2;

foo(); // 2
```

#### 隐含绑定

另一种要考虑的规则是：调用点是否有一个环境对象（`context object`），也称为拥有者（`owning`）或容器（`containing`）对象


```
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

obj.foo(); // 2
```

<p class="tip">无论 foo() 是否一开始就在 obj 上被声明，还是后来作为引用添加（如上面代码所示），这个 函数 都不被 obj 所真正“拥有”或“包含”.调用点 使用 obj 环境来 引用 函数，所以你 可以说 obj 对象在函数被调用的时间点上“拥有”或“包含”这个 函数引用。</p>


只有对象属性引用链的最后一层是影响调用点的。比如：

```
function foo() {
	console.log( this.a );
}

var obj2 = {
	a: 42,
	foo: foo
};

var obj1 = {
	a: 2,
	obj2: obj2
};

obj1.obj2.foo(); // 42
```

#### 隐含丢失


传递一个回调函数时：

```
function foo() {
	console.log( this.a );
}

function doFoo(fn) {
	// `fn` 只不过 `foo` 的另一个引用

	fn(); // <-- 调用点!
}

var obj = {
	a: 2,
	foo: foo
};

var a = "oops, global"; // `a` 也是一个全局对象的属性

doFoo( obj.foo ); // "oops, global"
```

那么如果接收你所传递回调的函数不是你的，而是语言内建的呢？没有区别，同样的结果。

```
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

var a = "oops, global"; // `a` 也是一个全局对象的属性

setTimeout( obj.foo, 100 ); // "oops, global"
```

正如我们刚刚看到的，我们的回调函数丢掉他们的 this 绑定是十分常见的事情。但是 this 使我们吃惊的另一种方式是，接收我们回调的函数故意改变调用的 this。那些很流行的 JavaScript 库中的事件处理器就十分喜欢强制你的回调的 this 指向触发事件的 DOM 元素。虽然有时这很有用，但其他时候这简直能气死人。不幸的是，这些工具很少给你选择。

#### 明确绑定

JavaScript 语言中的“所有”函数都有一些工具。具体地说，函数拥有 call(..) 和 apply(..) 方法。

这些工具如何工作？它们接收的第一个参数都是一个用于 this 的对象，之后使用这个指定的 this 来调用函数。因为你已经直接指明你想让 this 是什么，所以我们称这种方式为 明确绑定（explicit binding)。

```
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2
};

foo.call( obj ); // 2
```