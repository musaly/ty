# js 异常使用

```js
  try {
    // this.getAllMac_params = JSON.parse(this.input)
    // 代码块
  } catch (error) {
    this.$message.error('不合法的输入');
    return
  }
```
```js
try {
    1 = 1;  //非法语句
}
catch (error) {  //捕获错误
    console.log(error.name);  //访问错误类型
    console.log(error.message);  //访问错误详细信息
}
finally {  //清除处理
    console.log("1=1");  //提示代码
}
```