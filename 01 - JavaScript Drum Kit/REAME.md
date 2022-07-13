### 实现键盘按下后播放响应的音频。
给`Window`对象一个事件监听器，监听`keydown`事件，同时传入处理函数`playSound`。
```javascript
window.addEventListener("keydown", playSound);
```
接着实现playSound函数。

函数分为两部分，首先通过`document.querySelector`方法获取页面中所显示为按键的元素，查看`html`源代码可以发现其由`div`标签实现:
```html
<div data-key="76" class="key">
      <kbd>L</kbd>
      <span class="sound">tink</span>
</div>
```
可以看见这几个div标签都有类似的构成，因此使用如下语句进行获取，并将其存储在变量key中：
```javascript
const key = document.querySelector(`div[data-key="${e.keyCode}"]`);
```

同时，查阅html源代码可以发现有一堆audio标签，也就是在键盘按下后将要播放的音频，因此通过同样的方式将其存储在变量audio中，方便调用。
```javascript
const audio = document.querySelector(`audio[data-key="${e.keyCode}`);
```

接下来就可以实现播放功能了，具体代码如下：
```javascript
    if (!audio) return;               // 处理无效事件。
    key.classList.add("playing");     // 将 playing 加入类中，使得页面上的按键样式发生改变。
    audio.currentTime = 0;            // 重置音频播放时间，使得音频在每次按键按下时播放正常。
    audio.play();                     // 播放音频
```


```javascript
  function playSound(e) {
    const key = document.querySelector(`div[data-key="${e.keyCode}"]`);
    const audio = document.querySelector(`audio[data-key="${e.keyCode}`);
    
    if (!audio) return;
    key.classList.add("playing");
    audio.currentTime = 0;
    audio.play();
    
  }
```

现在，当你打开html文件，按下键盘后就能够听到对应的音频了，但是，你会发现在页面上按键的样式会保持改变，因此，接下来实现将这个问题解决

### 恢复键盘样式

想要实现这个功能，可以通过`transitionend`事件实现，这个事件在 CSS transition 完成后触发。但是我们想要实现的仅仅是在使得边框恢复原样，因此在处理时需要进行选择。
> The transitionend event is fired when a CSS transition has completed.

具体实现如下：
```javascript
    function removeTransition(e) {
    if (e.propertyName !== 'transform') return; // 过滤
    e.target.classList.remove('playing'); // 移除高亮的样式
  }
```
```javascript
  const keys = Array.from(document.querySelectorAll('.key')); // 获取页面所有按键元素
  keys.forEach(key => key.addEventListener('transitionend', removeTransition)); // 添加事件监听
```

如此，整个挑战就完成了。