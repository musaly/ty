1. 字符串
   1. `ary=txt.split('-')    `                     分割，返回数组
   2. `str.indexOf(str1)   `                      是否包含,返回第一个索引
   3. `str=str1.slice(0, 4)  `                    截取索引
   4. `str=str1.trim()`                           取消前后空格
   5. `trimStart()` 去除字符串开头连续的空格（`trimLeft` 是此方法的别名）
   6. `trimEnd()` 去除字符串末尾连续的空格（`trimRight` 是此方法的别名）
   6. `str.replace('a', 'b');`替换
2. 数学  
   1. `Math.random() `                            0-1的数不包括1
   2. `Math.floor() `                             取整(无视小数部分)
   3. Math.PI // 圆周率
   4. Math.floor() // 向下取整
   5. Math.ceil() // 向上取整
   6. Math.round() // 四舍五入，遇到  .5 往大了取
   7. Math.abs() // 绝对值
   8. Math.max() // 最大值
   9. Math.min() // 最小值
3. 数组
   1. `ary.unshift(el)`                           头部添加
   2. `ary.shift(el)  `                           头部删除
   3. `ary.push(el)`                              尾部添加
   4. `ary.pop(el)  `                             尾部删除
   5. `ary.splice(索引，删除数，元素1，元素2)    `                        替换
   6. `ary.reverse(el)     `                      倒序
   7. `filter((el)=>{return code})     `          筛选
   8. `arr.sort((pre, p2) => { pre-p2})`    升序
   9. `arr.forEach( (el) => {code} )`             对数组特点操作
   10. `array.map(function (currentValue, index, arr))`
   11. `array.some(function(currentValue, index, arr));`
   12. `arr.reduce((pre,cur)=>{},0)`
   13. `arr.indexOf(el)	` 索引
   14. `arr.join('分隔符')	` 字符串
   15. `arr1.includes(el)` 是否包含
   16. `Array.flat(i)`：展平一个多维数`i` 为要展开的层数
   17. `Array.prototype.flatMap`方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。
4. 对象
   1. `const keys = Object.keys(obj) `            汇总对象中所有的属性形成一个数组
   2. `Object.defineProperty(obj, prop, descriptor)`
   3. `Object.assign(target, sources)` es6 新增方法可以 浅拷贝。
   4. `Object.setPrototypeOf` 用于设置对象的原型对象，
   5. `Object.getPrototypeof` 用于获取对象的原型对象，相当于 `__proto__`。
   6. `Object.values()` 方法返回一个给定对象的所有可枚举属性值的数组
   7. `Object.entries()` 方法返回一个给定对象自身可遍历属性
   8. `Object.fromEntries()` 方法把可迭代对象的键值对列表转换为一个对象。 
5. JSON
   1. `JSON.stringify(userInfo)   `               转换成json格式
   2. `JSON.parse(userInfo)`                      json->js格式
6. Date
   1. `Date.now()      `                          时间戳
   2. Date() 时间
7. time
   1. `setTimeout(() => {code}, 1000)`
8. obj
   1. obj={...obj01,..obj02}                    对象合并
9.  
   2. typeof() 返回类型字符串
   3. instanceof  对象，是否为构造函数