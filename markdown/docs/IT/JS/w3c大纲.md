# w3c大纲

## Html
### 概念
- 浏览器 网页
- W3C标准：html  css js
- TDK标签 SEO优化

### 标签
- 语义化,属性()
1. `p,h,div,span`,文本格式化标签
2. `img,a`,特殊字符号`&nbsp;`
3. `table,tr,td,th,thead,tbody`合并单元格
4. `ul,ol,li`
5. `input`
   1. `type:button,checkbox,file,hidden,image,password,radio,reset,submit,text,	`
   2. `name,value,checked,maxlength,`
6. `label`
   1. `for`
7. `select,option`
8. `textarea`
   1. `rows,cols`
9. HTML5新增标签
   1. `<header><nav><article><section><asider><footer>`
   2. `vidio,audio`
   3. `input`
   4. 表单属性

## Css

### 概念
- 层叠样式表.语法规范
- 引用方式
- Emmet 语法
- 特性：层叠性、继承性、优先级

### 选择器
1. 基础选择器
   1. 标签选择器、类选择器、id 选择器和通配符选择器
   2. 类选择器-多类名
2. 复合选择器
   1. 后代选择器-子选择器-并集选择器-伪类选择器
   2. 链接伪类选择器-focus 伪类选择器-其他标准伪类选择器
3. CSS3 新增选择器
   1. 属性选择器-结构伪类选择器-伪元素选择器

### 属性
1. 字体-系列.大小.粗细.样式.复合写法
2. 文本-颜色.对齐.装饰.缩进.行间距
3. 背景-颜色.图片.平铺.位置.固定.复合写法.透明度

### css高级
1. 元素显示模式-块-行内-行内块-display
2. 盒子模型
   1. border-padding-margin-content
   2. CSS3.box-shadow.border-radius.text-shadow
3. 布局
   1. 普通流
   2. 浮动.float
      1. 清除浮动
         1. 额外标签法（隔墙法）. 父级添加 overflow 属性-父级添加 after 伪元素-父级添加双伪元素
   3. 定位
      1. 定位=定位模式+边偏移
      2. static.relative.absolute.fixed.sticky (了解).z-index
4. 显示与隐藏.visibility-display-overflow
5. 拓展
   1. 精灵图-字体图标-
   2. 三角图形-表单轮廓和文本域缩放
   3. 鼠标样式

### Css3
1. 渐变-滤镜-calc函数
2. 过渡-2D 转换-动画

### 移动端开发
1. 流式布局-视口-二倍图
2. flex布局
   1. `flex-direction.justify-container.flex-wrap.align-content.align-items.flex-flow.flex-direction.flow-wrap`
   2. 主轴方向，主轴排列，子元素换行，侧轴子排列
   3. 剩余空间，侧轴排列，顺序
3. rem 布局
   1. 媒体查询.Less.
4. 响应式开发

## js
### 概念
1. ECMAScript DOM BOM
2. 变量
3. 数据类型
   1. 简单数据类型：Number	Boolean	String	Undefined	Null
   2. symbol  object
4. 运算符
5. 流程控制 `if-else switch-case` `for while` `for in/of`
6. 函数-箭头函数
7. 数组
8. 对象
   1. 内置对象-数学对象 Math-日期对象 Date
9.  作用域概述
10. 简单类型与复杂类型-传参
11. 异常处理

### DOM 基础 BOM
1. 获取元素-事件基础-创（建）、增、删、改、查、属性操作。
2. 事件-注册-删除-事件流-事件委托-鼠标键盘事件
3. 窗口事件-this 指向问题-执行机制 location-navigator-history
4. 本地存储

### 高阶
1. 声明提升

### 面对对象
1. 三个特性,创建使用,属性方法
2. 构造函数和原型,原型链,this指向
3. 严格模式,高阶函数
4. 闭包.递归.浅拷贝与深拷贝
5. 正则表达式

### es6

1. let const 解构赋值 模板字符串 简化对象写法 箭头函数 函数参数默认值设定 rest参数 扩展运算符 symbol
2. 迭代器 Generator生成器函数 Promise 集合 Map class 数值扩展 对象方法扩展
3. 模块化
4. 指数运算符
5. async await
6. 类的私有属性 可选链 动态import导入 BigInt globalThis

### Promise
1. 基本使用 executor resolve reject then catch value reason  






