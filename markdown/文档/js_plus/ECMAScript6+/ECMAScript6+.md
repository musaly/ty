# （一）ECMAScript 相关介绍

## 1. 什么是 ECMA

ECMA（European Computer Manufacturers Association）中文名称为欧洲计算机制造商协会，这个组织的目标是评估、开发和认可电信和计算机标准。1994 年后该组织改名为Ecma 国际。

![ES6-1](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/JavaScript/ES6-1.4w4pcis4fva0.jfif)

## 2. 什么是 ECMAScript

ECMAScript 是由 Ecma 国际通过ECMA-262 标准化的脚本程序设计语言。

![ES6-2](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/JavaScript/ES6-2.6aq6tvkonsc0.jpg)

## 3. 什么是 ECMA-262

Ecma 国际制定了许多标准，而ECMA-262 只是其中的一个，所有标准列表查看：http://www.ecma-international.org/publications/standards/Standard.htm

ECMA-262 历史版本查看网址：
http://www.ecma-international.org/publications/standards/Ecma-262-arch.htm

- ES5 是 ECMAScript 第5版，2009年发布。
- ES6 是 ECMAScript 第6版，2015年发布，也叫 ES2015。
- 从 ES6 开始，每年发布一个版本，版本号比年份最后一位大 1。

## 4. 谁在维护 ECMA-262

TC39（Technical Committee 39）是推进ECMAScript 发展的委员会。其会员都是公司（其中主要是浏览器厂商，有苹果、谷歌、微软、因特尔等）。TC39 定期召开会议，会议由会员公司的代表与特邀专家出席。

## 5. 为什么要学习 ES6

- ES6 的版本变动内容最多，具有里程碑意义
- ES6 加入许多新的语法特性，编程实现更简单、高效
- ES6 是前端发展趋势，就业必备技能

## 6. ES6 兼容性

可查看兼容性：http://kangax.github.io/compat-table/es6/ 


# （二）ECMASript 6 新特性

## 1. let 关键字

`let` 关键字用来声明变量，使用 `let` 声明的变量有几个特点：
- 不允许重复声明
- 块级作用域
- 不存在变量提升
- 不影响作用域链

<font color=red>应用场景：以后声明变量使用let 就对了</font>

**案例1**：给多个 `div` 循环注册点击事件
- 错误示例:  
    ```js
    // 错误示例，divs.length === 3
    document.addEventListener('DOMContentLoaded', function () {
        let divs = document.querySelectorAll('.box div');
        for (var i = 0; i < divs.length; i++) {
            divs[i].addEventListener('click', function () {
                divs[i].style.backgroundColor = 'pink';
            });
        }
        console.log(i); // 3
    });
    /*
    i 为当前作用域下的共享变量。
    当每次点击 div 的时候，各个点击事件共享 i 的值。
    此时 i = 3，这将报错。
    */
    ```

- 正确实例：将以上代码中的 `var` 改为 `let`。

**案例2**：1s 后循环输出所有数字
- 错误示例：  
    ```js
    for (var i = 1; i <= 5; i++) {
        setTimeout(() => {
            console.log(i);
        }, 1000);
    }
    /*
    输出：6 6 6 6 6
    循环从1-5的时间很短暂，远不及 1s。
    此时五个异步事件瞬间加入到异步事件队列中，等待 1s后依次执行。
    而此时i为6，故瞬间输出 5 个 6。
    异步事件队头
    (1) console.log(i);
    (2) console.log(i);
    (3) console.log(i);
    (4) console.log(i);
    (5) console.log(i);
    */
    ```

- 正确示例：
    ```js
    for (let j = 1; j <= 5; j++) {
        setTimeout(() => {
            console.log(j);
        }, 1000);
    }
    // 输出：1 2 3 4 5
    // let 有块级作用域，每个 j 都会形成一个自己的块级作用域，与相应的异步事件共享：
    // {j = 1;} {j = 2;} {j = 3;} {j = 4;} {j = 5;}
    ```
- 解决方法2：
    ```js
    // 给每一个 i 设置一个立即执行函数，会形成自己的块级作用域，不影响外部变量。
    for (var i = 1; i <= 5; i++) {
        (function (i) {
            setTimeout(() => {
                console.log(i);
            }, 1000);
        })(i);
    }
    ```

## 2. const 关键字

`const` 关键字用来声明常量，`const` 声明有以下特点：
- 声明必须赋初始值
- 标识符一般为大写
- 不允许重复声明
- 值不允许修改
- 块级作用域

注意：对象属性修改和数组元素变化不会出发 `const` 错误  
<font color=red>应用场景：声明对象类型使用 const，非对象类型声明选择 let</font>

案例：
```js
const arr = [1, 2, 3, 4];
arr.push(5, 6);
console.log(arr);
// 不报错
```
```js
const obj = {
    uname: 'rick',
    age: 30
}
obj.age = 40;
// 只要不改变地址，就不报错
```

## 3. 变量的解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为 **解构赋值**。

数组的解构赋值：
```js
const arr = ['red', 'green', 'blue'];
let [r, g, b] = arr;
```

对象的解构赋值：
```js
const obj = {
    uname: 'rick',
    age: 30,
    sayHi: function () {
        console.log('hello');
    },
    sayBye() {
        console.log('Bye~');
    }
}
let {name, age, sayHi} = obj;
let {sayBye} = obj;
```

<font color=red>应用场景：频繁使用对象方法、数组元素，就可以使用解构赋值形式。</font>

## 4. 模板字符串

模板字符串（template string）是增强版的字符串，用反引号 ` 标识，特点：
- 字符串中可以出现换行符
- 可以使用 `${xxx}` 形式输出变量

```js
let name = 'jack';
console.log(`hello, ${name}`);
```

```js
let ul = `<ul>
    <li>apple</li>
    <li>banana</li>
    <li>peach</li>
    </ul>`
```

<font color=red>应用场景：当遇到字符串与变量拼接的情况使用模板字符串。</font>

## 5. 简化对象写法

ES6 允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

```js
let uname = 'rick';
let age = 30;
let sayHi = function () {
    console.log('Hi');
}
// 组建对象
const obj = {
    uname,
    age,
    sayHi() {
        console.log('Hi');
    }
}
```

<font color=red>应用场景：对象简写形式简化了代码，所以以后用简写就对了。</font>

## 6. 箭头函数

ES6 允许使用「箭头」`=>` 定义函数。

- `function` 写法：
    ```js
    function fn(param1, param2, …, paramN) { 
        // 函数体
        return expression; 
    }
    ```
- `=>` 写法：
    ```js
    let fn = (param1, param2, …, paramN) => {
        // 函数体
        return expression;
    }
    ```

箭头函数的 **注意点**:
- 如果形参只有一个，则小括号可以省略
- 函数体如果只有一条语句，则花括号可以省略，函数的返回值为该条语句的执行结果
- 箭头函数 `this` 始终指向声明时所在作用域下 `this` 的值
- 箭头函数不能作为构造函数实例化
- 不能使用 `arguments`

```js
// 省略小括号
let fn1 = n => {
    return n * n;
}

// 省略花括号
let fn2 = (a + b) => a + b;

