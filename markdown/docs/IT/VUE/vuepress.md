# 快速构建

## 安装
>> npm install -g vuepress

## 新建一个 markdown 文件
>> echo '# Hello VuePress!' > README.md

## 开始写作
>> vuepress dev .

## 构建静态文件
>> vuepress build .

## 链接
```md
<!-- 相对路径 -->
[首页](../README.md)  
[配置参考](../reference/config.md)  
[快速上手](./getting-started.md)  
<!-- 绝对路径 -->
[指南](/zh/guide/README.md)  
[配置参考 > markdown.links](/zh/reference/config.md#links)  
<!-- URL -->
[GitHub](https://github.com) 
```