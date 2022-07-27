### 在Checkbox 中实现按住 Shift 的进行多选的功能

首先获取所有input元素，并添加事件监听。
```javascript
    const checkboxes = document.querySelectorAll('.inbox input[type="checkbox"]');

  checkboxes.forEach(checkbox => checkbox.addEventListener('click', handelCheck));
```
实现函数handelCheck：
1. 需设定一个布尔值isBetween用于标识某项是否在选中的范围内。
2. 当第一项被选中后，记录该项，然后当按下 shift 和另外一项时遍历整个checkbox数组，将在范围内的项的inBetween进行反转。
3. 对所有inBetween发生变化的值进行相应的样式改变。