// 箭头函数 this 始终指向声明时所在作用域下 this 的值
const obj = {
    a: 10,
    getA () {
        let fn3 = () => {
            console.log(this); // obj {...}
            console.log(this.a); // 10
        }
        fn3();
    }

}
```

案例1：箭头函数 `this` 始终指向声明时所在作用域下 `this` 的值，`call` 等方法无法改变其指向。
```js
let obj = {
    uname: 'rick',
    age: 30
};
let foo = () => {
    console.log(this);
}
let bar = function () {
    console.log(this);
}
// call 对箭头函数无效
foo.call(obj); // window
bar.call(obj); // obj {...}
```

案例2：筛选偶数
```js
let arr = [2, 4, 5, 10, 12, 13, 20];
let res = arr.filter(v => v % 2 === 0);
console.log(res); // [2, ,4 10, 12, 20]
```

案例3：点击 div两秒后变成粉色
- 方案1：使用 `_this` 保存 `div` 下的 `this`，从而设置 `div` 的 `style` 属性。
    ```js
    div.addEventListener('click', function () {
        let _this = this;
        setTimeout(function () {
            console.log(_this); // <div>...<div>
            _this.style.backgroundColor = 'pink';
        }, 2000)
    });
    ```

- 方案2：使用 `=>` 箭头函数
    ```js
    div.addEventListener('click', function () {
        setTimeout(() => {
            console.log(thid); // <div>...</div>
            this.style.backgroundColor = 'pink';
        }, 2000);
    });
    ```

## 7. 函数参数默认值设定

ES6 允许给函数参数设置默认值，当调用函数时不给实参，则使用参数默认值。  

具有默认值的形参，一般要靠后。
```js
let add = (x, y, z=3) => x + y + z;
console.log(add(1, 2)); // 6
```

可与解构赋值结合：
```js
function connect({ host = '127.0.0.1', uesername, password, port }) {
    console.log(host); // 127.0.0.1
    console.log(uesername);
    console.log(password);
    console.log(port);
}
connect({
    // host: 'docs.mphy.top',
    uesername: 'root',
    password: 'root',
    port: 3306
})
```

## 8. rest 参数

ES6 引入 rest 参数，用于获取函数的实参，用来代替 `arguments`，作用与 `arguments` 类似。将接收的参数序列转换为一个数组对象。

用在函数形参中，语法格式：`fn(a, b, ...args)`，写在参数列表最后面。
```js
let fn = (a, b, ...args) => {
    console.log(a);
    console.log(b);
    console.log(args);
};
fn(1,2,3,4,5);
/*
1
2
[3, 4, 5]
*/
```

案例1：求不定个数数字的和
```js
let add = (...args) => {
    let sum = args.reduce((pre, cur) => pre + cur, 0);
    return sum;
}
console.log(add(1, 2, 3, 4, 5)); // 15
```

<font color=red>应用场景：rest 参数非常适合不定个数参数函数的场景</font>

## 9. spread 扩展运算符

扩展运算符（`spread`）也是三个点（`...`）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列，对数组进行解包。可用在调用函数时，传递的实参，将一个数组转换为参数序列。  

扩展运算符也可以将对象解包。

展开数组：
```js
function fn(a, b, c) {
    console.log(arguments);
    console.log(a + b + c);
}
let arr = ['red', 'green', 'blue']; 
fn(...arr)
// [Arguments] { '0': 'red', '1': 'green', '2': 'blue' }
// redgreenblue
```

案例1：数组合并
```js
let A = [1, 2, 3];
let B = [4, 5, 6];
let C = [...A, ...B];
console.log(C); // [1, 2, 3, 4, 5, 6]
```

案例2：数组克隆  
这种数组克隆属于浅拷贝。
```js
let arr1 = ['a', 'b', 'c'];
let arr2 = [...arr1];
console.log(arr2); // ['a', 'b', 'c']
```

案例3：将伪数组转换为真实数组
```js
const divs = document.querySelectorAll('div');
let divArr = [...divs];
console.log(divArr);
```

案例4：对象合并
```js
// 合并对象
let obj1 = {
    a: 123
};
let obj2 = {
    b: 456
};
let obj3 = {
    c: 789
};
let obj = { ...obj1, ...obj2, ...obj3 };
console.log(obj);
// { a: 123, b: 456, c: 789 }
```

## 10. Symbol

### 10.1 Symbol 基本介绍与使用

ES6 引入了一种新的原始数据类型 `Symbol`，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，是一种类似于字符串的数据类型。  

JavaScript 的七种基本数据类型：
- 值类型（基本类型）：string、number、boolean、undefined、null、symbol
- 引用数据类型：object（包括了array、function）

Symbol 的特点：
- Symbol 的值是唯一的，用来解决命名冲突的问题
- Symbol 值不能与其他数据进行运算
- Symbol 定义的对象属性不能使用 `for...in` 循环遍历，但是可以使用 `Reflect.ownKeys` 来获取对象的所有键名

Symbol 的创建：

- 创建一个 `Symbol`：
    ```js
    let s1 = Symbol();
    console.log(s1, typeof s1);
    // Symbol() symbol
    ```
- 添加具有标识的 `Symbol`：
    ```js
    let s2 = Symbol('1');
    let s2_1 = Symbol('1');
    console.log(s2 === s2_1); 
    // false
    // Symbol 都是独一无二的
    ```
- 使用 `Symbol.for()` 方法创建，名字相同的 `Symbol` 具有相同的实体。
    ```js
    let s3 = Symbol.for('apple');
    let s3_1 = Symbol.for('apple');
    console.log(s3 === s3_1); // true
    ```
- 输出 `Symbol` 变量的描述，使用 `description` 属性
    ```js
    let s4 = Symbol('测试');
    console.log(s4.description); // 测试
    ```

### 10.2 对象添加 Symbol 类型的属性

案例：安全的向对象中添加属性和方法。  
分析：如果直接向对象中添加属性或方法，则原来对象中可能已经存在了同名属性或方法，会覆盖掉原来的。所以使用 `Symbol` 生成唯一的属性或方法名，可以更加安全的添加。  

代码实现：
```js
// 这是一个 game 对象，假设我们不知道里面有什么属性和方法
const game = {
    uname: '俄罗斯方块',
    up: function () { },
    down: function () { }
}

// 通过 Symbol 生成唯一的属性名，然后给 game 添加方法
let [up, down] = [Symbol('up'), Symbol('down')];
game[up] = function () {
    console.log('up');
}
game[down] = function () {
    console.log('down');
}

