# vue.config.js

```js
module.exports = {
  publicPath: "./",//打包静态资源
  assetsDir: 'static',//静态资源地址
  lintOnSave: false,// 语法报错

  devServer: {// 开发模式跨域设置
    proxy: {
      "/qunli": {
        target: "http://192.168.31.193:8080",
        changeOrigin: true,
        pathRewrite: {
          "^/qunli": "/qunli"
        }
      },
    }
  },
  chainWebpack: config => {
    config
      .plugin('html')
      .tap(args => {
        args[0].title = 'musaly-github-blog'
        return args
      })
  },
  chainWebpack: config => {
    config.module
      .rule("md")
      .test(/\.md/)
      .use("vue-loader")
      .loader("vue-loader")
      .end()
      .use("vue-markdown-loader")
      .loader("vue-markdown-loader/lib/markdown-compiler")
      .options({
        raw: true,
        preventExtract: true
      });
  }
}
```

















