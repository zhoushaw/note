## 注释规范

```
/**
 * 
 * @method 方法名
 * @for 所属类名
 * @descript 函数功能简述、具体描述一些细节
 *
 * @param    {参数类型}参数名 参数说明
 * @param    {string}  address     地址
 * @param    {array}   com         商品数组
 * @param    {string}  pay_status  支付方式
 * @returns  {返回值类型} 返回值说明
 *
 * @date     2019-05-6
 * @author   sushi<sushi@mogu.com>
 */
```


## 起步

> compile

`sudo npm install typescript -g`

> vscode环境配置

1.项目目录下新建tsconfig.json文件

```
{
    "compilerOptions": {

        "module": "commonjs",
        "target": "es5",
        "noImplicitAny": false,
        "sourceMap": false,
        "outDir": "src"
    }
}
```
 2.使用快捷键 command ＋ shift + b

* 选择tsc构建: 创建typescript构建环境
* 选择tsc监视: 监视typescript

## 命令行

全局安装完`TypeScript`后，将会多出一个`tsc`命令，

> 编译

```
tsc test.ts // 将会把tst.ts转变成test.js是文件
```

> 参数

* `--strictNullcheck`,不可以赋值为`null


## 数据类型

> javascript原始类型

* string
* undefined
* number
* boolean
* null
* object
* symbol

> ts数据类型表示

1.布尔
`let isDone: boolean = false;`
2.数值
`let decLiteral: number = 6;`
3.字符串
`let myName: string = 'Tom';`
4.空值
`let unusable: void = undefined;`
5.任意
`let myFavoriteNumber: any = 'seven';`
6.undefined和null
`let num: number = undefined;`
`let n: null = null;`
**undefined和null类型的值可以赋给其他类型的值**
7.void
`let u: void;`
**不可以赋值给其他类型**

8.联合类型
`let myFavoriteNumber: string | number;`

> 注意

**在typescript中没有定义类型将会自动为其匹配对应的类型**


### 数组类型

> 「类型 + 方括号」表示法

```
let fibonacci: number[] = [1, 1, 2, 3, 5];
```

相等

```
let fibonacci: Array<number> = [1, 1, 2, 3, 5];
```

一般将`Array<number>`的写法称之为**泛型**


> 任意类型

```
let list: any[] = ['Xcat Liu', 25, { website: 'http://xcatliu.com' }];
```

> 元组

**限定长度和类型，不能越界**

```
let list: [number, string] = [12,'shaw'];
```


> 类数组

```
function sum() {
    let args: IArguments = arguments;
}
```

> 数组只读

```
let arr: ReadonlyArray<number> = [1,2,3,4];
arr[0] = 3;     // 编译过程中将发生error
```

> 索引

```
interface SquareConfig {
    color?: string;
    width?: number;
    [propName: string]: any;
}

// 只要不是color、width属性限制类型，其他任意属性都可以
```

### 枚举

枚举对应**数值**，将数字赋予意义

```
enum Color {
    Red = 1,
    Green,
    Blue
};

let g: Color = Color.Green; // 2
```

反向查找，**知道数字**，**查找名称**

```
let gName: Color = Color[2]; // Green
```

### 任意

在动态值或第三方库中，可能是多种类型的值，可以使用`any`类型来进行设置。

```
let list: any[] = [1,true,'free',{}];
```

### void

只能赋值给`null`、`undefined`

没有任何返回值

```
function say(): void{
    console.log('hello world');
}
```

### never

它必须是不能返回、或者报错、无限循环

```
// 报错
function err(message: string): never {
    throw new Error(message);
}