// 调用刚刚创建的方法
game[up]();
game[down]();
```

### 10.3 Symbol 内置值

除了定义自己使用的 Symbol 值以外，ES6 还提供了11 个内置的 Symbol 值，指向语言内部使用的方法。可以称这些方法为魔术方法，因为它们会在特定的场景下自动执行。

| 方法                         | 描述                                                                                                                 |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `Symbol.hasInstance`         | 当其他对象使用 `instanceof` 运算符，判断是否为该对象的实例时，会调用这个方法                                         |
| `Symbol.isConcatSpreadable ` | 对象的 `Symbol.isConcatSpreadable` 属性等于的是一个布尔值，表示该对象用于`Array.prototype.concat()` 时，是否可以展开 |
| `Symbol.species`             | 创建衍生对象时，会使用该属性                                                                                         |
| `Symbol.match`               | 当执行 `str.match(myObject)` 时，如果该属性存在，会调用它，返回该方法的返回值。                                      |
| `Symbol.replace `            | 当该对象被 `str.replace(myObject)` 方法调用时，会返回该方法的返回值。                                                |
| `Symbol.search `             | 当该对象被 `str.search(myObject)` 方法调用时，会返回该方法的返回值。                                                 |
| `Symbol.split `              | 当该对象被 `str.split(myObject)` 方法调用时，会返回该方法的返回值。                                                  |
| `Symbol.iterator `           | 对象进行` for...of` 循环时，会调用 `Symbol.iterator` 方法，返回该对象的默认遍历器                                    |
| `Symbol.toPrimitive `        | 该对象被转为原始类型的值时，会调用这个方法，返回该对象对应的原始类型值。                                             |
| `Symbol. toStringTag `       | 在该对象上面调用 `toString()` 方法时，返回该方法的返回值                                                             |
| `Symbol. unscopables `       | 该对象指定了使用 `with` 关键字时，哪些属性会被 `with` 环境排除。                                                     |

案例1：`Symbol.hasInstance` 方法判断是否属于这个对象时被调用。
```js
class A {
    static [Symbol.hasInstance]() {
        console.log('判断是否属于这个对象时被调用');
    }
}
let obj = {};
console.log(obj instanceof A
// 判断是否属于这个对象时被调用
// false
```


案例2：数组使用 `concat` 方法时，是否可以展开。
```js
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let arr3 = [4, 5, 6];
arr2[Symbol.isConcatSpreadable] = false;
console.log(arr1.concat(arr2));
// [ 1, 2, 3, [ 4, 5, 6, [Symbol(Symbol.isConcatSpreadable)]: false ] ]
console.log(arr1.concat(arr3));
// [ 1, 2, 3, 4, 5, 6 ]
```

## 11. 迭代器

### 11.1 定义

遍历器（`Iterator`）就是一种机制。它是一种接口，为各种不同的数据结构提
供统一的访问机制。任何数据结构只要部署 `Iterator` 接口，就可以完成遍历操作。

- ES6 创造了一种新的遍历命令 `for...of` 循环，`Iterator` 接口主要供 `for...of` 消费。
- 原生具备 `iterator` 接口的数据(可用for of 遍历)
    - `Array`
    - `Arguments`
    - `Set`
    - `Map`
    - `String`
    - `TypedArray`
    - `NodeList`

案例：使用 `next()` 方法遍历原生自带 `iterator` 接口的数据：
```js
// 遍历 Map
const mp = new Map();
mp.set('a', 1);
mp.set('b', 2);
mp.set('c', 3);
let iter1 = mp[Symbol.iterator]();
// next() 方法每执行一次，指针自增
console.log(iter1.next()); // { value: [ 'a', 1 ], done: false }
console.log(iter1.next()); // { value: [ 'b', 2 ], done: false }
console.log(iter1.next()); // { value: [ 'c', 3 ], done: false }
console.log(iter1.next()); // { value: undefined, done: true }
// 遍历数组
let xiyou = ['唐僧','孙悟空','猪八戒','沙僧'];
let iter2 = xiyou[Symbol.iterator]();
console.log(iter2.next()); // { value: '唐僧', done: false }
console.log(iter2.next()); // { value: '孙悟空', done: false }
console.log(iter2.next()); // { value: '猪八戒', done: false }
console.log(iter2.next()); // { value: '沙僧', done: false }
```

上面的案例只是为了证明他们自带 `iterator` 接口，实际上直接使用 `for...of` 方法遍历即可（`iterator` 接口为 `for...of`）服务。例如，可以使用 `for [k, v] of map` 来遍历 Map 数据结构中的键和值。
```js
const mp = new Map();
mp.set('a', 1);
mp.set('b', 2);
mp.set('c', 3);
for (let [k, v] of mp) {
    console.log(k, v);
}
/*
a 1
b 2
c 3
*/
```

### 11.2 工作原理

- 创建一个指针对象，指向当前数据结构的起始位置
- 第一次调用对象的 `next` 方法，指针自动指向数据结构的第一个成员
- 接下来不断调用 `next` 方法，指针一直往后移动，直到指向最后一个成员
- 每调用 `next` 方法返回一个包含 `value` 和 `done` 属性的对象

<font color=red>应用场景：需要自定义遍历数据的时候，要想到迭代器。</font>

### 11.3 自定义遍历数据

我们可以通过给数据结构添加自定义 `[Symbol.iterator]()` 方法来使该数据结构能够直接被遍历，从而使 `for...of` 能够直接遍历指定数据，达到为 `for...of` 服务的功能。

```js
// 需求：遍历对象中的数组
const xiaomi = {
    uname: '小明',
    course: [ '高数', '大物', '英语', '数据库' ],
    // 通过自定义 [Symbol.iterator]() 方法
    [Symbol.iterator]() {
        // 初始指针对象指向数组第一个
        let index = 0;
        // 保存 xiaomi 的 this 值
        let _this = this;
        return {
            next: function () {
                // 不断调用 next 方法，直到指向最后一个成员
                if (index < _this.course.length) {
                    return { value: _this.course[index++], done: false };
                } else {
                    // 每调用next 方法返回一个包含value 和done 属性的对象
                    return { value: undefined, done: true };
                }
            }
        }
    }
}
// for...of直接遍历达到目的
for (let v of xiaomi) {
    console.log(v);
}
```

## 12. Generator 生成器函数

### 12.1 生成器函数的声明和调用

生成器函数是 ES6 提供的一种 **异步编程解决方案**，语法行为与传统函数完全不同。  

- `*` 的位置没有限制
- 使用 `function * gen()` 和 `yield` 可以声明一个生成器函数。生成器函数返回的结果是迭代器对象，调用迭代器对象的 `next` 方法可以得到 `yield` 语句后的值。
- 每一个 `yield` 相当于函数的暂停标记，也可以认为是一个分隔符，每调用一次 `next()`，生成器函数就往下执行一段。
- `next` 方法可以传递实参，作为 `yield` 语句的返回值

例如以下生成器函数中，3 个 `yield` 语句将函数内部分成了 4 段。
```js
function* generator() {
    console.log('before 111'); // 生成器第 1 段
    yield 111;
    console.log('before 222'); // 生成器第 1 段
    yield 222;
    console.log('before 333'); // 生成器第 1 段
    yield 333;
    console.log('after 333'); // 生成器第 1 段
}
let iter = generator();
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
/*
before 111
{ value: 111, done: false }
before 222
{ value: 222, done: false }
before 333
{ value: 333, done: false }
after 333
{ value: undefined, done: true }
*/
```

### 12.2 生成器函数的参数传递

```js
function* generator(arg) {
    console.log(arg); // 生成器第 1 段
    let one = yield 111;
    console.log(one); // 生成器第 2 段
    let two = yield 222;
    console.log(two); // 生成器第 3 段
    let three = yield 333; 
    console.log(three); // 生成器第 4 段
}

let iter = generator('aaa'); // 传给生成器第 1 段
console.log(iter.next());
console.log(iter.next('bbb')); // 传给生成器第 2 段，作为这一段开始的 yield 语句返回值
console.log(iter.next('ccc')); // 传给生成器第 3 段，作为这一段开始的 yield 语句返回值
console.log(iter.next('ddd')); // 传给生成器第 4 段，作为这一段开始的 yield 语句返回值
/*
aaa
{ value: 111, done: false }
bbb
{ value: 222, done: false }
ccc
{ value: 333, done: false }
ddd
{ value: undefined, done: true }
*/
```

### 12.3 生成器函数案例

案例1：1s后输出111，2s后输出222，3s后输出333  
-  传统方式：嵌套太多，代码复杂，产生 **回调地狱**。
    ```js
    setTimeout(() => {
        console.log(111);
        setTimeout(() => {
            console.log(222);
            setTimeout(() => {
                console.log(333);
            }, 3000);
        }, 2000);
    }, 1000);
    ```
- 生成器实现：结构简洁明了
    ```js
    function one() {
        setTimeout(() => {
            console.log(111);
            iter.next();
        }, 1000);
    }

    function two() {
        setTimeout(() => {
            console.log(222);
            iter.next();
        }, 2000);
    }

    function three() {
        setTimeout(() => {
            console.log(333);
        }, 3000);
    }

    function* generator() {
        yield one();
        yield two();
        yield three();
    }

    let iter = generator();
    iter.next();
    ```

案例2：生成器函数模拟每隔1s获取商品数据

```js
function getUsers() {
    setTimeout(() => {
        let data = '用户数据';
        iter.next(data); // 传参给生成器函数的第 2 段，后面类似
    }, 1000);
}

function getOrders() {
    setTimeout(() => {
        let data = '订单数据';
        iter.next(data);
    }, 1000);
}

function getGoods() {
    setTimeout(() => {
        let data = '商品数据';
        iter.next(data);
    }, 1000);
}

function* generator() {
    let users = yield getUsers();
    console.log(users);
    let orders = yield getOrders();
    console.log(orders);
    let goods = yield getGoods();
    console.log(goods);
}

let iter = generator();
iter.next();
```

## 13. Promise

### 13.1 Promise 的定义和使用

`Promise` 是 ES6 引入的异步编程的新解决方案。语法上 Promise 是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果。  

一个 `Promise` 必然处于以下几种状态之一：
- 待定（`pending`）：初始状态，既没有被兑现，也没有被拒绝。
- 已兑现（`fulfilled`）：意味着操作成功完成。
- 已拒绝（`rejected`）：意味着操作失败。

`Promise` 的使用：
- Promise 构造函数：`new Promise((resolve, reject)=>{})`
- `Promise.prototype.then` 方法
- `Promise.prototype.catch` 方法

一个简单案例：
```js
let p = new Promise(function (resolve, reject) {
    // 使用 setTimeout 模拟请求数据库数据操作
    setTimeout(function () {
        // 这个异步请求数据库数据操作是否正确返回数据
        let isRight = true;
        if (isRight) {
            let data = '数据库中的数据';
            // 设置 Promise 对象的状态为操作成功
            resolve(data);
        } else {
            let err = '数据读取失败！'
            // 设置 Promise 对象的状态为操作失败
            reject(err);
        }
    }, 1000);
});
p.then(function (value) {
    console.log(value);
}, function (reason) {
    console.error(reason);
})
```

### 13.2 Promise 封装读取文件

```js
// 使用 nodejs 的 fs 读取文件模块
const fs = require('fs');

const p = new Promise(function (resolve, reject) {
    fs.readFile('./resources/为学.txt', (err, data) => {
        // err 是一个异常对象
        if (err) reject(err);
        resolve(data);
    })
})

p.then(function (value) {
    // 转为字符串输出
    console.log(value.toString());
}, function (reason) {
    console.log('读取失败!!');
})
```

### 13.3 Promise 封装 Ajax 请求

```js
const p = new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open('get', 'https://api.apiopen.top/getJoke');
    xhr.send();
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
            if (xhr.status >= 200 && xhr.status < 300) {
                // 成功
                resolve(xhr.response);
            } else {
                // 失败
                reject(xhr.status);
            }
        }
    }
});

