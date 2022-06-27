# （一）初识JS

## 1. JavaScript历史

布兰登艾奇（Brendan Eich， 1961年～）。
神奇的大哥在1995年利用10天完成JavaScript设计。
网景公司最初命名为LiveScript ，后来在与Sun合作之后将其改名为JavaScript.

## 2. JavaScript是什么

lavaScript是世界上最流行的语言之一，是一种运行在客户端的脚本语言（Script是脚本的意思）脚本语言：不需要编译，运行过程中由js解释器（js引擎）逐行来进行解释并执行。
现在也可以基于Nodejs技术进行服务器端编程


## 3. JavaScript的作

- 表单动态校验（密码强度检测） （ JS产生最初的目的）
- 网页特效
- 服务端开发（Node.js）
- 桌面程序（Electron）
- App(Cordova)
- 控制硬件—物联网（Ruff游戏F发(cocos2d-js)


## 4. 浏览器执行JS简介

浏览器分成两部分：==渲染引擎和JS引擎==

- 渲染引擎：用来解析HTML与CSS ，俗称内核，比如chrome浏览器的blink ，老版本的webkit

- JS引擎：也称为JS解释器。用来读取网页中的JavaScript代码，对其处理后运行，比如chrome浏览器的V8

==浏览器本身并不会执行JS代码，而是通过内置JavaScript引擎（解释器）来执行JS代码。JS引擎执行代码时逐行解释每一句源码（转换为机器语言） ，然后由计算机去执行，所以JavaScript语言归为脚本语言，会逐行解释执行。==

## 5. JS三大组成

- ECMAScript
- DOM
- BOM

### 5.1 ECMAScript

ECMAScript是由ECMA国际（原欧洲计算机制造商协会）进行标准化的一门编程语言，这种语言在万维网上应用广 泛，它往往被称为JavaScript或JScript ，但实际上后两者是ECMAScript语言的实现和扩展。

ECMAScript
- lavaScript 网景公司
- Jscript 微软公司

ECMAScript ： **ECMAScript规定了JS的编程语法和基础核心知识，是所有浏览器厂商共同遵守的一套JS语法工业标准。**


### 5.2 DOM—文档对象模型

文档对象模型（Document Object Model ，简称DOM ） ，是W3C组织推荐的处理可扩展标记语言的标准编程接口通过DOM提供的接口可以对页面上的各种元素进行操作（大小、位置、颜色等）。

### 5.3 BOM—浏览器对象模型

浏览器对象模型 （Browser Object Model ，简称BOM）是指浏览器对象模型，它提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。通过BOM可以操作浏览器窗口，比如弹出框、控制浏览器跳转、获取分辨率等。

## 6. JS 初体验

JS有3种书写位置，分别为行内、内嵌和外部

1. 行内式JS
    ```html
    <input type="button" value="click" onclick="alert('Hello, world!')">
    ```
    - 可以将单行或少量JS代码写在HTML标签的事件属性中（以on开头的属性） ，如： onclick
    - 注意单双引号的使用：在HEML中我们推荐使用双引号，JS中我们推荐使用单引号。
    - 可读性差，在html中编写JS大量代码时，不方便阅读；引号易错，引号多层嵌套匹配时，非常容易弄混；
    - 特殊情况下使用

2. 内嵌式
    ```html
    <script>
    alert("Hello world!");
    </script>
    ```
学习时常用。

3. 外部JS文件

```html
    <script src="newFile.js"></script>
```

- 利于HTML页面代码结构化，把大段JS代码独立到HTML页面之外，既美观，也方便文件级别的复用
- ==引用外部JS文件的script标签中间不可写代码==
- 适合于JS代码量比较大的情况


## 7. JS 注释

- 单行注释：
    ```js
    // 单行注释
    ```
- 多行注释：
    ```js
    /*
    多行注释
    */
    ```

## 8. JS输入输出语句

1. 输入框

`prompt` 方法返回一个 `string` 类型。

```js
 prompt('请输入你的名字：');
```
2. 警示框

```js
alert('你好');
```

3. 控制台打印

```js
console.log('我是程序员能看到的。');
```

# （二）变量

## 1. 变量的实质

变量是程序在内存中申请的一块用来存放数据的空间。

## 2. 变量的声明

1. 声明变量
2. 赋值

### 2.1 声明变量

```js
// 声明一个叫age的变量
var age;
let name;
const PI = 3.14;
```

- `var` 是一个JS关键字，用来声明变量（variable变量的意思），使用该关键字声明变量后，计算机会自动为变量分配内存空间，不需要程序员管
- `age` 是程序员定义的变量名，我们要通过变量名来访问内存中分配的空间

## 3. 变量的初始化

```js
var age = 18;
```

初始化：声明并赋值

## 4. 更新赋值

一个变量可以被重复赋值，变量值也会更新。

```js
var age = 18;
age = 81;
```

## 5. 同时声明多个变量

```js
var age = 18,
    url = 'https://mphy.top',
    myname = 'MurphyChen'
```

## 6. 声明不赋值

```js
var sex;
console.log(sex);
// undefined
console.log(aaa);
```

## 7. 直接输出

```js
console.log(tel);
// 报错
```

## 8. 不声明直接赋值

```js
qq = 12345;
console.log(qq);
// 12345 全局变量
```

## 9. 命名规范

- 由字母（A—Za—z）、数字（0—9）、下划线（）、美元符号（5）组成，如： usrAge， num01， name
- 严格区分大小写。var app；和var App；是两个变量
- 不能以数字开头。18age是错误的
- 不能是关键字、保留字。例如： var， for， while
- 变量名必须有意义。MMD BBD nl— age
- 遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。myFirstName推荐翻译网站：有道爱词霸
- 尽量不要使用 `name` 作为变量名

# （三）数据类型

## 1. 数据类型概述

### 1.1 为什么需要数据类型

在计算机中，不同的数据所需占用的存储空间是不同的，为了便于把数据分成所需内存大小不同的数据，充分利用存储空间，于是定义了不同的数据类型。

简单来说，数据类型就是数据的类别型号。比如姓名“张三” ，年龄18，这些数据的类型是不一样的。

### 1.2 变量的数据类型

变量是用来存储值的所在处，它们有名字和数据类型。变量的数据类型决定了如何将代表这些值的位存储到计算机的内存中。==JavaScript是一种弱类型或者说动态语言==。这意味着不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。

```js
var age = 10;
//这是一个数字型var arerouok =的； //这是一个字符串
```
在代码运行时，变量的数据类型是由JS引擎根据=右边变量值的数据类型来判断的，运行完毕之后，变量就确定了数据类型
JavaScript拥有动态类型，同时也意味着相同的变量可用作不同的类型：

```js
var x = 6;
// x为数字
var x = "Bill";
// x为字符串
```

## 2. 简单数据类型

### 2.1 简单数据类型（基本数据类型）

JavaScript中的简单数据类型及其说明如下：

