{{target:series-custom}}

# series.custom(Object)

**自定义系列**

自定义系列可以自定义系列中的图形元素渲染。从而能扩展出不同的图表。

同时，ECharts 会统一管理图形的创建删除、动画、与其他组件（如 [dataZoom](~dataZoom)、[visualMap](~visualMap)）的联动，使开发者不必纠结这些细节。

**例如，下面的例子使用 custom series 扩展出了 x-range 图：**
~[800x500](${galleryViewPath}custom-profile&reset=1&edit=1)

**更多的例子参见：[custom examples](http://echarts.baidu.com/examples.html#chart-type-custom)**

**[这里是个教程](http://echarts.baidu.com/tutorial.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%B3%BB%E5%88%97)**

<br>
**开发者自定义渲染逻辑（renderItem 函数）**

{{use: partial-custom-renderItem-common(
    galleryViewPath=${galleryViewPath}
)}}

<br>
**维度的映射（encode 和 dimensions 属性）**

`custom` 系列往往需要定义 [series.encode](~series-custom.encode)，主要用于指明 `data` 的哪些维度映射到哪些数轴上。从而，echarts 能根据这些维度的值的范围，画出合适的数轴刻度。
同时，encode.tooltip 和 encode.label 也可以被指定，指明默认的 tooltip 和 label 显示什么内容。[series.dimensions](~series-custom.dimensions) 也可以被指定，指明显示在 tooltip 中的维度名称，或者维度的类型。

例如：
```js
series: {
    type: 'custom',
    renderItem: function () {
        ...
    },
    encode: {
        x: [2, 4, 3],
        y: 1,
        label: 0,
        tooltip: [2, 4, 3]
    }
}
```

<br>
**与 dataZoom 组件的结合**

与 [dataZoom](~dataZoom) 结合使用的时候，常常使用会设置 [dataZoom.filterMode](~dataZoom.filterMode) 为 'weakFilter'，从而让 `dataItem` 部分超出坐标系边界的时候，不会整体被过滤掉。

<br>
**关于 `dataIndex` 和 `dataIndexInside` 的区别**
{{use: partial-custom-dataIndex-dataIndexInside}}


<br>
**Event listener**

```js
chart.setOption({
    // ...
    series: {
        type: 'custom',
        renderItem: function () {
            // ...
            return {
                type: 'group',
                children: [{
                    type: 'circle'
                    // ...
                }, {
                    type: 'circle',
                    name: 'aaa',
                    // 用户指定的信息，可以在 event handler 访问到。
                    info: 12345,
                    // ...
                }]
            };
        }
    }
});
chart.on('click', {element: 'aaa'}, function (params) {
    // 当 name 为 'aaa' 的图形元素被点击时，此回调被触发。
    console.log(params.info);
});
```


## type(string) = 'custom'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}

{{ use: partial-legend-hover-link() }}

{{ use: partial-coord-sys(
    seriesType="custom",
    coordSysDefault="'cartesian2d'",
    cartesian2d=true,
    polar=true,
    geo=true,
    calendar=true,
    none=true
) }}

## renderItem(Function)

{{use: partial-custom-renderItem-common(
    galleryViewPath=${galleryViewPath}
)}}

### arguments

renderItem 函数的参数。

#### params(Object)

renderItem 函数的第一个参数，含有：

```js
{
    context: // {Object} 一个可供开发者暂存东西的对象。生命周期只为：当前次的渲染。
    seriesId: // {string} 本系列 id。
    seriesName: // {string} 本系列 name。
    seriesIndex: // {number} 本系列 index。
    dataIndex: // {number} 数据项的 index。
    dataIndexInside: // {number} 数据项在当前坐标系中可见的数据的 index（即 dataZoom 当前窗口中的数据的 index）。
    dataInsideLength: // {number} 当前坐标系中可见的数据长度（即 dataZoom 当前窗口中的数据数量）。
    actionType: // {string} 触发此次重绘的 action 的 type。
    coordSys: // 不同的坐标系中，coordSys 里的信息不一样，含有如下这些可能：
    coordSys: {
        type: 'cartesian2d',
        x: // {number} grid rect 的 x
        y: // {number} grid rect 的 y
        width: // {number} grid rect 的 width
        height: // {number} grid rect 的 height
    },
    coordSys: {
        type: 'calendar',
        x: // {number} calendar rect 的 x
        y: // {number} calendar rect 的 y
        width: // {number} calendar rect 的 width
        height: // {number} calendar rect 的 height
        cellWidth: // {number} calendar cellWidth
        cellHeight: // {number} calendar cellHeight
        rangeInfo: {
            start: // calendar 日期开端
            end: // calendar 日期结尾
            weeks: // calendar 周数
            dayCount: // calendar 日数
        }
    },
    coordSys: {
        type: 'geo',
        x: // {number} geo rect 的 x
        y: // {number} geo rect 的 y
        width: // {number} geo rect 的 width
        height: // {number} geo rect 的 height
        zoom: // {number} 缩放的比率。如果没有缩放，则值为 1。例如 0.5 表示缩小了一半。
    },
    coordSys: {
        type: 'polar',
        cx: // {number} polar 的中心坐标
        cy: // {number} polar 的中心坐标
        r: // {number} polar 的外半径
        r0: // {number} polar 的内半径
    },
    coordSys: {
        type: 'singleAxis',
        x: // {number} singleAxis rect 的 x
        y: // {number} singleAxis rect 的 y
        width: // {number} singleAxis rect 的 width
        height: // {number} singleAxis rect 的 height
    }
}
```

其中，关于 `dataIndex` 和 `dataIndexInside` 的区别：
{{use: partial-custom-dataIndex-dataIndexInside}}


#### api(Object)

renderItem 函数的第二个参数。

##### value(Function)

得到给定维度的数据值。

```
@param {number} dimension 指定的维度（维度从 0 开始计数）。
@param {number} [dataIndexInside] 一般不用传，默认就是当前数据项的 dataIndexInside。
@return {number} 给定维度上的值。
```

##### coord(Function)

将数据值映射到坐标系上。

```
@param {Array.<number>} data 数据值。
@return {Array.<number>} 画布上的点的坐标，至少包含：[x, y]
        对于polar坐标系，还会包含其他信息：
        polar: [x, y, radius, angle]
```

##### size(Function)

给定数据范围，映射到坐标系上后的长度。

例如，cartesian2d中，`api.size([2, 4])` 返回 `[12.4, 55]`，表示 x 轴数据范围为 2 映射得到长度是 `12.4`，y 轴数据范围为 4 时应设得到长度为 `55`。

在一些坐标系中，如极坐标系（polar）或者有 log 数轴的坐标系，不同点的长度是不同的，所以需要第二个参数，指定获取长度的点。

```
@param {Array.<number>} dataSize 数据范围。
@param {Array.<number>} dataItem 获取长度的点。
@return {Array.<number>} 画布上的长度
```

##### style(Function)

能得到 [series.itemStyle](~series-custom.itemStyle) 中定义的样式信息和视觉映射得到的样式信息，可直接用于绘制图元。也可以用这种方式覆盖这些样式信息：`api.style({fill: 'green', stroke: 'yellow'})`。

```
@param {Object} [extra] 额外指定的样式信息。
@param {number} [dataIndexInside] 一般不用传，默认就是当前数据项的 dataIndexInside。
@return {Object} 直接用于绘制图元的样式信息。
```

##### styleEmphasis(Function)

能得到 [series.itemStyle.emphasis](~series-custom.itemStyle.emphasis) 中定义的样式信息和视觉映射的样式信息，可直接用于绘制图元。也可以用这种方式覆盖这些样式信息：`api.style({fill: 'green', stroke: 'yellow'})`。

```
@param {Object} [extra] 额外指定的样式信息。
@param {number} [dataIndexInside] 一般不用传，默认就是当前数据项的 dataIndexInside。
@return {Object} 直接用于绘制图元的样式信息。
```

##### visual(Function)

得到视觉映射的样式信息。比较少被使用。

```
@param {string} visualType 'color', 'symbol', 'symbolSize', ...
@param {number} [dataIndexInside] 一般不用传，默认就是当前数据项的 dataIndexInside。
@return {string|number} 视觉映射的样式值。
```


##### barLayout(Function)

当需要采用 barLayout 的时候，比如向柱状图上附加些东西，可以用这个方法得到 layout 信息。
参见 [例子](${galleryEditorPath}custom-bar-trend)。

```
@param {Object} opt
@param {number} opt.count 每个簇有多少个 bar。
@param {number|string} [opt.barWidth] bar 宽度。
        可以是绝对值例如 `40` 或者百分数例如 `'60%'`。
        百分数基于自动计算出的每一类目的宽度。
@param {number|string} [opt.barMaxWidth] bar 最大宽度。
        可以是绝对值例如 `40` 或者百分数例如 `'60%'`。
        百分数基于自动计算出的每一类目的宽度。
        比 `opt.barWidth` 优先级高。
@param {number|string} [opt.barMinWidth] bar 最小宽度。
        可以是绝对值例如 `40` 或者百分数例如 `'60%'`。
        百分数基于自动计算出的每一类目的宽度。
        比 `opt.barWidth` 优先级高。
@param {number} [opt.barGap] 每个簇的 bar 之间的宽度。
@param {number} [opt.barCategoryGap] 不同簇间的宽度。
@return {Array.<Object>} [{
        width: number bar 的宽度。
        offset: number bar 的偏移量，以bar最左为基准。
        offsetCenter: number bar 的偏移量，以bar中心为基准。
    }, ...]
```


##### currentSeriesIndices(Function)

得到系列的 当前index。**注意：**这个 index 不同于系列定义时的 index。这个 index 是当 legend 组件进行了系列筛选后，剩余的系列排列后的 index。

```
@return {number}
```

##### font(Function)

得到可以直接进行样式设置的文字信息字符串。

```
@param {Object} opt
@param {string} [opt.fontStyle]
@param {number} [opt.fontWeight]
@param {number} [opt.fontSize]
@param {string} [opt.fontFamily]
@return {string} font 字符串。
```

##### getWidth(Function)

```
@return {number} ECharts 容器的宽度。
```

##### getHeight(Function)

```
@return {number} ECharts 容器的高度。
```

##### getZr(Function)

```
@return {module:zrender} zrender 实例。
```

##### getDevicePixelRatio(Function)

```
@return {number} 得到当前 devicePixelRatio。
```


### return(Object)

图形元素。每个图形元素是一个 object。详细信息参见：[graphic](~graphic.elements)。（width\height\top\bottom 不支持）

如果什么都不渲染，可以不返回任何东西。

**例如：**
```js
// 单独一个矩形
{
    type: 'rect',
    shape: {
        x: x, y: y, width: width, height: height
    },
    style: api.style()
}
```

```js
// 一组图形元素
{
    type: 'group',
    // 如果 diffChildrenByName 设为 true，则会使用 child.name 进行 diff，
    // 从而能有更好的过度动画，但是降低性能。缺省为 false。
    // diffChildrenByName: true,
    children: [{
        type: 'circle',
        shape: {
            cx: cx, cy: cy, r: r
        },
        style: api.style()
    }, {
        type: 'line',
        shape: {
            x1: x1, y1: y1, x2: x2, y2: y2
        },
        style: api.style()
    }]
}
```


{{use: partial-zr-graphic-elements(
    prefix='##',
    hostName='return',
    symbolVisit='_',
    symbolDeclare='_',
    optionPath='series-custom.renderItem',
    usageType='customSeries'
)}}



## itemStyle(Object)

{{use:partial-item-style-desc}}

{{use:partial-item-style(
    prefix="##",
    useColorPalatte=true,
    hasCallback=false
)}}

## emphasis(Object)

高亮图形样式

### itemStyle(Object)
{{use:partial-item-style(
    prefix="###"
)}}


{{use:partial-series-dimensions(
    prefix="#"
)}}

{{use:partial-series-encode(
    prefix="#"
)}}

{{ use: partial-seriesLayoutBy }}

{{ use: partial-datasetIndex }}

## data(Array)

{{ use: partial-2d-data-desc(
    galleryEditorPath = ${galleryEditorPath}
)}}

### name(string)
数据项名称。

### value(number)
单个数据项的数值。

### itemStyle(Object)
{{use:partial-item-style(
    prefix="###"
)}}

### emphasis(Object)

#### itemStyle(Object)
{{use:partial-item-style(
    prefix="####"
)}}

{{use: partial-tooltip-in-series-data(
    galleryViewPath=${galleryViewPath}
)}}


{{use:partial-clip(
    prefix="#",
    defaultClip=false
) }}

{{use:partial-z-zlevel(
    prefix="#",
    componentName="自定义图"
) }}
{{ use:partial-silent(
    prefix="#"
) }}

{{use:partial-animation(
    prefix="#",
    galleryEditorPath=${galleryEditorPath}
)}}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}











{{target: partial-custom-renderItem-common}}

custom 系列需要开发者自己提供图形渲染的逻辑。这个渲染逻辑一般命名为 [renderItem](~series-custom.renderItem)。

**例如：**

```js
var option = {
    ...,
    series: [{
        type: 'custom',
        renderItem: function (params, api) {
            var categoryIndex = api.value(0);
            var start = api.coord([api.value(1), categoryIndex]);
            var end = api.coord([api.value(2), categoryIndex]);
            var height = api.size([0, 1])[1] * 0.6;

            var rectShape = echarts.graphic.clipRectByRect({
                x: start[0],
                y: start[1] - height / 2,
                width: end[0] - start[0],
                height: height
            }, {
                x: params.coordSys.x,
                y: params.coordSys.y,
                width: params.coordSys.width,
                height: params.coordSys.height
            });

            return rectShape && {
                type: 'rect',
                shape: rectShape,
                style: api.style()
            };
        },
        data: data
    }]
}
```

对于 `data` 中的每个数据项（为方便描述，这里称为 `dataItem`)，会调用此 [renderItem](~series-custom.renderItem) 函数。

