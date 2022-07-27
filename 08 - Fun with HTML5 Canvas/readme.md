### 实现绘画板

画板可供鼠标画画，颜色呈彩虹色渐变，画笔大小同样呈渐变效果。

### 开始实现
首先设置canvas的长宽，并获取上下文ctx。
```javascript
  const canvas = document.getElementById("draw");
  const ctx = canvas.getContext('2d');
  ctx.width = window.innerWidth;
  ctx.height = window.innerHeight;
```

然后设定ctx的属性。
```javascript
  ctx.strokeStyle = '#BADA55';  // 描边颜色
  ctx.lineJoin = 'round';       // 线条相交方式：圆交
  ctx.lineCap = 'round';        // 笔触形状：圆形
  ctx.lineWidth = 100;          // 线条宽度
```

最后开始实现绘画功能：
设定一个逻辑量表示绘画状态，然后给鼠标事件添加监听，对不同类型的事件将标记变量设为不同值。
```javascript
  canvas.addEventListener("mousedown", (e) => {
    isDrawing = true;
    [lastX, lastY]  = [ e.clientX, e.clientY ];
  });
  canvas.addEventListener("mousemove",draw);
  canvas.addEventListener("mouseup", () => isDrawing = false);
  canvas.addEventListener("mouseout", () => isDrawing = false);
```

然后实现draw函数。
```javascript
  let lastX = 0;
  let lastY = 0;

function draw(e) {
    if (!isDrawing) return;
    console.log(e);
    ctx.strokeStyle = `hsl(${hue}, 100%, 50%)`;
    ctx.beginPath();
    ctx.moveTo(lastX, lastY);
    ctx.lineTo(e.offsetX, e.offsetY);
    ctx.stroke();
    [lastX, lastY] = [e.offsetX, e.offsetY];
  }
```
此时查看效果发现能够成功绘制线条，但有一个问题，当你在canva中点击时，线条总会从canva原点开始，因此总是有条从左上角到鼠标所点击的区域，因此对mousedown事件监听器做如下改进：
```javascript
[lastX, lastY]  = [ e.clientX, e.clientY ];
```
这样处理后，当鼠标点击发生时，lastX，lastY的值会首先更新为鼠标当前的坐标值，从而使得多余的直线不再被绘制。

最后实现颜色的渐变和线条粗细的变化，这两个效果思路是一致的：
```javascript
    hue++;
    if (hue >= 360) {
      hue = 0;
    }
    
    if (ctx.lineWidth >= 100 || ctx.lineWidth <= 1) {
      direction = !direction;
    }

    if (direction) {
      ctx.lineWidth++;
    } else {
      ctx.lineWidth--;
    }
```

都是设定一个参考值，随着鼠标的移动，该参考值不断变化（增加或减少）从而到达颜色渐变和线条粗细随着鼠标的移动而发生变化的效果。