| 简单数据类型 | 说明                                                   | 默认值      |
| ------------ | ------------------------------------------------------ | ----------- |
| Number       | 数字型，包含整值和浮点值，如21、0.21                   | `0`         |
| Boolean      | 布尔值类型，如true、 false，等价于1和0                 | `false`     |
| String       | 字符串类型，如“张三”注意js 里面，字符串都带引号        | `""`        |
| Undefined    | `var a;` 声明了变量a但是没有给值，此时a =undefinedNull | `undefined` |
| Null         | `var a = null;` 声明了变量a为空值                      | `null`      |

### 2.2 数字型 Number

#### 1. 数字型进制

常见：二进制、八进制、十进制、十六进制

- `0123`: `0` 开头表示八进制
- `0b11`: `0b` 开头表示二进制
- `0x11`: `0x` 开头表示十六进制
- 直接打印出来会转化为十进制

#### 2. 数字型范围

```js
console.log(Number.MAX_VALUE);
console.log(Number.MIN_VALUE);
```

#### 3. 特殊值

```js
console.log(Infinity);
console.log(-Infinity);
console.log(NaN);
```

- `Infinity`：无穷大
- `-Infinity`：无穷小
- `NaN`：Not a number，代表一个非数值。

#### 4. isNaN()

`isNaN` 方法用来判断一个变量和或者一个值是数字类型，若不是数字类型则返回 `true`；否则返回 `false`。

### 2.3 字符串型 String

#### 1. 定义

字符长型可以是引号中的任意文本，其语法为双引号 `""` 和单引号 `''`。

#### 2. 字符串引号嵌套

JS可以用单引号嵌套双引号，或者用双引号嵌套单引号（外双内单，外单内双）

```js
var strmsg= '我是"高帅富"程序员';
var strmsg= "我是'高帅富'程序员";
```

#### 3. 字符串转义符

类似HTML里面的特殊字符，字符串中也有特殊字符，我们称之为转义符转义符都是\开头的，常用的转义符及其说明如下：

| 转义符 | 解释说明                    |
| ------ | --------------------------- |
| `\n`   | 换行符， n是 newline 的意思 |
| `\\`   | \                           |
| `\'`   | 单引号'                     |
| `\"`   | 双引号"                     |
| `\t`   | tab 缩进                    |
| `\b`   | 空格，b 是 blank 的意思     |

#### 4. 获取字符串长度 length

```js
var str = 'hello';
console.log(str.length);
```

#### 4. 字符串拼接

多个字符串之间可以使用+进行拼接，其拼接方式为 ==字符串+任何类型=拼接之后的新字符串== 拼接前会把与字符串相加的任何类型转成字符串，再拼接成一个新的字符串

#### 5. 字符串拼接加强

将字符串和变量相加，以后要更新最终的结果字符串，只需更新变量的值。

### 2.4 布尔型 Boolean

- 布尔型有两个值，`true` 和 `false`
- 布尔型（`true`，`false`）在参与加法时当作 `1` 和 `0` 使用

```js
console.log(true+1);
// 2
console.log(false+1);
// 1
```

### 2.5 Undefined

```js
console.log(undefined+1); // NaN
console.log(undefined+NaN); // NaN
console.log(undefined+true); // NaN
console.log(undefined+'aaa'); // undefinedaaa
console.log(undefined+undefined); // NaN
```

### 2.6 空值 Null

```js
console.log(null+1); // 1
console.log(null+undefined); // NaN
console.log(null+NaN); // NaN
console.log(null+true); // 1
console.log(null+'aaa'); // nullaaa
console.log(null+null); // 0
```

## 3. 获取变量数据类型

### 3.1 typeof 获取变量数据类型

`typeof variable` （`typeof(variable)`） 返回一个字符串，值为该变量的数据类型。

```js
console.log(typeof 1); // number
console.log(typeof false); // boolean
console.log(typeof 'aaa');    // string
console.log(typeof undefined);// undefined
console.log(typeof NaN); // number
console.log(typeof Infinity); // number
console.log(typeof null); // object
console.log(typeof typeof 1); // string
```

### 3.2 字面量

字面量是在源代码中一个固定的表示法，通俗来说，就是字面量如何表达这个值。

- 数字字面量：`1`、`0`
- 字符串字面量：`mphy`、`aaa`
- 布尔字面量：`true`、`false`

## 4. 数据类型转换

### 4.1 什么是数据类型转换

使用表单、prompt获取过来的数据默认是字符串类型的，此时就不能直接简单的进行加法运算，而需要转换变量的数据类型。
通俗来说，就是把一种数据类型的变量转换成另外一种数据类型
我们通常会实现3种方式的转换：

- 转换为字符串类型
- 转换为数字型
- 转换为布尔型

### 4.2 转换成字符串的三种方法

一般用第三种方式，隐式转换。

- `toString()` 方法
- `String()` 方法
- 加号 `+` 拼接字符串

```js
var num = 12;
console.log(num.toString());
console.log(String(num));
console.log(num + '');
```

引申：数字字符长转数字

```js
var str = '123'
console.log(str - '');
```

### 4.3 转换为数字型

| 方式                  | 说明                       | 案例                                  |
| --------------------- | -------------------------- | ------------------------------------- |
| `parseInt(str)` 函数  | string->整数型             | parseInt('10')                        |
| `parseFloat()` 函数   | string->浮点型             | parseFloat('3.14')                    |
| `Number()` 强转换函数 | string->数字型             | Number('12')                          |
| JS 隐式转换           | 算术运算符隐式转换为数字型 | `'12'-  0` 或 `'12' - ''` 或 `'12'*1` |

```js
console.log(parseInt('123')); // 123
console.log(parseFloat('3.14')); // 3.14
console.log('123' - 0); // 123
console.log('123' - ''); // 123
console.log(parseFloat('999')); // 999
console.log(parseInt('3.14159')); // 3
console.log(parseInt('120px')); // 120
console.log(Number('100')); // 100
console.log(Number('100.32')); // 100.32
console.log(Number('100px')); // NaN
console.log('100px' - ''); // NaN
```

注意：
1. 数字字符串（`'12.3'`，`12`）之间进行加法运算实际上是字符串的拼接，结果还是字符串；而数字字符串之间的减法运算是算术运算，结果是数字型。
2. 一个数字字符长和一个数字相乘，结果是算数运算结果，为数字型。

```js
console.log('10' + '2'); // 102
console.log('10' - '2'); // 8
console.log('10' + '3.2'); // 103.2
console.log('10' - '3.2'); // 6.8
console.log('12'*3); // 36
```

### 4.4 转换为布尔型

使用 `Boolean()` 函数转换。

- 转换值为 `false`：`''`, `0`, `NaN`, `null`, `undefined`（5个）
- 其他的转换值均为 `true`

```js
console.log(Boolean('')); // false
console.log(Boolean(0)); // false
console.log(Boolean(NaN)); // false
console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
console.log(Boolean([])); // true
```

## 5. 标识符、关键字、保留字

