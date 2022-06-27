# （一）JavaScript 面向对象

## 1. 面向对象编程介绍

### 1.1 两大编程思想

- 面向过程
- 面向对象

### 1.2 面向过程编程

**面向过程** 编程，即POP（Process-oriented programming）。面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用就可以了。

### 1.3 面向对象编程

**面向对象** 编程，即 OOP（Object Oriented Programming）
面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作。  

在面向对象程序开发思想中，每—个对象都是功能中心，具有明确分工。
面向对象编程具有灵活、代码可复用、容易维护和开发的优点，更适合多人合作的大型软件项目。   

面向对象的特性：
- 封装性
- 继承性
- 多态性

### 1.4 面向过程和面向对象的对比

#### 1.4.1 面向过程

- 优点：性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程。
- 缺点：没有面向对象易维护、易复用、易扩展。

#### 1.4.2 面向对象

- 优点：易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统更加灵活、更加易于维护
- 缺点：性能比面向过程低。

## 2. ES6 中的类和对象

### 2.1 对象

现实生活中：万物皆对象，对象是 **一个具体的事物**，看得见摸得着的实物。例如，一本书、一辆汽车、一个人可以是“对象”，一个数据库、一张网页、一个与远程服务器的连接也可以是“对象”。  

在 JavaScript 中，**对象是一组无序的相关属性和方法的集合，所有的事物都是对象**，例如字符串、数值、数组、函数等。  

对象是由属性和方法组成的：
- 属性：事物的 **特征**，在对象中用 **属性** 来表示（常用名词）
- 方法：事物的 **行为**，在对象中用 **方法** 来表示（常用动词）

### 2.2 类 class

在 ES6 中新增加了类的概念，可以使用 `class` 关键字声明—个类，之后以这个类来实例化对象。
- **类** 抽象了对象的公共部分，它泛指某一大类（class）
- **对象** 特指某一个，通过类实例化一个具体的对象

面向对象的思维特点：
- 抽取(抽象)对象共用的属性和行为组织(封装)成—个类（模板）
- 对类进行实例化,获取类的对象

### 2.3 创建类和对象

语法：
```js
class ClassName {
    // class body
}
```

创建实例：
```js
let obj = new ClassName();
```

> [!warning]
> 类必须使用 `new` 实例化对象

### 2.4 类 constructor 构造函数

`constructor()` 方法是类的构造函数（默认方法），用于传递参数，返回实例对象，通过new命令生成对象实例时，自动调用该方法。如果没有显示定义,类内部会自动给我们创建一个 `constructor()`。  

语法：
```js
// 创建一个学生类
class Student {
    constructor(uname, age, major) {
        this.uname = uname;
        this.age = age;
        this.major = major;
    }
}
```

类的实例化——创建对象
```js
let peter = new Student("Peter", 21, "CS");
console.log(peter.uname); // Peter
```

注意：
- 通过 `class` 关键字创建类, 类名我们还是习惯性定义首字母大写
- 类里面有个 `constructor` 函数,可以接受传递过来的参数,同时返回实例对象
- `constructor` 函数 只要 `new` 生成实例时,就会自动调用这个函数, 如果我们不写这个函数，类也会自动生成这个函数
- 生成实例 `new` 不能省略
- 最后注意语法规范, 创建类：类名后面不要加小括号。生成实例：类名后面加小括号, 构造函数不需要加 `function`

### 2.5 类中添加方法

语法：直接在类中写方法名和括号即可，如下所示。
```js
class Student {
    constructor(uname, age, major) {
        this.uname = uname;
        this.age = age;
        this.major = major;
    }
    // 类中添加方法
    sing() {
        console.log(this.uname + "会唱歌");
    }
}
```

创建实例：
```js
let peter = new Student("Peter", 18, "化学");
peter.sing(); // Peter会唱歌
```

> [!warning]
> 方法之间不能加逗号分隔，同时方法不需要添加 `function` 关键字。

### 2.6 static 静态成员

给成员属性或成员方法添加 `static`，该成员就成为静态成员，静态成员只能由该类调用。

```js
class Person {
    static eat() {
        console.log('eat');
    }
}
let  p = new Person();
Person.eat(); // eat
p.eat(); // 报错
```

### 2.7 配合 getter 和 setter

实际上，`getter` 和 `setter` 是 ES5（ES2009）提出的特性，这里不做详细说明，只是配合 `class` 使用举个例子。  
当属性拥有 `get`/`set` 特性时，属性就是访问器属性。代表着在访问属性或者写入属性值时，对返回值做附加的操作。而这个操作就是 `getter`/`setter` 函数。  

<font color=red>使用场景：</font> `getter` 是一种语法，这种 `get` 将对象属性绑定到 **查询该属性时将被调用的函数**。适用于某个需要动态计算的成员属性值的获取。`setter` 则是在修改某一属性时所给出的相关提示。

```js
class Test {
    constructor(log) {
        this.log = log;
    }
    get latest() {
        console.log('latest 被调用了');
        return this.log;
    }
    set latest(e) {
        console.log('latest 被修改了');
        this.log.push(e);
    }
}

let test = new Test(['a', 'b', 'c']);
// 每次 log 被修改都会给出提示
test.latest = 'd';
// 每次获取 log 的最后一个元素 latest，都能得到最新数据。
console.log(test.latest);
```

以上输出：
```
latest 被修改了
latest 被调用了
[ 'a', 'b', 'c', 'd' ]
```

## 3. 类的继承

### 3.1 继承

- 现实中的继承：子承父业，比如我们都继承了父亲的姓。
- 程序中的继承：子类可以继承父类的—些属性和方法。

语法：使用 `extends` 关键字。
```js
class Son extends Father {
    // class body
}
```

### 3.2 super 关键字

`super` 关键字用于访问和调用对象父类上的函数。**可以调用父类的构造函数**，也可以调用父类的普通函数。  

语法
```js
super([arguments]);
// 调用 父对象/父类 的构造函数

super.functionOnParent([arguments]);
// 调用 父对象/父类 上的方法
```

