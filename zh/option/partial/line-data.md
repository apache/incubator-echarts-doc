{{ target: partial-line-data-desc }}

每个数据项是一个数组，数组第一项是起点位置，第二项是终点位置，通过 `coord` 属性指定在相应的坐标系上的位置。

 **例如：** 
```js
data: [
    [{
        coord: [10, 20],
        // 数值大小
        value: 10
    }, {
        coord: [20, 30]
    }]
]
```