### 5.1 标识符

标识（zhi）符：就是指开发人员为变量、属性、函数、参数取的名字。标识符不能是关键字或保留字。

### 5.2 关键字

关键字：是指JS本身已经使用了的字，不能再用它们充当变量名、方法名。

包括: break, case, catch, continue, default, delete, do, else, finally. for, function, if, in instanceof, new. return, switch, this, throw, try, typeof, var, void, while, with等。

### 5.3 保留字

保留字：实际上就是预留的“关键字” ，意思是现在虽然还不是关键字，但是未来可能会成为关键字，同样不能使用它们当变量名或方法名。

包括: boolean, byte, char, class, const, debugger, double, enum, export, extends fimal, float. goto, implements, import, int, interface, long, mative, package private, protected, public, short, static, super, synchronized, throws, transient volatile等。

## 6. 拓展：8 种基本数据类型

8 种基本数据类型中，前 7 种为基本数据类型，最后 1 种为复杂数据类型（`object`）。

- `number`：用于任何类型的数字：整数或浮点数，在 $\pm(2^{53}-1)$ 范围内的整数。
- `bigint`：用于任意长的整数。
- `string`：字符串，一个字符串可以包含 0 个或多个字符，没有单独的单字符类型。
- `boolean`：值为 `true` 或 `false`
- `null`：未知的值，只有一个 `null` 值的独立类型。
- `undefined`：未定义得值，只有一个 `undefined` 值的独立类型。
- `symbol`：用于唯一的标识符。
- `object`：用于更复杂的数据结构。

使用 `typeof` 运算符查看变量的数据类型：
- 两种形式：`typeof x` 或 `typeof(x)`
- 以字符串的形式返回类型名称：例如 `string`
- `typeof null` 会返回 `"object"` —— 这是 JavaScript 编程语言的一个错误，实际上它并不是一个 `object`。


# （四）JS 运算符

运算符（ operator ）也被称为操作符，是用于实现赋值、比较和执行算数运算等功能的符号。
JavaScript常用的运算符有：

- 算术运算符
- 递增和递减运算符
- 比较运算符
- 逻辑运算符
- 赋值运算符

## 1. 算数运算符

- `+`
- `-`
- `*`
- `/`
- `%`

### 1.1 浮点数的精度问题

浮点数值的最高精度是17位小数，但在进行算术计算时其精确度远远不如整数。

```js
var result =0.1+0.2; //结果不是0.3,而是: 0.30000000000000004 
console.log(0.07 * 100); //结果不是7， 而是： 7.000000000000001
```

注意：

1. JS 中不要直接用浮点数之间进行运算，会产生精度误差。
2. 不要直接拿两个浮点数进行比较！

### 1.2 表达式和返回值

表达式：是由数字、运算符、变量等以能求得数值的有意义排列方法所得的组合
简单理解：是由数字、运算符、变量等组成的式子

==表达式最终都会有一个结果，返回给我们，我们成为返回值==

## 2. 递增递减运算符 

### 2.1 递增和递减运算符概述

如果需要反复给数字变量添加或减去1，可以使用递增（++）和递减（-- ）运算符来完成。
在JavaScript 中，递增（++）和递减（-- ）既可以放在变量前面，也可以放在变量后面。放在变量前面时，

我们可以称为前置递增（递减）运算符，放在变量后面时，我们可以称为后置递增（递减）运算符。

注意：递增和递减运算符必须和变量配合使用。

- 后置递增运算符 `i++`
- 前置递增运算符 `++i`
- 后置递减运算符 `i--`
- 前置递减运算符 `--i`

### 2.2 前置递增和后置递增小结

- 前置递增和后置递增运算符可以简化代码的编写，让变量的值+ 1 比以前写法更简单
- 单独使用时，运行结果相同
- 与其他代码联用时，执行结果会不同
- 后置：先原值运算，后自加（先人后己）
- 前置：先自加，后运算（先已后人）
- 开发时，大多使用后置递增/减，并且代码独占一行，例如：num++; 或者num--;

## 3. 比较运算符

### 3.1 概述

概念：比较运算符（关系运算符）是两个数据进行比较时所使用的运算符，比较运算后，会返回一个布尔值
（true / false）作为比较运算的结果。

| 比较运算符 | 说明                                                    |
| :--------: | ------------------------------------------------------- |
|    `<`     | 小于                                                    |
|    `>`     | 大于                                                    |
|    `<=`    | 大于或等于                                              |
|    `>=`    | 小于或等于                                              |
|    `==`    | 判等于                                                  |
|    `!=`    | 判不等                                                  |
|   `===`    | 全等于。要求值和数据类型均一致，则返回 `true`           |
|   `!==`    | 全不等于。要求值和数据类型至少一个不一致，则返回 `true` |

### 3.2 关于 == 与 ===

#### 3.2.1. 区别

需要注意的是 `==` 和 `===` 的区别。
- `==` 比较的时候只判断值，因为会进行隐式转换。值相等则返回 `true`
- `===` 比较判断的时同时需要值相等和类型相同，两者均满足则返回 `true`

#### 3.2.2 规律

结合以下例子体会。

- `''`、`0`、`false` 之间（或 `'1'`、`1`、`true`之间）进行 `==` 比较的结果为 `true`
- `NaN` 与其他任何数据类型之间 `==` 比较结果为 `false`
- `null` 只有在和自身以及 `undefined` 之间 `==` 比较时结果为 `true`
- `undefined` 只有在和自身以及 `null` 之间 `==` 比较时结果为 `true`
- 数字和数字字符串的值相等，则 `==` 比较的结果为 `true`
- 以上这些例子在全等比较 `===` 下的结果均为 `false`

```js
console.log('18' == 18); // true
console.log('' == false); // truw
console.log('' == 0); // truw
console.log(0 == false); // true
console.log('1' == 1 == true); // true

console.log('NaN与其他值比较:');
console.log(NaN == 0); // false
console.log(NaN == ''); // false
console.log(NaN == NaN); // false
console.log(NaN == null); // false
console.log(NaN == false); // false
console.log(NaN == undefined); // false

console.log('null与其他值：');
console.log(null == null); // true
console.log(null == undefined); // true
console.log(null == 0); // false
console.log(null == ''); // false
console.log(null == NaN); // false
console.log(null == false); // false

console.log('undefined与其他值比较:');
console.log(undefined == null);  // true
console.log(undefined == undefined);  // true
console.log(undefined == 0);  // false
console.log(undefined == '');  // false
console.log(undefined == NaN);  // false
console.log(undefined == false);  // false
```

## 4. 逻辑运算符

### 4.1 概述

- 逻辑与 `&&`
- 逻辑或 `||` 
- 逻辑非 `!`

### 4.2 逻辑中断（短路操作）

原理：多个表达式进行逻辑运算，当左边的表达式值可以确定最终结果时，不再继续运算右边其余的表达式。

#### 4.2.1 逻辑与 &&

