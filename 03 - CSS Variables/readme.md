### 基础知识

首先，查看源代码发现`<input>`元素含有一个名为`data-sizing`的属性，其值都是`px`。 这里涉及到一个知识，即 HTML5 中的自定义数据属性`dataset`，通过在元素中添加前缀为`data-`的属性就可以设置一个
自定义数据属性，在`javascript`中可以通过`dataset`属性访问其对应的值，这在后面代码中有用。

然后是本次涉及到的另一些知识：
- [CSS 自定义属性](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Using_CSS_custom_properties)：该特性允许通过声明一个格式为`--属性名：属性值`的自定义属性（或称变量）用以简化CSS代码或是 方便统一修改CSS样式，自定义属性的用法为`var(--属性名)`。
- `:root` 伪类：通过该元素可以匹配文档根元素，常用于声明全局的 CSS 自定义属性。
- filter：CSS属性 filter 将模糊或颜色偏移等图形效果应用于元素。

### 开始实现

首先，先获取全部input元素，并为每个input元素加上事件监听器用于实时更新样式。
```javascript
    const inputs = document.querySelectorAll(".controls input")
    inputs.forEach(input => input.addEventListener('change', handleUpdate))
    inputs.forEach(input => input.addEventListener('mousemove', handleUpdate))
```
然后实现handleUpdate函数，为了使得给定效果能够实现——即通过`input`元素进行实时控制元素样式，利用前面介绍的 CSS 自定义属性进行全局样式定义，并将其应用到对应的元素`<img>`上，这样就可以通过在`handleUpdate`函数中操控全局变量来实现该效果了。
```html
<style>
    :root {
        --base: #ffc600;
        --spacing: 10px;
        --blur: 10px;
    }

    img {
        padding: var(--spacing);
        background: var(--base);
        filter: blur(var(--blur));
    }

    .hl {
        color: var(--base);
    }
</style>
```
可以看到这里定义的全局变量和input元素中的name属性对应的值一致，因此在handleUpdate函数中就可以通过获取input元素新的name属性值和value属性值对CSS样式进行更新。
```javascript

```