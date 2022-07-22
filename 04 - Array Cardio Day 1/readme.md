### Array 的几个基本方法
1. filter：筛出函数运行结果是 true 的元素组成数组返回。
2. map：对每个元素都进行一次函数处理，然后返回新的数组。
3. sort：将数组以字符串的形式进行升序排列。
4. reduce：遍历数组的所有项，然后构建一个最终的返回值。

### 完成本次挑战
1. 筛选 16 世纪出生的发明家
   ```javascript
    const fifteen = inventors.filter(inventor => inventor.year > 1500 && inventor.year < 1600)
    console.table(fifteen)
   ```
2. 展示他们的姓和名
    ```javascript
    const fullNames = inventors.map(inventor => `${inventor.first} ${inventor.last}`);
    console.log(fullNames)
    ```
3. 把他们按照出生日期从大到小进行排序
    ```javascript
    const ordered = inventors.sort((a, b) => (a.year > b.year ? 1 : -1));
    console.log(ordered)
    ```
4. 计算所有的发明家加起来一共活了多少岁
    ```javascript
    const totalYears = inventors.reduce((total, inventor) => {
          return total + (inventor.passed - inventor.year)
        }, 0);
        console.log(totalYears)
    ```
5. 按照他们活了多久来进行排序
    ```javascript
    const oldest = inventors.sort((a, b) => ((a.passed - a.year) > (b.passed - b.year) ? 1 : -1));
        console.log(oldest)
    ```
6. 筛选出一个网页里含有某个词语的标题
7. 按照姓氏来进行排序
    ```javascript
    const alpha = people.sort((last, next) => {
          const [aLast, aFirst] = last.split(', ');
          const [bLast, bFirst] = next.split(', ');
          return aLast > bLast ? 1 : -1;
        });
        console.log(alpha);
    ```
8. 统计给出数组中各个物品的数量