- 语法：`expr1 && expr2 && ...`
- 若 `expr1` 为真，则返回 `expr2`
- 若 `expr1` 为假，则返回 `expr1`

```js
console.log(123 && 456); // 456
console.log(false && 123); // false
console.log(1 && 2 && 3); // 3
console.log(1 && 1 && false && 2); // false
```

#### 4.2.2 逻辑或 ||

- 语法：`expr1 || expr2 || ...`
- 若 `expr1` 为假，则返回 `expr2`
- 若 `expr1` 为真，则返回 `expr1`

```js
console.log(0 || 12); // 12
console.log(true ||  false || 2); // true
console.log(0 || false || true || -2); // true
```

## 5. 赋值运算符

- `+=`
- `-=`
- `*=`
- `/=`

## 6. 拓展：JS特殊运算符

### 6.1 数字转化：单目运算符 `+`

单目运算符 `+` 作用于数字无效，结果不变。但是可以用来转化非数字类型为数字，等效于 `Number()`。

```javascript
let x = false;
let y = "";
let z = "123.4";
console.log(+x); // 0
console.log(+y); // 0
console.log(+z); // 123.4
```

用于非数字型之间的数学运算，很简洁：

```javascript
let a = "12";
let b = "24";
console.log(+a + +b); // 36
```

### 6.2 逗号运算符 `,`

逗号运算符能让我们处理多个语句，使用 `,` 将它们分开。每个语句都运行了，**但是只有最后的语句的结果会被返回**。

```javascript
let a = (3 + 4, 5 + 6);
console.log(a); // 11
```

### 6.3 布尔值转换符 `!!`

两个相邻的非逻辑运算符组成的 `!!`，可以将一个值转换为对应的布尔值。等效于 `Boolean()`。

```javascript
console.log(!!"0"); // true
console.log(!!0); // false
console.log(!!undefined); //false
console.log(!!"aaa"); // true
```

### 6.4 空值合并运算符 `??`

我们将值既不是 `null` 也不是 `undefined` 的表达式定义为已定义的值（defined）。即：`??`。

`a ?? b` 结果为：
- 若 `a` 已定义，则结果为 `a`
- 若 `a` 不是已定义的，则结果为 `b`

等价于：

```javascript
(a !== null && a !== undefined) ? a : b;
```

# （五）流程控制

- 顺序结构
- 选择分支结构
- 循环结构


## 1. 顺序结构

## 2. 选择结构

- `if-else`
- `if-else if-else`
- `switch-case`

### 2.1 if-else

语法

```js
if (condition)
   statement1
[else
   statement2]
```

### 2.2 if-else if-else

语法

```js
if (condition1)
  statement1
else if (condition2)
  statement2
else if (condition3)
  statement3
...
else
  statementN
```

### 2.3 switch-case

语法

```js
switch (expression) {
  case value1:
    //Statements executed when the
    //result of expression matches value1
    [break;]
  case value2:
    //Statements executed when the
    //result of expression matches value2
    [break;]
  ...
  case valueN:
    //Statements executed when the
    //result of expression matches valueN
    [break;]
  [default:
    //Statements executed when none of
    //the values match the value of the expression
    [break;]]
}
```

## 3. 循环

### 3.1 概述

- `for` 
- `while` 
- `do...while`
- `label`
- `for...in`
- `for...of`

### 3.2 for 循环

语法

```js
for ([initExpr]; [condExpr]; [incExpr])
    statement
```
- initExpr: 变量初始化
- condExpr: 循环条件
- incExpr：增量表达式

例子

```js
for (let step = 0; step < 5; step++) {
  // Runs 5 times, with values of step 0 through 4.
  console.log('Walking east one step');
}
```

### 3.3 while 循环

语法

```js
while (condition) 
    statement
```

例子

```js
let n = 0;
let x = 0;
while (n < 3) {
    n++;
    x += n;
}
```

### 3.4 do...while

语法

```js
do 
    statement
while (condition);
```

例子

```js
let n = 5
do {
    console.log('hello');
} while (--n)
```

### 3.5 label

语法：

```js
label:
statement
```

- `label`: 任何不属于保留关键字的 JavaScript 标识符。
- `statement`: JS 语句。

说明：

可使用一个标签来唯一标记一个循环，然后使用 break 或 continue 语句来指示程序是否中断循环或继续执行。

需要注意的是，JavaScript 没有 goto 语句，==标记只能和 break 或 continue 一起使用。==

在严格模式中，你不能使用 “let” 作为标签名称。它会抛出一个 SyntaxError（因为 let 是一个保留的标识符）。

例子：

```js
var str = ''
aLoop:
for (let i = 0; i < 5; i++) {
    if (i == 2) {
        continue aLoop;
    }
    str += i;
}
console.log(str); // 0134
```

### 3.6 break 与 continue

- `break`：跳出当前循环，不再进行当前循环。
- `continue`：跳过本轮循环，进行当前循环的下一轮。
- `break` 与 `continue` 均可配合 `label` 语句使用来跳转循环。

### 3.7 for...in

语法：

```js
for (variable in object) {
    //statements
}
```

说明：

- `for...in` 语句用于对数组或者对象的属性进行循环操作。

- `for ... in` 循环中的代码每执行一次，就会对数组的元素或者对象的属性进行一次操作。

```js
var arr = new Array(1,2,3,4,5);
for (let i in arr) {
    console.log(i+'.');
}
```

### 3.8 for...of

语法：

```js
for (variable of iterable) {
    //statements
}
```

例子：

```js
let iterable = [10, 20, 30];
for (let value of iterable) {
    value += 1;
    console.log(value);
}
```

## 4. chrome 代码调试

- 断点调试：断点调试是指自己在程序的某一行设置一个断点，调试时，程序运行到这一行就会停住，然后你可以一步一步往下调试，调试过程中可以看各个变量当前的值，出错的话，调试到出错的代码行即显示错误，停下。
- 断点调试可以帮我们观察程序的运行过程
- 浏览器中按F12--> sources -->找到需要调试的文件-->在程序的某一行设置断点
- Watch: 监视，通过watch可以监视变量的值的变化，非常的常用。
- F11: 程序单步执行，让程序一行一行的执行，这个时候，观察watch中变量的值的变化。
- 代码调试的能力非常重要，只有学会了代码调试，才能学会自己解决bug的能力。初学者不要觉得调试代码麻烦就不去调试，
- 知识点花点功夫肯定学的会，但是代码调试这个东西，自己不去练，永远都学不会。
- 今天学的代码调试非常的简单，只要求同学们记住代码调试的这几个按钮的作用即可，后面还会学到很多的代码调试技巧。

# （六）函数

## 1. 概述

函数：就是封装了一段可被重复调用执行的代码块。通过此代码块可以实现大量代码的重复使用。
封装：把一个或者多个功能通过函数的方式封装起来，对外只提供一个简单的函数接口。

## 2. 函数的声明与调用

```js
// 声明
function funcName(params) {
    // function statements
}
funcName(params);
// 调用
```

