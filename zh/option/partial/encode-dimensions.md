{{target:partial-series-encode}}

#${prefix} encode(Object)

可以定义 `data` 的哪个维度被编码成什么。比如：

```js
option = {
    dataset: {
        source: [
            // 每一列称为一个『维度』。
            // 这里分别是维度 0、1、2、3、4。
            [12, 44, 55, 66, 2],
            [23, 6, 16, 23, 1],
            ...
        ]
    },
    series: {
        type: 'xxx',
        encode: {
            x: [3, 1, 5],      // 表示维度 3、1、5 映射到 x 轴。
            y: 2,              // 表示维度 2 映射到 y 轴。
            tooltip: [3, 2, 4] // 表示维度 3、2、4 会在 tooltip 中显示。
        }
    }
}
```

当使用 [dimensions](~series.dimensions) 给维度定义名称后，`encode` 中可直接引用名称。

**例如：**

```js
series: {
    type: 'xxx',
    dimensions: ['date', 'open', 'close', 'highest', 'lowest'],
    encode: {
        x: 'date',
        y: ['open', 'close', 'highest', 'lowest']
    }
}
```

`encode` 声明的基本结构如下，其中冒号左边是坐标系、标签等特定名称，如 `'x'`, `'y'`, `'tooltip'` 等，冒号右边是数据中的维度名（string 格式）或者维度的序号（number 格式，从 0 开始计数），可以指定一个或多个维度（使用数组）。通常情况下，下面各种信息不需要所有的都写，按需写即可。

下面是 encode 支持的属性：

```js
// 在任何坐标系和系列中，都支持：
encode: {
    // 使用 “名为 product 的维度” 和 “名为 score 的维度” 的值在 tooltip 中显示
    tooltip: ['product', 'score']
    // 使用 “维度 1” 和 “维度 3” 的维度名连起来作为系列名。（有时候名字比较长，这可以避免在 series.name 重复输入这些名字）
    seriesName: [1, 3],
    // 表示使用 “维度2” 中的值作为 id。这在使用 setOption 动态更新数据时有用处，可以使新老数据用 id 对应起来，从而能够产生合适的数据更新动画。
    itemId: 2,
    // 指定数据项的名称使用 “维度3” 在饼图等图表中有用，可以使这个名字显示在图例（legend）中。
    itemName: 3
}

// 直角坐标系（grid/cartesian）特有的属性：
encode: {
    // 把 “维度1”、“维度5”、“名为 score 的维度” 映射到 X 轴：
    x: [1, 5, 'score'],
    // 把“维度0”映射到 Y 轴。
    y: 0
}

// 单轴（singleAxis）特有的属性：
encode: {
    single: 3
}

// 极坐标系（polar）特有的属性：
encode: {
    radius: 3,
    angle: 2
}

// 地理坐标系（geo）特有的属性：
encode: {
    lng: 3,
    lat: 2
}

// 对于一些没有坐标系的图表，例如饼图、漏斗图等，可以是：
encode: {
    value: 3
}
```

这是个更丰富的 `encode` 的[示例](${galleryViewPath}dataset-encode1&edit=1&reset=1)：



特殊地，在 [自定义系列（custom series）](~series-custom) 中，`encode` 中轴可以不指定或设置为 `null/undefined`，从而使系列免于受这个轴控制，也就是说，轴的范围（extent）不会受此系列数值的影响，轴被 [dataZoom](~dataZoom) 控制时也不会过滤掉这个系列：

```js
var option = {
    xAxis: {},
    yAxis: {},
    dataZoom: [{
        xAxisIndex: 0
    }, {
        yAxisIndex: 0
    }],
    series: {
        type: 'custom',
        renderItem: function (params, api) {
            return {
                type: 'circle',
                shape: {
                    cx: 100, // x 位置永远为 100
                    cy: api.coord([0, api.value(0)])[1],
                    r: 30
                },
                style: {
                    fill: 'blue'
                }
            };
        },
        encode: {
            // 这样这个系列就不会被 x 轴以及 x
            // 轴上的 dataZoom 控制了。
            x: -1,
            y: 1
        },
        data: [ ... ]
    }
};
```



{{target:partial-series-dimensions}}

#${prefix} dimensions(Array)

使用 dimensions 定义 `series.data` 或者 `dataset.source` 的每个维度的信息。

**注意:**如果使用了 [dataset](~dataset)，那么可以在 [dataset.source](~dataset.source) 的第一行/列中给出 dimension 名称。于是就不用在这里指定 dimension。但是，如果在这里指定了 `dimensions`，那么 ECharts 不再会自动从 `dataset.source` 的第一行/列中获取维度信息。

**例如：**

```js
option = {
    dataset: {
        source: [
            // 有了上面 dimensions 定义后，下面这五个维度的名称分别为：
            // 'date', 'open', 'close', 'highest', 'lowest'
            [12, 44, 55, 66, 2],
            [23, 6, 16, 23, 1],
            ...
        ]
    },
    series: {
        type: 'xxx',
        // 定义了每个维度的名称。这个名称会被显示到默认的 tooltip 中。
        dimensions: ['date', 'open', 'close', 'highest', 'lowest']
    }
}
```

```js
series: {
    type: 'xxx',
    dimensions: [
        null,                // 如果此维度不想给出定义，则使用 null 即可
        {type: 'ordinal'},   // 只定义此维度的类型。
                             // 'ordinal' 表示离散型，一般文本使用这种类型。
                             // 如果类型没有被定义，会自动猜测类型。
        {name: 'good', type: 'number'},
        'bad'                // 等同于 {name: 'bad'}
    ]
}
```

`dimensions` 数组中的每一项可以是：
+ `string`，如 `'someName'`，等同于 `{name: 'someName'}`
+ `Object`，属性可以有：
    + name: `string`。
    + type: `string`，支持
        + `number`，默认，表示普通数据。
        + `ordinal`，对于类目、文本这些 string 类型的数据，如果需要能在数轴上使用，须是 'ordinal' 类型。ECharts 默认会自动判断这个类型。但是自动判断也是不可能很完备的，所以使用者也可以手动强制指定。
        + `float`，即 [Float64Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array)。
        + `int`，即 [Int32Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int32Array)。
        + `time`，表示时间类型。设置成 'time' 则能支持自动解析数据成时间戳（timestamp），比如该维度的数据是 '2017-05-10'，会自动被解析。时间类型的支持参见 [data](~series.data)。
    + displayName: 一般用于 tooltip 中维度名的展示。`string` 如果没有指定，默认使用 name 来展示。

值得一提的是，当定义了 `dimensions` 后，默认 `tooltip` 中对个维度的显示，会变为『竖排』，从而方便显示每个维度的名称。如果没有定义 `dimensions`，则默认 `tooltip` 会横排显示，且只显示数值没有维度名称可显示。





