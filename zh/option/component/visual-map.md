
{{target: component-visual-map}}

# visualMap(Array|Object)

`visualMap` 是视觉映射组件，用于进行『视觉编码』，也就是将数据映射到视觉元素（视觉通道）。

视觉元素可以是：<br>
{{use: partial-visual-map-visual-type}}

`visualMap` 组件可以定义多个，从而可以同时对数据中的多个维度进行视觉映射。

`visualMap` 组件可以定义为 [分段型（visualMapPiecewise）](~visualMap-piecewise) 或 [连续型（visualMapContinuous）](~visualMap-continuous)，通过 `type` 来区分。例如：

```javascript
option = {
    visualMap: [
        { // 第一个 visualMap 组件
            type: 'continuous', // 定义为连续型 visualMap
            ...
        },
        { // 第二个 visualMap 组件
            type: 'piecewise', // 定义为分段型 visualMap
            ...
        }
    ],
    ...
};
```

<br>
**✦ 视觉映射方式的配置 ✦**

既然是『数据』到『视觉元素』的映射，`visualMap` 中可以指定数据的『哪个维度』（参见[visualMap.dimension](~visualMap.dimension)）映射到哪些『视觉元素』（参见[visualMap.inRange](~visualMap.inRange) 和 [visualMap.outOfRange](~visualMap.outOfRange)）中。

<br>
在 visualMap 组件所控制的 series 中，如果 series 中某个数据项需要避开 visualMap 映射，可以这么配置：
```
series: {
    type: '...',
    data: [
        {name: 'Shanghai', value: 251},
        {name: 'Haikou', value: 21},
        // 设置 `visualMap: false` 则 visualMap 不对此项进行控制，此时系列
        // 可使用自身的视觉参数（color/symbol/ ...控制此项的显示。
        {name: 'Beijing', value: 821, visualMap: false},
        ...
    ]
}
```



<br>
**✦ 与 ECharts 2 中 dataRange 的关系 ✦**

`visualMap` 是由 ECharts 2 中的 `dataRange` 组件改名以及扩展而来。ECharts 3里 `option` 中的 `dataRange` 配置项仍然被兼容，会自动转换成 `visualMap` 配置项。在option中推荐写 `visualMap` 而非 `dataRange`。

<br>
**✦ 以下是visualMap各组件的详细介绍 ✦**

<br>
<br>


{{import: component-visual-map-continuous}}
{{import: component-visual-map-piecewise}}










{{target: partial-visual-map-range}}
`${rangeType}` 能定义目标系列（参见 [${visualMapName}.seriesIndex](~${visualMapName}.seriesIndex)）视觉形式，也同时定义了 `${visualMapName}` 本身的视觉样式。通俗来讲就是，假如 `${visualMapName}`控制的是散点图，那么 `${rangeType}` 同时定义了散点图的 `颜色`、`尺寸` 等，也定义了 `${visualMapName}` 本身的 `颜色`、`尺寸` 等。这二者能对应上。

定义方式，例如：

```javascript
visualMap: [
    {
        ...,
        ${rangeType}: {
            color: ['#121122', 'rgba(3,4,5,0.4)', 'red'],
            symbolSize: [30, 100]
        }
    }
]
```

如果想分别定义 `${visualMapName}` 本身的视觉样式和 `目标系列` 的视觉样式，则这样定义：

```javascript
visualMap: [
    {
        ...,
        // 表示 目标系列 的视觉样式。
        target: {
            ${rangeType}: {
                color: ['#121122', 'rgba(3,4,5,0.4)', 'red'],
                symbolSize: [60, 200]
            }
        },
        // 表示 ${visualMapName} 本身的视觉样式。
        controller: {
            ${rangeType}: {
                symbolSize: [30, 100]
            }
        }
    }
]
```

或者这样定义：
```javascript
visualMap: [
    {
        ...,
        // 表示 目标系列 的视觉样式 和 ${visualMapName} 共有的视觉样式。
        ${rangeType}: {
            color: ['#121122', 'rgba(3,4,5,0.4)', 'red'],
            symbolSize: [60, 200]
        },
        // 表示 ${visualMapName} 本身的视觉样式，会覆盖共有的视觉样式。比如，symbolSize 覆盖成为 [30, 100]，而 color 不变。
        controller: {
            ${rangeType}: {
                symbolSize: [30, 100]
            }
        }
    }
]
```