## 3. 形参与实参

声明时传入的为形参，调用时传入的为实参。

## 4. 实参个数与形参个数不匹配的情况

| 参数个数           | 说明                               |
| ------------------ | ---------------------------------- |
| 形参和实参个数相等 | 输出正确结果                       |
| 实参个数多于形参   | 只取到形参的个数                   |
| 实参个数少于形参   | 多的形参定义为undefined，结果为NaN |

```js
function sum(num1, num2) {
    console.log(num1 + num2);
}
sum(100, 200); // 300, 形参和实参个数相等，输出正确结果
sum(100, 400, 500, 700); // 500, 实参个数多于形参，只取到形参的个数
sum(200); // NaN, 实参个数少于形参，多的形参定义为undefined，结果为NaN
```

> 在JavaScript中，形参的默认值是 `undefined`。

## 5. 声明函数的三种方法

### 5.1 function 命令

```js
function funcName(params) {
    // function statements
}
```

### 5.2 函数表达式

```js
const funcName = function(params) {
    // function statements
}
```

### 5.3 箭头函数 `=>`

创建一个函数更加简洁的方式，有两种方式：
- 不带花括号：`(...args) => expression`，计算表达式，直接返回。
- 带花括号：`(...args) => { bodu }`，可以编写多行多个语句，需要 `return` 语句返回。

```javascript
let sum = (a, b) => a + b;
```

### 5.4 Function 构造函数

```js
const add = new Function(
    'x',
    'y',
    return 'x + y'
);
```

## 6. 注意

- 函数未指定返回值则默认返回 `undefined`

## 7. arguments 的使用

`arguments` 是所有JS函数内置的对象，但也只有函数具有。

```js
function test() {
    return arguments;
}
console.log(test(1,2,3,4));
```

输出：

```js
Arguments(4) [1, 2, 3, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```

函数的 `arguments` 是一种伪数组：

1. 具有数组的 `length` 属性
2. 按照索引方式进行存储
3. 没有真正数组的一些方法 `pop()`、`push()`

# （七）数组

## 1. 基本概念

- JS 数组都是动态创建的，可以自由增加数组长度，这点不同于 C/C++。
- 一个 JS 数组内可以存放不同类型的元素，例如 `['abc', 1, true, undefined]`，这点也不同于 C/C++/Java。

## 2. 创建数组

### 2.1 数组字面量创建数组

- 创建空数组
    ```js
    let arr = [];
    ```
- 创建一般数组
    ```js
    let arr = [1, 2, 3];
    ```

### 2.2 new Array 创建数组对象

1. 创建空数组
    ```js
    let arr = new Array();
    ```

2. 创建指定长度的数组，有2个空数组元素
    ```js
    let arr1 = new Array(2);
    ```

3. 创建放有指定元素的数组（[2, 3]）
    ```js
    let arr2 = new Array(2, 3);
    ```

4. 一些示例
    ```js
    let arr_0 = [1, true, "aaa"];
    let arr_1 = [];
    let arr_2 = new Array(); // []
    let arr_3 = new Array(2); // [empty × 2]
    let arr_4 = new Array(2,); // [empty × 2]
    let arr_5 = new Array(2, 3, 4); // [2, 3, 4]
    ``` 

## 3. 基本操作

1. 数组元素访问
    ```js
    let e = arr[index];
    ```

2. 获取数组长度
    ```js
    let len = arr.length;
    ```

3. 数组遍历  
    方式一：  
    ```js
    for (let i = 0; i < arr.length; i++) {
        console.log(arr[i]);
    }
    ```
    方式二：
    ```js
    for (const i in arr) {
        console.log(arr[i]);
    }
    ```

4. 数组逆转
    ```js
    // 反转数组
    function reverse(arr) {
        let res = [];
        for (let i = arr.length - 1; i >= 0; i--) {
            res[res.length] = arr[i];
        }
        return res;
    }
    console.log(reverse([1, 2, 3, 4, 0])); // [0, 4, 3, 2, 1]
    ```

## 4. 检测一个值是否为数组

### 4.1 instanceof

```js
function isArray(test) {
    if (test instanceof Array) return true;
    return false;
}
console.log(isArray([1, 2])); // true
console.log(isArray(1)); // false
```

### 4.2 Array.isArray() 

Array.isArray() 方法用于检测一个值是否为数组。

## 5. 添加删除数组元素的方法

| 方法名           | 说明                                                     | 返回值             |
| ---------------- | -------------------------------------------------------- | ------------------ |
| `push(arg1,...)` | 末尾添加一个或多个元素                                   | 返回新的长度       |
| `pop()`          | 删除数组最后一个元素，数组长度减 1，无参数，修改了原数组 | 返回所删除元素的值 |
| `unshift()`      | 向数组的开头添加一个或多个元素，修改了原数组             | 返回新的长度       |
| `shift()`        | 删除数组的第一个元素，数组长度减 1，无参数，修改了原数组 | 返回第一个元素的值 |

## 6. 数组排序

| 方法名      | 说明                       | 是否修改原数组           |
| ----------- | -------------------------- | ------------------------ |
| `reverse()` | 颠倒数组中元素顺序，无参数 | 会改变原数组，返回新数组 |
| `sort()`    | 对数组的元素进行排序       | 会改变原数组，返回新数组 |

`sort` 方法对数组进行原地排序，但是默认按照字典序排序。需要传入一个比较函数 `cmp(a, b)`，然后得到我们需要的排序效果。

```js
let arr = [1, 4, 17, 12, 9];

arr.sort();
console.log(arr); // [ 1, 12, 17, 4, 9 ]

let cmp = (a, b) => a - b;

arr.sort(cmp);
console.log(arr); // [ 1, 4, 9, 12, 17 ]
```

其中，`let cmp = (a, b) => a - b;` 为升序，`b - a` 为降序。

## 7. 数组索引方法

| 方法名          | 说明                                      | 返回值                            |
| --------------- | ----------------------------------------- | --------------------------------- |
| `indexOf()`     | 数组中查找指定元素的 **第一个索引**       | 若存在则返回索引号，否则返回 `-1` |
| `latsIndexOf()` | 查找指定元素在数组中的 **最后一个的索引** | 若存在则返回索引号，否则返回 `-1` |

`indexOf` 前面开始查找，`lastIndexOf` 从后面开始查找，但索引都是从前往后由 `0` 算起。
```js
let arr = ['red', 'green', 'blue', 'pink', 'blue'];

console.log(arr.indexOf('blue')); // 2
console.log(arr.lastIndexOf('blue')); // 4
console.log(arr.indexOf('yellow')); // -1
```

## 8. 数组去重

```js
// 数组去重
function unique(arr) {
    let res = [];
    for (let i = 0; i < arr.length; i++) {
        if (res.indexOf(arr[i]) === -1) {
            res.push(arr[i]);
        }
    }
    return res;
}

console.log(unique([ 2, 3, 3, 4, 5, 5 ])); // [ 2, 3, 4, 5 ]
```

