```js
    async SLRecord () {
      let params = {
        "outno": this.SLRecord_params.outno,
        "iid": this.SLRecord_params.iid,
      }
      axios({
        method: 'post',
        url: '/qunli/SLRecord',
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
    },
```