**✦ 关于视觉通道 ✦**

+ ${rangeType} 中，可以有任意几个的『视觉通道』定义（如 `color`、`symbolSize` 等）。这些视觉通道，会被同时采用。

+ 一般来说，建议使用 `透明度（opacity）` ，而非 `颜色透明度（colorAlpha）` （他们细微的差异在于，前者能也同时控制图元中的附属物（如 label）的透明度，而后者只能控制图元本身颜色的透明度）。

+ 视觉映射的方式：支持两种方式：线性映射、查表映射。


**✦ 视觉通道 -- 线性映射 ✦**

`线性映射` 表示 series.data 中的每一个值（dataValue）会经过线性映射计算，从 `[visualMap.min, visualMap.max]` 映射到设定的 `[visual value 1, visual value 2]` 区间中的某一个视觉的值（下称 visual value）。

例如，我们设置了 `[visualMap.min, visualMap.max] 为 [0, 100]`，并且我们有 `series.data: [50, 10, 100]`。我们想将其映射到范围为 `[0.4, 1]` 的 `opacity` 上，从而达到用透明度表达数值大小的目的。那么 visualMap 组件会对 series.data 中的每一个 dataValue 做线性映射计算，得到一个 opacityValue。最终得到的 opacityValues 为 `[0.7, 0.44, 1]`。

visual 范围也可以反向，例如上例，可以设定 `opacity` 范围为 `[1, 0.4]`，则上例得到的 opacityValues 为 `[0.7, 0.96, 0.4]`。

**注意：**[visualMap.min, visualMap.max] 需手动设置，不设置则默认取 [0, 100]，而非 series.data 中的 `dataMin` 和 `dataMax`。


如何设定为线性映射？以下情况时，会设定为 `线性映射`：

+ 当 `visualMap` 为 [visualMap-continuous](~visualMap-continuous) 时，或者

+ 当 `visualMap` 为 [visualMap-piecewise](~visualMap-piecewise) 且 未设置 [visualMap-piecewise.categories](~visualMap-piecewise.categories) 时。

视觉通道的值（visual value）：

+ 视觉通道的值一般都以 `Array` 形式表示，例如：`color: ['#333', '#777']`。

+ 如果写成 `number` 或 `string`，会转成 `Array`。例如，写成 `opacity: 0.4` 会转成 `opacity: [0.4, 0.4]`，`color: '#333'` 会转成 `color: ['#333', '#333']`。

+ 对于 `图形大小（symbolSize）`、`透明度（opacity）`、`颜色透明度（colorAlpha）`、`颜色明暗度（colorLightness）`、`颜色饱和度（colorSaturation）`、`色调（colorHue）`：形如`Array` 的视觉范围总是表示：`[最小数据值对应的视觉值, 最大数据值对应的视觉值]`。比如：`colorLightness: [0.8, 0.2]`，表示 series.data 中，和 `visualMap.min` 相等的值（如果有的话）映射到 `颜色明暗` 的 `0.8`，和 `visualMap.max` 相等的值（如果有的话）映射到 `颜色明暗` 的 `0.2`，中间其他数据值，按照线性计算出映射结果。

+ 对于 `颜色（color）`，使用数组表示例如：`['#333', '#78ab23', 'blue']`。意思就是以这三个点作为基准，形成一种『渐变』的色带，数据映射到这个色带上。也就是说，与 `visualMap.min` 相等的值会映射到 `'#333'`，与 `visualMap.max` 相等的值会映射到 `'blue'`。对于 `visualMap.min` 和 `visualMap.max` 中间的其他点，以所给定的 `'#333'`, `'#78ab23'`, `'blue'` 这三个颜色作为基准点进行分段线性插值，得到映射结果。

+ 对于 `图形类别（symbol）`：使用数据表示例如：`['circle', 'rect', 'diamond']`。与 `visualMap.min` 相等的值会映射到 `'circle'`，与 `visualMap.max` 相等的值会映射到 `'diamond'`。对于 中间的其他点，会根据他们和 `visualMap.min` 和 `visualMap.max` 的数值距离，映射到 `'circle'`, `'rect'`, `'diamond'` 中某个值上。


visual value 的取值范围：

+ `透明度（opacity）`、`颜色透明度（colorAlpha）`、`颜色明暗度（colorLightness）`、`颜色饱和度（colorSaturation）`，`visual value`

    取值范围是 `[0, 1]`。