## 9. 数组与字符串互转

### 9.1 数组转换为字符串

| 方法名           | 说明                                               | 返回值         | 是否改变原数组 |
| ---------------- | -------------------------------------------------- | -------------- | -------------- |
| `toString()`     | 将数组转换成字符串，逗号分隔每一个                 | 返回一个字符串 | 不改变         |
| `join('分隔符')` | 把数组中的所有元素转换为一个字符串，以指定符号分割 | 返回一个字符串 | 不改变         |

示例
```js
let a = ['a', 'b', 'c', 'd', 'e'];

console.log(a.toString());  // a,b,c,d,e
console.log(a.join('')); // abcde
console.log(a.join('-')); // a-b-c-d-e
console.log(a); // [ 'a', 'b', 'c', 'd', 'e' ]
```

### 9.2 字符串转换为数组

使用 `split()` 方法。

```js
let str = 'blue-green-pink-red';
let res = str.split('-');
console.log(res); // [ 'blue', 'green', 'pink', 'red' ]
```

## 10. 数组方法 splice


# （八）作用域

## 1. 作用域概述

通常来说，一段程序代码中所用到的名字并不总是有效和可用的，而限定这个名字的可用性的代码范围就是这个名字的作用域。作用域的使用提高 程序逻辑的局部性，增强了程序的可靠性，减少了名字冲突。

## 2. 全局变量

- 在全局作用域下声明的变量叫做全局变量（在函数外部定义的变量）。
- 全局变量在代码的任何位置都可以使用
- 在全局作用域下var声明的变量是全局变量。
- 特殊情况下，在函数内不使用var声明的变量也是全局变量（不建议使用）


## 3. 局部变量

在局部作用域下声明的变量叫做局部变量（在函数内部定义的变量）
- 局部变量只能在该函数内部使用
- 在函数内部var声明的变量是局部变量
- 函数的形参实际上就是局部变量

## 4. 全局变量与局部变量区别

- 全局变量：在任何一个地方都可以使用，只有在浏览器关闭时才会被销毁，因此比较占内存
- 局部变量：只在函数内部使用，当其所在的代码块被执行时，会被初始化；当代码块运行结束后，就会被销毁，因此更节省内存空间


## 5. var、let、const

ES6 以前，JS 没有块级作用域。ES6 新增 let 和 const 之后才有了块级作用域。
块级作用域是指用 `{}` 包括起来的一段代码，例如 if 、while 等等。
函数作用域就是指变量只在函数内部起作用。

- var 声明的是函数作用域的变量
- let 声明的是块级作用域的变量
- const 声明的是块级作用域的变量

## 6. 作用域链

- 只要是代码，就至少有一个作用域
- 写在函数内部的局部作用域
- 如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域
- 根据在内部函数可以访问外部函数变量的这种机制，用链式查找决定哪些数据能被内部函数访问，就称作作用域链



# （九） 声明提升

1. 我们js引擎运行js分为两步： 预解析，代码执行
    - 预解析js引擎会把js里面所有的var 还有function提升到当前作用域的最前面
    - 代码执行 按照代码书写的顺序从上往下执行
2. 预解析分为变量预解析（变量提升） 和函数预解析（函数提升）
    - 变量提升就是把所有的变量声明提升到当前的作用域最前面 不提升赋值操作
    - 函数提升就是把所有的函数声明提升到当前的作用域最前面，不调用操作

举例一

```JS
func();
var func = function () {
    console.log('hello');
}
// 出错，以上代码相当于：
var func;
func();
func = function () {
    console.log('hello');
}
```

举例二

```JS
f1()
console.log(c);
console.log(b);
console.log(a);
function f1() {
    var a = b = c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}
```

相当于

```JS
function f1() {
    var a;
    c = 9;
    b = c;
    a = b;
    console.log(a);
    console.log(b);
    console.log(c); 
}
f1();
console.log(c);
console.log(b);
console.log(a);
```


输出

```JS
// answer
/*
9
9
9
9
9
error
*/
```

# （十）对象

## 1. 对象

### 1.1 什么是对象？

在JavaScript中，对象是一组无序的相关属性和方法的集合，所有的事物都是对象，例如字符串、数值、数组、函数等。

对象是由属性和方法组成的。
- 属性：事物的特征，在对象中用属性来表示（常用名词）
- 方法：事物的行为，在对象中用方法来表示（常用动词）

### 1.2 为什么需要对象？

## 2. 创建对象

- 使用字面量创建对象
- 使用 `new Object` 创建对象
- 利用构造函数创建对象

### 2.1 字面量创建

使用 `{}` 创建，包含属性和方法，采用键值对表示，创建的对象称为对象字面量。

```js
var obj = {
    uname: 'MurphyChen',
    age: 18,
    sayHi: function () {
        console.log('Hi!);
    }
}
```

### 2.2 使用对象的属性和方法

1. 调用对象的属性

```js
// 方法一
objectName.attrName
// 方法二
objectName['attrName'] // 不要忘记引号
```

2. 调用对象的方法

```js
objectName.funcName();//不要忘记括号
```

### 2.3 使用 newObject 创建对象

```js
// 创建空对象
let obj = new Object();
//添加属性
obj.uname = 'MurphyChen';
obj.age = 18;
obj.sayHi = function() {
    console.log('Hi!');
}
```

### 2.4 利用构造函数创建对象

前两种创建对象的方法，每次都只能创建一个对象。但需要多个具有相同属性和方法的对象的时候，就需要使用构造函数来创建。

构造函数将相同的属性和方法封装在一个函数里。

构造函数语法：

```js
// 定义
function ConFuncName(params) {
    this.attr = value;
    this.methods = function() {};
}
// 调用
let obj = new ConFuncName(params);
```

- 构造函数名单词首字母均大写
- 函数不需要返回值

举例

```js
function Star(uname, age, sex) {
    this.name = uname;
    this.age = age;
    this.sex = sex;
}
let ldh = new Star('刘德华', 18, '男');
let zxy = new Star('张学友', 19, '男');
console.log(typeof ldh); // object
console.log(ldh.sex); // 男
console.log(zxy.name); // 张学友
```

<h4>构造函数的实质</h4>

==构造函数相当于创建了一个抽象的类==，使用关键字 `new` 创建一个对象的过程称为类的实例化，对象是具体的。

<h4>new 关键字的执行过程</h4>

1. 在内存中创建一个空的对象；
2. `this` 指向这个空对象；
3. 执行构造函数里面的代码，给空对象添加属性和方法；
4. 返回此对象。

## 3. 遍历对象

`for...in` 可以对数组和对象进行遍历。

语法

```js
for (const key in obj) {
    console.log(key); // 遍历属性名
    console.log(obj[key]); // 遍历属性值
}
```

# （十一）内置对象

## 1. 内置对象

