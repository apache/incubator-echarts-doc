{{ target: partial-2d-data-label-formatter }}

标签内容格式器，支持字符串模板和回调函数两种形式，字符串模板与回调函数返回的字符串均支持用 `\n` 换行。

**字符串模板**
模板变量有：
+ `{a}`：系列名。
+ `{b}`：数据名。
+ `{c}`：数据值。
+ `{@xxx}：数据中名为 `'xxx'` 的维度的值，如 `{@product}` 表示名为 `'product'` 的维度的值。
+ `{@[n]}：数据中维度 `n` 的值，如 `{@[3]}` 表示维度 3 的值，从 0 开始计数。

**例如：**
```js
formatter: '{b}: {@score}'
```

**回调函数**

回调函数格式：
```js
(params: Object|Array) => string
```
参数 `params` 是 formatter 需要的单个数据集。格式如下：
{{ use: partial-formatter-params-structure() }}。


{{ target: partial-seriesLayoutBy }}

## seriesLayoutBy(string) = 'column'

当使用 [dataset](~dataset) 时，`seriesLayoutBy` 指定了 `dataset` 中用行还是列对应到系列上，也就是说，系列“排布”到 `dataset` 的行还是列上。可取值：

+ 'column'：默认，`dataset` 的列对应于系列，从而 `dataset` 中每一列是一个维度（dimension）。
+ 'row'：`dataset` 的行对应于系列，从而 `dataset` 中每一行是一个维度（dimension）。

