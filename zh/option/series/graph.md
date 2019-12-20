{{target: series-graph}}
# series.graph(Object)

**关系图**

用于展现节点以及节点之间的关系数据。

**注意：** ECharts 2.x 中 `force` 类型的图表不再在 ECharts 3 中提供支持，转为统一使用 `graph` 去展现关系数据。如果要使用力引导布局，可以将 [layout](~series-graph.layout) 配置项设为`'force'`。

 **例如：** 

~[600x400](${galleryViewPath}graph&reset=1&edit=1)

## type(string) = 'graph'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}

{{ use: partial-legend-hover-link() }}

{{ use: partial-coord-sys(
    seriesType="graph",
    coordSysDefault="null",
    none=true,
    cartesian2d=true,
    polar=true,
    geo=true,
    calendar=true
) }}

## hoverAnimation(boolean)
是否开启鼠标 hover 节点的提示动画效果。

## layout(string) = 'none'
图的布局。

**可选：**
+ `'none'` 不采用任何布局，使用[节点](~series-graph.data)中提供的 [x](~series-graph.data.x)， [y](~series-graph.data.y) 作为节点的位置。

+ `'circular'` 采用环形布局，见示例 [Les Miserables](${galleryEditorPath}graph-circular-layout)，布局相关的配置项见 [graph.circular](~series-graph.circular)

+ `'force'` 采用力引导布局，见示例 [Force](${galleryEditorPath}graph-force)，布局相关的配置项见 [graph.force](~series-graph.force)

## circular(Object)
环形布局相关配置

### rotateLabel(boolean) = false
是否旋转标签，默认不旋转

## force(Object)
力引导布局相关的配置项，力引导布局是模拟弹簧电荷模型在每两个节点之间添加一个斥力，每条边的两个节点之间添加一个引力，每次迭代节点会在各个斥力和引力的作用下移动位置，多次迭代后节点会静止在一个受力平衡的位置，达到整个模型的能量最小化。

力引导布局的结果有良好的对称性和局部聚合性，也比较美观。

### initLayout(string)
进行力引导布局前的初始化布局，初始化布局会影响到力引导的效果。

默认不进行任何布局，使用[节点](~series-graph.data)中提供的 [x](~series-graph.data.x)， [y](~series-graph.data.y) 作为节点的位置。如果不存在的话会随机生成一个位置。

也可以选择使用环形布局 `'circular'`。

### repulsion(Array|number) = 50
节点之间的斥力因子。

支持设置成数组表达斥力的范围，此时不同大小的值会线性映射到不同的斥力。值越大则斥力越大

### gravity(number) = 0.1
节点受到的向中心的引力因子。该值越大节点越往中心点靠拢。

### edgeLength(Array|number) = 30
边的两个节点之间的距离，这个距离也会受 [repulsion](~series-graph.force.repulsion)。

支持设置成数组表达边长的范围，此时不同大小的值会线性映射到不同的长度。值越小则长度越长。

 **例如：** 

```js
// 值最大的边长度会趋向于 10，值最小的边长度会趋向于 50
edgeLength: [10, 50]
```

### layoutAnimation(boolean) = true
因为力引导布局会在多次迭代后才会稳定，这个参数决定是否显示布局的迭代动画，在浏览器端节点数据较多（>100）的时候不建议关闭，布局过程会造成浏览器假死。

## roam(boolean|string) = false
{{ use: partial-roam }}

## nodeScaleRatio(number) = 0.6
鼠标漫游缩放时节点的相应缩放比例，当设为`0`时节点不随着鼠标的缩放而缩放

## draggable(boolean) = false
节点是否可拖拽，只在使用力引导布局的时候有用。

## focusNodeAdjacency(boolean) = false
是否在鼠标移到节点上的时候突出显示节点以及节点的边和邻接节点。

{{ use: partial-symbol(
    prefix='#',
    defaultSymbol="'circle'",
    defaultSymbolSize=10,
    name='关系图节点',
    hasCallback=true
) }}

## edgeSymbol(Array|string) = ['none', 'none']
边两端的标记类型，可以是一个数组分别指定两端，也可以是单个统一指定。默认不显示标记，常见的可以设置为箭头，如下：

```js
edgeSymbol: ['circle', 'arrow']
```

## edgeSymbolSize(Array|number) = 10
边两端的标记大小，可以是一个数组分别指定两端，也可以是单个统一指定。

{{ use: partial-cursor }}

## itemStyle(Object)
{{use:partial-item-style-desc}}
{{use:partial-item-style(
    prefix="##",
    useColorPalatte=true,
    hasCallback=true
)}}

## lineStyle(Object)
关系边的公用线条样式。其中 [lineStyle.color](~series-graph.lineStyle.color) 支持设置为`'source'`或者`'target'`特殊值，此时边会自动取源节点或目标节点的颜色作为自己的颜色。

{{use:partial-line-style(
    prefix="##",
    defaultColor="'#aaa'",
    defaultWidth=1,
    defaultOpacity=0.5,
    hasCurveness=true
)}}


## label(Object)
{{use:partial-label-desc}}
{{use:partial-label(
    prefix="##",
    defaultPosition="'inside'",
    formatter2d=true
)}}

