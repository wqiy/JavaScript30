### 实现输入匹配
利用json数据进行输入匹配，首先读取数据，利用fetch发送请求并对返回数据进行处理存入数组中。
```javascript
const cities = [];
fetch(endpoint)
    .then(response => response.json())
    .then(data => cities.push(...data))
```

而后实现匹配函数，用于对输入内容进行匹配：
```javascript
function findMatches(wordToMatch, cities) {
  return cities.filter(place => {
    const regex = new RegExp(wordToMatch, 'gi') // 将输入转化成正则表达式
    return place.city.match(regex) || place.state.match(regex)
  });
}
```

最后实现匹配结果对函数并对input及ul元素添加监听事件：
```javascript
function displayMatcher() {
  const matchArray = findMatches(this.value, cities);
  //构造高亮匹配结果的ul元素
  const html = matchArray.map(place => {
    const regex = new RegExp(this.value, 'gi');
    const cityName = place.city.replace(regex, `<span class="hl">${this.value}</span>`);
    const stateName = place.state.replace(regex, `<span class="hl">${this.value}</span>`);
    return `
      <li>
        <span class="name">${cityName}, ${stateName}</span>
        <span class="population">${numberWithCommas(place.population)}</span>
      </li>
    `;
  }).join('');
  suggestions.innerHTML = html
}


```