+ `色调（colorHue）`

    取值范围是 `[0, 360]`。

+ `颜色（color）`：

    颜色可以使用 RGB 表示，比如 `'rgb(128, 128, 128)'`，如果想要加上 alpha 通道，可以使用 RGBA，比如 `'rgba(128, 128, 128, 0.5)'`，也可以使用十六进制格式，比如 '#ccc'。

+ `图形类别（symbol）`：

    {{ use: partial-icon }}


**✦ 视觉通道 -- 查表映射 ✦**

`查表映射` 表示 series.data 中的所有值（dataValue）是可枚举的，会根据给定的映射表查表得到映射结果。

例如，在 [visualMap-piecewise](~visualMap-piecewise) 中，我们设定了 [visualMap-piecewise.categories](~visualMap-piecewise.categories) 为 `['Demon Hunter', 'Blademaster', 'Death Knight', 'Warden', 'Paladin']`。我们有 series.data: `['Demon Hunter', 'Death Knight', 'Warden', 'Paladin']`。然后我们可以定立查表映射规则：`color: {'Warden': 'red', 'Demon Hunter': 'black'}`，于是 `visualMap` 组件会按照表来将 `dataValue` 映射到 `color`。

如何设定为查表映射？当 `visualMap` 为 [visualMap-piecewise](~visualMap-piecewise) 且 设置了 [visualMap-piecewise.categories](~visualMap-piecewise.categories) 时，会进行查表映射。

视觉通道的值（visual value）：一般使用 `Object` 或 `Array` 来表示，例如：

```javascript
visualMap: {
    type: 'piecewise',
    // categories 定义了 visualMap-piecewise 组件显示出来的项。
    categories: [
        'Demon Hunter', 'Blademaster', 'Death Knight', 'Warden', 'Paladin'
    ],
    ${rangeType}: {
        // visual value 可以配成 Object：
        color: {
            'Warden': 'red',
            'Demon Hunter': 'black',
            '': 'green' // 空字串，表示除了'Warden'、'Demon Hunter'外，都对应到 'green'。
        }
        // visual value 也可以只配一个单值，表示所有都映射到一个值，如：
        color: 'green',
        // visual value 也可以配成数组，这个数组须和 categories 数组等长，
        // 每个数组项和 categories 数组项一一对应：
        color: ['red', 'black', 'green', 'yellow', 'white']
    }
}
```

[参见示例](${galleryEditorPath}doc-example/scatter-visualMap-categories&edit=1&reset=1)





{{target: partial-visual-map-merge}}

**✦ 修改视觉编码 ✦**

如果在图表被渲染后（即已经使用 `setOption` 设置了初始 `option` 之后），想修改 ${componentMainType} 的各种 `视觉编码`，按照惯例，再次使用 `setOption` 即可。例如：

```javascript
chart.setOption({
    ${componentMainType}: {
        inRange: {color: ['red', 'blue']}
    }
});
```

**注意:**

+ ${componentMainType} option 中的这几个属性，`inRange`, `outOfRange`, `target`, `controller`，在 setOption 时不支持 merge。否则会带来过于复杂的 merge 逻辑。也就是说，`setOption` 时，一旦修改了以上几个属性中的一项，其他项也会被清空，而非保留当前状态。所以，设置 visual 值时，请一次性全部设置，而非只设置一部分。

+ **不推荐使用 `getOption -> 修改option -> setOption` 的方式：**

```javascript
// 不推荐这样做（尽管也能达到和上面的例子相同的结果）：
var option = chart.getOption(); // 获取所有option。
option.${componentMainType}.inRange.color = ['red', 'blue']; // 改动color（我想要改变 color）。

// 如下两处也要进行同步改动，否则可能达不到期望效果。
option.${componentMainType}.target.inRange.color = ['red', 'blue'];
option.${componentMainType}.controller.inRange.color = ['red', 'blue'];

chart.setOption(option); // option设置回 ${componentMainType}
```






{{target: partial-visual-map-inRange-outOfRange}}

##${prefix} inRange(Object)

定义 **在选中范围中** 的视觉元素。（用户可以和 visualMap 组件交互，用鼠标或触摸选择范围）

可选的视觉元素有：

{{use: partial-visual-map-visual-type}}

---