- Javascript中的对象分为3种：自定义对象、内置对象、浏览器对象
- 前面两种对象是IS基础内容，属于ECMAScript ；第三个浏览器对象属于我们JS独有的，我们JS APl讲解
- **内置对象就是指JS语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或是最基本而必要的功能（属性和方法）**

## 2. 数学对象 Math

### 2.1 Math 的使用

查询 MDN 文档

```js
const arr = [3,4,11,24,89,2,34]
console.log(Math.max(...arr)); // 89
console.log(Math.PI); // 3.141592653589793
console.log(Math.max()); // -Infinity
```

### 2.1 自定义自己的 Math 对象

我们可以自定义自己的对象。

```js
const myMath = {
    PI: 3.141592654,
    max: function () {
        let max = arguments[0];
        for (let i = 1; i < arguments.length; i++) {
            max = arguments[i] > max ? arguments[i] : max;
        }
        return max;
    },
    min: function () {
        let min = arguments[0];
        for (let i = 1; i < arguments.length; i++) {
            min = arguments[i] < min ? arguments[i] : min;
        }
        return min;
    }
}
```

### 2.3 Math 常用方法

```js
Math.PI // 圆周率
Math.floor() // 向下取整
Math.ceil() // 向上取整
Math.round() // 四舍五入，遇到  .5 往大了取
Math.abs() // 绝对值
Math.max() // 最大值
Math.min() // 最小值
```

```js
console.log(Math.abs('-1')); // 1
console.log(Math.floor(-2.5)); // 3
console.log(Math.ceil(-2.5)); // -2
console.log(Math.round(-3.5)); // -3
console.log(Math.round(3.5)); // 4
```

### 2.4  Math.random 随机数

 `Math.random` 方法返回一个位于区间 `[0, 1)` 的伪随机浮点数。

 ```js
Math.random(); // 0.41713485547506424
 ```

获取闭区间 `[a, b]` 之间的整数：

```js
let ran = parseInt(Math.random() * (b - a + 1)) + a;
```

获取前闭后开区间 `[a, b)` 之间的整数：

```js
let ran = parseInt(Math.random() * (b - a)) + a;
```

实例：定义自己的取整函数

```js
// [a, b)
function getRandom1(a, b) {
    return parseInt(Math.random() * (b -a)) + a;
}

// [a, b]
function getRandom2(a, b) {
    return parseInt(Math.random() * (b - a + 1)) + a;
}
```

应用：随机点名

```js
let names = new Array('Peter', 'Murphy', 'Jack', 'Darcy', 'Alice');
console.log(names[getRandom2(0, names.length-1)]);
```

## 3. 日期对象 Date

### 3.1 时间格式化

`Date` 对象是一个构造函数，需要使用 `new` 来创建日期对象（实例化）。

若没有参数，则默认返回当前系统的当前时间

```js
let date = new Date();
console.log(date);
```

若有参数，则返回参数里面的时间。
参数常用写法

```js
let date = new Date();
console.log(date);
// 2021-03-15T05:39:52.204Z
let date1 = new Date(2019, 10, 1);
console.log(date1);
// 2019-10-31T16:00:00.000Z
let date2 = new Date('2019-10-1 8:8:8');
console.log(date2);
// 2019-10-01T00:08:08.000Z
```

一般使用以下参数形式

```js
let date3 = new Date('2019-10-1 10:10:10');
let date4 = new Date('2019/10/1');
```

常用返回日期格式：

```js
let date = new Date();
console.log(date.getFullYear()); // 2021
console.log(date.getMonth() + 1); // 3，注意得到的月份要加 1
console.log(date.getDate()); // 15
console.log(date.getDay()); // 1
```

实例一：返回 `今天是 2021 年 3 月 15 日 周一` 的日期格式。

```js
let year = date.getFullYear();
let month = date.getMonth() + 1;
let dates = date.getDate();
let day = date.getDay();
let days = ['日', '一', '二', '三', '四', '五', '六']
console.log(`今天是 ${year} 年 ${month} 月 ${dates} 日 周${days[day]}`);
```

实例二：输出时分秒 `15:06:09` 格式化时间串。



```js
function getTime() {
    let time = new Date();
    let h, m, s;
    [h, m, s] = [time.getHours(), time.getMinutes(), time.getSeconds()]
    function check(t) {
        return t < 10 ? '0' + t : t;
    }
    [h, m, s] = [check(h), check(m), check(s)];
    return h + ':' + m  + ':' +s;
}
console.log(getTime());
```

### 3.2 时间戳（获取1971年1月1日至今过去的毫秒数）

```js
// 1. valueOf(), getTime()
let date = new Date();
console.log(date.valueOf());
console.log(date.getTime());

// 2. 推荐写法
let date1 = +new Date();
console.log(date1);

// 3. H5新增写法
let date2 = Date.now();
console.log(date2);
```

## 4. 字符串对象

### 4.1 基本包装类型

- 对象才有属性和方法
- 复杂数据类型才有属性和方法
- 那么为什么简单数据类型 `'aaa'` 有 `length` 属性呢？
- **基本包装类型：把简单数据类型包装成复杂数据类型，这样基本数据类型也有了属性和方法**

```js
// 1. 简单数据类型包装成复杂数据类型
let temp = new String('aaa');
// 2. 把临时变量赋值给 str
str = temp;
// 3. 销毁临时变量
```

- 三种基本包装类型： `String`、`Number`、`Boolean`

### 4.2 字符串的不可变

指的是其值不变。虽然看上去是可以改变的，但其实是地址变了，内存中开辟了一个内存空间。

### 4.3 根据字符串返回位置

语法
从 `start` 索引开始查找 `c` 。
```js
str.indexOf('c', start)
```

### 4.4 根据位置返回字符

1. charAt()

    ```js
    str.charAt(index);
    ```

2. charCodeAt()
    返回该位置的字符的 ASCII 值。一般用于判断用户按下了哪个键。
    ```js
    str.charCodeAt(i)
    ```

3. str[index] 
    H5 新增写法。
    ```js
    str[i];
    ```

### 4.5 拼接以及截取字符串

1. 字符长拼接
    ```js
    str.concat(str1, str2, str3, ...)
    ```
2. 获取子串，[start, start+length]
    ```js
    str.substr(start, length)
    ```
3. 切片，前闭后开：[start, end)
    ```js
    str.slice(start, end)
    ```
4. 获取子串，前闭后开：[start, end)
    ```js
    str.substring(start, end)
    ```

> [!warning]
> 警告： 尽管 `String.prototype.substr()` 没有严格被废弃 (as in "removed from the Web standards"), 但它被认作是遗留的函数并且可以的话应该避免使用。它并非JavaScript核心语言的一部分，未来将可能会被移除掉。如果可以的话，使用 `substring()` 替代它.

### 4.6 替换、转换为数组

- 替换 `replace`，只换一次。
    ```js
    str.replace('a', 'b');
    ```
