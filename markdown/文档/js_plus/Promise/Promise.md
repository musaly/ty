# （一）前置准备

## 1. 实例对象与函数对象

- 函数对象: 将函数作为对象使用时, 简称为函数对象
- 实例对象: `new` 函数产生的对象, 称为实例对象，简称为对象


```js
function Fn() { } 

let fn = new Fn() //- -实例对象-构造函数
console.log(fn)
console.log(Fn.prototype)//函数对象
console.log(Fn.bind())
```
输出：
```
Fn {}
{}
[Function: bound Fn]
```

`fn` 是通过 `new` 构造函数的形式产生的对象，所以 `fn` 是实例对象。`Fn` 是 `function` 定义的，所以 `Fn` 是函数，同时，`Fn` 具有 `prototype` 属性，按照语法格式说明 `Fn` 也是一个对象，所以 `Fn` 是一个函数对象。

## 2. 两种回调函数

### 2.1 理解

回调函数：函数被作为实参传入另一函数，并在该外部函数内被调用，用以来完成某些任务的函数，称为回调函数。

- 同步回调
  - 理解: 立即执行, 完全执行完了才结束，不会放入回调队列中
  - 例子: 数组遍历相关的回调函数 / Promise的excutor函数
- 异步回调: 
  - 理解: 不会立即执行，会放入回调队列中将来执行
  - 例子: 定时器回调 / ajax回调 / Promise的成功|失败的回调

### 2.2 举例

**同步回调举例**

```js
function hello(s) {
  console.log(s)
}
function say(callback) {
  console.log('say hello')
  callback('hello')//回调函数
}
say(hello)
```
输出：
```
say hello
hello
```
回调函数就是把函数作为参数，然后再当前函数执行完后，再执行的函数。同步回调就是当前函数执行完后，会立即执行内部的回调函数。

**异步回调举例**

```js
setTimeout(() => {
  console.log(2)
}, 0)
console.log(1)
```

这里的 `setTimeout` 接收一个箭头函数作为参数，形成了回调函数，而且是异步回调。异步回调函数不会立即执行，而是先放在一个回调队列中，后面才会执行。所以结果如下：
```js
1
2
```

## 3. Error 对象

ECMA-262 规范了 7 种错误类型，具体说明如下。其中 `Error` 是基类，其他 6 种错误类型是子类，都继承 `Error` 基类。`Error` 类型的主要用途是自定义异常对象。

`Error` 创建自定义异常:
```js
new Error([message])
```

内置的错误类型，继承自 `Error`：
- `Error`：普通异常。与 `throw` 语句和 `try/catch` 语句一起使用，`message` 属性可以读写详细错误信息。
- `EvalError`：不正确的使用 `eval()` 方法时抛出。
- `SyntaxError`：出现语法错误时抛出。
- `RangeError`：数字超出合法范围时抛出、
- `ReferenceError`：读取不存在的变量时抛出，无效引用。
- `TypeError`：变量或参数不属于有效类型。
- `URIError`：URI 编码和解码错误时抛出。例如，给 `encodeURI()` 或 `decodeURI()` 传递的参数无效。

使用 `try/catch/finally` 可以捕获并处理异常，具体请查看：
https://docs.mphy.top/#/JavaScript/ch13

# （二）Promise 的理解和使用

## 1. Promise 的理解

### 1.1 定义

MDN 上的定义：一个 `Promise` 对象代表一个在这个 `Promise` 被创建出来时不一定已知的值。它让您能够 **把异步操作最终的成功返回值或者失败原因和相应的处理程序关联起来**。 这样使得异步方法可以像同步方法那样返回值：**异步方法并不会立即返回最终的值，而是会返回一个 promise，以便在未来某个时候把值交给使用者**。

- 抽象表达：Promise 是 ES6 引入的异步编程的新解决方案。在 Promise 出现之前，只是单纯的使用回调函数。
- 具体表达：Promise 是一个构造函数，由 Promise 产生的对象用来封装一个异步操作，并且可以获取其成功/失败的最终结果。

### 1.2 Promise 的状态

一个 `Promise` 必然处于以下几种状态之一：
- 待定（`pending`）: 初始状态，既没有被兑现，也没有被拒绝。
- 成功（`fulfilled`）: 意味着操作成功完成。
- 失败（`rejected`）: 意味着操作失败。

一个 `Promise` 的状态只能由 `pending` 变为 `fulfilled`，或者变为 `rejected`，且只能改变一次。

链式调用：`Promise` 对象具有 `then` 和 `catch` 方法来处理下一步的操作。因为 `Promise.prototype.then` 和 `Promise.prototype.catch` 方法返回的是 `Promise`，所以它们可以被链式调用。

### 1.3 Promise 的基本流程

![Promise](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/front-end/Promise.rtseidrtnm8.webp)

一个 `Promise` 对象刚被创建时的初始状态为 `pending`。接下来会执行异步操作，若异步操作成功，则执行 `resolve()` 函数，可将成功返回的数据通过 `resolve(data)` 返回。若异步操作失败，则执行 `reject()` 函数，将失败的信息返回。

无论成功还是失败，返回的都是 `Promise` 对象，具有 `then()`成功失败 和 `catch()`只有失败 方法。

返回的 `Promise` 使用 `then()` 调用：
```js
promise.then(successCallback, failureCallback);
```
其中，`successCallback` 是成功的回调函数，`failureCallback` 是失败的回调函数。一般格式为：
```js
promise.then(value=>{}, reason=>{})
```

### 1.4 Promise 的基本使用

构造函数 `Promise()`内部自动执行一个 **执行器函数**，也叫 `executor`。这个执行器函数又接收两个参数，第一个为执行成功的回调函数（`resolve`），第二个为操作成功的回调函数（`reject`）。

需要注意，**executor 执行器函数是同步回调函数**。  
例如有以下代码：
```js
new Promise(
  // 执行器函数开始
  (resolve, reject) => {
    console.log(1)
    // 异步操作
    setTimeout(() => {
      console.log(2)
    }, 0)
    console.log(3)
  }
)
console.log(4)
```
打印结果是：1、3、4、2

**基本使用流程**
```js
const promise = new Promise((resolve, reject) => {

  // 执行异步操作
  // 操作成功，可将数据传入
  resolve(data)
  // 操作失败，可将错误信息传入
  reject(err_msg)

})

// 处理返回结果
promise.then(
  // 操作成功的回调
  value => { },
  // 操作失败的回调
  reason => { }
)
```