// 指定回调
p.then(function (value) {
    console.log(value);
}, function (reason) {
    console.error(reason);
})
```

### 13.4 Promise.prototype.then 方法

先复习一下一个 `Promise` 的三种状态：
- 待定（`pending`）：初始状态，既没有被兑现，也没有被拒绝。
- 已兑现（`fulfilled`）：意味着操作成功完成。
- 已拒绝（`rejected`）：意味着操作失败。

`Promise.prototype.then` 方法返回的结果依然是 `Promise` 对象，**对象状态由回调函数的执行结果决定**。

具体情况如下：
- 若 `then` 方法没有返回值，则 `then` 方法返回的对象的状态值为成功 `fulfilled`，返回结果值为 `undefined`。
    ```js
    const p = new Promise((resolve, reject) => {
        setTimeout(() => {
            // resolve('用户数据')
            reject('出错了');
        }, 1000);
    })
    // 未设定返回值
    const res = p.then((value) => {
        console.log(value);
    }, (reason) => {
        console.warn(reason);
    })
    // 打印 then 方法的返回值
    console.log(res);
    ```
    打印的结果：
    ![es6-3](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/es6-3.504usmc4kes0.png)
- 如果回调函数中返回的结果是非 `Promise` 类型的属性，则 `then` 方法返回的对象，其状态为成功（`fulfilled`），返回结果值取决于 `then` 方法所执行的是哪个函数（`resolve` 或 `reject`）。
    ```js
    const p = new Promise((resolve, reject) => {
        setTimeout(() => {
            // resolve('用户数据')
            reject('出错了');
        }, 1000);
    })
     // 返回的非 Promise 对象
    const res = p.then((value) => {
        console.log(value);
        return '成功了！！';
    }, (reason) => {
        console.warn(reason);
        return '出错啦！！'
    })
    // 打印 then 方法的返回值
    console.log(res);
    ```
    打印结果：
    ![es6-4](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/es6-4.2xdcb1x8jya0.png)
- 如果回调函数中返回的结果是 `Promise` 类型（`return new Promise()`），则 `then` 方法返回的 `Promise` 对象状态与该返回结果的状态相同，返回值也相同。
    ```js
    const p = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('用户数据')
            // reject('出错了');
        }, 1000);
    })
    const res = p.then((value) => {
        console.log(value);
        // 返回 Promise 对象
        return new Promise((resolve, reject) => {
            resolve('（1）成功了！！！');
            // reject('（1）出错了！！！')
        })
    }, (reason) => {
        console.warn(reason);
        return new Promise((resolve, reject) => {
            // resolve('（2）成功了！！！');
            reject('（2）出错了！！！')
        })
    })
    // 打印 then 方法的返回值
    console.log(res);
    ```
    打印结果：
    ![es6-5](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/es6-5.6z1msm3xzpc0.png)
- 如果回调函数中返回的结果是 `throw` 语句抛出异常，则 `then` 方法的对象的状态值为 `rejected`，返回结果值为 `throw` 抛出的字面量或者 `Error` 对象。
    ```js
    const p = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('用户数据');
        }, 1000);
    });
    const res = p.then((value) => {
        console.log(value);
        return new Promise((resolve, reject) => {
            throw new Error('错误了！！');
        })
    });
    // 打印结果
    console.log(res);
    ```
    打印结果如下：
    ![es6-6](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/es6-6.2c3aibc6l05c.png)

### 13.4 链式调用

`Promise.prototype.then` 方法返回的结果还是 `Promise` 对象，这意味着我们可以继续在该结果上使用 `then` 方法，也就是链式调用。

```js
const p = new Promise(resolve=>{}, reject=>{});
p.then(value=>{}, reason=>{})
.then(value=>{}, reason=>{})
.then(value=>{}, reason=>{})
...
```

### 13.5 链式调用练习-多个文件读取

```js
const fs = require('fs');

let p = new Promise((resolve, reject) => {
    fs.readFile('./resources/users.md', (err, data) => {
        // 传给下一轮文件读取操作
        resolve(data);
    })
});