// 无限循环
function inifiniteLoop(): never {
    while(true){
    
    }
}
```

### 函数类型

**一个函数有输入和输出，要在 TypeScript 中对其进行约束，需要把输入和输出都考虑到**

```
function sum(x: number, y: number): number {
    return x + y;
}
```

**函数表达式**

```
let mySum = function (x: number, y: number): number {
    return x + y;
};
```
**在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。**

```
let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
```

**接口定义函数形状**


```
interface SearchFunc {
    (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
    return source.search(subString) !== -1;
}
```

**可选参数**

```
function buildName(firstName: string, lastName?: string) {
    if (lastName) {
        return firstName + ' ' + lastName;
    } else {
        return firstName;
    }
}
let tomcat = buildName('Tom', 'Cat');
let tom = buildName('Tom');
```
**可选参数后面不允许再出现必须参数了**

**默认参数**

```
function buildName(firstName: string, lastName: string = 'Cat') {
    return firstName + ' ' + lastName;
}
let tomcat = buildName('Tom', 'Cat');
let tom = buildName('Tom');
```

**重载**

重载允许一个函数接受不同数量或类型的参数时，作出不同的处理

```
let suits = ["hearts", "spades", "clubs", "diamonds"];

function pickCard(x: {suit: string; card: number; }[]): number;
function pickCard(x: number): {suit: string; card: number; };
function pickCard(x): any {
    // Check to see if we're working with an object/array
    // if so, they gave us the deck and we'll pick the card
    if (typeof x == "object") {
        let pickedCard = Math.floor(Math.random() * x.length);
        return pickedCard;
    }
    // Otherwise just let them pick the card
    else if (typeof x == "number") {
        let pickedSuit = Math.floor(x / 13);
        return { suit: suits[pickedSuit], card: x % 13 };
    }
}

```

> this

**this: Deck**，指定this的对外接口

```
interface Card {
    suit: string;
    card: number;
}
interface Deck {
    suits: string[];
    cards: number[];
    createCardPicker(this: Deck): () => Card;
}
let deck: Deck = {
    suits: ["hearts", "spades", "clubs", "diamonds"],
    cards: Array(52),
    createCardPicker: function(this: Deck) {
        return () => {
            let pickedCard = Math.floor(Math.random() * 52);
            let pickedSuit = Math.floor(pickedCard / 13);

            return {suit: this.suits[pickedSuit], card: pickedCard % 13};
        }
    }
}
```

> 泛型

使用泛型来创建可重用的组件，一个组件可以支持多种类型的数据。 这样用户就可以以自己的数据类型来使用组件

场景一: 一个函数传参类型必须与**返回类型相同**，但又不指定**某种特定的类型**

```
function print<T>(arg: T): T {
    return arg;
}
```

两种使用方式：

* 传入所有的参数，包含类型参数
    * `let output = print<string>("myString"); `
* 类型推论,编译器会根据传入的参数自动地帮助我们确定T的类型
    * `let output = print("myString"); `

场景二: **泛型部分变量，数组泛型**

```
function loggerLength<T>(arg: T[]): T[] {
    console.log(arg.length);
    return arg;
}
```

两种创建方式：

* `function loggerLength<T>(arg: T[]): T[] {}`
* `function loggerLength<T>(arg: Array<T>): Array<T> {}`

场景三: **泛型接口**

两种定义方式：

```
function identity<T>(arg: T): T {
    return arg;
}

let myIdentity: {<T>(arg: T): T} = identity;
```

相等：

```
interface GenericIdentityFn {
    <T>(arg: T): T;
}

function identity<T>(arg: T): T {
    return arg;
}

let myIdentity: GenericIdentityFn = identity;

// 可以指定泛型类型

interface GenericIdentityFn<T> {
    (arg: T): T;
}

function identity<T>(arg: T): T {
    return arg;
}

let myIdentity: GenericIdentityFn<number> = identity;
```

> 泛型约束

约束泛型取值,指定泛型存在指定变量

```
interface Lengthwise {
    length: number;
}
function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length);
    return arg;
}
```

案例二：获取对象指定`key`值

```
function getProperty <T, K extends keyof T>(obj: T,key: K) {
    return obj[key];
}
let x = {a: '1', b: 'hello world'};
getProperty(x, 'a'); // 成功
getProperty(x, 'ss'); // 编译失败
```

### 类型保护

```
interface Bird {
    fly();
    layEggs();
}

interface Fish {
    swim();
    layEggs();
}