**查看 [示例]**(http://echarts.baidu.com/examples/editor.html?c=dataset-series-layout-by&theme=lite)

{{ target: partial-datasetIndex }}

## datasetIndex(number) = 0

如果 [series.data](~series.data) 没有指定，并且 [dataset](~dataset) 存在，那么就会使用 [dataset](~dataset)。`datasetIndex` 指定本系列使用那个 [dataset](~dataset)。



{{ target: partial-2d-data-desc }}

系列中的数据内容数组。数组项通常为具体的数据项。

**注意:**如果系列没有指定 `data`，并且 option 有 [dataset](~dataset)，那么默认使用第一个 [dataset](~dataset)。如果指定了 `data`，则不会再使用 [dataset](~dataset)。

可以使用 `series.datasetIndex` 指定其他的 [dataset](~dataset)。

通常来说，数据用一个二维数组表示。如下，每一列被称为一个『维度』。
```js
series: [{
    data: [
        // 维度X   维度Y   其他维度 ...
        [  3.4,    4.5,   15,   43],
        [  4.2,    2.3,   20,   91],
        [  10.8,   9.5,   30,   18],
        [  7.2,    8.8,   18,   57]
    ]
}]
```

+ 在 [直角坐标系 (grid)](~grid) 中『维度X』和『维度Y』会默认对应于 [xAxis](~xAxis) 和 [yAxis](~yAxis)。
+ 在 [极坐标系 (polar)](~polar) 中『维度X』和『维度Y』会默认对应于 [radiusAxis](~radiusAxis) 和 [angleAxis](~anbleAxis)。
+ 后面的其他维度是可选的，可以在别处被使用，例如：
    + 在 [visualMap](~visualMap) 中可以将一个或多个维度映射到颜色，大小等多个图形属性上。
    + 在 [series.symbolSize](~series.symbolSize) 中可以使用回调函数，基于某个维度得到 symbolSize 值。
    + 使用 [tooltip.formatter](~tooltip.formatter) 或 [series.label.formatter](~series.label.formatter) 可以把其他维度的值展示出来。

特别地，当只有一个轴为类目轴（axis.type 为 `'category'`）的时候，数据可以简化用一个一维数组表示。例如：
```js
xAxis: {
    data: ['a', 'b', 'm', 'n']
},
series: [{
    // 与 xAxis.data 一一对应。
    data: [23,  44,  55,  19]
    // 它其实是下面这种形式的简化：
    // data: [[0, 23], [1, 44], [2, 55], [3, 19]]
}]
```

<br>
**『值』与 [轴类型](~xAxis.type) 的关系：**

+ 当某维度对应于数值轴（axis.type 为 `'value'` 或者 `'log'`）的时候：

    其值可以为 `number`（例如 `12`）。（也可以兼容 `string` 形式的 number，例如 `'12'`）

+ 当某维度对应于类目轴（axis.type 为 `'category'`）的时候：

    其值须为类目的『序数』（从 `0` 开始）或者类目的『字符串值』。例如：
    ```js
    xAxis: {
        type: 'category',
        data: ['星期一', '星期二', '星期三', '星期四']
    },
    yAxis: {
        type: 'category',
        data: ['a', 'b', 'm', 'n', 'p', 'q']
    },
    series: [{
        data: [
            // xAxis    yAxis
            [  0,        0,    2  ], // 意思是此点位于 xAxis: '星期一', yAxis: 'a'。
            [  '星期四',  2,    1  ], // 意思是此点位于 xAxis: '星期四', yAxis: 'm'。
            [  2,       'p',   2  ], // 意思是此点位于 xAxis: '星期三', yAxis: 'p'。
            [  3,        3,    5  ]
        ]
    }]
    ```
    双类目轴的示例可以参考 [Github Punchcard](${galleryEditorPath}scatter-punchCard) 示例。

+ 当某维度对应于时间轴（type 为 `'time'`）的时候，值可以为：
    + 一个时间戳，如 `1484141700832`，表示 UTC 时间。
    + 或者字符串形式的时间描述：
        + [ISO 8601](http://www.ecma-international.org/ecma-262/5.1/#sec-15.9.1.15) 的子集，只包含这些形式（这几种格式，除非指明时区，否则均表示本地时间，与 [moment](https://momentjs.com/) 一致）：
            + 部分年月日时间: `'2012-03'`, `'2012-03-01'`, `'2012-03-01 05'`, `'2012-03-01 05:06'`.
            + 使用 `'T'` 或空格分割: `'2012-03-01T12:22:33.123'`, `'2012-03-01 12:22:33.123'`.
            + 时区设定: `'2012-03-01T12:22:33Z'`, `'2012-03-01T12:22:33+8000'`, `'2012-03-01T12:22:33-05:00'`.
        + 其他的时间字符串，包括（均表示本地时间）:
          `'2012'`, `'2012-3-1'`, `'2012/3/1'`, `'2012/03/01'`,
          `'2009/6/12 2:00'`, `'2009/6/12 2:05:08'`, `'2009/6/12 2:05:08.123'`
    + 或者用户自行初始化的 Date 实例：
        + 注意，用户自行初始化 Date 实例的时候，[浏览器的行为有差异，不同字符串的表示也不同](http://dygraphs.com/date-formats.html)。
        + 例如：在 chrome 中，`new Date('2012-01-01')` 表示 UTC 时间的 2012 年 1 月 1 日，而 `new Date('2012-1-1')` 和 `new Date('2012/01/01')` 表示本地时间的 2012 年 1 月 1 日。在 safari 中，不支持 `new Date('2012-1-1')` 这种表示方法。
        + 所以，使用 `new Date(dataString)` 时，可使用第三方库解析（如 [moment](https://momentjs.com/)），或者使用 `echarts.number.parseDate`，或者参见 [这里](http://dygraphs.com/date-formats.html)。

<br>
**当需要对个别数据进行个性化定义时：**

数组项可用对象，其中的 `value` 像表示具体的数值，如：
```js
[
    12,
    34,
    {
        value : 56,
        //自定义标签样式，仅对该数据项有效
        label: {},
        //自定义特殊 itemStyle，仅对该数据项有效
        itemStyle:{}
    },
    10
]
// 或
[
    [12, 33],
    [34, 313],
    {
        value: [56, 44],
        label: {},
        itemStyle:{}
    },
    [10, 33]
]
```

<br>
**空值：**

当某数据不存在时（ps：*不存在*不代表值为 0），可以用 `'-'` 或者 `null` 或者 `undefined` 或者 `NaN` 表示。

例如，无数据在折线图中可表现为该点是断开的，在其它图中可表示为图形不存在。

<br><br>