{{use: partial-visual-map-range(
    rangeType='inRange',
    visualMapName=${visualMapName},
    galleryEditorPath=${galleryEditorPath}
)}}

---

{{use: partial-visual-map-merge(
    componentMainType='visualMap'
)}}

**注意:** inRange 没有指定，则会默认会设置 color: `['#f6efa6', '#d88273', '#bf444c']`，如果你不想要这个color，可以
`inRange: {color: null}` 来去除。


##${prefix} outOfRange(Object)

定义 **在选中范围外** 的视觉元素。（用户可以和 visualMap 组件交互，用鼠标或触摸选择范围）

可选的视觉元素有：

{{use: partial-visual-map-visual-type}}

---

{{use: partial-visual-map-range(
    rangeType='outOfRange',
    visualMapName=${visualMapName},
    galleryEditorPath=${galleryEditorPath}
)}}

---

{{use: partial-visual-map-merge(
    componentMainType='visualMap'
)}}




{{target: partial-visual-map-common}}


## show(boolean) = true

是否显示 ${visualMapName} 组件。如果设置为 `false`，不会显示，但是数据映射的功能还存在。


## dimension(number)

指定用数据的『哪个维度』，映射到视觉元素上。『数据』即 [series.data](~series.data)。
可以把 [series.data](~series.data) 理解成一个二维数组，例如：

```javascript
[
    [12, 23, 43],
    [12, 23, 43],
    [43, 545, 65],
    [92, 23, 33]
]
```

其中每个列是一个维度，即 `dimension`。
例如 `dimension` 为 1 时，取第二列（即 23，23，545，23），映射到视觉元素上。

默认取 `data` 中最后一个维度。


## seriesIndex(number|Array)

指定取哪个系列的数据，即哪个系列的 [series.data](~series.data)。

默认取所有系列。


## hoverLink(boolean) = true

打开 `hoverLink` 功能时，鼠标悬浮到 `visualMap` 组件上时，鼠标位置对应的数值 在 图表中对应的图形元素，会高亮。

反之，鼠标悬浮到图表中的图形元素上时，在 `visualMap` 组件的相应位置会有三角提示其所对应的数值。


{{use: partial-visual-map-inRange-outOfRange(
    prefix="",
    visualMapName=${visualMapName},
    galleryEditorPath=${galleryEditorPath}
)}}


## controller(Object)

visualMap 组件中，`控制器` 的 `inRange` `outOfRange` 设置。如果没有这个 `controller` 设置，`控制器` 会使用外层的 `inRange` `outOfRange` 设置；如果有这个 `controller` 设置，则会采用这个设置。适用于一些控制器视觉效果需要特殊定制或调整的场景。

{{use: partial-visual-map-inRange-outOfRange(
    prefix="#",
    visualMapName=${visualMapName},
    galleryEditorPath=${galleryEditorPath}
)}}



{{ use: partial-rect-layout(
    componentName="visualMap ",
    defaultZ="4",
    defaultLeft="0",
    defaultRight="auto",
    defaultTop="auto",
    defaultBottom="0"
) }}




## orient(string) = 'vertical'

如何放置 visualMap 组件，水平（`'horizontal'`）或者竖直（`'vertical'`）。


## padding(number|Array) = 5

{{ use: partial-padding(componentName=${visualMapName})}}


## backgroundColor(Color) = 'rgba(0,0,0,0)'

背景色。


## borderColor(Color) = '#ccc'

边框颜色。


## borderWidth(number) = 0

边框线宽，单位px。


## color(Array) = ['#bf444c', '#d88273', '#f6efa6']

这个配置项，是为了兼容 ECharts 2 而存在，ECharts 3 中已经不推荐使用。它的功能已经移到了 [${visualMapName}.inRange](~${visualMapName}.inRange) 和 [${visualMapName}.outOfRange](~${visualMapName}.outOfRange) 中。

如果要使用，需注意，`color`属性中的顺序是由数值 `大` 到 `小`，但是 [${visualMapName}.inRange](~${visualMapName}.inRange) 或 [${visualMapName}.outOfRange](~${visualMapName}.outOfRange) 中 `color` 的顺序，总是由数值 `小` 到 `大`。二者不一致。


## textStyle(Object)

{{ use:partial-simple-text-style(
    prefix='##',
    name='visualMap ',
    defaultColor='#333'
) }}