function getSmallPet(): Fish | Bird {
    // ...
}

let pet = getSmallPet();
pet.layEggs(); // okay
pet.swim();    // errors

if (pet.swim) { // errors
    pet.swim();
}
```

> 定义类型保护

```
function isFish(pet: Fish | Bird): pet is Fish {
    return (<Fish>pet).swim !== undefined;
}
if (isFish(pet)) {
    pet.swim(); // okay
}
```

### 类型断言

**类型断言（Type Assertion）可以用来手动指定一个值的类型。**

语法:
`<类型>`+ `value`    或       `value` as `类型`

> 为何需要类型断言

**当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候，我们只能访问此联合类型的所有类型里共有的属性或方法**
number类型中没有length属性，会报错

```
function getLength(something: string | number): number {
    return something.length;
}
```

这时可以将变量断言成某种类型

```
function getLength(something: string | number): number {
    if ((<string>something).length) {
        return (<string>something).length;
    } else {
        return something.toString().length;
    }
}
```

## 对象的类型——接口


简单来说接口是对象的**描述**

```
interface Person {
    name: string;
    age: number;
}

let tom: Person = {
    name: 'Tom',
    age: 25
};
```

> 可选属性

```
interface Person {
    name: string;
    age?: number;
}

let tom: Person = {
    name: 'Tom'
};
```

> 任意属性

```
interface Person {
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    name: 'Tom',
    gender: 'male'
};
```

> 只读

```
interface Person {
    readonly id: number;
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    name: 'Tom',
    gender: 'male'
};

tom.id = 89757;
```

> 索引签名

```
interface Square {
    color: string,
    width: number,
    [propsName]: stirng
}
```

> 继承

```
interface Shape {
    color: string;
}

interface Square extends Shape {
    sideLength: number;
}
```

## 类接口定义

功能定义：

* 定义内容

可以将类的接口定义分为：实例类型、静态部分类型。


* 实例部分： `new` 实例化的类型
* 静态部分： 普通方法

> 静态部分

```

interface ClockInterface {
    currentTime: Date
    setTime(d: Date): string
}

class Clock implements ClockInterface {
    currentTime: Date

    setTime (day: Date) {
        return 'hello world';
    }
}
```

> 实例部分

```
interface ClockConstructor {
    new (hour: number, minute: number)
}
interface ClockInterface {
    tick();
}

function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
    return new ctor(hour, minute);
}

class DigitalClock implements ClockInterface {
    constructor(h: number, m: number) { }
    tick() {
        console.log("beep beep");
    }
}

let analog = createClock(DigitalClock, 7, 32);
```

```
type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
function getName(n: NameOrResolver): Name {
    if (typeof n === 'string') {
        return n;
    }
    else {
        return n();
    }
}

```

> 接口继承类

接口继承类后，将会继承它的属性

```
class Control {
    private state: string
}

interface ControlStruct extends Control {
    sayHello()
}

// 正确
class SubControl extends Control implements ControlStruct{
    sayHello() {}
}

// 错误，未继承其state属性
class SubControl implements ControlStruct{
    sayHello() {}
}
```


### 继承

```
class Animal {
    move(distanceInMeters: number = 0) {
        console.log(`Animal moved ${distanceInMeters}m.`);
    }
}

class Dog extends Animal {
    bark() {
        console.log('Woof! Woof!');
    }
}

const dog = new Dog();
dog.bark();
dog.move(10);
dog.bark();
```

### 公共，私有与受保护的修饰符

> public

类的属性和方法默认使用`public`来声明属性和方法，表明**属性和方法是公共**的。可在类的**外部访问**

> private

当成员被标记成`private`时，它不能在声明它的外部访问，在**派生类**中也无法访问。

```
class Person {
    private name: string
    constructor(name) {
        this.name = name;
    }
}

let person = new Person('shaw');
console.log(person.name); // 发生错误不能访问私有成员

