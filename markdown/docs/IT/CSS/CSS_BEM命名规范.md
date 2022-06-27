# CSS_BEM命名规范

## Block

> 一个功能独立的页面组件，可以重复使用

```css
<!--
    good
-->
<div  class = "header" > </ div >

<!--
    bad
    red-text 是描述外观
-->
<div  class = "red-text" > </ div >

- 连接
```

## Element

> 块的复合部分，不能单独使用

```css
<!-- 块 `search-form` -->
<form class="search-form">
    <!-- `input button` 元素 在 `search-form` 块中 -->
    <input class="search-form__input">
    <button class="search-form__button">Search</button>
</form>

__ 连接块
```

## Modifier

> 定义块或元素的外观，状态或行为的实体

```css
<form class="search-form search-form_focused">
    <input class="search-form__input">

    <!-- 'disabled' 是 'button' 的元素 -->
    <button class="search-form__button search-form__button_disabled">Search</button>
</form>

.连接方法
```