具体例子如下：
```js
// 1. 创建 Promise 对象，此时为 pending 状态
const promise = new Promise((resolve, reject) => {
  // 2. 执行异步操作，这里是定时器函数
  setTimeout(() => {
    let time = Date.now()
    if (time % 2 === 1) {
      // 2.1 假定 time 为奇数时为操作成功，则执行 resolve
      resolve('成功的值：' + time)
    } else {
      // 2.1 假定 time 为偶时为操作失败，则执行 reject
      reject('失败的值：' + time)
    }
  }, 1000)
})

// 3. promise 能指定成功或失败的回调函数来获取成功的 value，或失败的 reason
promise.then(
  // 3.1 操作成功（resolve）的回调函数
  value => {
    console.log(value)
  },
  // 3.1 操作失败哦（reject）的回调函数
  reason => {
    console.log(reason)
  }
)
```

## 2. 为什么要使用 Promise

原因：
- 指定回调函数的方式更加灵活
- 支持链式调用，解决回调地狱问题

### 2.1 指定回调函数的方式更加灵活

- 在出现 Promise 以前，纯回调方式：在启动异步任务的同时，必须先指定好回调函数，否则会拿不到数据。
- Promise：启动异步任务 => 返回 Promise 对象 => 给 promise 绑定回调函数。甚至可以在异步任务结束后再指定回调函数，而这在单纯的回调方式中是不行的。

下面举例说明。

#### 2.1.1 MDN 上的例子

使用 MDN 上的例子：假设现在有一个名为 `createAudioFileAsync()` 的函数，它接收一些配置和两个回调函数，然后异步地生成音频文件。一个回调函数在文件成功创建时被调用，另一个则在出现异常时被调用。创建一个文件需要一些时间，因此是一个异步回调。

> 参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_promises

为了方便说明，下面都是伪代码。

```js
// 成功的回调函数
function successCallback(result) {
  console.log("声音文件创建成功: " + result);
}
// 失败的回调函数
function failureCallback(error) {
  console.log("声音文件创建失败: " + error);
}
```

传统的纯回调方式，需要先指定好成功和失败的回调函数。也就是说，在文件创建的结果出来之前，回调函数必须先指定好，否则文件的结果无法处理。

```js
createAudioFileAsync(audioSettings, successCallback, failureCallback)
```

对于 `Promise`，无需考虑这方面。**在启动异步任务之前或者之后，都可以指定好回调函数。这样，异步任务指定回调函数的方式就更加灵活了**。

```js
const promise = createAudioFileAsync(audioSettings);
promise.then(successCallback, failureCallback);
```

#### 2.1.2 实际例子

上述说明比较抽象，下面来一个实际情况的例子。

假如现在有一个 ajax 请求，获取服务器的某用户的名字。从发出请求到获得结果需要花费一些时间，这里使用定时器模拟请求。

```js
function success(name) {
  console.log('成功：' + name)
}

function failure(msg) {
  console.log('失败：' + msg)
}
```

**传统纯回调方式**

```js
function ajax(success, failure) {
  setTimeout(() => {
    // 这里可以假设获取数据成功或失败
    success('peter')
  }, 1000)
}

// 在启动异步任务的同时，必须先指定好 success 和 failure
ajax(success, failure)
// 输出：peter
```

**Promise 方式**

```js
const promise = new Promise((resolve, reject) => {
  // 模拟 ajax 请求，1s后获取到数据
  setTimeout(() => {
    resolve('peter')
  }, 1000)
})
// 此时异步任务已启动，不必先指定回调
```

可以在异步任务启动之后，在指定好回调函数

```js
promise.then(value => {
  success(value)
}, reason => {
  failure(reason)
})
// 输出：peter
```

甚至可以在异步任务完成后指定。请求在 1s 完成，而指定回调队列在 2s 完成。

```js
setTimeout(() => {
  promise.then(value => {
    success(value)
  }, reason => {
    failure(reason)
  })
}, 2000)
// 输出：peter
```

### 2.2 支持链式调用，解决回调地狱问题

#### 2.2.1 回调地狱

回调地狱：回调函数嵌套调用，**外部回调函数异步执行的结果是嵌套的回调函数执行的条件**。  
回调地狱的缺点：**不便于阅读，不便于异常处理**。

开发中经常会遇到多重异步操作，就会出现下面的写法（伪代码）：
```js
doSomething(function(result) {
  doSomethingElse(result, function(newResult) {
    doThirdThing(newResult, function(finalResult) {
      console.log('Got the final result: ' + finalResult);
    }, failureCallback);
  }, failureCallback);
}, failureCallback);
```

例如，现在要获取一个用户所有的商品数据，首先要根据用户名获取用户ID，然后根据ID获取订单信息，根据订单信息获取商品信息。一共要发起三次请求，前面的请求结果是后面请求的条件。

#### 2.2.2 链式调用，解决回调地狱

一个 `Promise` 对象具有 `then` 和 `catch` 方法，而 `then` 和 `catch` 的返回结果依然是一个 `Promise` 对象，因此可以使用 `.` 符号进行链式调用。

对于上述伪代码，使用 `Promise`的形式改写如下：

```js
// 把回调绑定到返回的 Promise 上，形成一个 Promise 链
doSomething().then(function(result) {
  return doSomethingElse(result);
})
.then(function(newResult) {
  return doThirdThing(newResult);
})
.then(function(finalResult) {
  console.log('Got the final result: ' + finalResult);
})
.catch(failureCallback);
```

链式调用格式：
```js
const p = new Promise(resolve=>{}, reject=>{});
p.then(value=>{}, reason=>{})
.then(value=>{}, reason=>{})
.then(value=>{}, reason=>{})
...
```

### 2.3 终极方案：使用 async/await

`Promise` 链式调用已经解决了回调地狱函数层层嵌套的问题了，还需要解决什么问题么？没错，我们还要砍掉 `Promise` 的回调函数，**回调函数太多，代码写的很长**。

`async/await` 是 ES8 出的一个更加优雅的异步编程解决方案，它可以让异步操作代码变得像同步代码一样，看起来非常优雅而直观。

上述例子，使用 `async/await` 改写的形式：
```js
async function request() {
  try {
    const result = await doSomething()
    const newResult = await doSomethingElse(result)
    const finalResult = await doThirdThing(newResult)
    console.log('Got the final result: ' + finalResult);
  } catch (error) {
    failureCallback(error)
  }
}
```

这里提一下，后面会详细讲解。

## 3. 如何使用 Promise 

### 3.1 Promise API

> [!TIP]
> 本节参考MDN，加上自己的理解，以及老师的PPT，强烈建议阅读原文。
> MDN链接：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/all

