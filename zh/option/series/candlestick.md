
{{target: series-candlestick}}

# series.candlestick(Object)

[Candlestick](https://en.wikipedia.org/wiki/Candlestick_chart) 即我们常说的 `K线图`。

在 ECharts3 中，同时支持 `'candlestick'` 和 `'k'`这两种 `'series.type'`（`'k'` 会被自动转为 `'candlestick'`）。

 **例如：** 

~[600x400](${galleryViewPath}candlestick-sh&edit=1&reset=1)


<br>
**关于『涨』『跌』的颜色：**

不同国家或地区对于 K线图 的颜色定义不一样，可能是『红涨绿跌』或『红涨蓝跌』（如大陆、台湾、日本、韩国等），可能是『绿涨红跌』（如西方国家、香港、新加坡等）。K线图也不一定要用红蓝、红绿来表示涨跌，也可以是『有色/无色』等表示方法。

默认配置项，采用的是『红涨蓝跌』。如果想更改这个颜色配置，在这些配置项中更改即可：

+ [series-candlestick.itemStyle.color](~series-candlestick.itemStyle.color)：阳线填充色（即『涨』）
+ [series-candlestick.itemStyle.color0](~series-candlestick.itemStyle.color0)：阴线填充色（即『跌』）
+ [series-candlestick.itemStyle.borderColor](~series-candlestick.itemStyle.borderColor)：阳线边框色（即『涨』）
+ [series-candlestick.itemStyle.borderColor0](series-candlestick.itemStyle.borderColor0)：阴线边框色（即『跌』）


<br>
<br>

## type(string) = 'candlestick'

{{use: partial-component-id(prefix="#")}}

{{use: partial-coord-sys(
    seriesType="cartesian2d",
    coordSysDefault="'cartesian2d'",
    cartesian2d=true
)}}

{{ use: partial-series-name }}

{{ use: partial-legend-hover-link }}


## hoverAnimation(boolean) = true

是否开启 hover 在 box 上的动画效果。


## layout(string) = null

布局方式。

**可选：**

+ `'horizontal'`：水平排布各个 box。

+ `'vertical'`：竖直排布各个 box。

默认值根据当前坐标系状况决定：如果 `category` 轴为横轴，则水平排布；否则竖直排布；如果没有 `category` 轴则水平排布。


## barWidth(number)

指定柱宽度。可以使用绝对数值（如 `10`）或百分比（如 `'20%'`，表示 band width 的百分之多少）。默认自适应。

## barMinWidth(number)

指定柱最小宽度。可以使用绝对数值（如 `10`）或百分比（如 `'20%'`，表示 band width 的百分之多少）。默认自适应。

## barMaxWidth(number)

指定柱最大宽度。可以使用绝对数值（如 `10`）或百分比（如 `'20%'`，表示 band width 的百分之多少）。默认自适应。

## itemStyle(Object)

K 线图的图形样式。

{{use: partial-candlestick-item-style-detail(
    prefix="##",
    defaultColor="#c23531",
    defaultColor0="#314656",
    defaultBorderColor="#c23531",
    defaultBorderColor0="#314656",
    defaultBorderWidth=1
)}}


## emphasis(Object)

K 线图的高亮图形样式。

### itemStyle(Object)

{{use: partial-candlestick-item-style-detail(
    prefix="###",
    defaultColor="#c23531",
    defaultColor0="#314656",
    defaultBorderColor="#c23531",
    defaultBorderColor0="#314656",
    defaultBorderWidth=2
)}}


{{use: partial-large(
    prefix="#",
    defaultLarge=true,
    defaultLargeThreshold=600
)}}

{{ use:partial-progressive(
    prefix='#',
    supportProgressiveChunkMode=true,
    defaultProgressive=3000,
    defaultProgressiveThreshold=10000,
    defaultProgressiveChunkMode='mod'
) }}

{{use:partial-series-dimensions(
    prefix="#"
)}}

{{use:partial-series-encode(
    prefix="#"
)}}


## data(Array)

数据格式是如下的二维数组。

```javascript
[
    [2320.26, 2320.26, 2287.3,  2362.94],
    [2300,    2291.3,  2288.26, 2308.38],
    { // 数据项也可以是 Object，从而里面能含有对此数据项的特殊设置。
        value: [2300,    2291.3,  2288.26, 2308.38],
        itemStyle: {...}
    },
    ...
]
```

二维数组的每一数组项（上例中的每行）是渲染一个box，它含有四个量值，依次是：

```javascript
[open, close, lowest, highest] （即：[开盘值, 收盘值, 最低值, 最高值]）
```

### name(string)

数据项名称。

### value(Array)

数据项值。


```javascript
[open, close, lowest, highest] （即：[开盘值, 收盘值, 最低值, 最高值]）
```

### itemStyle(Object)

单个 K 线图数据的图形样式。

{{use: partial-candlestick-item-style-detail(
    prefix="###",
    defaultColor="#c23531",
    defaultColor0="#314656",
    defaultBorderColor="#c23531",
    defaultBorderColor0="#314656",
    defaultBorderWidth=1
)}}

### emphasis(Object)

单个 K 线图数据的高亮图形样式。

#### itemStyle(Object)

{{use: partial-candlestick-item-style-detail(
    prefix="####",
    defaultColor="#c23531",
    defaultColor0="#314656",
    defaultBorderColor="#c23531",
    defaultBorderColor0="#314656",
    defaultBorderWidth=2
)}}


{{use: partial-tooltip-in-series-data(
    galleryViewPath=${galleryViewPath}
)}}


{{use: partial-marker(
    prefix="#",
    seriesType="candlestick",
    galleryEditorPath=${galleryEditorPath},
    hasCoord=true,
    hasType=true
)}}

{{use:partial-z-zlevel(
    prefix="#",
    componentName="K线图"
) }}

{{ use:partial-silent(
    prefix="#"
) }}

{{use: partial-animation-init(
    prefix="#",
    defaultAnimationEasing='linear',
    defaultAnimationDuration=300,
    galleryEditorPath=${galleryEditorPath}
)}}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}






{{target: partial-candlestick-item-style-detail}}

#${prefix} color(Color)=${defaultColor}

`阳线` 图形的颜色。

{{ use: partial-color-desc }}

#${prefix} color0(Color)=${defaultColor0}

`阴线` 图形的颜色。

{{ use: partial-color-desc }}

#${prefix} borderColor(Color) = ${defaultBorderColor}

`阳线` 图形的描边颜色。

{{ use: partial-color-desc }}

#${prefix} borderColor0(Color) = ${defaultBorderColor0}

`阴线` 图形的描边颜色。

{{ use: partial-color-desc }}

#${prefix} borderWidth(number) = ${defaultBorderWidth}

candlestick 描边线宽。为 0 时无描边。

{{ use:partial-style-shadow-opacity(
    prefix=${prefix},
    defaultOpacity=${defaultOpacity},
    defaultShadowBlur=${defaultShadowBlur},
    defaultShadowColor=${defaultShadowColor},
    defaultShadowOffsetX=${defaultShadowOffsetX},
    defaultShadowOffsetY=${defaultShadowOffsetY}
) }}
