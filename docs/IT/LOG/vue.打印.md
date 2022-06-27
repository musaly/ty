# 打印


```js main.js
import Print from './plugins/print'
Vue.use(Print) // 注册
```

```js 组件中
    <div ref="print"></div> 
    printin () {
      this.$print(this.$refs.print)
    }
```
