#### 1. Promise 构造函数

Promise 构造函数接收一个执行器 `executor`，来启动这个 Promise。

```js
new Promise(executor)
```

这个 `executor` 执行器函数又接收两个参数 `resolve` 和 `reject`，分别表示操作成功和操作失败。

```js
new Promise((resolve, reject) => {
  resolve()
  // reject()
})
```

- `executor` 函数：执行器 `(resolve, reject) => { }`  
- `resolve` 函数：内部定义成功时我们调用的函数 `value => {}`
- `reject` 函数：内部定义失败时我们调用的函数 `reason => {}`

> [!TIP]
> executor 会在 Promise 内部立即同步调用，而异步操作则在 executor 执行器中执行。

#### 2. Promise.prototype.then()

`Promise.prototype.then` 方法绑定在原型 `prototype` 上，意味着这是一个实例方法，必须在实例对象上才能使用。该方法返回的结果依然是一个 `Promise` 对象，意味着我们可以进行链式调用。

语法：
```js
p.then(onFulfilled, onRejected);

p.then(value => {
  // fulfillment
}, reason => {
  // rejection
});
```

参数：
- `onFulfilled` 函数：成功的回调函数 `(value) => {}`
- `onRejected` 函数：失败的回调函数 `(reason) => {}`

返回值：  
如果 `then` 中的回调函数：
- 返回了一个值，那么 `then` 返回的 Promise 将会成为接受状态（`fulfilled`），并且将返回的值作为接受状态的回调函数的参数值。
- 没有返回任何值，那么 `then` 返回的 Promise 将会成为接受状态（`fulfilled`），并且该接受状态的回调函数的参数值为 undefined。
- 抛出一个错误，那么 `then` 返回的 Promise 将会成为拒绝状态（`rejected`），并且将抛出的错误作为拒绝状态的回调函数的参数值。
- 返回一个已经是接受状态（`fulfilled`）的 Promise，那么 `then` 返回的 Promise 也会成为接受状态，并且将那个 Promise 的接受状态的回调函数的参数值作为该被返回的Promise的接受状态回调函数的参数值。
- 返回一个已经是拒绝状态（`rejected`）的 Promise，那么 `then` 返回的 Promise 也会成为拒绝状态，并且将那个 Promise 的拒绝状态的回调函数的参数值作为该被返回的Promise的拒绝状态回调函数的参数值。
- 返回一个未定状态（`pending`）的 Promise，那么 `then` 返回 Promise 的状态也是未定的，并且它的终态与那个 Promise 的终态相同；同时，它变为终态时调用的回调函数参数与那个 Promise 变为终态时的回调函数的参数是相同的。

> [!TIP]
> 以上参考MDN，个人觉得讲的很详细。链接：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/then

#### 3. Promise.prototype.catch()

`catch()` 方法返回一个 `Promise`，并且处理操作失败的情况。它的行为与调用 `Promise.prototype.then(undefined, onRejected)` 相同。但是用起来更方便了，可以看作是一种 **语法糖**（让我们执行某些操作更加方便简洁的方法）。

语法：
```js
p.catch(onRejected);

p.catch(reason => {
   // 操作失败
});
```

等同于：
```js
p.then(undefined, onFulfilled);

p.then(undefined, reason => {
  // 操作失败
})
```

参数：
- `onRejected`：操作失败时的回调函数 `(reason) => {}`

返回值：
- 返回一个 `Promise` 对象。如果 `onRejected` 抛出一个错误或返回一个本身失败的 `Promise`，那么 `catch()` 返回的 `Promise` 的状态为 `rejected`；否则，状态为 `fulfilled`。

#### 4. Promise.resolve()

`Promise.resolve()` 是一个函数对象方法，意味着只能用在函数对象 `Promise` 上。它接收一个 `value` 参数，返回一个这个给定值解析后的 `Promise` 对象。

语法：
```js
Promise.resolve(value);
```

参数：
- `value`：被解析的参数，可以是一个值，也可以是一个 Promise 对象，或者是一个 thenable

返回结果：
- 若给定值为一个普通数、字符串或数组等等之类的，则返回一个成功的 Promise
- 若参数本身就是一个 Promise 对象，则直接返回这个 Promise 对象。
- 由此可知，`resolve()` 方法可以返回一个成功或者失败的 Promise 对象

#### 5. Promise.reject()

`Promise.reject()` 方法返回一个失败的 Promise 对象，接收一个 `value` 参数，表示失败的原因。

语法：
```js
Promise.reject(reason);
```

参数：
- `reason`：表示操作失败的原因

返回值：
- 返回一个失败（状态为 `rejected` ）的 Promise 对象

#### 6. Promise.all()

`Promise.all()` 方法接收由多个 promise 组成的可迭代类型（Array、Map、Set等），然后返回一个新的 promise。它等待所有 promise 完成，或者第一个失败的 promise。

```js
Promise.all(iterable);

Promise.all(promise1, promise2, ...)

const p = Promise(promise1, promise2)
p.then(values=>)
```

参数：
- `iterable`：可迭代类型，一般为数组

返回值：
- 若传入的参数为空的可迭代对象，例如 `Promise.all([])`，则返回一个已完成状态（`fulfilled`）的 Promise
- 若传入的参数不包含任何 promise，则返回一个异步完成（`asynchronously resolved`）的 Promise。例如 `Promise.all([1, 2])`
- 其它情况下返回一个处理中（`pending`）的 Promise。只有接收的参数的 promise 全部成功，这个返回的 Promise 才会是成功的，只要有一个失败，则返回一个失败的 Promise，且返回的值为第一个失败的值。
- 若所有 promise 都成功，则返回的 Promise 的值为一个包含了多个结果的数组

Promise.all 的同步与异步：
- **当如果传入的可迭代对象是空的，就是同步；其他情况都是异步**。

举例:  
参数为非空的数组，异步的：
```js
const p = Promise.all([1])
setTimeout(() => {
  console.log(p)
})
console.log('同步代码')
console.log(p) // (1)
// 输出：
// 同步代码
// Promise {<pending>}
// Promise {<fulfilled>: Array(1)}
```
注意：此时（1）输出状态为 `pending`，因为同步代码先执行，而此时异步 promise 的结果还未知

参数为空数组，同步的：
```js
const p1 = Promise.all([])
setTimeout(() => {
  console.log(p1)
})
console.log('同步代码')
console.log(p1) // （1）
// 输出
// 同步代码
// Promise {<fulfilled>: Array(0)}
// Promise {<fulfilled>: Array(0)}
```
注意：此时（1）输出状态为 `fulfilled`，说明此时 `Promise.all` 是同步的。

