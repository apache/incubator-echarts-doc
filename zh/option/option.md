{{target: option}}

{{import: component-title}}
{{import: component-legend}}
{{import: component-grid}}
{{import: component-x-axis}}
{{import: component-y-axis}}
{{import: component-polar}}
{{import: component-radius-axis}}
{{import: component-angle-axis}}
{{import: component-radar}}
{{import: component-data-zoom}}
{{import: component-visual-map}}
{{import: component-tooltip}}
{{import: component-axisPointer}}
{{import: component-toolbox}}
{{import: component-brush}}
{{import: component-geo}}
{{import: component-parallel}}
{{import: component-parallel-axis}}
{{import: component-single-axis}}
{{import: component-timeline}}
{{import: component-graphic}}
{{import: component-calendar}}
{{import: component-dataset}}
{{import: component-aria}}


{{import: series-line}}
{{import: series-bar}}
{{import: series-pie}}
{{import: series-scatter}}
{{import: series-effectScatter}}

{{import: series-radar}}
{{import: series-tree}}
{{import: series-treemap}}
{{import: series-sunburst}}
{{import: series-boxplot}}
{{import: series-candlestick}}
{{import: series-heatmap}}
{{import: series-map}}
{{import: series-parallel}}
{{import: series-lines}}
{{import: series-graph}}
{{import: series-sankey}}
{{import: series-funnel}}
{{import: series-gauge}}
{{import: series-pictorialBar}}
{{import: series-themeRiver}}
{{import: series-custom}}

# color(Array)

调色盘颜色列表。如果系列没有设置颜色，则会依次循环从该列表中取颜色作为系列颜色。

默认为：
```js
['#c23531','#2f4554', '#61a0a8', '#d48265', '#91c7ae','#749f83',  '#ca8622', '#bda29a','#6e7074', '#546570', '#c4ccd3']
```

# backgroundColor(Color) = 'transparent'
背景色，默认无背景。

{{ use: partial-color-desc() }}


# textStyle(Object)
全局的字体样式。
{{ use: partial-simple-text-style(
    prefix='#',
    defaultFontSize=12
) }}

{{import: partial-animation }}


# blendMode(string) = 'source-over'

图形的混合模式，不同的混合模式见 https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/globalCompositeOperation 。

默认为 `'source-over'`。 支持每个系列单独设置。

`'lighter'` 也是比较常见的一种混合模式，该模式下图形数量集中的区域会颜色叠加成高亮度的颜色（白色）。常常能起到突出该区域的效果。见示例 [全球飞行航线](${galleryEditorPath}lines-airline)

# hoverLayerThreshold(number) = 3000

图形数量阈值，决定是否开启单独的 hover 层，在整个图表的图形数量大于该阈值时开启单独的 hover 层。

单独的 hover 层主要是为了在高亮图形的时候不需要重绘整个图表，只需要把高亮的图形放入单独的一个 canvas 层进行绘制，防止在图形数量很多的时候因为高亮重绘所有图形导致卡顿。

ECharts 2 里是底层强制使用单独的层绘制高亮图形，但是会带来很多问题，比如高亮的图形可能会不正确的遮挡所有其它图形，还有图形有透明度因为高亮和正常图形叠加导致不正确的透明度显示，还有移动端上因为每个图表都要多一个 canvas 带来的额外内存开销。因此 3 里默认不会开启该优化，只有在图形数量特别多，有必要做该优化时才会自动开启。


# useUTC(boolean) = false

是否使用 UTC 时间。

+ `true`: 表示 `axis.type` 为 `'time'` 时，依据 UTC 时间确定 tick 位置，并且 `axisLabel` 和 `tooltip` 默认展示的是 UTC 时间。
+ `false`: 表示 `axis.type` 为 `'time'` 时，依据本地时间确定 tick 位置，并且 `axisLabel` 和 `tooltip` 默认展示的是本地时间。

默认取值为false，即使用本地时间。因为考虑到：

+ 很多情况下，需要展示为本地时间（无论服务器存储的是否为 `UTC` 时间）。
+ 如果 data 中的时间为 '2012-01-02' 这样的没有指定时区的时间表达式，往往意为本地时间。默认情况下，时间被展示时需要和输入一致而非有时差。

**注意:** 这个参数实际影响的是『展示』，而非用户输入的时间值的解析。
关于用户输入的时间值（例如 `1491339540396`, `'2013-01-04'` 等）的解析，参见 [date 中时间相关部分](~series-line.data)。
