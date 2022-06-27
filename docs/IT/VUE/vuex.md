# vuex

## 核心概念

- state
- state
- state
- state
- state

### state 普通属性

- 获取 state 属性

```js
// store 实例中读取状态最简单的方法就是在计算属性 (opens new window)中返回某个状态：
  computed: {
    msg () {
      return this.$store.state.msg
    },
  }
// mapState 辅助函数
import { mapState } from 'vuex'
export default {
  // ...
  computed: {
    localComputed () { /* ... */ },
    // 使用对象展开运算符将此对象混入到外部对象中
    ...mapState(['msg'])
  }
}
```

### Getter 计算属性

- 设置 Getter 属性
```js
// Vuex 允许我们在 store 中定义“getter”（可以认为是 store 的计算属性）。就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。
const getters = {
  doneTodos: (state) => {
    return state.todos.filter(todo => todo.done)
  },
// Getter 也可以接受其他 getter 作为第二个参数：
  doneTodosCount: (state, getters) => {
    return getters.doneTodos.length
  },
// 你也可以通过让 getter 返回一个函数，来实现给 getter 传参。在你对 store 里的数组进行查询时非常有用。
  getTodoById: (state) => (id) => {
    return state.todos.find(todo => todo.id === id)
  }
}
```
- 获取 Getter 属性
```js
// 我们可以很容易地在任何组件中使用它：
  computed: {
    doneTodosCount () {
      return this.$store.getters.doneTodosCount
    }
  }
// 使用对象展开运算符将 getter 混入 computed 对象中
  computed: {
    ...mapGetters(['doneTodosCount','anotherGetter',])
  }
```































