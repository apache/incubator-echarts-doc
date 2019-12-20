{{ target: partial-axisPointer-introduction}}

坐标轴指示器是指示坐标轴当前刻度的工具。

如下例，鼠标悬浮到图上，可以出现标线和刻度文本。

~[600x450](${galleryViewPath}doc-example/candlestick-axisPointer&edit=1&reset=1)

上例中，使用了 [axisPointer.link](~axisPointer.link) 来关联不同的坐标系中的 axisPointer。

坐标轴指示器也有适合触屏的交互方式，如下：

~[600x400](${galleryViewPath}line-tooltip-touch&edit=1&reset=1)

坐标轴指示器在多轴的场景能起到辅助作用：

~[600x300](${galleryViewPath}multiple-y-axis&edit=1&reset=1)
~[600x300](${galleryViewPath}multiple-x-axis&edit=1&reset=1)



---

> **注意:**
> 一般来说，axisPointer 的具体配置项会配置在各个轴中（如 [xAxis.axisPointer](~xAxis.axisPointer)）或者 `tooltip` 中（如 [tooltip.axisPointer](~tooltip.axisPointer)）。

> 但是这几个选项只能配置在全局的 axisPointer 中：[axisPointer.triggerOn](~axisPointer.triggerOn)、[axisPointer.link](~axisPointer.link)。

---

**如何显示 axisPointer：**

直角坐标系 [grid](~grid)、极坐标系 [polar](~polar)、单轴坐标系 [single](~single) 中的每个轴都自己的 axisPointer。

他们的 axisPointer 默认不显示。有两种方法可以让他们显示：

+ 设置轴上的 `axisPointer.show`（例如 [xAxis.axisPointer.show](~xAxis.axisPointer.show)）为 `true`，则显示此轴的 axisPointer。

+ 设置 [tooltip.trigger](~tooltip.trigger) 设置为 `'axis'` 或者 [tooltip.axisPointer.type](~tooltip.axisPointer.type) 设置为 `'cross'`，则此时坐标系会自动选择显示哪个轴的 axisPointer，也可以使用 [tooltip.axisPointer.axis](~tooltip.axisPointer.axis) 改变这种选择。注意，轴上如果设置了 axisPointer，会覆盖此设置。

---

**如何显示 axisPointer 的 label：**

axisPointer 的 label 默认不显示（也就是默认只显示指示线），除非：

+ 设置轴上的 `axisPointer.label.show`（例如 [xAxis.axisPointer.label.show](~xAxis.axisPointer.show)）为 `true`，则显示此轴的 axisPointer 的 label。

+ 设置 [tooltip.axisPointer.type](~tooltip.axisPointer.type) 为 `'cross'` 时会自动显示 axisPointer 的 label。

---

**关于触屏的 axisPointer 的设置**

设置轴上的 `axisPointer.handle.show`（例如 [xAxis.axisPointer.handle.show](~xAxis.axisPointer.handle.show) 为 `true` 则会显示出此 axisPointer 的拖拽按钮。（polar 坐标系暂不支持此功能）。

**注意：**
如果发现此时 tooltip 效果不良好，可设置 [tooltip.triggerOn](~tooltip.triggerOn) 为 `'none'`（于是效果为：手指按住按钮则显示 tooltip，松开按钮则隐藏 tooltip），或者 [tooltip.alwaysShowContent](~tooltip.alwaysShowContent) 为 `true`（效果为 tooltip 一直显示）。

参见[例子](${galleryEditorPath}line-tooltip-touch&edit=1&reset=1)。

---

**自动吸附到数据（snap）**

对于数值轴、时间轴，如果开启了 [snap](~xAxis.axisPointer.snap)，则 axisPointer 会自动吸附到最近的点上。


---










{{ target: partial-axisPointer-common}}

#${prefix} show(boolean) = false

默认不显示。但是如果 [tooltip.trigger](~tooltip.trigger) 设置为 `'axis'` 或者 [tooltip.axisPointer.type](~tooltip.axisPointer.type) 设置为 `'cross'`，则自动显示 axisPointer。坐标系会自动选择显示显示哪个轴的 axisPointer，也可以使用 [tooltip.axisPointer.axis](~tooltip.axisPointer.axis) 改变这种选择。

#${prefix} type(string) = 'line'

指示器类型。

**可选：**

+ `'line'`：直线指示器。

+ `'shadow'`：阴影指示器。

+ `'none'`：无指示器。

{{ use: partial-axisPointer-tooltip-shared(
    prefix=${prefix},
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
)}}

#${prefix} triggerTooltip(boolean) = true

是否触发 tooltip。如果不想触发 tooltip 可以关掉。

#${prefix} value(number) = null

当前的 value。在使用 [axisPointer.handle](xAxisPointer.handle) 时，可以设置此值进行初始值设定，从而决定 axisPointer 的初始位置。

#${prefix} status(boolean)

当前的状态，可取值为 `'show'` 和 `'hide'`。

