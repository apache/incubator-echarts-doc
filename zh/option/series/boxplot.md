
{{target: series-boxplot}}

# series.boxplot(Object)

[Boxplot](https://en.wikipedia.org/wiki/Box_plot) 中文可以称为『箱形图』、『盒须图』、『盒式图』、『盒状图』、『箱线图』，是一种用作显示一组数据分散情况资料的统计图。它能显示出一组数据的最大值、最小值、中位数、下四分位数及上四分位数。

 **例如：** 

~[600x400](${galleryViewPath}boxplot-light-velocity&edit=1&reset=1)

<br>
也支持多个 `series` 在同一个坐标系中，参见 [例子](${galleryEditorPath}boxplot-multi&edit=1&reset=1)。

<br>
<br>

## type(string) = 'boxplot'

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


## boxWidth(Array) = [7, 50]

box 的宽度的上下限。数组的意思是：`[min, max]`。

可以是绝对数值，如 `[7, 50]`，也可以是百分比，如 `['40%', '90%']`。百分比的意思是，最大可能宽度（bandWidth）的百分之多少。


## itemStyle(Object)

盒须图样式。

{{use: partial-item-style(
    prefix="##",
    useColorPalatte=true,
    name="boxplot",
    defaultColor="#fff",
    defaultBorderWidth=1
)}}

## emphasis(Object)

盒须图高亮样式

### itemStyle(Object)

{{use: partial-item-style(
    prefix="###",
    useColorPalatte=true,
    name="boxplot",
    defaultColor="#fff",
    defaultBorderWidth=2,
    defaultShadowBlur=5,
    defaultShadowOffsetX=2,
    defaultShadowOffsetY=2,
    defaultShadowColor="rgba(0,0,0,0.4)"
)}}


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
    [655, 850, 940, 980, 1175],
    [672.5, 800, 845, 885, 1012.5],
    [780, 840, 855, 880, 940],
    [621.25, 767.5, 815, 865, 1011.25],
    { // 数据项也可以是 Object，从而里面能含有对此数据项的特殊设置。
        value: [713.75, 807.5, 810, 870, 963.75],
        itemStyle: {...}
    },
    ...
]
```

二维数组的每一数组项（上例中的每行）是渲染一个box，它含有五个量值，依次是：

```javascript
[min,  Q1,  median (or Q2),  Q3,  max]
```

**数据的处理**

ECharts 并不内置对原始数据的处理，输入给 `boxplot` 的数据须是如上五个统计结果量值。

但是 ECharts 也额外提供了简单的 [原始数据处理函数](https://github.com/apache/incubator-echarts/tree/master/extension/dataTool)，如这个 [例子](${galleryEditorPath}boxplot-light-velocity&edit=1&reset=1) 使用了`echarts.dataTool.prepareBoxplotData` 来进行简单的数据统计。


### name(string)

数据项名称。

### value(Array)

数据值。

```javascript
[min,  Q1,  median (or Q2),  Q3,  max]
```


### itemStyle(Object)

单个数据盒须图样式。

{{use: partial-item-style(
    prefix="###",
    useColorPalatte=true,
    name="boxplot",
    defaultColor="#fff",
    defaultBorderWidth=1
)}}

### emphasis(Object)

单个数据盒须图高亮样式

#### itemStyle(Object)

{{use: partial-item-style(
    prefix="####",
    useColorPalatte=true,
    name="boxplot",
    defaultColor="#fff",
    defaultBorderWidth=2,
    defaultShadowBlur=5,
    defaultShadowOffsetX=2,
    defaultShadowOffsetY=2,
    defaultShadowColor="rgba(0,0,0,0.4)"
)}}


{{use: partial-tooltip-in-series-data(
    galleryViewPath=${galleryViewPath}
)}}


{{use: partial-marker(
    prefix="#",
    seriesType="boxplot",
    galleryEditorPath=${galleryEditorPath},
    hasCoord=true,
    hasType=true
)}}

{{use:partial-z-zlevel(
    prefix="#",
    componentName="盒须图"
) }}

{{ use:partial-silent(
    prefix="#"
) }}

{{use: partial-animation-init(
    prefix="#",
    defaultAnimationEasing='elasticOut',
    defaultAnimationDuration=800,
    galleryEditorPath=${galleryEditorPath}
)}}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}