**Promise.all 方法举例**

```js
// 参数为空的数组
const p1 = Promise.all([])

// 参数为不包含 promise 的数组
const p2 = Promise.all([1, 2, 3])

// 参数为全部是成功的 promise 的数组
let pm1 = Promise.resolve(1)
let pm2 = Promise.resolve(2)
let pm3 = Promise.resolve(3)
const p3 = Promise.all([pm1, pm2, pm3])

// 结果
setTimeout(() => {
  console.log(p1)
  console.log(p2)
  console.log(p3)
  // Promise {<fulfilled>: Array(0)}
  // Promise {<fulfilled>: Array(3)}
  // Promise {<fulfilled>: Array(3)}
})

// 参数为包含失败的 promise 的数组
let pe1 = Promise.resolve(1)
let pe2 = Promise.reject('error')
let pe3 = Promise.resolve(3)
const p4 = Promise.all([pe1, pe2, pe3])

setTimeout(() => {
  console.log(p4)
})
// 输出
// Promise {<rejected>: 'error'}
```

#### 7. Promise.race()

`Promise.race()` 也是接收一个可迭代类型，例如一个包含了多个 promise 的数组。然后返回一个新的 promise，第一个完成的 promise 的结果状态就是最终返回的结果状态。

需要注意，这里最终返回的结果的状态不一定是参数数组中位于前面的 promise，具体要看哪一个最先完成，所以 `race()` 方法的返回结果可能为成功或失败的。

语法：
```js
Promise.race(iterable);
```

参数：
- `iterable`：可迭代对象，一般为包含多个 promise 的数组

返回值：
- 返回一个 promise，只要给定的可迭代对象中的 promise 有一个先完成（成功或失败），就采用它的值作为最终 promise 的值，状态与这个完成的 promise 相同。

Promise.race 的异步性（没有同步性）：
```js
const p = Promise.race([Promise.resolve(10), Promise.resolve(20)])

// 立即输出p，此时p状态为 pending
console.log(p)

setTimeout(() => {
  // 等栈中代码执行完毕之后执行，可得到完成的promise
  console.log('the stack is now empty');
  console.log(p)
})

// 输出：
// Promise { <state>: "pending" }
// the stack is now empty
// Promise { <state>: "fulfilled", <value>: 33 }
```
注意：`Promise.race` 没有同步性

### 3.2 Promise 的几个关键问题

#### 1. 如何改变 Promise 的状态？

- `resolve(value)`：如果当前是 pending 就会变为 resolved
- `reject(reason)`：如果当前是 pending 就会变为 rejected
- 抛出异常：如果当前是 pending 就会变为 rejected

#### 2. 一个promise指定多个成功/失败回调函数，都会调用吗?

当 promise 改变为对应状态时都会调用。
```js
let p = new Promise((resolve, reject) => {
  throw 100
})
p.then(
  value => { },
  reason => {
    console.log('reason1 ' + reason)
  }
)
p.then(
  value => { },
  reason => {
    console.log('reason2 ' + reason)
  }
)
// 输出
// reason1 100
// reason2 100
```

#### 3. 改变 promise 状态和指定回调函数谁先谁后？

1. 都有可能，正常情况下是先指定回调再改变状态，但也可以先改状态再指定回调
2. 如何先改状态再指定回调?
    - 在执行器中直接调用 `resolve()/reject()`
    - 延迟更长时间才调用 `then()`
3. 什么时候才能得到数据?
    - 如果先指定的回调，那当状态发生改变时，回调函数就会调用，得到数据
    - 如果先改变的状态，那当指定回调时，回调函数就会调用，得到数据

```js
// 正常情况，先指定回调再改变状态
const p2 = new Promise((resolve, reject) => {
  // setTimeout 第三个参数，该参数将传入第一个函数参数
  setTimeout(resolve, 1000, '成功的数据') // 后改变数据，同时传入值
}).then(
  // 先指定回调函数，保存当前回调函数
  value => {
    console.log(value)
  }
)

// 先改状态，在指定回调函数
const p1 = new Promise((resolve, reject) => {
  resolve(100) // 先改变数据，同时传入值
}).then(
  // 后指定回调函数，异步执行回调函数
  value => {
    console.log(value)
  }
)
```
> [!TIP]
> 注意：new Promise(executor) 中的执行器以及 `.then`、`.catch` 都是同步的，但是执行器中的异步操作是异步的，`.then` 和 `.catch` 中的回调函数也是异步的。

#### 4. promise.then() 返回的新promise 的结果状态由什么决定？

- 简单表达：由 `then()` 指定的回调函数执行的结果决定
- 详细表达：
  1. 如果抛出异常，新 promise 变为 `rejected`, reason为抛出的异常
  2. 如果返回的是非 promise 的任意值，新promise变为 `resolved`，value 为返回的值
  3. 如果返回的是另一个新 promise，此 promise 的结果就会成为新 promise 的结果

#### 5. promise 如何串连多个操作任务?

- promise的 `then()` 返回一个新的 promise，可以看成 `then()` 的链式调用
- 通过 `then` 的 **链式调用串连多个同步/异步任务**

> [!TIP]
> `.then()` 中可以处理同步任务，也可以处理异步任务。处理异步任务时需要新创建一个 `Promise`。 

```js
// 任务1
const p = new Promise((resolve, reject) => {
  setTimeout(resolve, 0, '任务1的数据(异步)')
})

p.then(
  value => {
    console.log(value)
    // 任务2（同步）
    return '任务2的数据(同步)'
  },
  reason => {
    console.log(reason)
  },
).then(
  value => {
    // 任务3（异步）
    return new Promise((resolve, reject) => {
      console.log(value)
      setTimeout(reject, 0, '任务3的错误信息(异步)')
    })
  },
  reason => {
    console.log(reason)
  }
).catch(reason => {
  console.log(reason)
})
// 输出
// 任务1的数据(异步)
// 任务2的数据(同步)
// 任务3的错误信息(异步)
```

#### 6. 异常传透

在 Promise 的链式调用链中，当所有的 `.then` 中都没有指定错误处理的回调，则前面出现的异常会在最后失败的回调中处理。

```js
new Promise((resolve, reject) => {
  reject(1)
}).then(
  value => {
    console.log(value)
  }
).then(
  value => {
    console.log(value)
  }
).catch(reason => {
  console.log('异常：' + reason)
})
```

