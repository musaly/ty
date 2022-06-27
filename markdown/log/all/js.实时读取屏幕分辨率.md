# 实时读取屏幕分辨率

```js
    this.screenWidth = document.body.clientWidth;
    window.onresize = () => {
      this.screenWidth = document.body.clientWidth;
      console.log(this.screenWidth);
    };
```