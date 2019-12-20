{{target:series-line}}

# series.line(Object)

**折线/面积图**

折线图是用折线将各个数据点[标志](~series-line.symbol)连接起来的图表，用于展现数据的变化趋势。可用于[直角坐标系](~grid)和[极坐标系](~polar)上。

**Tip:** 设置 [areaStyle](~series-line.areaStyle) 后可以绘制面积图。

**Tip:** 配合分段型 [visualMap](~visualMap-piecewise) 组件可以将折线/面积图通过不同颜色分区间。如下示例

~[600x400](${galleryViewPath}line-aqi&edit=1&reset=1)

## type(string) = 'line'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}

{{ use: partial-coord-sys(
    seriesType="bar",
    coordSysDefault="'cartesian2d'",
    cartesian2d=true,
    polar=true,
    geo=false
) }}

{{ use:partial-symbol(
    seriesType="line",
    defaultSymbol="'emptyCircle'",
    defaultSymbolSize=4,
    prefix="#",
    hasCallback=true
) }}

## showSymbol(boolean) = true
是否显示 symbol, 如果 `false` 则只有在 tooltip hover 的时候显示。

## showAllSymbol(boolean) = 'auto'
只在主轴为类目轴（`axis.type` 为 `'category'`）时有效。

**可选：**
+ `'auto'`：默认，如果有足够空间则显示标志图形，否则随主轴标签间隔隐藏策略。
+ `true`：显示所有图形。
+ `false`：随主轴标签间隔隐藏策略。

## hoverAnimation(boolean) = true
是否开启 hover 在拐点标志上的提示动画效果。

{{ use: partial-legend-hover-link }}

## stack(string) = null
数据堆叠，同个类目轴上系列配置相同的`stack`值后，后一个系列的值会在前一个系列的值上相加。

下面示例可以通过右上角 [toolbox](~toolbox) 中的堆叠切换看效果：

~[600x400](${galleryViewPath}doc-example/line-stack-tiled&edit=1&reset=1)

{{ use: partial-cursor }}

## connectNulls(boolean) = false
是否连接空数据。

{{use:partial-clip(
    prefix="#"
) }}

## step(string|boolean) = false

是否是阶梯线图。可以设置为 `true` 显示成阶梯线图，也支持设置成 `'start'`, `'middle'`, `'end'` 分别配置在当前点，当前点与下个点的中间点，下个点拐弯。

不同的配置效果如下：

~[600x400](${galleryViewPath}line-step&edit=1&reset=1)


## label(Object)
{{use: partial-label-desc}}
{{use: partial-label(
    prefix="##",
    defaultPosition="'top'",
    formatter=true
)}}

## itemStyle(Object)
折线拐点标志的样式。
{{use: partial-item-style(
    prefix="##",
    useColorPalatte=true,
    hasCallback=true
)}}

## lineStyle(Object)
线条样式。

**注：** 修改 `lineStyle` 中的颜色不会影响图例颜色，如果需要图例颜色和折线图颜色一致，需修改 [itemStyle.color](~series-line.itemStyle.color)，线条颜色默认也会取该颜色。

{{use:partial-line-style(
    prefix="##",
    defaultWidth=2
)}}

## areaStyle(Object)
区域填充样式。
{{use: partial-area-style(prefix="##", hasOrigin=true)}}

## emphasis(Object)
图形的高亮样式。

### label(Object)
{{use: partial-label(
    prefix="###",
    formatter=true
)}}
### itemStyle(Object)
{{use: partial-item-style(prefix="###")}}


## smooth(boolean|number) = false
是否平滑曲线显示。

如果是 `boolean` 类型，则表示是否开启平滑处理。如果是 `number` 类型（取值范围 0 到 1），表示平滑程度，越小表示越接近折线段，反之则反。设为 `true` 时相当于设为 `0.5`。

如果需要修改平滑算法，请参考 [smoothMonotone](~series-line.smoothMonotone)。

## smoothMonotone(string)

折线平滑后是否在一个维度上保持单调性，可以设置成`'x'`, `'y'`来指明是在 x 轴或者 y 轴上保持单调性。

通常在双数值轴上使用。

下面两张图分别是双数值轴中的折线图`smoothMonotone`不设置以及设置为`'x'`的区别。

+ 不设置`smoothMonotone`:

![300xauto](~smooth-monotone-none.png)

+ 设置为 `'x'`:

![300xauto](~smooth-monotone-x.png)

## sampling(string)

折线图在数据量远大于像素点时候的降采样策略，开启后可以有效的优化图表的绘制效率，默认关闭，也就是全部绘制不过滤数据点。

**可选：**
+ `'average'`：取过滤点的平均值。
+ `'max'`：取过滤点的最大值。
+ `'min'`：取过滤点的最小值。
+ `'sum'`：取过滤点的和。


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
) }}

### name(string)
数据项名称。

### value(number)
单个数据项的数值。

{{ use:partial-symbol(
    defaultSymbol="'circle'",
    defaultSymbolSize=4,
    prefix="##",
    name="单个数据"
) }}

### label(Object)
单个拐点文本的样式设置。
{{ use: partial-label(
    prefix="###",
    defaultPosition="top"
) }}

### itemStyle(Object)
单个拐点标志的样式设置。
{{use: partial-item-style(prefix="###")}}


### emphasis(Object)
单个拐点的高亮样式和标签设置。
#### itemStyle(Object)
{{use: partial-item-style(prefix="####")}}
#### label(Object)
{{ use: partial-label(prefix="####") }}


{{use: partial-tooltip-in-series-data(
    galleryViewPath=${galleryViewPath}
)}}


{{use: partial-marker(
    prefix="#",
    seriesType="line",
    galleryEditorPath=${galleryEditorPath},
    hasCoord=true,
    hasType=true
)}}

{{use:partial-z-zlevel(
    prefix="#",
    componentName="折线图"
) }}

{{ use:partial-silent(
    prefix="#"
) }}

{{use: partial-animation(
    prefix="#",
    defaultAnimationEasing='linear',
    galleryEditorPath=${galleryEditorPath}
)}}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}