注意：
- `.catch` 所谓的异常穿透并不是一次失败状态就触发 `catch`，而是一层一层的传递下来的
- 异常穿透的前提条件是所有的 `.then` 都没有指定失败状态的回调函数。
- 如果 `.catch` 前的所有 `.then` 都指定了失败状态的回调函数，`.catch` 就失去了意义。

#### 7. 值传透

值穿透指的是，链式调用的参数不是函数时，会发生值穿透，就传入的非函数值忽略，传入的是之前的函数参数。

```js
Promise.resolve(1)
  .then(2)
  .then(Promise.resolve(3))
  .then(console.log) // 1
```

只有传入的是函数才会传递给下一个链式调用。
```js
Promise.resolve(1)
  .then(2)
  .then(() => 3)
  .then(4)
  .then(console.log) // 3
```

```js
Promise.resolve(1)
  .then(function () {
    return 2
  })
  .then(() => { Promise.resolve(3) }) // 没有返回值，默认 undefined
  .then(4)
  .then(console.log) // undefined
```

#### 8. 中断 Promise 链

- 什么是中断：当使用 promise 的 `then` 链式调用时，在中间中断，不再调用后面的回调函数
- 中断的方法：在回调函数中返回一个 `pendding` 状态的 promise 对象

如何返回一个 `pendding` 状态的 promise 对象：
```js
return new Promise(() => { }) // pending
```
或者使用 `Promise.race([])`，`race` 方法接收一个空的可迭代对象时，该 Promise 会一直处于 `pendding` 状态。
```js
return Promise.race([]) // pending
```

中断之前：
```js
Promise.resolve(1)
  .then(value => {
    console.log(value) // 1
  }) // 下面都会打印
  .then(value => console.log(value)) // undefined
  .then(value => console.log(value)) // undefined
```

中断之后：
```js
Promise.resolve(1)
  .then(value => {
    console.log(value) // 1
    // 返回一个 pending 状态的 promise 来中断这个调用链
    return new Promise(() => { })
    // 或者：return Promise.race([])
  }) // 下面都不会打印
  .then(value => console.log(value))
  .then(value => console.log(value))
```



# （三）手写 Promise

## 1. 构造函数实现

使用 `IIFI` 模块化，`function` 构造函数手写 Promise。
```js
/*
  * 自定义 Promise 函数模块：IIFE立即执行函数
  * 关键：then方法实现
  * 构造函数实现
*/
(function (window) {

  const PENDING = 'pending'
  const RESOLVED = 'fulfilled'
  const REJECTED = 'rejected'

  /*
    Promise 构造函数
    executor: 执行器函数，立即同步执行
  */
  function Promise(executor) {
    const that = this
    // Promise对象状态属性，初始值为pending
    that.status = PENDING
    // 存储结果数据
    that.data = 'undefined'
    // 保存待执行的回调函数，数据结构：{onResolved(){},onRejected(){}}
    that.callbacks = []

    function resolve(value) {
      // 若当前状态不是 pending，直接结束
      if (that.status !== PENDING) {
        return
      }
      // 修改状态
      that.status = RESOLVED
      // 修改值
      that.data = value
      // 如有待执行的 callback 函数，立即异步执行回调函数 onResolved
      if (that.callbacks.length > 0) {
        // 模拟异步执行所有成功的回调函数
        setTimeout(() => {
          that.callbacks.forEach(callbacksObj => {
            callbacksObj.onResolved(value)
          });
        })

      }
    }

    function reject(reason) {
      // 若当前状态不是 pending，直接结束
      if (that.status !== PENDING) {
        return
      }
      // 修改状态
      that.status = REJECTED
      // 修改值
      that.data = reason
      // 如有待执行的 callback 函数，立即异步执行回调函数 onRejected
      if (that.callbacks.length > 0) {
        // 模拟异步执行所有成功的回调函数
        setTimeout(() => {
          that.callbacks.forEach(callbacksObj => {
            callbacksObj.onRejected(reason)
          });
        })

      }
    }

    // 立即同步执行
    try {
      executor(resolve, reject)
    } catch (error) {
      // 若执行器异常，promise 对象变为 rejected 状态
      reject(error)
    }

  }

  /*
    Promise原型对象 then 方法，
    两个回调函数 成功 onResolved ，失败onRejected
    返回一个新的Promise对象
    返回promise的结果由onResolved/onRejected执行结果决定
  */
  Promise.prototype.then = function (onResolved, onRejected) {

    const that = this

    onResolved = typeof onResolved === 'function' ? onResolved : value => value
    onRejected = typeof onRejected === 'function' ? onRejected : reason => { throw reason }

    // 返回一个新的 promise
    return new Promise((resolve, reject) => {
      // 使用指定函数处理，根据执行结果，改变return的promise的状态
      function handle(callback) {
        /* 1.回调函数抛出异常，则返回的Promise就会失败，reason就是error
          2. 回调函数返回的不是 promise，则返回的promise就会成功，value就是result
          3.回调函数返回的是promise，则返回的promise取决于这个promise
        */
        try {
          const result = callback(that.data)
          if (result instanceof Promise) {
            // 3.回调函数返回的是promise，则返回的promise取决于这个promise
            result.then(
              value => resolve(value), // 当result成功，返回的promise也成功
              reason => reject(reason) // 当result失败，返回的promise也失败
            )
            // result.then(resolve, reject) // 等同写法
          } else {
            //2. 回调函数返回的不是 promise，则返回的promise就会成功，value就是result
            resolve(result)
          }
        } catch (error) {
          // 1.回调函数抛出异常，则返回的Promise就会失败，reason就是error
          reject(error)
        }
      }

      // pending状态，保存回调函数
      if (that.status === PENDING) {
        that.callbacks.push({
          onResolved(value) {
            handle(onResolved)
          },
          onRejected(reason) {
            handle(onRejected)
          }
        })
        // resolved状态，异步执行回调函数，改变return的promise的状态
      } else if (this.status === RESOLVED) {
        setTimeout(() => {
          handle(onResolved)
        })
      } else { // 'rejected'，异步执行回调函数，改变return的promise的状态
        setTimeout(() => {
          handle(onRejected)
        })
      }
    })

  }

  /*
    Promise原型对象 catch ,参数为失败的回掉函数 onRejected
    返回一个新的Promise对象
  */
  Promise.prototype.catch = function (onRejected) {
    return this.then(undefined, onRejected)
  }


  /*
    Promise函数对象的 resolve 方法
    返回一个新的Promise对象,Promise.resolve()中可以传入Promise
    返回新promise得结果：
     - 若非promise，则返回成功的promise，value就是这个传入的参数
     - 若为promise，则返回成功或失败的promsie，取决于传入的promise的成功或失败
  */
  Promise.resolve = function (value) {

    return new Promise((resolve, reject) => {
      // 若为promise，则返回成功或失败的promsie，取决于传入的promise的成功或失败
      if (value instanceof Promise) {
        value.then(resolve, reject)
      } else { // 若非promise，则返回成功的promise，value就是这个传入的参数
        resolve(value)
      }
    })

  }

  /*
  Promise函数对象的 reject 方法
   返回一个新的Promise对象 Promise.reject中不能再传入Promise
 */
  Promise.reject = function (reason) {
    return new Promise((resolve, reject) => {
      reject(reason)
    })
  }

  /*
    Promise函数对象的 all 方法,接受一个promise类型的数组
    返回一个新的Promise对象
    所有promise成功则返回成功，只要有一个失败就失败
  */
  Promise.all = function (promises) {
    // 成功的promise的值
    const values = new Array(promises.length)
    // 记录成功的promise的数目
    let count = 0
    return new Promise((resolve, reject) => {
      // 遍历promises，获取每个promise的结果
      promises.forEach((p, index) => {
        // 使用  Promise.resolve(p) 再包装一遍，以接收字面量参数
        Promise.resolve(p).then(
          value => {
            count++
            values[index] = value
            // 全部成功，返回所有成功的值的数组
            if (count === promises.length) {
              resolve(values)
            }

          },
          reason => {
            // 出现失败就返回失败
            resolve(reason)
          }
        )
      })

    })
  }

  /*
    Promise函数对象的 race 方法,接受一个promise类型的数组
    返回一个新的Promise对象
  */
  Promise.race = function (promises) {
    return new Promise((resolve, reject) => {
      promises.forEach(p => {
        Promise.resolve(p).then(
          value => {
            resolve(value)
          },
          reason => {
            reject(reason)
          }
        )
      })
    })
  }

  /*
    resolveDelay：扩展工具方法，延迟返回结果
  */
  Promise.resolveDelay = function (value, time) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (value instanceof Promise) {
          value.then(resolve, reject)
        } else {
          resolve(value)
        }
      }, time)
    })
  }

  /*
    rejectDelay：扩展工具方法，延迟返回结果
  */
  Promise.rejectDelay = function (reason, time) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        reject(reason)
      }, time)
    })
  }

  // 向外暴露 Promise 函数
  window.Promise = Promise
})(window)
```