[renderItem](~series-custom.renderItem) 函数提供了两个参数：
+ [params](~series-custom.renderItem.arguments.params)：包含了当前数据信息和坐标系的信息。
+ [api](~series-custom.renderItem.arguments.api)：是一些开发者可调用的方法集合。

[renderItem](~series-custom.renderItem) 函数须返回根据此 `dataItem` 绘制出的图形元素的定义信息，参见 [renderItem.return](~series-custom.renderItem.return)。

一般来说，[renderItem](~series-custom.renderItem) 函数的主要逻辑，是将 `dataItem` 里的值映射到坐标系上的图形元素。这一般需要用到 [renderItem.arguments.api](~series-custom.renderItem.arguments.api) 中的两个函数：
+ [api.value(...)](~series-custom.renderItem.arguments.api.value)，意思是取出 `dataItem` 中的数值。例如 `api.value(0)` 表示取出当前 `dataItem` 中第一个维度的数值。
+ [api.coord(...)](~series-custom.renderItem.arguments.api.coord)，意思是进行坐标转换计算。例如 `var point = api.coord([api.value(0), api.value(1)])` 表示 `dataItem` 中的数值转换成坐标系上的点。

有时候还需要用到 [api.size(...)](~series-custom.renderItem.arguments.api.size) 函数，表示得到坐标系上一段数值范围对应的长度。

返回值中样式的设置可以使用 [api.style(...)](~series-custom.renderItem.arguments.api.style) 函数，他能得到 [series.itemStyle](~series-custom.itemStyle) 中定义的样式信息，以及视觉映射的样式信息。也可以用这种方式覆盖这些样式信息：`api.style({fill: 'green', stroke: 'yellow'})`。








{{target: partial-custom-dataIndex-dataIndexInside}}
+ `dataIndex` 指的 `dataItem` 在原始数据中的 index。
+ `dataIndexInside` 指的是 `dataItem` 在当前数据窗口（参见 [dataZoom](~dataZoom)）中的 index。

[renderItem.arguments.api](~series-custom.renderItem.arguments.api) 中使用的参数都是 `dataIndexInside` 而非 `dataIndex`，因为从 `dataIndex` 转换成 `dataIndexInside` 需要时间开销。

