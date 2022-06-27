# 调用二维码

```js
<div id="qrcode"
      ref="qrCodeUrl"></div>

    // 创建二维码
    creatQrCode (params) {
      let js = JSON.stringify(params)
      let jp = JSON.parse(js)
      var qrcode = new QRCode(this.$refs.qrCodeUrl, {
        text: js, // 需要转换为二维码的内容
        // text: 'sssssssssssss', // 需要转换为二维码的内容
        width: 90,
        height: 90,
        colorDark: '#000000',
        colorLight: '#ffffff',
        correctLevel: QRCode.CorrectLevel.H
      })
    },

```