## 2. ES6 class 类实现

```js
/*
  * 自定义 Promise 函数模块：IIFE立即执行函数
  * 关键：then方法实现 
  * class类实现
*/
(function (window) {
  const PENDING = 'pending'
  const RESOLVED = 'fulfilled'
  const REJECTED = 'rejected'

  /*
    Promise 构造函数
    executor: 执行器函数，立即同步执行
  */
  class Promise {
    constructor(executor) {
      const that = this
      // Promise对象状态属性，初始值为pending
      that.status = PENDING
      // 存储结果数据
      that.data = 'undefined'
      // 保存待执行的回调函数，数据结构：{onResolved(){},onRejected(){}}
      that.callbacks = []

      function resolve(value) {
        // 若当前状态不是 pending，直接结束
        if (that.status !== PENDING) {
          return
        }
        // 修改状态
        that.status = RESOLVED
        // 修改值
        that.data = value
        // 如有待执行的 callback 函数，立即异步执行回调函数 onResolved
        if (that.callbacks.length > 0) {
          // 模拟异步执行所有成功的回调函数
          setTimeout(() => {
            that.callbacks.forEach(callbacksObj => {
              callbacksObj.onResolved(value)
            });
          })

        }
      }

      function reject(reason) {
        // 若当前状态不是 pending，直接结束
        if (that.status !== PENDING) {
          return
        }
        // 修改状态
        that.status = REJECTED
        // 修改值
        that.data = reason
        // 如有待执行的 callback 函数，立即异步执行回调函数 onRejected
        if (that.callbacks.length > 0) {
          // 模拟异步执行所有成功的回调函数
          setTimeout(() => {
            that.callbacks.forEach(callbacksObj => {
              callbacksObj.onRejected(reason)
            });
          })

        }
      }

      // 立即同步执行
      try {
        executor(resolve, reject)
      } catch (error) {
        // 若执行器异常，promise 对象变为 rejected 状态
        reject(error)
      }

    }
    /*
      Promise原型对象 then 方法，
      两个回调函数 成功 onResolved ，失败onRejected
      返回一个新的Promise对象
      返回promise的结果由onResolved/onRejected执行结果决定
    */
    then(onResolved, onRejected) {

      const that = this

      onResolved = typeof onResolved === 'function' ? onResolved : value => value
      onRejected = typeof onRejected === 'function' ? onRejected : reason => { throw reason }

      // 返回一个新的 promise
      return new Promise((resolve, reject) => {
        // 使用指定函数处理，根据执行结果，改变return的promise的状态
        function handle(callback) {
          /* 1.回调函数抛出异常，则返回的Promise就会失败，reason就是error
            2. 回调函数返回的不是 promise，则返回的promise就会成功，value就是result
            3.回调函数返回的是promise，则返回的promise取决于这个promise
          */
          try {
            const result = callback(that.data)
            if (result instanceof Promise) {
              // 3.回调函数返回的是promise，则返回的promise取决于这个promise
              result.then(
                value => resolve(value), // 当result成功，返回的promise也成功
                reason => reject(reason) // 当result失败，返回的promise也失败
              )
              // result.then(resolve, reject) // 等同写法
            } else {
              //2. 回调函数返回的不是 promise，则返回的promise就会成功，value就是result
              resolve(result)
            }
          } catch (error) {
            // 1.回调函数抛出异常，则返回的Promise就会失败，reason就是error
            reject(error)
          }
        }

        // pending状态，保存回调函数
        if (that.status === PENDING) {
          that.callbacks.push({
            onResolved(value) {
              handle(onResolved)
            },
            onRejected(reason) {
              handle(onRejected)
            }
          })
          // resolved状态，异步执行回调函数，改变return的promise的状态
        } else if (this.status === RESOLVED) {
          setTimeout(() => {
            handle(onResolved)
          })
        } else { // 'rejected'，异步执行回调函数，改变return的promise的状态
          setTimeout(() => {
            handle(onRejected)
          })
        }
      })

    }
    /*
      Promise原型对象 catch ,参数为失败的回掉函数 onRejected
      返回一个新的Promise对象
    */
    catch(onRejected) {
      return this.then(undefined, onRejected)
    }

    /*
    Promise函数对象的 resolve 方法
    返回一个新的Promise对象,Promise.resolve()中可以传入Promise
    返回新promise得结果：
    - 若非promise，则返回成功的promise，value就是这个传入的参数
    - 若为promise，则返回成功或失败的promsie，取决于传入的promise的成功或失败
  */
    static resolve = function (value) {

      return new Promise((resolve, reject) => {
        // 若为promise，则返回成功或失败的promsie，取决于传入的promise的成功或失败
        if (value instanceof Promise) {
          value.then(resolve, reject)
        } else { // 若非promise，则返回成功的promise，value就是这个传入的参数
          resolve(value)
        }
      })

    }

    /*
Promise函数对象的 reject 方法
返回一个新的Promise对象 Promise.reject中不能再传入Promise
*/
    static reject = function (reason) {
      return new Promise((resolve, reject) => {
        reject(reason)
      })
    }

    /*
    Promise函数对象的 all 方法,接受一个promise类型的数组
    返回一个新的Promise对象
    所有promise成功则返回成功，只要有一个失败就失败
  */
    static all = function (promises) {
      // 成功的promise的值
      const values = new Array(promises.length)
      // 记录成功的promise的数目
      let count = 0
      return new Promise((resolve, reject) => {
        // 遍历promises，获取每个promise的结果
        promises.forEach((p, index) => {
          // 使用  Promise.resolve(p) 再包装一遍，以接收字面量参数
          Promise.resolve(p).then(
            value => {
              count++
              values[index] = value
              // 全部成功，返回所有成功的值的数组
              if (count === promises.length) {
                resolve(values)
              }

            },
            reason => {
              // 出现失败就返回失败
              resolve(reason)
            }
          )
        })

      })
    }

    /*
      Promise函数对象的 race 方法,接受一个promise类型的数组
      返回一个新的Promise对象
    */
    static race = function (promises) {
      return new Promise((resolve, reject) => {
        promises.forEach(p => {
          Promise.resolve(p).then(
            value => {
              resolve(value)
            },
            reason => {
              reject(reason)
            }
          )
        })
      })
    }

    /*
      resolveDelay：扩展工具方法，延迟返回结果
    */
    static resolveDelay = function (value, time) {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          if (value instanceof Promise) {
            value.then(resolve, reject)
          } else {
            resolve(value)
          }
        }, time)
      })
    }

    /*
    rejectDelay：扩展工具方法，延迟返回结果
  */
    static rejectDelay = function (reason, time) {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          reject(reason)
        }, time)
      })
    }

  }

  // 向外暴露 Promise 函数
  window.Promise = Promise
})(window)
```