p.then(value => {
    return new Promise((resolve, reject) => {
        // value 为第一次读取的文件数据，data 为第二次（当前）读取的数据
        fs.readFile('./resources/orders.md', (err, data) => {
            // 将上轮读取结果和本轮合并传到下一轮轮读取操作
            resolve([value, data]);
        });
    });
}).then(value => {
    return new Promise((resolve, reject) => {
        fs.readFile('./resources/goods.md', (err, data) => {
            // value 为上一轮传递过来的文件数据数组
            value.push(data);
            // 传给下一轮操作
            resolve(value);
        });
    });
}).then(value => {
    // 合并数组元素，输出
    console.log(value.join('\n'));
});
```

### 13.6 Promise.prototype.catch

`catch()` 方法返回一个 `Promise`，并且处理拒绝的情况。它的行为与调用 `Promise.prototype.then(undefined, onRejected)` 相同。

即：
```js
obj.catch(onRejected);
```
等同于：
```js
obj.then(undefined, onRejected);
```

语法：
```js
p.catch(onRejected);

p.catch(function(reason) {
   // 拒绝
});
```

举例：
```js
var p1 = new Promise(function (resolve, reject) {
    resolve('Success');
});

p1.then(function (value) {
    console.log(value); // "Success!"
    throw 'oh, no!';
}).catch(function (e) {
    console.log(e); // "oh, no!"
}).then(function () {
    console.log('有 catch 捕获异常，所以这句输出');
}, function () {
    console.log('没有 catch 捕获异常，这句将不会输出');
});
```
输出结果：
```
Success
oh, no!
有 catch 捕获异常，所以这句输出
```

> 以上只是 Promise 的入门，更多还要进一步深入学习。

## 14. Set

### 14.1 Set 的定义和使用

ES6 提供了新的数据结构 `Set`（集合）。它类似于数组，但 **成员的值都是唯一的**，集合实现了 `iterator` 接口，所以可以使用『扩展运算符』和『`for...of`』进行遍历。  

定义一个 Set 集合：
```js
let st1 = new Set();
let st2 = new Set([可迭代对象]);
```

集合（这里假设有一个集合 `st`）的属性和方法：

- `st.size`：返回集合个数
- `st.add(item)`：往集合中添加一个新元素 `item`，返回当前集合
- `st.delete(item)`：删除集合中的元素，返回 `boolean` 值
- `st.has(item)`：检测集合中是否包含某个元素，返回 `boolean` 值
- `st.clear()`：清空集合
- 集合转为数组：`[...st]`
- 合并两个集合：`[...st1, ...st2]`

### 14.2 集合案例

案例1： 数组去重
```js
let arr1 = [1, 2, 2, 3, 3, 3, 4, 1, 2];
let res1 = [...new Set(arr1)];
console.log(res1); // [ 1, 2, 3, 4 ]
```

案例2：数组求交集
```js
let arr2_1 = [1, 2, 2, 3, 4, 5];
let arr2_2 = [3, 6, 6, 7, 1, 4];
let res2 = arr2_1.filter(v => new Set(arr2_2).has(v))
console.log(res2); // [ 1, 3, 4 ]
```

案例3：数组求并集
```js
let arr3_1 = [1, 2, 2, 3, 4, 5];
let arr3_2 = [3, 6, 6, 7, 1, 4];
let res3 = [...new Set([...arr3_1, ...arr3_2])];
console.log(res3); // [ 1, 2, 3, 4, 5, 6, 7 ]
```

案例4：数组求差集
```js
let arr4_1 = [1, 2, 2, 3, 4, 5];
let arr4_2 = [3, 6, 6, 7, 1, 4];
let res4 = [...new Set(arr4_1)].filter(v => !(new Set(arr4_2).has(v)))
console.log(res4); // [ 2, 5 ]
```

## 15. Map

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合。但是 “键” 的范围不限于字符串，各种类型的值（包括对象）都可以当作键。Map 也实现了 iterator 接口，所以可以使用『扩展运算符』和『for...of』进行遍历。

定义一个 Map：
```js
let mp1 = new Map();
mp1.set('aaa', 111);
mp1.set('bbb', 222);
mp1.set('ccc', 333);

let mp2 = new Map([
    ['aaa', 111],
    ['bbb', 222],
    ['ccc', 333]
]);

console.log(mp1['aaa']); // 111
console.log(mp2.get('bbb')); // 222
```

Map 的属性和方法：（`k` 为键，`v`为值）
- `size`：返回 Map 的元素（键值对）个数
- `set(k, v)`：增加一个键值对，返回当前 Map
- `get(k)`：返回键值对的键值
- `has()`：检测 Map 中是否包含某个元素
- `clear()`：清空集合，返回 `undefined`

## 16. class 类

这部分在 JS 高级也涉及，故可以前往 [JS 高阶 class](https://docs.mphy.top/#/JS-Advance/ch01) 学习。，那部分的笔记更加详细，有原理。所以这一节后面部分只给出例子。  

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过class 关键字，可以定义类。基本上，ES6 的 `class` 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 `class` 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

### 16.1 复习 ES5 function 构造函数 的继承

> 具体知识点可以前往：[JS高级](https://docs.mphy.top/#/JS-Advance/ch02)

```js
//手机
function Phone(brand, price){
    this.brand = brand;
    this.price = price;
}

Phone.prototype.call = function(){
    console.log("我可以打电话");
}

//智能手机
function SmartPhone(brand, price, color, size){
    Phone.call(this, brand, price);
    this.color = color;
    this.size = size;
}

//设置子级构造函数的原型
SmartPhone.prototype = new Phone;
// 矫正 constructor 指向
SmartPhone.prototype.constructor = SmartPhone;

//声明子类的方法
SmartPhone.prototype.photo = function(){
    console.log("我可以拍照")
}

SmartPhone.prototype.playGame = function(){
    console.log("我可以玩游戏");
}

const chuizi = new SmartPhone('锤子',2499,'黑色','5.5inch');

console.log(chuizi);
```

### 16.2 extends 类继承和方法的重写

ES6 中直接使用 `extends` 语法糖（更简洁高级的实现方式）来实现继承，同时可以重写父类的方法，直接在子类中重新写一次要重写的方法即可覆盖父类方法。

```js
class Phone{
    //构造方法
    constructor(brand, price){
        this.brand = brand;
        this.price = price;
    }
    //父类的成员属性
    call(){
        console.log("我可以打电话!!");
    }
}

class SmartPhone extends Phone {
    //构造方法
    constructor(brand, price, color, size){
        super(brand, price);// Phone.call(this, brand, price)
        this.color = color;
        this.size = size;
    }

    photo(){
        console.log("拍照");
    }

    // 方法的重写
    call(){
        console.log('我可以进行视频通话');
    }
}