示例：
```js
class Person {
    constructor (uname, age) {
        this.uname =uname;
        this.age = age;
    }
}
class Student extends Person {
    constructor (uname, age, major) {
        // super 将子类的参数传递给父类构造函数，减少代码量
        super(uname, age);
        // 子类可以有自己独有的属性
        this.major = major;
    }
}
let rick = new Student("Rick", 22, "数学");
```

> [!warning]
> 注意: 子类在构造函数中使用 `super`, 必须放到 `this` 前面（必须先调用父类的构造方法，再使用子类构造方法）

#### 3.2.1 super 传值问题

观察以下代码，运行将产生错误。
```js
class Father {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    sum() {
        console.log(this.x + this.y);
    }
}
class Son extends Father {
    constructor(x, y) {
        this.x = this.x;
        this.y = this.y;
    }
}
let obj = new Son(10, 20);
obj.sum();
```

解释说明：若子类没有写构造函数 `constructor`，则实例化时默认调用父类的，这时候程序运行无误。若子类写了构造函数，那么子类在调用 `sum` 方法的时候，参数的值没有传给父类，父类无法调用参数的值，也就无法执行 `sum` 方法。  


正确：加入 `super`。
```js
class Father {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    sum() {
        console.log(this.x + this.y);
    }
}
class Son extends Father {
    constructor(x, y) {
        super(x, y);
    }
}
let obj = new Son(10, 20);
obj.sum(); // 30
```

#### 3.2.2 super 调用父类普通函数

```js
class Parent {
    sayHi() {
        return "Father: hello";
    }
}
class Child extends Parent {
    sayHi() {
        // super 调用父类普通函数
        console.log(super.sayHi());
    }
}
let man = new Child();
man.sayHi(); // Father: hello
```

#### 3.2.3 继承中属性和方法查找原则

继承中的属性或者方法查找原则：就近原则
- 继承中，如果实例化子类输出一个方法，先看子类有没有这个方法，如果有就先执行子类的
- 继承中，如果子类里面没有，就去查找父类有没有这个方法，如果有，就执行父类的这个方法（就近原则）

```js
class Parent {
    sayHi() {
        console.log("Father: hello");
    }
}
class Child extends Parent {
    sayHi() {
        console.log("Son: hello");
    }
}
let man = new Child();
man.sayHi(); // Son: hello
```

#### 3.2.4 super 必须放到子类 this 之前

子类在构造函数中使用 `super`, 必须放到 `this` 前面。

```js
class Father {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
}
class Son extends Father {
    constructor(x, y, z) {
        super(x, y, z);
        this.z = this.z;
    }
}
let obj = new Son();
```

### 3.3 使用类的注意点

- 在 ES6 中类没有变量提升，所以必须先定义类，才能通过类实例化对象
- 类里面的共有属性和方法一定要加 `this` 使用
- 类里面的 `this` 指向问题：`constructor` 里面的 `this` 指向实例对象, 方法里面的 `this` 指向这个方法的调用者

案例分析如下：

```js
let that;
class Star {
    constructor (uname, age) {
        that = this;
        this.uname = uname;
        this.age = age;
        // btn按钮调用sing方法
        this.btn = document.querySelector("button");
        this.btn.onclick = this.sing;
            // constructor 里面的this 指向的是 创建的实例对象
        console.log("constructor: ", this);
    }
    sing() {
        // 这个sing方法里面的 this 指向的是 btn 这个按钮，因为这个按钮调用了这个函数
        console.log("sing:", this); // button
        console.log(that.uname); // that里面存储的是constructor里面的this
        // 使用构造函数
    }
    dance() {
        // 这个dance里面的this 指向的是实例对象 ldh 因为ldh 调用了这个函数
        console.log("dance:", this);
    }
}
let rick = new Star("Rick", 20);
rick.dance();
```

## 4. 面向对象案例

### 4.1 源码素材

> [!TIP]
> 我用阿里云盘分享了「09-面向对象案例」，你可以不限速下载🚀
> 链接：https://www.aliyundrive.com/s/p6YYAbggHpU

### 4.2 分析

#### 4.2.1 类的基本架构

```js
class Tab {
    constructor(id) {
        // 获取相关元素节点
        // 根据传入的id选择器构建主节点
        this.main = document.querySelector(id);
    }
    // 初始化，绑定各个事件
    init() {}
    // 更新节点，同步整个状态
    updateNode() {}
    // 1. 切换功能
    toggleTab() {}
    // 2. 添加功能
    addTab() {}
    // 3. 删除功能
    removeTab() {}
    // 4. 修改功能
    editTab() {}
}
```

#### 4.2.2 一些要点

- 在 `init()` 中绑定事件时，不需要即时执行的话，则事件名后面不加括号。
- 若需要主节点，则声明一个 `that` 变量，在 `constructor()` 里面赋值 `that = this`。
- `insertAdjacentHTML()` 方法：可以在指定元素的指定位置添加一个节点字符串。（[MDN insertAdjacentHTML](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/insertAdjacentHTML  )）
- `appendChild` 不支持追加字符串的子元素，`insertAdjacentHTML` 支持追加字符串的元素
- `node` 是某一个节点，在其上绑定节点的时候需要提前判断该节点存在再绑定事件，可使用 `node && node.click()`。
- 自动执行某事件而不需要手动触发，使用 `node.click()`、`node.blur()` 等等。
- 双击事件：`ondblick`。
- 双击禁止选中文字：
    ```js
    window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
    ```
- 双击禁止选中文字（CSS做法）：`user-select: none;`

# （二）构造函数和原型