## edgeLabel(Object)
{{use: graph-edge-label(
    prefix="##"
)}}

## emphasis(Object)
高亮的图形样式。
### itemStyle(Object)
{{use:partial-item-style(prefix="###")}}
### lineStyle(Object)
{{ use:partial-line-style(
    prefix="###"
) }}
### label(Object)
{{use:partial-label(
    prefix="###",
    defaultShow=true,
    formatter2d=true
)}}
### edgeLabel(Object)
{{use: graph-edge-label(
    prefix="###"
)}}


## categories(Array)
节点分类的类目，可选。

如果节点有分类的话可以通过 [data[i].category](~series-graph.data.category) 指定每个节点的类目，类目的样式会被应用到节点样式上。[图例](~legend)也可以基于`categories`名字展现和筛选。

### name(string)
类目名称，用于和 [legend](~legend) 对应以及格式化 [tooltip](~tooltip) 的内容。

{{ use: partial-symbol(
    prefix='##',
    name='该类目节点'
) }}

### itemStyle(Object)
该类目节点的样式。
{{use:partial-item-style(prefix="###", useColorPalatte=true)}}

### label(Object)
该类目节点标签的样式。
{{ use:partial-label(
    prefix="###",
    defaultPosition="inside",
    formatter2d=true
) }}

### emphasis(Object)
#### itemStyle(Object)
{{use:partial-item-style(prefix="####")}}
#### label(Object)
{{ use:partial-label(prefix="####") }}


## data(Array)

关系图的节点数据列表。

 **例如：** 
```js
data: [{
    name: '1',
    x: 10,
    y: 10,
    value: 10
}, {
    name: '2',
    x: 100,
    y: 100,
    value: 20,
    symbolSize: 20,
    itemStyle: {
        color: 'red'
    }
}]
```

**注意:** 节点的`name`不能重复。

### name(string)
数据项名称。

### x(number)
节点的初始 x 值。在不指定的时候需要指明`layout`属性选择布局方式。
### y(number)
节点的初始 y 值。在不指定的时候需要指明`layout`属性选择布局方式。
### fixed(boolean)
节点在力引导布局中是否固定。

### value(number|Array)
数据项值。
### category(number)
数据项所在类目的 index。

{{ use: partial-symbol(
    prefix='##',
    name='该类目节点'
) }}

### itemStyle(Object)
该节点的样式。
{{use:partial-item-style(prefix="###", useColorPalatte=true)}}

### label(Object)
该节点标签的样式。
{{ use:partial-label(
    prefix="###"
) }}

### emphasis(Object)

#### itemStyle(Object)
{{use:partial-item-style(prefix="####")}}
#### label(Object)
{{ use:partial-label(
    prefix="####"
) }}


{{use: partial-tooltip-in-series-data(
    galleryViewPath=${galleryViewPath}
)}}


## nodes(Array)
别名，同 [data](~series-graph.data)

## links(Array)
节点间的关系数据。

 **例如：** 
```js
links: [{
    source: 'n1',
    target: 'n2'
}, {
    source: 'n2',
    target: 'n3'
}]
```
### source(string|number)
边的[源节点名称](~series-graph.data.name)的字符串，也支持使用数字表示源节点的索引。
### target(string|number)
边的[目标节点名称](~series-graph.data.name)的字符串，也支持使用数字表示源节点的索引。
### value(number)
边的数值，可以在力引导布局中用于映射到边的长度。

### lineStyle(Object)
关系边的线条样式。
{{use:partial-line-style(
    prefix="###"
)}}
#### curveness(number) = 0
边的曲度，支持从 0 到 1 的值，值越大曲度越大。

### label(Object)
{{use: graph-edge-label(
    prefix="###"
)}}

### emphasis(Object)
#### label(Object)
{{use: graph-edge-label(
    prefix="####"
)}}
#### lineStyle(Object)
{{use:partial-line-style(
    prefix="####"
)}}

### symbol(Array|string)
边两端的标记类型，可以是一个数组分别指定两端，也可以是单个统一指定。

### symbolSize(Array|string)
边两端的标记大小，可以是一个数组分别指定两端，也可以是单个统一指定。

## edges(Array)
别名，同 [links](~series-graph.links)

{{use: partial-marker(
    prefix="#",
    seriesType="graph",
    hasType=true,
    hasCoord=true
)}}


{{ use: partial-rect-layout-width-height(
    defaultLeft="'center'",
    defaultTop="'middle'",
    defaultWidth='自适应',
    defaultHeight='自适应'
) }}

{{ use:partial-silent(
    prefix="#"
) }}
{{ use: partial-animation(
    prefix="#",
    galleryEditorPath=${galleryEditorPath}
) }}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}


{{ target: graph-edge-label }}

#${prefix} show(boolean) = ${defaultShowLabel|default(false)}
是否显示标签。
#${prefix} position(string) = 'middle'
标签位置。

**可选：**
+ `'start'`：线的起始点。
+ `'middle'`：线的中点。
+ `'end'`：的结束点。
#${prefix} formatter(string|Function)
{{ use: partial-2d-data-label-formatter }}

{{ use: partial-text-style(prefix=${prefix}) }}