- 转换为数组 `split()`
    ```js
    let str1 = 'red pink blue';
    console.log(str1.split(' '))
    // [ 'red', 'pink', 'blue' ]
    let str2 = 'red&pink&blue';
    console.log(str2.split('&'))
    // [ 'red', 'pink', 'blue' ]
    ```

### 4.7 查找某个字符出现的位置和次数

```js
// 查找某个字符出现的位置和次数
function findLocation(str, char) {
    let res = {
        loc: [],
        count: 0
    };
    for (let i = 0; i < str.length; i++) {
        if (str[i] === char) {
            res.loc.push(i);
            res.count++;
        }
    }
    return res;
}

let ans = findLocation("abcaaadef", "a");
console.log(ans.count, ans.loc); // 4 [ 0, 3, 4, 5 ]
```

### 4.8 统计出现次数最多的字符

```js
function findMost(str) {
    let res = {};
    for (const i in str) {
        if (str[i] in res) {
            res[str[i]]++;
        } else {
            res[str[i]] = 1;
        }
    }
    let temp = -Infinity;
    let ans;
    for (const k in res) {
        if (res[k] > temp) {
            temp = res[k];
            ans = k;
        }
    }
    return [ans, temp];
};
console.log(findMost("abbcaaa")); // [ 'a', 4 ]
```

# （十二） 复杂类型

## 1. 简单类型与复杂类型

简单类型又叫做基本数据类型或者值类型，复杂类型又叫做引用类型。
- 值类型：简单数据/基本数据类型，在存储时变量中存的是值本身，因此叫做值类型。例如 string, number, boolean, undefined, null
- 引用类型：复杂数据类型，在存储时变量中存储的仅仅是地址（引用），因此叫做引用数据类型。通过 `new` 关键字创建的对象（系统对象、自定义对象），如 `Object`、`Date` 等。

## 2. 堆和栈

堆栈空间分配区别︰

1. 栈（操作系统）：由操作系统自动分配释放存放函数的参数值、局部变量的值等。其操作方式类似于数据结构中的栈；
==简单数据类型存放到栈里面==

2. 堆（操作系统）︰存储复杂类型(对象)，一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收。
==复杂数据类型存放到堆里面==

![avatar](https://cdn.jsdelivr.net/gh/hacker-c/Picture-Bed@main/js1.png)

- 简单数据类型 `null` 返回的是一个空对象：`Object`。若有一个变量打算存储为对象但是没想好放什么，就可以给 `null` 值。
- 简单数据类型是存放在栈里面，直接开辟空间存放值。
- 复杂数据类型，首先在栈里面存放地址（十六进制），然后在堆里面存放值。

## 3. 简单数据类型传参

函数的形参也可以看做是一个变量，当我们把一个值类型变量作为参数传给函数的形参时，其实是把变量在栈空间里的值复制了一份给形参，那么在方法内部对形参做任何修改，都不会影响到的外部变量。

## 4. 复杂数据类型传参

函数的形参也可以看做是一个变量，当我们把引用类型变量传给形参时，其实是把变量在栈空间里保存的堆地址复制给了形参，形参和实参其实保存的是同一个堆地址，所以操作的是同一个对象。

# （十三）异常处理

## 1. try/catch/finally

`try/catch/finally` 是 JavaScript 异常处理语句。
```js
try {
    //调试代码块
} catch(e) {
    //捕获异常，并进行异常处理的代码块
} finally{
    //后期清理代码块
}
```

在正常情况下，JavaScript 按顺序执行 `try` 子句中的代码，如果没有异常发生，将会忽略 `catch` 子句，跳转到 `finally` 子句中继续执行。

如果在 `try` 子句运行时发生错误，或者使用 throw 语句主动抛出异常，则执行 `catch` 子句中的代码，同时传入一个参数，引用 `Error` 对象。  

不管 `try` 语句是否完全执行，`finally` 语句最后都必须要执行，即使使用了跳转语句跳出了异常处理结构，也必须在跳出之前先执行 `finally` 子句。


## 2. Error

通过 `Error` 的构造器可以创建一个错误对象。当运行时错误产生时，`Error` 的实例对象会被抛出。`Error` 对象也可用于用户自定义的异常的基础对象。  

创建自定义异常的语法：
```js
new Error([message])
```

参数说明：
- `message`：可选。可阅读的错误描述信息。

ECMA-262 规范了 7 种错误类型，具体说明如下。其中 `Error` 是基类，其他 6 种错误类型是子类，都继承 `Error` 基类。`Error` 类型的主要用途是自定义异常对象。  
下面列出了各种内建的标准错误类型。

- `Error`：普通异常。与 `throw` 语句和 `try/catch` 语句一起使用，属性 `name` 可以读写异常类型，`message` 属性可以读写详细错误信息。
- `EvalError`：不正确的使用 `eval()` 方法时抛出。
- `SyntaxError`：出现语法错误时抛出。
- `RangeError`：数字超出合法范围时抛出、
- `ReferenceError`：读取不存在的变量时抛出，无效引用。
- `TypeError`：变量或参数不属于有效类型。
- `URIError`：URI 编码和解码错误时抛出。例如，给 `encodeURI()` 或 `decodeURI()` 传递的参数无效。

## 3. throw

`throw` 语句用来抛出一个用户自定义的异常。当前函数的执行将被停止（`throw` 之后的语句将不会执行），并且控制将被传递到调用堆栈中的第一个 `catch` 块。如果调用者函数中没有 `catch` 块，程序将会终止。

```js
try {
    console.log('before throw');
    throw new TypeError('This is a TypeError');
    console.log('after throw'); // 这条语句不会执行
} catch (e) {
    console.log(e.name);
    console.log(e.message);
}
/*
before throw
TypeError
This is a TypeError
*/
```

## 4. 关于嵌套的 try 块

任何给定的异常只会被离它最近的封闭 `catch` 块捕获一次。当然，在 “inner” 块抛出的任何新异常 （因为 `catch` 块里的代码也可以抛出异常），将会被 “outer” 块所捕获。

```js
try {
    try {
        throw new Error('oops')
    } catch (e) {
        console.log('[inner] ' + e.message);
        throw e;
    } finally {
        console.log('[inner] finally');
    }
} catch (e) {
    console.log("[outer] " + e.message);
}
/*
[inner] oops
[inner] finally
[outer] oops
*/
```

如果从 `finally` 块中返回一个值，那么这个值将会成为整个 `try-catch-finally` 的返回值，无论是否有 `return` 语句在 `try` 和 `catch` 中。这包括在 `catch` 块里抛出的异常。

```js
try {
    try {
        throw new Error('oops')
    } catch (e) {
        console.log('[inner] ' + e.message);
        throw e; // 这里抛出的异常被 return 语句给覆盖了，所以外层无法捕获
    } finally {
        console.log('[inner] finally');
        return;
    }
} catch (e) {
    console.log("[outer] " + e.message); // 无法捕获内层抛出的异常
} finally {
    console.log('[outer] finally');
}
/*
[inner] oops
[inner] finally
[outer] finally
*/
```

#
#