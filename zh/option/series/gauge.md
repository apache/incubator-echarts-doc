
{{target: series-gauge}}

# series.gauge(Object)

**仪表盘**

 **例如：** 
~[600x500](${galleryViewPath}gauge-car)

## type(string) = 'gauge'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}

{{ use: partial-circular-layout }}
<!-- overwrite radius -->
## radius(number|string) = '75%'
仪表盘半径，可以是相对于容器高宽中较小的一项的一半的百分比，也可以是绝对的数值。

{{ use partial-legend-hover-link }}

## startAngle(number) = 225
仪表盘起始角度。[圆心](~series-gauge.center) 正右手侧为`0`度，正上方为`90`度，正左手侧为`180`度。

## endAngle(number) = -45
仪表盘结束角度。

## clockwise(boolean) = true
仪表盘刻度是否是顺时针增长。

## data(Array)
{{ use: partial-1d-data-desc }}
### name(string)
数据项名称。
### value(number)
数据值。

## min(number) = 0
最小的数据值，映射到 [minAngle](~series-gauge.minAngle)。

## max(number) = 100
最大的数据值，映射到 [maxAngle](~series-gauge.maxAngle)。

## splitNumber(number) = 10
仪表盘刻度的分割段数。

## axisLine(Object)
仪表盘轴线相关配置。
### show(boolean) = true
是否显示仪表盘轴线。
### lineStyle(Object)
仪表盘轴线样式。
#### color(Array)
仪表盘的轴线可以被分成不同颜色的多段。每段的结束位置和颜色可以通过一个数组来表示。

默认取值：
```js
[[0.2, '#91c7ae'], [0.8, '#63869e'], [1, '#c23531']]
```
#### width(number) = 30
轴线宽度。
{{ use: partial-style-shadow-opacity(prefix="###") }}

## splitLine(Object)
分隔线样式。
### show(boolean) = true
是否显示分隔线。
### length(number|string) = 30
分隔线线长。支持相对半径的百分比。
### lineStyle(Object)
{{ use: partial-line-style(
    prefix='###',
    defaultColor='#eee',
    defaultWidth=2,
    defaultType="'solid'"
) }}

## axisTick(Object)
刻度样式。
### show(boolean) = true
是否显示刻度。
### splitNumber(number) = 5
分隔线之间分割的刻度数。
### length(number|string) = 8
刻度线长。支持相对半径的百分比。
### lineStyle(Object)
{{ use: partial-line-style(
    prefix='###',
    defaultColor='#eee',
    defaultWidth=1,
    defaultType="'solid'"
) }}

## axisLabel(Object)
刻度标签。
### show(boolean) = true
是否显示标签。
### distance(number) = 5
标签与刻度线的距离。
### formatter(string|Function)
刻度标签的内容格式器，支持字符串模板和回调函数两种形式。

 **例如：** 
```js
// 使用字符串模板，模板变量为刻度默认标签 {value}
formatter: '{value} kg'

// 使用函数模板，函数参数分别为刻度数值
formatter: function (value) {
    return value + 'km/h';
}
```
{{ use: partial-text-style(
    prefix="##",
    noAlign=true,
    noVerticalAlign=true
) }}


## pointer(Object)
仪表盘指针。
### show(boolean) = true
是否显示指针。
### length(string|number) = '80%'
指针长度，可以是绝对数值，也可以是相对于[半径](~series-gauge.radius)的半分比。
### width(number) = 8
指针宽度。

## itemStyle(Object)
仪表盘指针样式。
{{ use: partial-item-style(prefix="##") }}
<!-- overwrite color -->
### color(Color) = 'auto'
指针颜色，默认取数值所在的[区间的颜色](~series-gauge.axisLine.lineStyle.color)


## emphasis(Object)
高亮的仪表盘指针样式

### itemStyle
{{ use: partial-item-style(prefix="###") }}

## title(Object)
仪表盘标题。
### show(boolean) = true
是否显示标题。
### offsetCenter(Array) = [0, '-40%']
相对于仪表盘中心的偏移位置，数组第一项是水平方向的偏移，第二项是垂直方向的偏移。可以是绝对的数值，也可以是相对于仪表盘半径的百分比。
{{ use: partial-text-style(
    prefix="##",
    defaultColor = "'#333'",
    defaultFontSize = 15,
    noAlign=true,
    noVerticalAlign=true
) }}

## detail(Object)
仪表盘详情，用于显示数据。
### show(boolean) = true
是否显示详情。
### width(number) = 100
详情宽度。
### height(number) = 40
详情高度。
### backgroundColor(Color) = 'transparent'
详情背景色。
### borderWidth(number) = 0
详情边框宽度。
### borderColor(Color) = '#ccc'
详情边框颜色。
### offsetCenter(Array) = [0, '40%']
相对于仪表盘中心的偏移位置，数组第一项是水平方向的偏移，第二项是垂直方向的偏移。可以是绝对的数值，也可以是相对于仪表盘半径的百分比。
### formatter(Function)
格式化函数或者字符串

```js
formatter: function (value) {
    return value.toFixed(0);
}
```

{{ use: partial-text-style(
    prefix="##",
    defaultColor = "'auto'",
    defaultFontSize = 15,
    noAlign=true,
    noVerticalAlign=true
) }}
<!-- overwrite color -->
#### color(Color) = 'auto'
文本颜色，默认取数值所在的[区间的颜色](~series-gauge.axisLine.lineStyle.color)

{{use: partial-marker(
    prefix="#",
    galleryEditorPath=${galleryEditorPath},
    seriesType="gauge"
)}}

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