#${prefix} handle(Object)

拖拽手柄，适用于触屏的环境。参见 [例子](${galleryEditorPath}line-tooltip-touch&edit=1&reset=1)。

##${prefix} show(boolean) = false

当 show 设为 `true` 时开启，这时显示手柄，并且 axisPointer 会一直显示。

##${prefix} icon

手柄的图标。

{{ use: partial-icon-image-path }}

参见 [使用图片的例子](${galleryEditorPath}doc-example/axisPointer-handle-image&edit=1&reset=1)

##${prefix} size(number|Array) = 45

手柄的尺寸，可以设置单值，如 `45`，也可以设置为数组：`[width, height]`。

##${prefix} margin(number) = 50

手柄与轴的距离。
**注意:**这是手柄中心点和轴的距离。

##${prefix} color(string) = '#333'

手柄颜色。

##${prefix} throttle(number) = 40

手柄拖拽时触发视图更新周期，单位毫秒，调大这个数值可以改善性能，但是降低体验。

{{ use:partial-style-shadow(
    prefix='#' + ${prefix},
    defaultShadowBlur=3,
    defaultShadowColor='#aaa',
    defaultShadowOffsetX=2
) }}
















{{ target: partial-axisPointer-tooltip-shared}}

#${prefix} snap(boolean)

坐标轴指示器是否自动吸附到点上。默认自动判断。

这个功能在数值轴和时间轴上比较有意义，可以自动寻找细小的数值点。

#${prefix} z(number)

坐标轴指示器的 z 值。控制图形的前后顺序。`z`值小的图形会被`z`值大的图形覆盖。

#${prefix} label(Object)

坐标轴指示器的文本标签。

##${prefix} show(boolean) = false

是否显示文本标签。如果 [tooltip.axisPointer.type](~tooltip.axisPointer.type) 设置为 `'cross'` 则默认显示标签，否则默认不显示。

##${prefix} precision(number|string) = 'auto'

文本标签中数值的小数点精度。默认根据当前轴的值自动判断。也可以指定如 `2` 表示保留两位小数。

##${prefix} formatter(string|Function) = null

文本标签文字的格式化器。

如果为 `string`，可以是例如：`formatter: 'some text {value} some text`，其中 `{value}` 会被自动替换为轴的值。

如果为 `function`，可以是例如：

**参数：**

`{Object}` params: 含有：

`{Object}` params.value: 轴当前值，如果 axis.type 为 'category' 时，其值为 axis.data 里的数值。如果 axis.type 为 `'time'`，其值为时间戳。

`{Array.<Object>}` params.seriesData: 一个数组，是当前 axisPointer 最近的点的信息，每项内容为

`{string}` params.axisDimension: 轴的维度名，例如直角坐标系中是 `'x'`、`'y'`，极坐标系中是 `'radius'`、`'angle'`。

`{number}` params.axisIndex: 轴的 index，`0`、`1`、`2`、...

{{ use: partial-formatter-params-structure }}

{{ use: partial-formatter-params-axisPointer }}


**返回值：**

显示的 string。

例如：
```js
formatter: function (params) {
    // 假设此轴的 type 为 'time'。
    return 'some text' + echarts.format.formatTime(params.value);
}
```

##${prefix} margin(boolean) = 3

label 距离轴的距离。


{{ use: partial-simple-text-style(
    prefix='#' + ${prefix},
    defaultColor="'#fff'"
)}}

##${prefix} padding(string|Array) = [5, 7, 5, 7]

{{ use: partial-padding(componentName='axisPointer')}}


##${prefix} backgroundColor(string) = 'auto'

文本标签的背景颜色，默认是和 [axis.axisLine.lineStyle.color](~xAxis.axisLine.lineStyle.color) 相同。

##${prefix} borderColor(string) = null

文本标签的边框颜色。

##${prefix} borderWidth(string) = 0

文本标签的边框宽度。

{{ use:partial-style-shadow(
    prefix='#' + ${prefix},
    defaultShadowBlur=3,
    defaultShadowColor='#aaa'
) }}


#${prefix} lineStyle(Object)

[axisPointer.type](~tooltip.axisPointer.type) 为 `'line'` 时有效。

{{ use: partial-line-style(prefix="#" + ${prefix}, defaultColor="#555", defaultWidth=1, defaultType='solid') }}

#${prefix} shadowStyle(Object)

[axisPointer.type](~tooltip.axisPointer.type) 为 `'shadow'` 时有效。

{{ use: partial-area-style(prefix="#" + ${prefix}, defaultColor="'rgba(150,150,150,0.3)") }}








{{ target: partial-formatter-params-axisPointer }}

每项内容还包括轴的信息：

```js
{
    axisDim: 'x', // 'x', 'y', 'angle', 'radius', 'single'
    axisId: 'xxx',
    axisName: 'xxx',
    axisIndex: 3,
    axisValue: 121, // 当前 axisPointer 对应的 value。
    axisValueLabel: '文本'
}
```