没添加 `Function` 的原型链：
![原型链](https://s1.ax1x.com/2022/03/08/bgAurV.png)

添加 `Function` 后的原型链：
![原型2](https://s1.ax1x.com/2022/03/08/bg8UEj.png)

## 1. 构造函数和原型

### 1.1 概述

在典型的 OOP 的语言中（如 Java），都存在类的概念，类就是对象的模板，对象就是类的实例，但在 ES6之前， JS 中并没用引入类的概念。  

ES6， 全称 ECMAScript 6.0 ，2015.06 发版。但是目前浏览器的 JavaScript 是 ES5 版本，大多数高版本的浏览器也支持 ES6，不过只实现了 ES6 的部分特性和功能。
在 ES6 之前 ，对象不是基于类创建的，而是用一种称为 **构建函数** 的特殊函数来定义对象和它们的特征。  

创建对象可以通过以下三种方式：
1. 对象字面量
2. `new Object()`
3. 自定义构造函数

### 1.2 构造函数

**构造函数** 是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总与 `new` 一起使用。我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里面。  

在 JS 中，使用构造函数时要注意以下两点：
1. 构造函数用于创建某一类对象，其首字母要大写
2. 构造函数要和 `new` 一起使用才有意义

`new` 在执行时会做四件事情：
1. 在内存中创建一个新的空对象。
2. 让 `this` 指向这个新的对象。
3. 执行构造函数里面的代码，给这个新对象添加属性和方法。
4. 返回这个新对象（所以构造函数里面不需要 `return`）。

### 1.3 静态成员和实例成员

JavaScript 的构造函数中可以添加一些成员，可以在构造函数本身上添加，也可以在构造函数内部的 this 上添加。通过这两种方式添加的成员，就分别称为 **静态成员** 和 **实例成员**。  
- 静态成员：在构造函数本上添加的成员称为 **静态成员，只能由构造函数本身来访问**
- 实例成员：在构造函数内部创建的对象成员称为 **实例成员，只能由实例化的对象来访问**

```js
function Human(uname, age) {
    this.uname = uname;
    this.age = age;
}
Human.x = 10; // 静态成员
let rick = new Human("rick", 35);
// console.log(rick.x); // 实例化的对象不能调用静态成员
console.log(Human.x); // 静态成员只能由构造函数本身来访问
```

### 1.4 构造函数的问题

构造函数方法很好用，但是 **存在浪费内存的问题**。

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
    this.sing = function() {
        console.log('我会唱歌');
    }
}
var ldh = new Star('刘德华', 18);
var zxy = new Star('张学友', 19);
```

函数内容一样的函数（`sing()`），会在内存中产生两份，占两份空间。
我们希望 **所有的对象使用同一个函数，这样就比较节省内存**，于是就有了构造函数原型 `prototype`。

### 1.5 构造函数原型 prototype

构造函数通过原型分配的函数是所有对象所 **共享的**。  

JavaScript 规定，每一个构造函数都有一个 `prototype` 属性，指向另一个对象。注意这个 `prototype` 就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有。  

我们可以 **把那些不变的方法，直接定义在 `prototype` 对象上，这样所有对象的实例就可以共享这些方法**。

关键概念理解：
- 原型是一个对象，我们也称为 `prototype` 为原型对象。
- 原型的作用：共享方法。

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
}
Star.prototype.sing = function () {
        console.log('我会唱歌');
}
var ldh = new Star('刘德华', 18);
var zxy = new Star('张学友', 19);
console.log(ldh.sing === zxy.sing); // true
```

上述代码将输出 `true`，因为 `sing` 方法已被共享。

### 1.6 对象原型 `__proto__`

对象都会有一个属性 `__proto__` 指向构造函数的 `prototype` 原型对象，之所以我们对象可以使用构造函数 `prototype` 原型对象的属性和方法，就是因为对象有 `__proto__` 原型的存在。  

`__proto__` 对象原型和构造函数的原型对象 `prototype` 是等价的。

`__proto__` 对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是 **它是一个非标准属性，因此实际开发中，不可以使用这个属性**，它只是内部指向原型对象 `prototype`。

> [!warning]
> `Object.prototype.__proto__` 已废弃: 该特性已经从 Web 标准中删除，虽然一些浏览器目前仍然支持它，但也许会在未来的某个时间停止支持，请尽量不要使用该特性。为了更好的支持，建议只使用 `Object.getPrototypeOf()`。
> ——[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/proto)

以后要得到某实例对象的原型，尽量使用 `Object.getPrototypeOf()`。

案例：
```js
function Human(uname, age) {
    this.uname = uname;
    this.age = age;
}
Human.prototype.sayHi = function () {
    console.log("Hey");
}
let rick = new Human('rick', 35);
let jack = new Human('jack', 33);
console.log(Object.getPrototypeOf(rick) === Human.prototype); // true
console.log(Object.getPrototypeOf(rick) === rick.__proto__); // true
```

### 1.7 constructor 构造函数

对象原型（`__proto__`）和构造函数（`prototype`）原型对象里面都有一个属性 `constructor` 属性 ，`constructor` 我们称为构造函数，因为它指回构造函数本身。
`constructor` 主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数。  

**一般情况下，对象的方法都在构造函数的原型对象中设置**。如果有多个对象的方法，我们可以 **给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容**，这样修改后的原型对象 `constructor`  就不再指向当前构造函数了。此时，我们 **可以在修改后的原型对象中，添加一个 `constructor` 指向原来的构造函数**。

```js
function Human(uname, age) {
    this.uname = uname;
    this.age = age;
}
Human.prototype = {
    // 添加一个 constructor 指向原来的构造函数
    constructor: Human,
    sayHi: function () {
        console.log("Hey!");
    },
    eat: function () {
        console.log("Eat something.");
    }
}
let rick = new Human('rick', 35);
console.log(Object.getPrototypeOf(rick).constructor); 
// Human(uname, age) {...}
```

### 1.8 构造函数、实例、原型对象三者之间的关系


![prototype1](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/JavaScript/prototype1.h8mujzc530g.png)

关于 实例对象能指向构造函数的解释：实例对象通过 `ldh.__proto__` （`Obj.getPrototypeOf(ldh)`）指向原型 `prototype`，而 `prototype` 能通过 `prototype.constructor` 指向原来的构造函数。

### 1.9 JavaScript 的成员查找机制（规则）

- 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
- 如果没有就查找它的原型（也就是 `__proto__` 指向的 `prototype` 原型对象）。
- 如果还没有就查找原型对象的原型（`Object`）的原型对象）。
- 依此类推一直找到 `Object` 为止（`null`）。
- `__proto__` 对象原型的 **意义就在于为对象成员查找机制提供一个方向，或者说一条路线**。

### 1.10 原型对象this指向

构造函数中的 `this` 指向我们实例对象.
原型对象里面放的是方法,  这个方法里面的 `this` 指向的是 这个方法的调用者, 也就是这个实例对象。

### 1.11 扩展内置对象

可以通过原型对象，对原来的内置对象进行扩展自定义的方法。比如给数组增加自定义求偶数和的功能。

> [!TIP]
> 注意：数组和字符串内置对象不能给原型对象覆盖操作 `Array.prototype = {}` ，只能是 `Array.prototype.xxx = function(){}` 的方式。

举例：给数组增加自定义求偶数和的功能。
```js
// !不能写成对象字面量形式
Array.prototype.sumOfEven = function () {
    let sum = 0;
    for (let i = 0; i < this.length; i++) {
        // 位运算判断奇偶
        if (!(this[i]&1)) {
            sum += this[i];
        }
    }
    return sum;
}
let arr = [1,2,3,4,5,6];
console.log(arr.sumOfEven());
```

## 2. 继承

ES6之前并没有给我们提供 `extends` 继承。我们可以通过 **构造函数+原型对象** 模拟实现继承，被称为 **组合继承**。

### 2.1 call()

功能：调用这个函数, 并且修改函数运行时的 `this` 指向。

```js
fun.call(thisArg, arg1, arg2, ...) 
```

- `fun`：被调用并被修改函数运行时 `this` 指向的函数
- `thisArg`：当前调用函数 `this` 的指向对象
- `arg1, arg2`：传递的其他参数

举例：
```js
function Foo(uname, age) {
    this.uname = uname;
    this.age = age;
    console.log(this);
}
let obj = {x: 1};
Foo.call(obj, 'rick', 30);
```
以上代码输出：`{x: 1, uname: 'rick', age: 30}`，说明函数内部指向改变为了指向 `obj`。

### 2.2 借用构造函数继承父类型属性

核心原理： 通过 `call()` 把父类型的 `this` 指向子类型的 `this` ，这样就可以实现子类型继承父类型的属性。

```js
// 父类
function Person(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
}
// 子类
function Student(name, age, sex, score) {
    // 此时父类的 this 指向子类的 this，同时调用这个函数
    Person.call(this, name, age, sex);  
    this.score = score;
}
var s1 = new Student('zs', 18, '男', 100);
console.log(s1); 
```

输出如下，说明子类成功通过 `call` 方法继承了父类的属性。

![output1](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/JavaScript/output1.4ezc1vfpb5o0.png)

### 2.3 借用原型对象继承父类型方法

有了上述方法还不够，一般不能继承父类的方法，因为 **一般情况下，对象的方法都在构造函数的原型对象中设置，通过构造函数无法继承父类方法**。  

这个时候 **原型对象** 就起了作用。我们可以令子类构造函数的原型对象等于父类构造函数的原型对象，这样子类也可以使用父类构造函数的原型对象上的成员方法了。即：
```js
childFoo.prototype = parentFoo.prototype;
```

但是这样又产生了一个问题：这样指定之后，子类构造函数和父类构造函数的对象原型 `prototype` 就 **指向同一个内存地址了**。也就是说，**你在子类原型对象上绑定其特有的成员方法，父类上也会有**，显然这是不合理的。

解决方法：利用父类的实例对象。核心原理： 
1. 将子类所共享的方法提取出来，然后让：
    ```
    子类的 prototype 原型对象 = new 父类();
    ```
2. 本质：子类原型对象等于是实例化父类，因为父类实例化之后 **另外开辟空间，就不会影响原来父类原型对象**
3. 将子类的 `constructor` 重新指向子类的构造函数


举例：
```js
// 父构造函数
function Human(uname, age) {
    this.uname = uname;
    this.age = age;
}
// 父构造成员方法
Human.prototype.eat = function () {
    console.log("eat something");
}
// 子构造函数
function Student(uname, age, major) {
    Human.call(this, uname, age);
    this.major = major;
}
// 创建实例对象，将子类原型对象指向实例对象
Student.prototype = new Human();
// 将子类的 constructor 重新指向子类的构造函数
Student.prototype.constructor = Student;
// 子构造函数特有成员方法
Student.prototype.exam = function () {
    console.log("I have exams");
}
let jack = new Student('Jack', 20, 'Math');
jack.eat();
jack.exam();
console.log(Human.prototype);
```

运行上述代码，观察（最后一行输出）到父类的原型对象上没有 `exam` 成员方法。

### 2.4 类的本质

回忆下之前学的，在 ES5 之前通过 **构造函数 + 原型** 实现面向对象编程。其中，这种面向对象有这些特点：
- 构造函数有原型对象 `prototype`
- 构造函数原型对象 `prototype` 里面有 `constructor` 指向构造函数本身
- 构造函数可以通过原型对象添加方法
- 构造函数创建的实例对象有 `__proto__` 原型指向 构造函数的原型对象

而在 ES6 中，我们可以用 `class` 实现面向对象，那么这两者有什么联系呢？  

实质上，<font color=red>ES6 的类的本质还是 function</font>。对应的，ES6 的 `class` 声明的类有以下特点：
- 类有原型对象 `prototype`
- 类有原型对象 `prototype`，里面也有 `constructor` 指向类的本身
- 类的所有方法都定义在类的 `prototype` 属性上
- 类创建的实例，里面也有 `__proto__` 指向类的`prototype` 原型对象

所以 ES6 的类它的绝大部分功能，ES5 都可以做到，新的 `class`写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已

**ES6 的类其实就是一种语法糖。**
语法糖：语法糖就是一种便捷写法。简单理解, 有两种方法可以实现同样的功能, 但是一种写法更加清晰、方便,那么这个方法就是语法糖

可运行以下代码自行体验：

```js
class Foo { };
let foo = new Foo();
foo.__proto__ = {
    constructor: Foo,
    test1: function () {
        console.log('test1');
    },
    test2: function () {
        console.log('test2');
    }
}
console.log(Foo.prototype);
console.log(foo.__proto__);
console.log(Foo.prototype == foo.__proto__);
foo.test1();
foo.test2();
console.log(foo.__proto__.constructor.prototype.__proto__.__proto__);
```

## 3. ES5 中的新增方法

### 3.1 概述

ES5 中给我们新增了一些方法，可以很方便的操作数组或者字符串，这些方法主要包括：
- 数组方法
- 字符串方法
- 对象方法

### 3.2 数组方法

迭代（遍历）方法：`forEach()`、`map()`、`filter()`、`some()`、`every()`

#### 3.2.1 forEach

`forEach` 方法用于遍历数组，不对原数组进行修改。

```js
array.forEach(function(currentValue, index, arr), thisArg);
```

该方法接收一个函数 `function` 参数，其中，该函数内又有三个参数：
- `currentValue`：数组当前项的值
- `index`：数组当前项的索引
- `arr`：数组对象本身

一般可以省略后面回调函数中后两个参数和 `thisArg` 参数，即：
```js
array.forEach(function(currentValue));
```

#### 3.2.2 map

`map()` 方法遍历一个数组，首先创建一个新数组，新数组中的每个元素是是调用一次所提供的函数参数后的返回值，然后 **返回这个新数组**。

```js
let newArray = array.map(function (currentValue, index, arr));
```

`map` 方法接收一个 `function` 参数，该函数有三个参数：
- `currentValue`：数组当前项的值
- `index`：数组当前项的索引
- `arr`：方法调用的数组对象本身

#### 3.2.3 filter

```js
array.filter(function(currentValue, index, arr));
```

`filter()` 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，主要 **用于筛选数组**，注意它 **返回一个新数组**。

- `currentValue`: 数组当前项的值
- `index`：数组当前项的索引
- `arr`：数组对象本身

#### 3.2.4 some

```js
array.some(function(currentValue, index, arr));
```

`some()` 方法用于检测数组中的元素是否满足指定条件。通俗点：查找数组中是否有满足条件的元素。
注意 **它返回值是布尔值**，如果查找到这个元素，就返回 `true`，如果查找不到就返回 `false`。

- `currentValue`: 数组当前项的值
- `index`：数组当前项的索引
- `arr`：数组对象本身

### 3.3 字符串方法 trim()

`trim()` 方法会从一个字符串的两端删除空白字符。

```js
str.trim()
```

`trim()` 方法并不影响原字符串本身，它返回的是一个新的字符串。

### 3.4 对象方法

#### 3.4.1 Object.keys()

`Object.keys()` 用于获取对象自身所有的属性，返回一个数组。

```js
Object.keys(obj)
```

- 效果类似 `for...in`
- 返回一个由属性名组成的数组

#### 3.4.2 Object.defineProperty()

`Object.defineProperty()` 定义对象中新属性或修改原有的属性。

```js
Object.defineProperty(obj, prop, descriptor)
```

参数：
- `obj`：必需。目标对象 
- `prop`：必需。需定义或修改的属性的名字
- `descriptor`：必需。目标属性所拥有的特性

`Object.defineProperty()` 第三个参数 `descriptor` 说明： 以对象形式 `{ }` 书写。

```js
// descriptor 对象的参数值均为默认值
Object.defineProperty(obj, prop, {
    value: undefined,
    writable: false,
    enumerable: false,
    configurable: false
})
```

- `value`：设置属性的值  默认为 `undefined`
- `writable`：值是否可以重写。`true | false`  默认为 `false`
- `enumerable`：目标属性是否可以被枚举。`true | false` 默认为 `false`
- `configurable`：目标属性是否可以被删除或是否可以再次修改特性 `true | false`，默认为 `false`

> [!TIP]
> `descriptor` 对象的参数默认值说明，使用 `defineProperty` 新增一个对象属性，该属性只读，不可迭代，不可再被修改特性。

# （三）函数进阶

## 1. 函数的定义和调用

### 1.1 函数的定义方式

#### 1.1.1 function 声明式

函数声明方式 `function` 关键字 (命名函数)

#### 1.1.2 函数表达式

函数表达式 (匿名函数)：
```js
let func = function() {};
```

#### 1.1.3 Function 生成对象

```js
let fn = new Function('a', 'b', 'console.log(a + b);');
```

- `Function` 里面参数都必须是字符串格式
- 第三种方式执行效率低，也不方便书写，因此较少使用
- 所有函数都是 `Function` 的实例化对象
- 函数也属于对象
- `Function` 方式效率低，操作麻烦，作了解

函数也属于对象，同样有原型对象，原型链：
![function1](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/JavaScript/function1.50ysdtr2sfk0.png)

### 1.2 函数的调用方式

- 普通函数：直接加括号，`fn()`
- 对象的方法：加小数点方式， `obj.fn()`
- 构造函数：`new` 构造函数
- 绑定事件函数：触发相应事件，例如 `click` 点击触发函数
- 定时器函数：`setInterval`，每隔一段时间调用函数
- 立即执行函数：`(function() {})()`，自动调用，直接执行

## 2. this

### 2.1 函数内 this 的指向

| 调用方式     | `this` 指向                                |
| ------------ | ------------------------------------------ |
| 普通函数     | `window`                                   |
| 构造函数     | 实例对象，原型对象里面的方法也指向实例对象 |
| 对象的方法   | 该方法所属对象                             |
| 绑定事件函数 | 绑定事件对象                               |
| 定时器函数   | `window`                                   |
| 立即执行函数 | `window`                                   |

### 2.2 改变函数内部 this 指向

JavaScript 为我们专门提供了一些函数方法来帮我们更优雅的处理函数内部 `this` 的指向问题，常用的有 `bind()`、`call()`、`apply()` 三种方法。

#### 2.2.1 call

`call()` 方法调用一个对象。简单理解为调用函数的方式，但是它可以改变函数的 `this` 指向。

```js
fun.call(thisArg, arg1, arg2, ...);
```

参数说明：
- `thisArg`：在 `fun` 函数运行时指定的 `this` 值
- `arg1`，`arg2`：传递的其他参数
- 返回值就是函数的返回值，因为它就是调用函数
- 因此当我们想改变 `this` 指向，同时想调用这个函数的时候，可以使用 `call`，比如继承

#### 2.2.2 apply

`apply()` 方法调用一个函数。简单理解为调用函数的方式，但是它可以改变函数的 `this` 指向。

```js
fun.apply(thisArg, [argsArray])
```

- `thisArg`：在fun函数运行时指定的 `this` 值
- `argsArray`：传递的值，必须包含在数组里面
- 返回值就是函数的返回值，因为它就是调用函数
- 因此 `apply` 主要跟数组有关系，比如使用 `Math.max()` 求数组的最大值

案例：`apply` + `Math.max()`求数组的最大值：

```js
let arr = [-10, 2, 12, 3, 1];
let max = Math.max.apply(Math, arr);
console.log(max); // 12
```

#### 2.2.3 bind

`bind()` 方法不会调用函数。但是能改变函数内部 `this` 指向。

```js
let fn = fun.bind(thisArg, arg1, arg2, ...)
```

- `thisArg`：在 `fun` 函数运行时指定的 `this` 值
- `arg1`，`arg2`：传递的其他参数
- 返回由指定的 `this` 值和初始化参数改造的 **原函数拷贝**
- 因此当我们只是想改变 `this` 指向，并且不想调用这个函数的时候，可以使用 `bind`

举例：
```js
let obj = {
    x: 'a',
    y: 'b'
};
let fn = function () {
    console.log(this);
};
let f = fn.bind(obj);
f(); // { x: 'a', y: 'b' }
```

#### 2.2.3 call apply bind 总结

相同点：都可以改变函数内部的 `this` 指向  

区别点:  
- `call` 和 `apply` 会调用函数, 并且改变函数内部this指向
-  `call` 和 `apply` 传递的参数不一样，`call` 传递参数 `aru1, aru2..` 形式，`apply` 必须数组形式 `[arg]`
- `bind` 不会调用函数，可以改变函数内部 `this` 指向，并返回一个原函数的拷贝


## 3. 严格模式

### 3.1 什么是严格模式

JavaScript 除了提供正常模式外，还提供了 **严格模式（strict mode）**。ES5 的严格模式是采用具有限制性 JavaScript 变体的一种方式，即在严格的条件下运行 JS 代码。  

严格模式在 IE10 以上版本的浏览器中才会被支持，旧版本浏览器中会被忽略。  

严格模式对正常的 JavaScript 语义做了一些更改： 
- 消除了 Javascript 语法的一些不合理、不严谨之处，减少了一些怪异行为。
- 消除代码运行的一些不安全之处，保证代码运行的安全。
- 提高编译器效率，增加运行速度。
- 禁用了在 ECMAScript 的未来版本中可能会定义的一些语法，为未来新版本的 Javascript 做好铺垫。比如一些保留字如：class, enum, export, extends, import, super 不能做变量名

### 3.2 开启严格模式

严格模式可以应用到整个脚本或个别函数中。因此在使用时，我们可以将严格模式分为为脚本开启严格模式和为函数开启严格模式两种情况。

#### 3.2.1 为脚本开启严格模式

为整个脚本文件开启严格模式，需要在所有语句之前放一个特定语句：在所有语句之前放一个特定语句 `"use strict";`（或`'use strict';`）
```html
<script>
    'use strict';
    console.log('严格模式已开启');
<script/>
```

因为 `"use strict"` 加了引号，所以老版本的浏览器会把它当作一行普通字符串而忽略。

有的 `script` 基本是严格模式，有的 `script` 脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样独立创建一个作用域而不影响其他 `script` 脚本文件。

```html
<script>
    (function (){
        "use strict";
        var num = 10;
    })();
</script>
```

#### 3.2.2 为函数开启严格模式

要给某个函数开启严格模式，需要把 `"use strict";`（或 `'use strict';`）声明放在函数体所有语句之前。  

将 "use strict" 放在函数体的第一行，则整个函数以 "严格模式" 运行。
```js
function fn(){
　　"use strict";
　　return "这是严格模式。";
}
function foo() {
    console.log("这不是严格模式");
}
```

### 3.3 严格模式中的变化

严格模式对 Javascript 的语法和行为，都做了一些改变。

#### 3.3.1 变量规定

- 在正常模式中，如果一个变量没有声明就赋值，默认是全局变量。严格模式禁止这种用法，变量都必须先用 `var` （`let`、`const`）命令声明，然后再使用。  

- 严禁删除已经声明变量。例如：`delete x;` 语法是错误的。

#### 3.2.2 严格模式下 this 指向问题

- 以前在全局作用域函数中的 `this` 指向 `window` 对象。
- **严格模式下全局作用域中函数中的 `this` 是 `undefined`。**
- 以前构造函数时不加 `new` 也可以 调用,当普通函数，`this` 指向全局对象
- 严格模式下,如果 构造函数不加 `new` 调用, `this` 指向的是 `undefined` 如果给他赋值则会报错
- `new` 实例化的构造函数指向创建的对象实例。
- 定时器 `this` 还是指向 `window`。
- 事件、对象还是指向调用者。

#### 3.2.3 函数变化

函数不能有重名的参数。  

函数必须声明在顶层。新版本的 JavaScript 会引入 “块级作用域”（ ES6 中已引入）。为了与新版本接轨，**不允许在非函数的代码块内声明函数**。

更多严格模式要求参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode


## 4. 高阶函数

高阶函数是对其他函数进行操作的函数，它 **接收函数作为参数** 或 **将函数作为返回值输出**。

举例1：
```js
function fn(callback){
    callback&&callback();
}
fn(function(){alert('hi')}
```

举例2：
```js
function fn(){
    return function() {}
}
 fn();
```

此时 `fn` 就是一个高阶函数。  

函数也是一种数据类型，同样可以作为参数，传递给另外一个参数使用。最典型的就是作为回调函数。  

同理函数也可以作为返回值传递回来

## 5. 闭包

### 5.1 变量作用域

变量根据作用域的不同分为两种：全局变量和局部变量。
1. 函数内部可以使用全局变量。
2. 函数外部不可以使用局部变量。
3. 当函数执行完毕，本作用域内的局部变量会销毁。

### 5.2 闭包的概念

**闭包（`closure`）指有权访问另一个函数作用域中变量的函数**。（--JavaScript 高级程序设计）  

简单理解就是，一个作用域可以访问另外一个函数内部的局部变量。 

```js
function fn1() {
    var s = "hello"; // x 是一个被 fn1 创建的局部变量
    function fn2() { // fn2() 是内部函数，一个闭包
        console.log(s); // 使用了父函数中声明的变量
    }
    fn2();
}
fn1();
```

### 5.3 在 chrome 中调试闭包

1. 打开浏览器，按 F12 键启动 chrome 调试工具。
2. 设置断点。
3. 找到 Scope 选项（Scope 作用域的意思）。
4. 当我们重新刷新页面，会进入断点调试，Scope 里面会有两个参数（global 全局作用域、local 局部作用域）。
5. 当执行到 `fn2()` 时，Scope 里面会多一个 `Closure` 参数 ，这就表明产生了闭包。

### 5.4 闭包的作用

如何在 `fn1()` 函数外面访问 `fn1()` 中的局部变量 `x` ？

```js
function fn1() {
    let x = 10;
    // fn2 是一个闭包
    function fn2() {
        console.log(x);
    }
    return fn2;
}
let f = fn1();
f(); // 10
```

闭包作用：**延伸变量的作用范围**。

### 5.5 闭包的案例

> [!warning]
> 以下案例都是在ES5前提下，所以没有提及 let、const

有以下节点：
```html
<ol>
    <li>Banana</li>
    <li>Apple</li>
    <li>Peach</li>
</ol>
```

#### 5.5.1 闭包应用-点击li输出当前索引号

循环注册 “点击li输出当前li索引号”。  

错误示例：
```js
for (var i = 0; i < lis.length; i++) {
    lis[i].onclick = function () {
        console.log(i); 
        // 一直输出最后一个的索引号
    }
}
```

方案1：设置 `index` 属性
```js
for (var i = 0; i < lis.length; i++) {
lis[i].index = i;
    lis[i].onclick = function () {
        console.log(this.index);
    }
}
```

方案2：闭包
```js
for (var i = 0; i < lis.length; i++) {
    (function (i) {
        // 每一个点击事件的函数成为一个闭包，点击事件内部访问到了来自立即执行函数的变量 i
        lis[i].onclick = function () {
            console.log(i);
        }
    })(i);
}
```

#### 5.5.2 闭包应用-3s后打印所有li内容

```js
for (var i = 0; i < lis.length; i++) {
    (function (i) {
        setTimeout(function () {
            console.log(lis[i].innerHTML);
        }, 3000);
    })(i);
}
```

#### 5.5.3 闭包应用-计算打车价格

问题： 闭包应用-计算打车价格 
- 打车起步价 13（3 公里内）,  之后每多一公里增加 5 块钱，用户输入公里数就可以计算打车价格
- 如果有拥堵情况，总价格多收取 10 块钱拥堵费

```js
var car = (function() {
    var start = 13; // 起步价  局部变量
    var total = 0; // 总价  局部变量
    return {
        // 正常的总价（闭包）
        price: function(n) {
            if (n <= 3) {
                total = start;
            } else {
                total = start + (n - 3) * 5
            }
            return total;
        },
        // 拥堵之后的费用（闭包）
        yd: function(flag) {
            return flag ? total + 10 : total;
        }
    }
})();
```

### 5.6 闭包总结

- 闭包是什么  
    闭包是一个函数（一个作用域可以访问另外一个函数的局部变量）。
- 闭包的作用是什么  
    延伸变量的作用范围。

## 6. 递归

### 6.1 什么是递归

如果 **一个函数在内部可以调用其本身**，那么这个函数就是 **递归函数**。  
简单理解:函数内部自己调用自己, 这个函数就是递归函数。  
递归函数的作用和循环效果一样。  

由于递归很容易发生 “栈溢出” 错误（`stack overflow`），所以必须要加退出条件 `return`。

### 6.2 递归举例

#### 6.2.1 求阶乘

```js
let factorial = function (n) {
    if (n == 0 || n == 1) return 1;
    return n * factorial(n - 1);
}
```

#### 6.2.2 斐波那契数列

```js
let fibonacci = function (n) {
    if (n < 2) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
};
```

### 6.3 浅拷贝与深拷贝

- 浅拷贝只是拷贝一层, 更深层次对象级别的只拷贝引用（**修改目标对象的值，源对象的值也会改变，因为对象属性指向同一地址**）。
- 深拷贝拷贝多层，每一级别的数据都会拷贝。
- `Object.assign(target, ...sources)` es6 新增方法可以 **浅拷贝**。


# （四）正则表达式

## 1. 正则表达式概述

### 1.1 什么是正则表达式

**正则表达式（ Regular Expression ）**是用于匹配字符串中字符组合的模式。在 JavaScript 中，正则表达式也是对象。  

正则表通常被用来检索、替换那些符合某个模式（规则）的文本，例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文（**匹配**）。此外，正则表达式还常用于过滤掉页面内容中的一些敏感词（**替换**），或从字符串中获取我们想要的特定部分（**提取**）等 。  

其他语言也会使用正则表达式，本阶段我们主要是利用 JavaScript 正则表达式完成表单验证。

### 1.2 正则表达式的特点

1. 灵活性、逻辑性和功能性非常的强。
2. 可以迅速地用极简单的方式达到字符串的复杂控制。
3. 对于刚接触的人来说，比较晦涩难懂。比如： `^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$`
4. 实际开发，一般都是直接复制写好的正则表达式。但是要求会使用正则表达式并且根据实际情况修改正则表达式。比如用户名：`/^[a-z0-9_-]{3,16}$/`

## 2. 正则表达式在 JavaScript 中的使用

### 2.1 创建正则表达式

在 JavaScript 中，可以通过两种方式创建一个正则表达式。  

- 通过调用 RegExp 对象的构造函数创建
    ```js
    var regexp = new RegExp(/表达式/); 
    ```

- 通过字面量创建
    ```js
    var regexp = /表达式/;
    ```

### 2.2 测试正则表达式 test

`test()` 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 `true` 或 `false`，其参数是测试字符串。

```js
regexObj.test(str);
```

- `regexObj` 是写的正则表达式
- `str` 我们要测试的文本
- 检测 `str` 文本是否符合我们写的正则表达式规范

## 3. 正则表达式中的特殊字符

### 3.1 正则表达式的组成

一个正则表达式可以 **由简单的字符构成**，比如 `/abc/`，也可以是 **简单和特殊字符的组合**，比如 `/ab*c/` 。其中特殊字符也被称为 **元字符**，在正则表达式中是具有特殊意义的专用符号，如 `^` 、`$` 、`+` 等。  

特殊字符非常多，可以参考： 
- MDN：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions
- 正则测试工具: http://tool.oschina.net/regex

这里我们把元字符划分几类学习。

### 3.2 边界符

正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符。

| 边界符 | 说明                           |
| ------ | ------------------------------ |
| `^`    | 表示匹配行首的文本（以谁开始） |
| `$`    | 表示匹配行尾的文本（以谁结束） |

如果 `^` 和 `$` 在一起，表示必须是 **精确匹配**（不能多不能少，只能是这些）。

```js
let regexp = /^he$/;
console.log(regexp.test('hello')); // flase
console.log(regexp.test('he')); // true
```

### 3.3 字符类

字符类表示有一系列字符可供选择，只要匹配其中一个就可以了。所有可供选择的字符都放在方括号内。

#### 3.3.1 `[]` 方括号

```js
/[abc]/.test('andy')
// true 
```

正则含义：后面的字符串只要包含 `abc` 中任意一个字符，都返回 `true`。

#### 3.3.2 `[-]`  方括号内部 `-` 范围符 

```js
/^[a-z]$/.test('c')
// true 
```

含义：方括号内部加上 `-` 表示范围，这里表示 `a` 到 `z` 26个英文字母都可以。

#### 3.3.3 `[^]`  方括号内部 取反符 `^`

```js
/[^abc]/.test('andy')
// false
```

方括号内部加上 `^` 表示 **取反**，只要包含方括号内的字符，都返回 `false` 。

> [!warning]
> 注意和边界符 `^` 区别，边界符写到方括号外面。  

#### 3.3.4 字符组合

```js
/[a-z1-9]/.test('andy')
// true
```

方括号内部可以使用字符组合，这里表示包含 `a` 到 `z` 的 26 个英文字母和 1 到 9 的数字都可以。

### 3.4 量词符

量词符用来设定 **某个模式出现的次数**。

| 量词    | 说明             |
| ------- | ---------------- |
| `*`     | 重复次数 ≥ 0     |
| `+`     | 重复次数 ≥ 1     |
| `?`     | 重复 0 次或 1 次 |
| `{n}`   | 重复 n 次        |
| `{n,}`  | 重复次数 ≥ n     |
| `{n,n}` | 重复 n 次到 m 次 |

### 3.5 括号总结

- 大括号：量词符。里面表示重复次数。
- 中括号：字符集合。匹配方括号中的任意字符。
- 小括号：表示优先级。

在线测试: https://c.runoob.com/

### 3.6 预定义类

| 预定类 | 说明                                                           |
| ------ | -------------------------------------------------------------- |
| `\d`   | 匹配 0-9 之间的任一数字，相当于 `[0-9]`                        |
| `\D`   | 匹配所有 0-9 以外的字符，相当于 `[^0-9]`                       |
| `\w`   | 匹配任意的字母、数字和下划线，相当于 `[A-Za-z0-9_]`            |
| `\W`   | 除所有字母、数字和下划线以外的字符，相当于 `[^A-Za-z0-9_]`     |
| `\s`   | 匹配空格（包括换行符、制表符、空格符等），相等于`[\t\r\n\v\f]` |
| `\S`   | 匹配非空格的字符，相当于 `[^\t\r\n\v\f]`                       |

### 3.7 正则案例

- 手机号码：`/^1[3|4|5|7|8][0-9]{9}$/`
- QQ：`[1-9][0-9]{4,}`（腾讯QQ号从10000开始）
- 昵称是中文：`^[\u4e00-\u9fa5]{2,8}$`

## 4. 正则表达式中的替换

### 4.1 replace 替换

`replace()` 方法可以实现替换字符串操作，用来替换的参数可以是一个字符串或是一个正则表达式。

```js
stringObject.replace(regexp/substr,replacement)
```

- 第一个参数：被替换的字符串 或者  正则表达式
- 第二个参数：替换为的字符串
- 返回值：一个替换完毕的新字符串

### 4.2 正则表达式参数

当 `replace` 中第一个参数为正则表达式的时候，还有一个 `switch` 参数可选。

```js
/表达式/[switch]
```

`switch`（也称为修饰符）按照什么样的模式来匹配. 有三种值：
- `g`：全局匹配 
- `i`：忽略大小写 
- `gi`：全局匹配 + 忽略大小写

举例：
```js
let msg = 'what\'s the fuck? Damn it!';
msg = msg.replace(/fuck|damn/gi, '****');
console.log(msg); 
// what's the ****? **** it!
```

#