# （四）JS 异步之宏队列与微队列

1. JS中用来 **存储待执行回调函数的队列包含 2 个不同特定的列队**
2. **宏队列**：用来保存待执行的宏任务（回调），比如：**定时器回调/DOM事件回调/ajax回调**
3. **微队列**：用来保存待执行的微任务（回调），比如：**promise回调/MutationObserver回调**
4. JS执行时会区别这两个队列  
    - JS引擎首先必须 **先执行所有的初始化同步任务代码**
    - 每次准备 **取出第一个宏任务执行前，都要将所有的微任务一个一个取出来执行**
5. Promise 的链式 `then` 方法执行前，都要等前面的任务执行完毕才能执行。
6. 哪个 promise 的状态先确定下来，就先执行哪个 `then` 方法

![promise2](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/promise2.6ocfwz4cb6s0.webp)

> [!TIP]
> 具体实例见下一节面试题。

# （五）Promise 相关面试题

**题1**

```js
setTimeout(() => {
  console.log(1)
}, 0)
Promise.resolve().then(() => {
  console.log(2)
})
Promise.resolve().then(() => {
  console.log(4)
})
console.log(3)
```

<details>
<summary>解析</summary>

```js
setTimeout(() => {
  console.log(1)
}, 0) // 入宏队列
Promise.resolve().then(() => {
  console.log(2)
}) // 入微队列
Promise.resolve().then(() => {
  console.log(4)
}) // 入微队列
console.log(3) // 主线程同步执行
```

```
同步任务：3
宏队列：[1]
微队列：[2 4]
同步任务先执行，宏队列要等微队列中的任务执行完毕才能取出执行。
```
最后输出顺序：3 2 4 1

</details>

---

**题2**

```js
setTimeout(() => {
  console.log(1)
}, 0)
new Promise((resolve) => {
  console.log(2)
  resolve()
}).then(() => {
  console.log(3)
}).then(() => {
  console.log(4)
})
console.log(5)
```

<details>
<summary>解析</summary>

```js
setTimeout(() => {
  console.log(1) // 入宏队列
}, 0)
new Promise((resolve) => {
  console.log(2) // 同步立即执行
  resolve() // 立即返回成功状态
}).then(() => {
  console.log(3) // 入微队列
}).then(() => {
  console.log(4) // 等待前面 3 的任务执行完后才能入微队列
})
console.log(5) // 同步立即执行
```

```
同步任务：2 5
宏队列：[1]
微队列：[3 4]
需要注意打印 4 的任务需要等前面打印 3 的任务执行后，才能放入微队列。
```
最后输出顺序：2 5 3 4 1

</details>

---

**题3**

```js
const first = () => (new Promise((resolve, reject) => {
  console.log(3)
  let p = new Promise((resolve, reject) => {
    console.log(7)
    setTimeout(() => {
      console.log(5)
      resolve(6)
    }, 0)
    resolve(1)
  })
  resolve(2)
  p.then((arg) => {
    console.log(arg)
  })
}))
first().then((arg) => {
  console.log(arg)
})
console.log(4)
```

<details>
<summary>解析</summary>

```js
const first = () => (new Promise((resolve, reject) => {
  console.log(3) // 同步立即执行
  let p = new Promise((resolve, reject) => {
    console.log(7) // 同步立即执行
    setTimeout(() => {
      console.log(5) // 加入宏队列
      resolve(6) // resolve(1) 已改变状态，状态只能改变一次，失效
    }, 0)
    resolve(1) // 同步立即改变状态，1为成功的值，先执行p的 then，这里跳往 p.then
  })
  resolve(2) // first 状态确定，去执行 first().then，成功值为2，入队列
  p.then((arg) => {
    console.log(arg) // 输出 1 添加到微队列
  })
}))
first().then((arg) => {
  console.log(arg) // arg=2，入微队列
})
console.log(4) // 同步立即执行
```

