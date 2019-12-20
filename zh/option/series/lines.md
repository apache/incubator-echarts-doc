
{{target: series-lines}}

# series.lines(Object)

**线图**

用于带有起点和终点信息的线数据的绘制，主要用于地图上的航线，路线的可视化。

ECharts 2.x 里会用地图上的 `markLine` 去绘制迁徙效果，在 ECharts 3 里建议使用单独的 `lines` 类型图表。


## type(string) = 'lines'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}


{{ use: partial-coord-sys(
    seriesType="lines",
    coordSysDefault="'geo'",
    cartesian2d=true,
    polar=false,
    geo=true
) }}

## polyline(boolean) = false
是否是多段线。

默认为 `false`，只能用于绘制只有两个端点的线段，线段可以通过 [lineStyle.curveness](~series-lines.lineStyle.curveness) 配置为曲线。

如果该配置项为 `true`，则可以在 [data.coords](~series-lines.data.coords) 中设置多于 2 个的顶点用来绘制多段线，在绘制路线轨迹的时候比较有用，见示例 [北京公交路线](${galleryEditorPath}lines-bmap-bus)，设置为多段线后 [lineStyle.curveness](~series-lines.lineStyle.curveness) 无效。

## effect(Object)
线特效的配置，见示例 [模拟迁徙](${galleryEditorPath}geo-lines) 和 [北京公交路线](${galleryEditorPath}lines-bmap-effect)

**注意：** 所有带有尾迹特效的图表需要单独放在一个层，也就是需要单独设置 [zlevel](~series-lines.zlevel)，同时建议关闭该层的动画（[animation](~series-lines.animation): false）。不然位于同个层的其它系列的图形，和动画的[标签](~series-lines.label)也会产生不必要的残影。

### show(boolean) = false
是否显示特效。
### period(number) = 4
特效动画的时间，单位为 s。

### delay(number|Function)
特效动画的延时，支持设置成数字或者回调。单位`ms`

### constantSpeed(number) = 0
配置特效图形的移动动画是否是固定速度，单位`像素/秒`，设置为大于 0 的值后会忽略 [period](~series-lines.effect.period) 配置项。

### symbol(string) = 'circle'
特效图形的标记。
{{ use: partial-icon }}

上面示例中就是使用自定义 path 的 symbol 表现飞机的图形。

**Tip:** symbol 的角度会随着轨迹的切线变化，如果使用自定义 path 的 symbol，需要保证 path 图形的朝向是朝上的，这样在 symbol 沿着轨迹运动的时候可以保证图形始终朝着运动的方向。

### symbolSize(Array|number) = 3
特效标记的大小，可以设置成诸如 `10` 这样单一的数字，也可以用数组分开表示高和宽，例如 `[20, 10]` 表示标记宽为`20`，高为`10`。

### color(Color)
特效标记的颜色，默认取 [lineStyle.color](~series-lines.lineStyle.color)。

### trailLength(number) = 0.2
特效尾迹的长度。取从 0 到 1 的值，数值越大尾迹越长。

### loop(boolean) = true
是否循环显示特效。

## large(boolean) = false
是否启用大规模线图的优化，在数据图形特别多的时候（>=5k）可以开启。

开启后配合 [largeThreshold](~series-lines.largeThreshold) 在数据量大于指定阈值的时候对绘制进行优化。

缺点：优化后不能自定义设置单个数据项的样式，不能启用 [effect](~series-lines.effect)。

## largeThreshold(number) = 2000
开启绘制优化的阈值。

## symbol(string|Array) = 'none'
线两端的标记类型，可以是一个数组分别指定两端，也可以是单个统一指定。
具体支持的格式可以参考 [标线的 symbol](~series-line.markLine.data.0.symbol)

## symbolSize(number|Array) = 10
线两端的标记大小，可以是一个数组分别指定两端，也可以是单个统一指定。
**注意：** 这里无法像一般的 `symbolSize` 那样通过数组分别指定高宽。

## lineStyle(Object)
{{ use: partial-line-style(
    prefix= '##',
    useColorPalatte=true,
    defaultOpacity=0.5,
    hasCallback=true
) }}

### curveness(number) = 0
边的曲度，支持从 0 到 1 的值，值越大曲度越大。

## label(Object)
标签相关配置。在 [polyline](~series-lines.polyline) 设置为 `true` 时无效。
{{ use: lines-label(prefix="##")}}

## emphasis(Object)

高亮的线条和标签样式。

### lineStyle(Object)
{{ use: partial-line-style(
    prefix='###'
) }}
### label(Object)
{{ use: lines-label(prefix="###") }}



{{ use:partial-progressive(
    prefix='#'
) }}



## data(Array)
线数据集。

**注：** 为了更好点支持多段线的配置，线数据的格式在 3.2.0 做了一定调整，如下：
```js
// 3.2.0 之前
// [{
//    // 起点坐标
//    coord: [120, 66],
//    lineStyle: { }
// }, {
//    // 终点坐标
//    coord: [122, 67]
// }]

// 从 3.2.0 起改为如下配置
{
    coords: [
        [120, 66],  // 起点
        [122, 67]   // 终点
        ...         // 如果 polyline 为 true 还可以设置更多的点
    ],
    // 统一的样式设置
    lineStyle: {
    }
}
```

### name(string)
数据名称

### coords(Array)
一个包含两个到多个二维坐标的数组。在 [polyline](~series-lines.polyline) 设置为 `true` 时支持多于两个的坐标。

### lineStyle(Object)
单个数据（单条线）的样式设置。
{{ use: partial-line-style(
    prefix="###",
    hasCurveness=true
) }}

### label(Object)
单个数据（单条线）的标签设置。在 [polyline](~series-lines.polyline) 设置为 `true` 时无效。
{{ use: lines-label(
    prefix="###"
) }}

### emphasis(Object)
#### lineStyle(Object)
{{ use: partial-line-style(
    prefix="####",
    hasCurveness=true
) }}
#### label(Object)
{{ use: lines-label(
    prefix="####"
) }}


{{use: partial-marker(
    prefix="#",
    galleryEditorPath=${galleryEditorPath},
    seriesType="lines"
)}}

{{use:partial-clip(
    prefix="#"
) }}

{{use:partial-z-zlevel(
    prefix="#",
    componentName="线图"
) }}

{{ use:partial-silent(
    prefix="#"
) }}

{{ use: partial-animation(
    prefix="#",
    galleryEditorPath=${galleryEditorPath}
) }}


{{ target: lines-label }}
#${prefix} show(boolean) = ${defaultShowLabel|default(false)}
是否显示标签。
#${prefix} position(string) = 'end'
标签位置。

**可选：**
+ `'start'`：线的起始点。
+ `'middle'`：线的中点。
+ `'end'`：线的结束点。
#${prefix} formatter(string|Function)
{{ use: partial-2d-data-label-formatter }}

{{ use: partial-text-style(prefix=${prefix}) }}