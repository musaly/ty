
1. 简单调用
```js main
import axios from 'axios'
Vue.prototype.$http = axios
```

```js 组件中
async signin () {
  let params = {}
  await this.$http.post('/qunli/login', params).then((res) => {
  }).catch((res) => {
  })
},
```

2. 封装
```js @/utils/request.js
import axios from 'axios'
//创建axios实例
const request = axios.create({
  timeout: 60000 //请求超时时间
})
export default request
```

```js @/api/login.js
import request from '@/utils/request';
export default {
  login (userno, userpswmd5) {
    return request({
      url: '/qunli/login',
      method: 'post',
      data: {
        userno,
        userpswmd5
      }
    });
  },
  JWPOST (url, params) {
    return request({
      method: 'post',
      url: url,
      data: params,
      transformRequest: [
        function (data) {
          let ret = ''
          for (let it in data) {
            ret += encodeURIComponent(it) + '=' + encodeURIComponent(data[it]) + '&'
          }
          ret = ret.substring(0, ret.lastIndexOf('&'));
          return ret
        }
      ],
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded'
      }
    })
  }
}
```

```js @/store/store.js
import login from "@/api/login"
const actions = {
  JWPOST ({ commit }, api) {
    return login.JWPOST(api.url, api.params)
  },
}
```



















































