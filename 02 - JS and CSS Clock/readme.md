### 首先让指针转起来

首先获取时钟的三个指针。
```javascript
    const secondHand = document.querySelector('.second-hand');
    const minsHand = document.querySelector('.min-hand');
    const hourHand = document.querySelector('.hour-hand');
```

然后创建一个函数，用于实现转动，首先获取当前时间的小时、分钟、秒作为基础数据，用于后续计算对应角度：
```javascript
    const now = new Date();
```

先分析秒钟的转动，每隔1秒秒针应该转动 （（1s/60）*360）度，另外因为三个指针开始时都是水平，所以每个指针对应的度数都要加上90度，通过如下代码即可实现：
```javascript
    const seconds = now.getSeconds();
    const secondsDegrees = ((seconds / 60) * 360) + 90;
    secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
```

同理可得其余时针、分针的对应代码：
```javascript
    const mins = now.getMinutes();
    const minsDegrees = ((mins / 60) * 360) + ((seconds/60)*6) + 90;
    minsHand.style.transform = `rotate(${minsDegrees}deg)`;

    const hour = now.getHours();
    const hourDegrees = ((hour / 12) * 360) + ((mins/60)*30) + 90;
    hourHand.style.transform = `rotate(${hourDegrees}deg)`;
```

最后通过定时器自动更新时间：
```javascript
    setInterval(setDate, 1000);
```

### 最后一步

完成上述代码后，查看网页，你会发现三个指针并没有如你所想的那样处于正确的位置，这是因为CSS的`transform-origin`属性现在对应的
值是center，只要将其改为正确的值即可：
```css
    .hand {
    transform-origin: 100%;
}
```
另外，按照在前面的度数的计算时所说的，首先需要将三个指针选择90度：
```css
    .hand {
    transform: rotate(90deg);
}
```
完成上述代码后，基本上的功能的实现了，增加如下样式可以使得时钟更真实：
```css
    .hand {
    transition: all 0.05s;
    transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
}
```
给表盘增添一个中心点：
```html
      <div class="clock-face">
        <div class="hand hour-hand"></div>
        <div class="hand min-hand"></div>
        <div class="hand second-hand"></div>
        <div class="circle"></div>
      </div>
```
```css
    .circle {
      width: 10%;
      height: 10%;
      background: #ffffff;
      border-radius: 50%;
      box-shadow: 0 0 2px 2px rgba(147, 145, 145, 0.69);
      position: absolute;
      top: 45%;
      left: 45%;
    }
```

如此，第二个挑战就完成了。