const xiaomi = new SmartPhone('小米',799,'黑色','4.7inch');
xiaomi.call();
xiaomi.photo();
```

### 16.3 getter 和 setter

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

## 17. 数值扩展

1. `Number.EPSILON` 是 JavaScript 表示的最小精度，一般用来处理浮点数运算。例如可以用于两个浮点数的比较。
    ```js
    let equal = (x, y) => Math.abs(x - y) < Number.EPSILON;
    console.log(0.1 + 0.2 === 0.3); // false
    console.log(equal(0.1 + 0.2, 0.3)); // true
    ```

2. 二进制和八进制：二进制以 `0b` 开头，八进制以 `0o` 开头。
    ```js
    let b = 0b1010;
    let o = 0o777;
    let d = 100;
    let x = 0xff;
    console.log(x);
    ```

3. `Number.isFinite` 检测一个数值是否为有限数。
    ```js
    console.log(Number.isFinite(100)); // false
    console.log(Number.isFinite(100 / 0)); // true
    console.log(Number.isFinite(Infinity)); // false
    ```

4. Number.parseInt 和 Number.parseFloat  
    ES6 给 `Number` 添加了 `parseInt` 方法，`Number.parseInt` 完全等同于 `parseInt`。将字符串转为整数，或者进行进制转换。`Number.parseFloat` 则等同于 `parseFloat()`
    ```js
    Number.parseInt === parseInt; // true
    Number.parseFloat === parseFloat; // true
    ```
    ```js
    Number.parseInt(s, base);
    ```
    - `s`：待转换的字符串
    - `base`：进位制的基数
    ```js
    console.log(Number.parseInt('5211314love')); // 5211314
    console.log(Number.parseFloat('3.1415926神奇')); // 3.1415926
    ```

5. `Number.isInteger()` 判断一个数是否为整数。
    ```js
    console.log(Number.isInteger(5)); // true
    console.log(Number.isInteger(2.5)); // false
    ```

6. `Math.trunc()` 将数字的小数部分抹掉。
    ```js
    console.log(Math.trunc(3.5)); // 3
    ```

7. `Math.sign` 判断一个数到底为正数 负数 还是零

## 18. 对象方法扩展

ES6 新增了一些 `Object` 对象的方法。
- Object.is 比较两个值是否严格相等，与『===』行为 **基本一致**
- `Object.assign` 对象的合并，将源对象的所有可枚举属性，复制到目标对象
- `__proto__`、`setPrototypeOf`、`setPrototypeOf` 可以直接设置对象的原型

### 18.1 Object.is()

`Object.is()` 方法判断两个值是否完全相同。`Object.is` 比较两个值是否严格相等，与 `===` 行为 **基本一致**。返回一个 `Boolean` 类型。
```js
Object.is(value1, value2);
```

`Object.is()` 方法判断两个值是否为同一个值。如果满足以下条件则两个值相等：
- 都是 `undefined`
- 都是 `null`
- 都是 `true` 或 `false`
- 都是相同长度的字符串且相同字符按相同顺序排列
- 都是相同对象（意味着每个对象有同一个引用）
- 都是数字且
    - 都是 `+0`
    - 都是 `-0`
    - 都是 `NaN`
    - 或都是非零而且非 `NaN` 且为同一个值

与 `==` 运算不同。 `==` 运算符在判断相等前对两边的变量（如果它们不是同一类型）进行强制转换 (这种行为的结果会将 `"" == false` 判断为 `true`)，而 `Object.is` 不会强制转换两边的值。  

与 `===`算也不相同。 === 运算符 (也包括 `==` 运算符) 将数字 `-0` 和 `+0` 视为相等，而将 `Number.NaN` 与 `NaN` 视为不相等。

### 18.2 Object.assign

`Object.assign` 对象的合并，相当于浅拷贝。

```js
const config1 = {
    host: 'localhost',
    port: 3306,
    name: 'root',
    pass: 'root',
    test: 'test'
};
const config2 = {
    host: 'http://atguigu.com',
    port: 33060,
    name: 'atguigu.com',
    pass: 'iloveyou',
    test2: 'test2'
}
console.log(Object.assign(config1, config2));
```

### 18.3 Object.setPrototypeOf 和 Object.getPrototypeof

`Object.setPrototypeOf` 用于设置对象的原型对象，`Object.getPrototypeof` 用于获取对象的原型对象，相当于 `__proto__`。
```js
const school = {
    name: '尚硅谷'
}
const cities = {
    xiaoqu: ['北京','上海','深圳']
}
Object.setPrototypeOf(school, cities);
console.log(Object.getPrototypeOf(school));
console.log(school);
```

## 19. ES6 模块化

模块化是指将一个大的程序文件，拆分成许多小的文件，然后将小文件组合起来。

### 19.1 模块化的好处

模块化的优势有以下几点：
- 防止命名冲突
- 代码复用
- 高维护性

### 19.2 模块化规范产品

ES6 之前的模块化规范有：
- CommonJS => NodeJS、Browserify
- AMD => requireJS
- CMD => seaJS

### 19.3 ES6 模块化语法

模块功能主要由两个命令构成：`export` 和 `import`。
- `export` 命令用于规定模块的对外接口
- `import` 命令用于输入其他模块提供的功能

#### 19.3.1 模块导出数据语法

1. 单个导出
    ```js
    // 单个导出
    export let uname = 'Rick';
    export let sayHello = function () {
        console.log('Hi, bro!');
    }
    ```
2. 合并导出
    ```js
    let uname = 'Rick';
    let sayHello = function () {
        console.log('Hi, bro!');
    }
    // 合并导出
    export { uname, sayHello };
    ```
3. 默认导出
    ```js
    // 默认导出
    export default {
        uname: 'Rick',
        sayHello: function () {
            console.log('Hi, bro!');
        }
    }
    ```

#### 19.3.2 模块导入数据语法

1. 通用导入方式
    ```js
    import * as m1 from './js/m1.js';
    import * as m2 from './js/m2.js';
    import * as m3 from './js/m3.js';
    ```

2. 解构赋值导入
    ```js
    import { uname, sayHello } from './js/m1.js';
    // 有重复名可以设置别名
    import { uname as uname2, sayHello as sayHello2 } from './js/m2.js';
    console.log(uname);
    // 配合默认导出
    import {default as m3} from "./src/js/m3.js";
    ```

3. 简便方式导入，针对默认暴露
    ```js
    import m3 from "./src/js/m3.js";
    ```

#### 19.3.3 ES6 使用模块化方式二

将文件导入都写进一个 app.js 文件中，然后在里面写入要导入的模块。app.js 中的内容如下：
```js
import * as m1 from './js/m1.js';
import * as m2 from './js/m2.js';
import * as m3 from './js/m3.js';

