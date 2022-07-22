### 查看文件
初始文件已经将样式、动画等准备完善，只需要完成不同状态下的页面布局以及事件监听即可。

首先将panel元素下等文本进行布局：
```css
.panels {
      min-height: 100vh;
      overflow: hidden;
      display: flex;
    }

.panel {
    ...
    flex: 1;
    justify-content: center;
    display: flex;
    flex-direction: column;
}

.panel > * {
    ...
    flex: 1 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
}
```

完成上述代码后，页面将实现五等分，且每一等分中等文字是水平、垂直居中的，接下来将文本移出画面：

```css
    .panel > *:first-child { transform: translateY(-100%); }
    .panel > *:last-child { transform: translateY(100%); }
```

然后添加如下代码：

```css
    .panel.open-active > *:first-child { transform: translateY(0); }
    .panel.open-active > *:last-child { transform: translateY(0); }
    .panel.open {
        flex: 5;
        font-size: 40px;
    }
```

可以看见代码的选择器变成来.panel.open-active，而初始代码并没有匹配的元素，因此这段代码显然是队点击后的元素进行样式定义的。

### 实现动态效果

通过定义两个函数进行效果实现，一个toggleOpen函数为元素添加open属性，实现字体放大及图片占比变宽的效果。

```javascript
    const panels = document.querySelectorAll('.panel');
    
    function toggleOpen() {
    this.classList.toggle('open');
    }
```

另一个函数toggleActive函数实现将之前移出的文字重新移回的效果：

```javascript
    function toggleActive(e) {
          if (e.propertyName.includes('flex')) {
            this.classList.toggle('open-active');
          }
        } 
```

最后为每个panel元素添加监听事件即可：
```javascript
    panels.forEach(panel => panel.addEventListener('click', toggleOpen));
    panels.forEach(panel => panel.addEventListener('transitionend', toggleActive));
```