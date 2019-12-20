{{target: component-radar}}

# radar(Object)

雷达图坐标系组件，只适用于[雷达图](~series-radar)。

雷达图坐标系与极坐标系不同的是它的每一个轴（indicator 指示器）都是一个单独的维度，可以通过 [name](~radar.name)、[axisLine](~radar.axisLine)、[axisTick](~radar.axisTick)、[axisLabel](~radar.axisLabel)、[splitLine](~radar.splitLine)、 [splitArea](~radar.splitArea) 几个配置项配置指示器坐标轴线的样式。


下面是一个 radar 组件的一个自定义例子。

~[400x400](${galleryViewPath}doc-example/radar&edit=1&reset=1)

{{use: partial-component-id(prefix="#")}}

{{use: component-circular-layout(
    defaultRadius="75%"
)}}

## startAngle(number) = 90

坐标系起始角度，也就是第一个指示器轴的角度。

## name(Object)

雷达图每个指示器名称的配置项。

### show(boolean) = true

是否显示指示器名称。默认显示。

### formatter(string|Function)

指示器名称显示的格式器。支持字符串和回调函数，如下示例：

```js
// 使用字符串模板，模板变量为指示器名称 {value}
formatter: '【{value}】'
// 使用回调函数，第一个参数是指示器名称，第二个参数是指示器配置项
formatter: function (value, indicator) {
    return '【' + value + '】';
}
```

{{ use: partial-text-style(
    prefix='##',
    defaultColor="'#333'",
    noAlign=true,
    noVerticalAlign=true
)}}

## nameGap(number) = 15

指示器名称和指示器轴的距离。

## splitNumber(number) = 5

指示器轴的分割段数。

## shape(string) = 'polygon'

雷达图绘制类型，支持 `'polygon'` 和 `'circle'`。

## scale(boolean) = false

是否是脱离 0 值比例。设置成 `true` 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。

{{ use: partial-axis-common-axis-line(
    prefix="#"
)}}

{{ use: partial-axis-common-axis-tick(
    prefix="#",
    hasLabelInterval=false,
    hasAlignWithLabel=false,
    hasInside=false
) }}

{{ use: partial-axis-common-axis-label(
    prefix="#",
    hasLabelInterval=false,
    hasInside=false
) }}

{{ use: partial-axis-common-split-line(
    prefix="#",
    hasLabelInterval=false
)}}

{{ use: partial-axis-common-split-area(
    prefix="#",
    hasLabelInterval=false,
    defaultShow=true
)}}

## indicator(Array)

雷达图的指示器，用来指定雷达图中的多个变量（维度）。

**例如：**
```js
indicator: [
   { name: '销售（sales）', max: 6500},
   { name: '管理（Administration）', max: 16000, color: 'red'}, // 标签设置为红色
   { name: '信息技术（Information Techology）', max: 30000},
   { name: '客服（Customer Support）', max: 38000},
   { name: '研发（Development）', max: 52000},
   { name: '市场（Marketing）', max: 25000}
]
```

### name(string)

指示器名称。

### max(number)

指示器的最大值，可选，建议设置。

### min(number)

指示器的最小值，可选，默认为 0。

### color(string)

标签特定的颜色。