```
同步任务：3 7 4
宏队列：[5]
微队列：[1 2]
```
最后输出顺序：3 7 4 1 2 5

</details>

---

**题4**

```js
setTimeout(() => {
  console.log("0")
}, 0)
new Promise((resolve, reject) => {
  console.log("1")
  resolve()
}).then(() => {
  console.log("2")
  new Promise((resolve, reject) => {
    console.log("3")
    resolve()
  }).then(() => {
    console.log("4")
  }).then(() => {
    console.log("5")
  })
}).then(() => {
  console.log("6")
})

new Promise((resolve, reject) => {
  console.log("7")
  resolve()
}).then(() => {
  console.log("8")
})
```

这题文字不好解析，就当课后作业，自行分析吧:) 参考：
```
宏队列：[0]
微队列：[2 8 4 6 5]
```

最后答案：1 7 2 3 8 4 6 5 0

# （六）async 与 await

## 1. MDN 文档

文档上讲的很清楚，建议阅读文档上的例子和解释。

- async 函数：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function
- await：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/await

建议阅读：[掘金-ES8 中的 async/await——异步函数](https://juejin.cn/post/7031914178210185230)

## 2. async 函数

- 函数的返回值为 `promise` 对象
-  `promise` 对象的结果由 `async` 函数执行的返回值决定

## 3. await 表达式

- `await` 右侧的表达式一般为 `promise` 对象,但也可以是其它的值
- 如果表达式是 `promise` 对象，`await` 返回的是 `promise` 成功的值
- 如果表达式是其它值，直接将此值作为 `await` 的返回值
- `async/await` 中真正起作用的是 `await`，可以把 `async` 关键字简单的当作一个 标识符. 因为如果 **异步函数** 中不使用 `await` 关键字，其执行基本上跟普通函数没有什么区别，但是对于 **异步函数** 的返回值还是会和 **普通函数** 有区别

## 4.注意

- `await` 必须写在 `async` 函数中，但 `async` 函数中可以没有 `await`
- 如果 `await` 的  `promise` 失败了，就会抛出异常，需要通过 `try..catch` 捕获处理
- 当一个 promise 抛出异常时，要使用 `try...catch` 捕获异常，必须使用 `await` 使回调函数变为异步回调，否则 `try...catch` 无法捕获到错误。

```js
// 正确示例
async function fn1() {
  return new Promise((resolve, reject) => {
    reject('哈哈哈')
  }, 1000)
}
async function fn() {
  try {
    const res = await fn1() // 将 await 去掉，则catch 无法捕获异常
    console.log('成功：' + res)
  } catch (error) {
    console.log('异常：' + error)
  }
}
fn()
// 输出：'异常：哈哈哈'
```

- 在 `async function` 中是否有 `await` 是不一样的。若 `async function` 中没有 `await`，则这个函数就是纯同步执行，只是返回值是一个 `Promise`。
- 在 `async function` 中添加了 `await` 后，此行代码之前为立即执行，此行代码之后的语句一起作为 **整体** 变为微队列中的异步回调。相当于给后面的代码套了一层 `then` 方法。
- 在使用 `try..catch` 捕获了 `await` 中的异常后，`await` 后面代码将不会再执行。

```js
// 不使用 await
async function async1() {
  let a = "aaa";
  console.log(a);
}
async1();
console.log('bbb')
// 先输出 aaa，后输出 bbb
```

```js
// 使用 await
async function async1() {
  let a = await "aaa";
  console.log(a);
}
async1();
console.log('bbb')
// 先输出 bbb，后输出 aaa
```

# （七）异步综合面试题

解析较为简略，提供大致思路，还是建议自己分析。部分题目来自：[CSDN-async/await 面试题](https://blog.csdn.net/weixin_45345105/article/details/109691328)

**题目1**

```js
async function async1 () {
  let a = await new Promise((resolve) => {
    resolve();
  });
  console.log(a); 
}
async1();
```

<details>
<summary>解析</summary>

`await` 返回的是右边 promise 的最后结果值，没有返回参数默认为 `undefined`。所以打印结果是 `undefined`。
</details>

**题目2**

```js
async function async1() {
  let a = await new Promise((resolve) => {
    resolve("hello");
  }).then(() => {
    return "lala";
  });
  console.log(a);
}
async1();
```


<details>
<summary>解析</summary>

`await` 等待右边 Promise 最终返回的 `Promise` 的值，因此打印结果为 `lala`。

</details>

**题目3**

```js
async function async1() {
  let a = await "aaa";
  console.log(a);
}
async1();
console.log('bbb')
```

<details>
<summary>解析</summary>

`await` 右边接一个字面量值，则立即返回该值。然后使这行后面的代码变为异步回调，放入微队列中。先执行同步任务打印出 `bbb`，然后执行微队列中的任务，打印出 `aaa`。
```
微队列：[aaa]
同步任务：bbb
打印顺序：bbb aaa
```

</details>

**题目4**

```js
async function async1() {
  console.log('aaa')
  let a = await async2()
  console.log(a)
  setTimeout(() => {
    console.log('bbb')
  }, 0)
}
async function async2() {
  console.log('ccc')
  return Promise.resolve('ddd')
}
async1()
setTimeout(() => {
  console.log('eee')
}, 0)
console.log('fff')
```

<details>
<summary>解析</summary>

```
同步任务：aaa ccc fff 
宏队列：[eee bbb]
微队列：[ddd ]
打印顺序：aaa ccc fff ddd eee bbb
```
关键是明白 `async/await` 中真正起作用的是 `await`，`await` 前面代码同步执行，出现 `await` 则等待 Promise 结果并使后面代码变为异步任务。

</details>

**题目5**

```js
async function async1() {
  console.log('aaa')
  try {
    let res = await async2()
    console.log(res)
  } catch (e) {
    console.log(e)
  } finally {
    setTimeout(() => {
      console.log('bbb')
    }, 0)
  }
}

async function async2() {
  console.log('ccc')
  return Promise.reject('ddd')
}

async1()
setTimeout(() => {
  console.log('eee')
}, 0)
Promise.resolve().then(() => {
  console.log('fff')
})
console.log('ggg')
```

<details>
<summary>解析</summary>

```
同步任务：[aaa ccc ggg]
宏队列：[eee bbb]
微队列：[fff ddd]
打印顺序：aaa ccc ggg fff ddd eee bbb
```

这里关键是理清楚宏队列和微队列中异步任务入队的顺序。
</details>

#

#