class Man extends Person{
    constructor(name) {
        super(name);
    }
    say () {
        console.log(this.name) // 发生错误，派生类中不能访问基类的私有成员
    }
}
```

> protected

`protected`**修饰符**与 `private`修饰符的**行为很相似**，但有一点不同， `protected`成员在**派生类**中仍然可以访问。例如：

```
class Person {
    private name: string
    constructor(name) {
        this.name = name;
    }
}

class Man extends Person{
    constructor(name) {
        super(name);
    }
    say () {
        console.log(this.name) //shaw
    }
}
let person = new Man('shaw');
```

### 存取器

TypeScript支持对`getters/setters`来**截取对对象成员的访问**

设置名称时检测用户是否密码正确

```
let passcode = "secret passcode";

class Employee {
    private _fullName: string;

    get fullName(): string {
        return this._fullName;
    }

    set fullName(newName: string) {
        if (passcode && passcode == "secret passcode") {
            this._fullName = newName;
        }
        else {
            console.log("Error: Unauthorized update of employee!");
        }
    }
}

let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
    alert(employee.fullName);
}
```

### 静态属性

上面所有**访问的属性**都是类的**实例成员**,下面要访问的是**类**上的属性，存在于类或可以称之为函数中的静态属性

> 错误使用:

```

class Grid {
    static origin = {};

    say () {
        console.log(this.origin) // 发生错误，origin成员是静态属性，不是实例属性，不可直接通过this访问
    }
}
```

> 正确使用:

```

class Grid {
    static origin = {name: 'shaw'};

    say () {
        console.log(Grid.name) // {name: 'shaw'}
    }
}
```
### 抽象类

特点：

* 抽象类做为其它派生类的基类使用。 它们一般不会直接被实例化
* 抽象类中的抽象方法不包含具体实现并且必须在派生类中实现

```
abstract class Department {

    constructor(public name: string) {
    }

    printName(): void {
        console.log('Department name: ' + this.name);
    }

    abstract printMeeting(): void; // 必须在派生类中实现
}

class AccountingDepartment extends Department {

    constructor() {
        super('Accounting and Auditing'); // 在派生类的构造函数中必须调用 super()
    }

    printMeeting(): void {
        console.log('The Accounting Department meets each Monday at 10am.');
    }

    generateReports(): void {
        console.log('Generating accounting reports...');
    }
}

let department: Department; // 允许创建一个对抽象类型的引用
department = new Department(); // 错误: 不能创建一个抽象类的实例
department = new AccountingDepartment(); // 允许对一个抽象子类进行实例化和赋值
department.printName();
department.printMeeting();
department.generateReports(); // 错误: 方法在声明的抽象类中不存在
```

### 高级技巧

> 原有类功能修改

```
class Greeter {
    static standardGreeting = "Hello, there";
    greet() {
        console.log(Greeter.standardGreeting);
    }
}
```

### 泛型类

```
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) { return x + y; };
```

## 声明文件

**假如我们想使用第三方库，比如 jQuery，我们通常这样获取一个 id 是 foo 的元素，但是在 TypeScript 中，我们并不知道 $ 或 jQuery 是什么东西**

```
declare var jQuery: (string) => any;
jQuery('#foo');
```
> 声明文件

**通常我们会把类型声明放到一个单独的文件中，这就是声明文件**

```
// jQuery.d.ts
declare var jQuery: (string) => any;
```

引入申明文件

```
/// <reference path="./jQuery.d.ts" />
jQuery('#foo');
```

> 申明方法

[npm](https://blogs.msdn.microsoft.com/typescript/2016/06/15/the-future-of-declaration-files/)


## 内置对象

> ECMAScript 标准提供的内置对象

**Boolean**、**Error**、**Date**、**RegExp** 等。

定义方式:

```
let b: Boolean = new Boolean(1);
let e: Error = new Error('Error occurred');
let d: Date = new Date();
let r: RegExp = /[a-z]/;
```

> DOM 和 BOM 的内置对象

```
let body: HTMLElement = document.body;
let allDiv: NodeList = document.querySelectorAll('div');
document.addEventListener('click', function(e: MouseEvent) {
  // Do something
});
```