console.log(m1);
console.log(m2);
console.log(m3);
```
在 index.html 中引入 app.js 文件内容：
```html
<script src="./app.js" type="module"></script>
```

### 19.4 使用 babel 对模块化代码转换

有的浏览器不支持 ES6 语法，这时候就需要使用 babel 来将其转换成 ES5 等价语法。

1. 安装工具
    ```
    npm i babel-cli babel-preset-env browserify(webpack) -D
    ```
2. 编译
    ```
    npx babel src/js -d dist/js --presets=babel-preset-env
    ```
3. 打包
    ```
    npx browserify dist/js/app.js -o dist/bundle.js
    ```

### 19.5 ES6 模块化引入 npm 安装的包

```
npm install jquery
```
再通过 `import` 导入即可。
![es6-7](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/es6-7.216iomdsx9mo.png)

# （三）ECMASript 7 新特性

## 1. Array.prototype.includes

`includes` 方法用来检测数组中是否包含某个元素，返回布尔类型值。
```js
let arr1 = [1, 2, 2, 3, 3, 3, 4, 1, 2];
console.log(arr1.includes(2));
```


## 2. 指数运算符

在 ES7 中引入指数运算符 `**`，用来实现幂运算，功能与 `Math.pow(a, b)` 结果相同。

```js
2 ** 3 // 8
Math.pow(2, 3) // 8
```

# （四）ECMAScript 8 新特性

## 1. async 和 await

`async` 和 `await` 两种语法结合可以让异步代码像同步代码一样。（即：看起来是同步的，实质上是异步的。）

先从字面意思理解，`async` 意为异步，可以用于声明一个函数前，该函数是异步的。`await` 意为等待，即等待一个异步方法完成。

### 1.1 async

`async` 声明（`function`）的函数成为 async 函数，语法：
```js
async function funcName() {
    //statements 
}
```
`async` 内部可以使用 `await`，也可以不使用。
`async` 函数的返回值是一个 `Promise` 对象，因此执行这个函数时，可以使用 `then` 和 `catch` 方法。
根据 **函数体内部** 的返回值， `async` 函数返回值具体情况如下：
- 函数体内不返回任何值，则 `async` 函数返回值为一个成功（`fulfilled`）的 `Promise` 对象，状态值为 `undefined`。
  ```js
  let a = async function() {}
  let res = a()
  console.log(res)
  // Promise{<fullfilled>: undefined}
  ```
- 返回结果不是一个 `Promise` ，则 `async` 函数返回值为一个成功（`fulfilled`）的 `Promise` 对象，状态值为这个内部返回值。
  ```js
  let a = async function () {
    return 'hello'
  }
  let res = a()
  console.log(res) 
  // Promise{<fullfilled>: 'hello'}
  ```
- 内部抛出错误，则 `async` 函数返回值为一个失败的 `Promise` 对象。
  ```js
  let a = async function foo() {
    throw new Error('出错了')
  }
  a().catch(reason => {
    console.log(reason)
  })
  ```
- 若函数内部返回值是一个 `Promise` 对象，则 `async` 函数返回值的状态取决于这个 `Promise` 对象。
  ```js
  let a = async function () {
    return new Promise((resolve, reject) => {
      resolve("成功")
    })
  }
  a().then(value => {
    console.log(value)
  })
  ```

### 1.2 await

`await` 相当于一个运算符，右边接一个值。一般为一个 `Promise` 对象，也可以是一个非 `Promise` 类型。当右接一个非 `Promise` 类型，`await` 表达式返回的值就是这个值；当右接一个 `Promise` 对象，则 `await` 表达式会阻塞后面的代码，等待当前 `Promise` 对象 `resolve` 的值。

综合 `async` 和 `await` 而言。`await` 必须结合 `async` 使用，而 `async` 则不一定需要 `await`。 `async` 会将其后的函数的返回值封装成一个 `Promise` 对象，而 `await` 会等待这个 `Promise` 完成，然后返回 `resolve` 的结果。当这个 `Promise` 失败或者抛出异常时，需要时使用 `try-catch` 捕获处理。

`Promise` 使用链式调用解决了传统方式回调地狱的问题，而 `async-await` 又进一步优化了代码的可读性。

```js
const p = new Promise((resolve, reject)=>{
  resolve('成功')
})
async function main() {
  let res = await p
  console.log(res)
}
main()
// '成功'
```
```js
const p = new Promise((resolve, reject)=>{
  reject('失败')
})
async function main() {
  try {
    let res = await p
    console.log(res)
  } catch(e) {
    console.log(e)
  }
}
main()
// '失败'
```

### 1.3 综合应用-读取文件

需求：先读取用户数据 user，然后读取订单数据 order，最后读取商品数据 goods。

对于这种异步操作很容易想到使用 `Promise`，代码如下：
```js
const fs = require('fs')

let p = new Promise((resolve, reject) => {
  fs.readFile('./files/user.md', (err, data) => {
    if (err) reject(err)
    resolve(data)
  })
})

p.then(value => {
  return new Promise((resolve, rejecet) => {
    fs.readFile('./files/order.md', (err, data) => {
      if (err) rejecet(err)
      resolve([value, data])
    })
  })
}, reason => {
  console.log(reason)
}).then(value => {
  return new Promise((resolve, reject) => {
    fs.readFile('./files/goods.md', (err, data) => {
      if (err) reject(err)
      value.push(data)
      resolve(value)
    })
  })
}, reason => {
  console.log(reason)
}).then(value => {
  console.log(value.join('\n'))
}, reason => {
  console.log(reason)
})
```
但是，使用 `Promise` 链式调用虽然避免了回调地狱，但这种链式调用过多难免引起代码复杂，看起来不直观。可以使用 `async` 和 `await` 方法优化，代码如下：
```js
const fs = require('fs')

function readUser() {
  return new Promise((resolve, reject) => {
    fs.readFile('./files/user.md', (err, data) => {
      if (err) reject(err)
      resolve(data)
    })
  })
}

function readOrder() {
  return new Promise((resolve, reject) => {
    fs.readFile('./files/order.md', (err, data) => {
      if (err) reject(err)
      resolve(data)
    })
  })
}

function readGoods() {
  return new Promise((resolve, reject) => {
    fs.readFile('./files/goods.md', (err, data) => {
      if (err) reject(err)
      resolve(data)
    })
  })
}

async function read() {
  let user = await readUser()
  let order = await readOrder()
  let goods = await readGoods()
  console.log([user, order, goods].join('\n'))
}

read()
```
这样，代码看起来很直观，就好像是同步代码一样，实际上是异步操作。

### 1.4 综合应用-封装ajax

```js
function sendAjax(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest()
    xhr.open('get', url)
    xhr.send()
    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4) {
        if (xhr.status >= 200 && xhr.status < 300) {
          resolve(JSON.parse(xhr.response))
        }
        reject(xhr.status)
      }
    }
  })
}

async function main() {
  let res = await sendAjax('http://poetry.apiopen.top/sentences')
  let poem = res.result.name + '——' + res.result.from
  document.body.innerText = poem
}

main()
```

这里封装的ajax还不能体现 `async-await` 的作用所在，因为没有出现多个 ajax 请求。在又多个 ajax 请求并且后续的请求依赖于前一个请求的结果的时候，`async-await` 的优点就体现出来了。

## 2. Object.values 和 Object.entries

- `Object.values()` 方法返回一个给定对象的所有可枚举属性值的数组，类似于 `Object.keys()`，只是前者返回属性值，后者返回键值组合的数组。
  ```js
  let obj = {
    a: 1,
    b: {1:2},
    c: [1,2,3]
  }
  console.log(Object.values(obj))
  // [1, {1: 2}, [1,2,3]]
  console.log(Object.keys(obj))
  // ['a', 'b', 'c']
  ```
- `Object.entries()` 方法返回一个给定对象自身可遍历属性 `[key,value]` 的数组（数组元素也是一个个的数组的数组）
  ```js
  const obj = {a: 1, b: 2, c: 3};
  console.log(Object.entries(obj))
  // [ [ 'a', 1 ], [ 'b', 2 ], [ 'c', 3 ] ]
  ```
  返回的是一个数组，这样就可以使用 `for...of` 遍历了。
  ```js
  const obj = { a: 1, b: 2, c: 3 };
  for (let [k, v] of Object.entries(obj)) {
    console.log(k, v)
  }
  ````



# （六）ECMAScript 10 新特性

## 1. Object.fromEntries

Object.fromEntries() 方法把可迭代对象的键值对列表转换为一个对象。  
语法：
```js
Object.fromEntries(iterable)
```
- `iterable`：类似 Array 、 Map 或者其它实现了可迭代协议的可迭代对象。
- 返回值：一个由该迭代对象条目提供对应属性的新对象。
- 相当于 `Object.entries` （ES8）的逆运算。

```js
const mp = new Map([
  [1, 2],
  [3, 4]
])
const obj = Object.fromEntries(mp)
console.log(obj)
// { '1': 2, '3': 4 }
```
```js
const arr = [[1, 2]]
console.log(Object.fromEntries(arr))
// {'1': 2}
```

## 2. trimStart() 和 trimEnd()

