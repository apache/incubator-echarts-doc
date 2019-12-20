
{{target: component-axisPointer}}

# axisPointer(Object)

这是坐标轴指示器（axisPointer）的全局公用设置。

---

{{ use: partial-axisPointer-introduction(
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
) }}

---

{{use: partial-component-id(prefix="#")}}

{{ use: partial-axisPointer-common(
    prefix="#",
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
)}}

## link(Array)

不同轴的 axisPointer 可以进行联动，在这里设置。联动表示轴能同步一起活动。轴依据他们的 axisPointer 当前对应的值来联动。

联动的效果可以看这两个例子：[例子A](${galleryViewPath}candlestick-brush&edit=1&reset=1)，[例子B](${galleryViewPath}scatter-nutrients-matrix&edit=1&reset=1)。

link 是一个数组，其中每一项表示一个 link group，一个 group 中的坐标轴互相联动。

**例如：**

```js
link: [
    {
        // 表示所有 xAxisIndex 为 0、3、4 和 yAxisName 为 'someName' 的坐标轴联动。
        xAxisIndex: [0, 3, 4],
        yAxisName: 'someName'
    },
    {
        // 表示左右 xAxisId 为 'aa'、'cc' 以及所有的 angleAxis 联动。
        xAxisId: ['aa', 'cc'],
        angleAxis: 'all'
    },
    ...
]
```

如上所示，每个 link group 中可以用这些方式引用坐标轴：

```js
{
    // 以下的 'some' 均表示轴的维度，也就是表示 'x', 'y', 'radius', 'angle', 'single'
    someAxisIndex: [...], // 可以是一个数组或单值或 'all'
    someAxisName: [...],  // 可以是一个数组或单值或 'all'
    someAxisId: [...],    // 可以是一个数组或单值或 'all'
}
```

---

**如何联动不同类型（[axis.type](~xAxis.type)）的轴？**

如果 axis 的类型不同，比如 axisA type 为 'category'，axisB type 为 'time'，可以在每个 link group 中写转换函数（mapper）来进行值的转换，例如：

```js
link: [{
    xAxisIndex: [0, 1],
    yAxisName: ['yy'],
    mapper: function (sourceVal, sourceAxisInfo, targetAxisInfo) {
        if (sourceAxisInfo.axisName === 'yy') {
            // from timestamp to '2012-02-05'
            return echarts.format.formatTime('yyyy-MM-dd', sourceVal);
        }
        else if (targetAxisInfo.axisName === 'yy') {
            // from '2012-02-05' to date
            return echarts.number.parseDate(dates[sourceVal]);
        }
        else {
            return sourceVal;
        }
    }
}]
```

mapper 的输入参数：

`{number}` sourceVal

`{Object}` sourceAxisInfo 里面包含 {axisDim, axisId, axisName, axisIndex} 等信息

`{Object}` targetAxisInfo 里面包含 {axisDim, axisId, axisName, axisIndex} 等信息

mapper 的返回值：

`{number}` 转换结果



## triggerOn(string) = 'mousemove|click'

提示框触发的条件，可选：

+ `'mousemove'`

    鼠标移动时触发。

+ `'click'`

    鼠标点击时触发。

+ `'none'`

    不在 `'mousemove'` 或 `'click'` 时触发。
