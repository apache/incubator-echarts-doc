
{{target: component-grid}}

# grid(Object)

直角坐标系内绘图网格，单个 grid 内最多可以放置上下两个 X 轴，左右两个 Y 轴。可以在网格上绘制[折线图](~series-line)，[柱状图](~series-bar)，[散点图（气泡图）](~series-scatter)。

在 ECharts 2.x 里单个 ECharts 实例中最多只能存在一个 grid 组件，在 ECharts 3 中可以存在任意多个 grid 组件。

**例如：**下面这个 Anscombe Quartet 的示例

~[600x400](${galleryViewPath}scatter-anscombe-quartet&edit=1&reset=1)

{{use: partial-component-id(prefix="#")}}

## show(boolean) = false

是否显示 grid 区域。默认不显示。

{{ use: partial-rect-layout-width-height(
    componentName="grid ",
    defaultLeft="'10%'",
    defaultTop=60,
    defaultRight="'10%'",
    defaultBottom=60
) }}

## containLabel(boolean) = false

grid 区域是否包含坐标轴的[刻度标签](~yAxis.axisLabel)。

+ containLabel 为 `false` 的时候：
    + `grid.left` `grid.right` `grid.top` `grid.bottom` `grid.width` `grid.height` 决定了是由坐标轴形成的矩形的尺寸和位置。
    + 这比较适用于多个 `grid` 进行对齐的场景，因为经常多个 `grid` 对齐的时候，是依据坐标轴来对齐的。
    + containLabel 为 `true` 的时候：
    + `grid.left` `grid.right` `grid.top` `grid.bottom` `grid.width` `grid.height` 决定的是包括了坐标轴标签在内的所有内容所形成的矩形的位置。
    + 这常用于防止标签溢出的场景。标签溢出指的是标签长度动态变化时，可能会溢出容器或者覆盖其他组件。

{{ use:partial-component-common-style(componentName="网格", prefix='#', needShow=true) }}

{{use: partial-tooltip-in-coords(
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
)}}