- `trimStart()` 去除字符串开头连续的空格（`trimLeft` 是此方法的别名）
- `trimEnd()` 去除字符串末尾连续的空格（`trimRight` 是此方法的别名）

## 3. Array.prototype.flat 和 Array.prototype.flatMap

- `Array.prototype.flat(i)`：展平一个多维数，`i` 为要展开的层数，默认为1，即展开一层。
  ```js
  let arr1 = [1, [2, 3], [4, 5]]
  console.log(arr1.flat(1)) 
  // [1,2,3,4,5]
  let arr2 = [1, [2, 3, [4, 5]]]
  console.log(arr2.flat(2))
  // [1,2,3,4,5]
  ```
  使用 `Infinity` 作为深度，展开任意深度的嵌套数组
  ```js
  [1, [2, 3, [4, 5]]].flat(Infinity)
  // [1, 2, 3, 4, 5, 6]
  ```
  也可以使用 `flat` 来去除数组空项
  ```js
  let arr = [1,2,3,,4]
  arr.flat() // [1,2,3,4]
  ```
- `Array.prototype.flatMap`：相当于 `map` 和 `flat` 的结合，方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。
  ```js
  let arr = [1,2,3,4]
  let res1 = arr.map(x => [x ** 2])
  console.log(res1)
  // [[1],[4],[9],[16]]
  let res2 = arr.flatMap(x => [x ** 2])
  console.log(res2)
  // [1,4,9,16]
  ```

## 4. Symbol.prototype.description

使用 `Symbol()` 创建的 `Symbol` 字面量，可以直接使用 `description` 获取该字面量的描述。
```js
let sym = Symbol('hello')
console.log(sym.description)
// hello
```


# （七）ECMAScript 11 新特性

## 1. 类的私有属性

ES11 提供了类的私有属性，在类的外部无法访问该属性。只有再类的内部能访问。

```js
class Person{
  //公有属性
  name;
  //私有属性
  #age;
  #weight;
  //构造方法
  constructor(name, age, weight){
    this.name = name;
    this.#age = age;
    this.#weight = weight;
  }

  intro(){
    console.log(this.name);
    console.log(this.#age);
    console.log(this.#weight);
  }
}

//实例化
const girl = new Person('晓红', 18, '45kg');

// 外部无法直接访问
// console.log(girl.name);
// console.log(girl.#age);
// console.log(girl.#weight);

girl.intro();
```

## 2. allSettled

该 `Promise.allSettled()` 方法返回一个在所有给定的 `promise` 都已经 `fulfilled` 或 `rejected` 后的 `promise`，并带有一个对象数组，每个对象表示对应的 `promise` 结果。`allSettled` 方法返回的 `Promise` 对象始终是成功（`fulfilled`）的。  
使用场景：
- 有多个彼此不依赖的异步任务成功完成时使用。
- 想得到每个 `promise` 的结果时使用。

对比于 `Promise.all()`，`all()` 也接受一个 `Promise` 对象数组参数，只要有一个失败（`rejected`），那么返回的  `Promise` 对象就是失败（`rejected`）的。  
使用场景：
- 传进去的 `Promise` 对象彼此依赖，且需要在其中任何一个失败的时候停止。

两个 `Promise` 都是成功的情况：
```js
let p1 = new Promise((resolve, reject) => {
  resolve('用户数据-1')
})

let p2 = new Promise((resolve, reject) => {
  resolve('订单数据-2')
})

let res1 = Promise.allSettled([p1, p2])
let res2 = Promise.all([p1, p2])
console.log(res1)
console.log(res2)
```
输出结果：
![es11-1](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/es11-1.2fgw7vvkb0kk.png)

一个成功，一个失败：
```js
let p1 = new Promise((resolve, reject) => {
  resolve('用户数据-1')
})

let p2 = new Promise((resolve, reject) => {
  reject('失败了')
})

let res1 = Promise.allSettled([p1, p2])
let res2 = Promise.all([p1, p2])
console.log(res1)
console.log(res2)
```
打印结果：
![ES11-2](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/ES11-2.17q27y7sy9mk.png)

## 3. matchAll

`matchAll()` 方法返回一个包含所有匹配正则表达式的结果及分组捕获组的迭代器。

```js
const regexp = /t(e)(st(\d?))/g;
const str = 'test1test2';

const array = [...str.matchAll(regexp)];

console.log(array[0]);
// expected output: Array ["test1", "e", "st1", "1"]

console.log(array[1]);
// expected output: Array ["test2", "e", "st2", "2"]
```

## 4. 可选链

### 4.1 定义

可选链 `?.` 是一种访问嵌套对象属性的安全的方式。即使中间的属性不存在，也不会出现错误。  
原则：如果可选链 `?.` 前面的部分是 `undefined` 或者 `null`，它会停止运算并返回该部分。

```js
let user = {
  address: {
  }
}
console.log( user?.address?.street ); // undefined（不报错）
```

### 4.2 短路效应

短路效应：正如前面所说的，如果 `?.` 左边部分不存在，就会立即停止运算（“短路效应”）。所以，如果后面有任何函数调用或者副作用，它们均不会执行。  
这有和 `&&` 的作用类似，但上述改用 `&&` 会显得代码冗余度高：
```js
console.log(user && user.address && user.address.street)
```



### 4.3 其它变体：?.()，?.[]

可选链 `?.` 不是一个运算符，而是一个特殊的语法结构。它还 **可以与函数和方括号一起使用**。  
例如，将 `?.()` 用于调用一个可能不存在的函数（即使不存在也不报错）。
```js
function foo() {
  console.log('hello')
}
foo?.()
// hello
```
`?.[]` 允许从一个可能不存在的对象上安全地读取属性。（即使不存在也不报错）。
```js
let obj = {
  key: 123
}
console.log(obj?.['key'])
// 123
```

## 5. 动态 import 导入

```js
const btn = document.getElementById('btn');

btn.onclick = function(){
  import('./hello.js').then(module => {
    module.hello();
}
```

## 6. BigInt

`BigInt` 是一种特殊的数字类型，它提供了对任意长度整数的支持。

创建 `bigint` 的方式有两种：在一个整数字面量后面加 `n` 或者调用 `BigInt` 函数，该函数从字符串、数字等中生成 `bigint`。

```js
let n1 = 123n
let n2 = 456n
let n3 = BigInt(789)
console.log(typeof n1) // bigint
console.log(n1+n2) // 579n
console.log(n2+n3) // 1245n
```

比较运算符：
- 例如 `<` 和 `>`，使用它们来对 `bigint` 和 nu`mber 类型的数字进行比较没有问题：
  ```js
  alert( 2n > 1n ); // true
  alert( 2n > 1 ); // true
  ```
- 但是请注意，由于 `number` 和 `bigint` 属于不同类型，它们可能在进行 `==` 比较时相等，但在进行 `===`（严格相等）比较时不相等：
```js
alert( 1 == 1n ); // true
alert( 1 === 1n ); // false
```

## 7. globalThis

全局对象提供可在任何地方使用的变量和函数。默认情况下，这些全局变量内置于语言或环境中。  
在浏览器中，它的名字是 `window`，对 Node.js 而言，它的名字是 `global`，其它环境可能用的是别的名字。  
ES11中 `globalThis` 被作为全局对象的标准名称加入到了 JavaScript 中，所有环境都应该支持该名称。所有主流浏览器都支持它。  
使用场景：
假设我们的环境是浏览器，我们将使用 `window`。如果你的脚本可能会用来在其他环境中运行，则最好使用 `globalThis`。
