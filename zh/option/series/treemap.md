
{{target: series-treemap}}

# series.treemap(Object)

[Treemap](https://en.wikipedia.org/wiki/Treemapping) 是一种常见的表达『层级数据』『树状数据』的可视化形式。它主要用面积的方式，便于突出展现出『树』的各层级中重要的节点。

**示例：**

~[700x580](${galleryViewPath}treemap-obama&edit=1&reset=1)


<br>
**视觉映射：**

treemap 首先是把数值映射到『面积』这种视觉元素上。

此外，也支持对数据的其他维度进行视觉映射，例如映射到颜色、颜色明暗度上。

{{ use: partial-treemap-visual-detial }}


<br>
**下钻（drill down）：**

`drill down` 功能即点击后才展示子层级。
设置了 [leafDepth](~series-treemap.leafDepth) 后，下钻（`drill down`）功能开启。

**如下是 drill down 的例子：**
~[800x500](${galleryViewPath}treemap-drill-down&edit=1&reset=1)


<br>
<br>
<br>
注：treemap 的配置项 和 ECharts 2 相比有一些变化，一些不太成熟的配置方式不再支持或不再兼容：

+ `center/size` 方式的定位不再支持，而是统一使用 `left/top/bottom/right/width/height` 方式定位。

+ `breadcrumb` 的配置被移动到了 `itemStyle/itemStyle.emphasis` 外部，和 `itemStyle` 平级。

+ `root` 的设置暂时不支持。目前可以使用 `zoom` 的方式来查看树更下层次的细节，或者使用 [leafDepth](~series-treemap.leafDepth) 开启 "drill down" 功能。

+ `label` 的配置被移动到了 `itemStyle/itemStyle.emphasis` 外部，和 `itemStyle` 平级。

+ `itemStyle.childBorderWidth`、`itemStyle.childBorderColor`不再支持（因为这个配置方式只能定义两层的treemap）。统一使用 [series-treemap.levels](~series-treemap.levels) 来进行各层级的定义。

<br>
<br>

## type(string) = 'treemap'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}

{{ use: partial-rect-layout-width-height(
    componentName='treemap ',
    defaultLeft: 'center',
    defaultRight: null,
    defaultTop: 'middle',
    defaultBottom: null,
    defaultWidth: '80%',
    defaultHeight: '80%'
) }}

## squareRatio(number)

期望矩形长宽比率。布局计算时会尽量向这个比率靠近。

默认为黄金比：`0.5 * (1 + Math.sqrt(5))`。


## leafDepth(number) = null

设置了 `leafDepth` 后，下钻（`drill down`）功能开启。`drill down` 功能即点击后才展示子层级。

`leafDepth` 表示『展示几层』，层次更深的节点则被隐藏起来。点击则可下钻看到层次更深的节点。

例如，`leafDepth` 设置为 `1`，表示展示一层节点。

默认没有开启 `drill down`（即 `leafDepth` 为 `null` 或 `undefined`）。

**drill down 的例子：**
~[800x500](${galleryViewPath}treemap-drill-down&edit=1&reset=1)

## drillDownIcon(string) = '▶'

当节点可以下钻时的提示符。只能是字符。

## roam(boolean|string) = true

是否开启拖拽漫游（移动和缩放）。可取值有：

+ `false`：关闭。
+ `'scale'` 或 `'zoom'`：只能够缩放。
+ `'move'` 或 `'pan'`：只能够平移。
+ `true`：缩放和平移均可。


## nodeClick(boolean|string) = 'zoomToNode'

点击节点后的行为。可取值为：

+ `false`：节点点击无反应。
+ `'zoomToNode'`：点击节点后缩放到节点。
+ `'link'`：如果节点数据中有 [link](~series-treemap.data.link) 点击节点后会进行超链接跳转。



## zoomToNodeRatio(number) = 0.32*0.32

点击某个节点，会自动放大那个节点到合适的比例（节点占可视区域的面积比例），这个配置项就是这个比例。


## levels(Array) = []

**多层配置**

treemap 中采用『三级配置』：

```
『每个节点』->『每个层级』->『每个系列』。
```

即我们可以对每个节点进行配置，也可以对树的每个层级进行配置，也可以 series 上设置全局配置。节点上的设置，优先级最高。

最常用的是『每个层级进行配置』，`levels` 配置项就是每个层级的配置。例如：

```javascript
// Notice that in fact the data structure is not "tree", but is "forest".
// 注意，这个数据结构实际不是『树』而是『森林』
data: [
    {
        name: 'nodeA',
        children: [
            {name: 'nodeAA'},
            {name: 'nodeAB'},
        ]
    },
    {
        name: 'nodeB',
        children: [
            {name: 'nodeBA'}
        ]
    }
],
levels: [
    {...}, // 『森林』的顶层配置。即含有 'nodeA', 'nodeB' 的这层。
    {...}, // 下一层配置，即含有 'nodeAA', 'nodeAB', 'nodeBA' 的这层。
    {...}, // 再下一层配置。
    ...
]
```

<br>
**视觉映射的规则**

treemap中首要关注的是如何在视觉上较好得区分『不同层级』、『同层级中不同类别』。这需要合理得设置不同层级的『矩形颜色』、『边界粗细』、『边界颜色』甚至『矩形颜色饱和度』等。

参见这个[例子](${galleryEditorPath}treemap-disk&edit=1&reset=1)，最顶层级用颜色区分，分成了『红』『绿』『蓝』等大块。每个颜色块中是下一个层级，使用颜色的饱和度来区分（参见 `colorSaturation`）。最外层的矩形边界是『白色』，下层级的矩形边界是当前区块颜色加上饱和度处理（参见 `borderColorSaturation`）。

`treemap` 是通过这样的规则来支持这种配置的：每个层级计算用户配置的 `color`、`colorSaturation`、`borderColor`、`borderColorSaturation`等视觉信息（在levels中配置）。如果子节点没有配置，则继承父的配置，否则使用自己的配置）。

这样，可以做到：父层级配置 `color` 列表，子层级配置 `colorSaturation`。父层级的每个节点会从 `color` 列表中得到一个颜色，子层级的节点会从 `colorSaturation` 中得到一个值，并且继承父节点得到的颜色，合成得到自己的最终颜色。


<br>
**维度与『额外的视觉映射』**

例子：每一个 `value` 字段是一个 Array，其中每个项对应一个维度（dimension）。

```javascript
[
    {
        value: [434, 6969, 8382],
        children: [
            {
                value: [1212, 4943, 5453],
                id: 'someid-1',
                name: 'description of this node',
                children: [...]
            },
            {
                value: [4545, 192, 439],
                id: 'someid-2',
                name: 'description of this node',
                children: [...]
            },
            ...
        ]
    },
    {
        value: [23, 59, 12],
        children: [...]
    },
    ...
]
```

treemap 默认把第一个维度（Array 第一项）映射到『面积』上。而如果想表达更多信息，用户可以把其他的某一个维度（[series-treemap.visualDimension](~series-treemap.viusalDimension)），映射到其他的『视觉元素』上，比如颜色明暗等。参见[例子](${galleryEditorPath}treemap-obama&edit=1&reset=1)中，legend选择 `Growth`时的状态。

<br>
{{ use: partial-treemap-borderColor-setting(galleryEditorPath=${galleryEditorPath}) }}


<br>
**borderWidth, gapWidth, borderColor 的解释**

![500xauto](~treemap-border-gap.png)


{{use: partial-treemap-level-props(
    prefix="##",
    galleryEditorPath=${galleryEditorPath},
    galleryViewPath=${galleryViewPath}
)}}



{{use: partial-treemap-level-props(
    prefix="#",
    galleryEditorPath=${galleryEditorPath},
    galleryViewPath=${galleryViewPath}
)}}


## breadcrumb(Object)

面包屑，能够显示当前节点的路径。


### show(boolean) = true

是否显示面包屑。


{{ use: partial-rect-layout(
    componentName="asdf ",
    prefix="##",
    noZ=true,
    defaultLeft="'center'",
    defaultBottom=0
) }}


### height(number) = 22

面包屑的高度。


### emptyItemWidth(number) = 25

当面包屑没有内容时候，设个最小宽度。


### itemStyle(Object)

{{ use: partial-item-style-desc }}


{{use: partial-item-style(
    prefix="###",
    name="boxplot",
    defaultColor="rgba(0,0,0,0.7)",
    defaultBorderColor="rgba(255,255,255,0.7)",
    defaultBorderWidth=1,
    defaultShadowColor='rgba(150,150,150,1)',
    defaultShadowBlur=3,
    defaultShadowOffsetX=0,
    defaultShadowOffsetY=0
)}}


##### textStyle(Object)

{{use: partial-text-style(
    prefix="#####",
    defaultColor="#fff"
)}}


### emphasis
#### itemStyle(Object)
{{use: partial-item-style(
    prefix="####",
    name="boxplot",
    defaultColor="rgba(0,0,0,0.7)",
    defaultBorderColor="rgba(255,255,255,0.7)",
    defaultBorderWidth=1,
    defaultShadowColor='rgba(150,150,150,1)',
    defaultShadowBlur=3,
    defaultShadowOffsetX=0,
    defaultShadowOffsetY=0
)}}
##### textStyle(Object)

{{use: partial-text-style(
    prefix="#####",
    defaultColor="#fff"
)}}


## data(Array)

[series-treemap.data](~series-treemap.data) 的数据格式是树状的，例如：

```javascript
[ // 注意，最外层是一个数组，而非从某个根节点开始。
    {
        value: 1212,
        children: [
            {
                value: 2323,    // value字段的值，对应到面积大小。
                                // 也可以是数组，如 [2323, 43, 55]，则数组第一项对应到面积大小。
                                // 数组其他项可以用于额外的视觉映射，详情参见 series-treemp.levels。
                id: 'someid-1', // id 不是必须设置的。
                                // 但是如果想使用 API 来改变某个节点，需要用 id 来定位。
                name: 'description of this node', // 显示在矩形中的描述文字。
                children: [...],
                label: {        // 此节点特殊的 label 定义（如果需要的话）。
                    ...         // label的格式参见 series-treemap.label。
                },
                itemStyle: {    // 此节点特殊的 itemStyle 定义（如果需要的话）。
                    ...         // label的格式参见 series-treemap.itemStyle。
                }
            },
            {
                value: 4545,
                id: 'someid-2',
                name: 'description of this node',
                children: [
                    {
                        value: 5656,
                        id: 'someid-3',
                        name: 'description of this node',
                        children: [...]
                    },
                    ...
                ]
            }
        ]
    },
    {
        value: [23, 59, 12]
        // 如果没有children，可以不写
    },
    ...
]
```

### value(number|Array)

每个树节点的值，对应到面积大小。可以是number，也可以是数组，如 `[2323, 43, 55]`，则数组第一项对应到面积大小。

### id(string)

每个树节点的id。id 不是必须设置的。但是如果想使用 API 来改变某个节点，需要用 id 来定位。

### name(string)

显示在矩形中的描述文字。


{{use: partial-treemap-level-props(
    prefix="##",
    galleryEditorPath=${galleryEditorPath},
    galleryViewPath=${galleryViewPath}
)}}

### link(string)

点击此节点可跳转的超链接。须 [series-treemap.nodeClick](~series-treemap.nodeClick) 值为 `'link'` 时才生效。

参见 [series-treemap.data.target](~series-treemap.data.target)。

### target(string) = 'blank'

意义同 `html` `<a>` 标签中的 `target`，参见 [series-treemap.data.link](~series-treemap.data.link)。可选值为：`'blank'` 或 `'self'`。

### children(Array)

子节点，递归定义，格式同 [series-treemap.data](~series-treemap.data)。

{{use: partial-tooltip-in-series-data(
    galleryViewPath=${galleryViewPath}
)}}


{{ use:partial-silent(
    prefix="#"
) }}


{{use: partial-animation-init(
    prefix="#",
    defaultAnimationEasing='quinticInOut',
    defaultAnimationDuration=1500,
    galleryEditorPath=${galleryEditorPath}
)}}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}






{{target: partial-treemap-level-props}}

#${prefix} visualDimension(number) = 0

`treemap` 中支持对数据其他维度进行视觉映射。

首先，treemap的数据格式（参见 [series-treemap.data](~series-treemap.data)）中，每个节点的 `value` 都可以是数组。数组每项是一个『维度』（dimension）。`visualDimension` 指定了额外的『视觉映射』使用的是数组的哪一项。默认为第 `0` 项。

{{ use: partial-treemap-visual-detial }}
{{use: partial-treemap-prop-location-desc(name="visualDimension")}}

#${prefix} visualMin(number) = null

当前层级的最小 value 值。如果不设置则自动统计。

手动指定 `visualMin`、`visualMax` ，即手动控制了 visual mapping 的值域（当 [colorMappingBy](~series-treemap.levels.colorMappingBy) 为 `'value'` 时有意义）。

#${prefix} visualMax(number) = null

当前层级的最大 value 值。如果不设置则自动统计。

手动指定 `visualMin`、`visualMax` ，即手动控制了 visual mapping 的值域（当 [colorMappingBy](~series-treemap.levels.colorMappingBy) 为 `'value'` 时有意义）。

{{ if: ${prefix} !== '#' }}
#${prefix} color(Array)

表示同一层级的节点的 颜色 选取列表（选择规则见 [colorMappingBy](~series-treemap.colorMappingBy)）。默认为空时，选取系统color列表。

{{ use: partial-treemap-visual-detial }}
{{use: partial-treemap-prop-location-desc(name="color")}}

{{ /if }}
#${prefix} colorAlpha(Array) = null

{{ if: ${prefix} !== '#' }}表示同一层级的节点的{{ else }}本系列默认的{{ /if }} 颜色透明度 选取范围。数值范围 0 ~ 1。

例如, `colorAlpha` 可以是 `[0.3, 1]`.

{{ use: partial-treemap-visual-detial }}
{{use: partial-treemap-prop-location-desc(name="colorAlpha")}}


#${prefix} colorSaturation(number) = null

{{ if: ${prefix} !== '#' }}表示同一层级的节点的{{ else }}本系列默认的{{ /if }} 颜色饱和度 选取范围。数值范围 0 ~ 1。

例如, `colorSaturation` 可以是 `[0.3, 1]`.

{{ use: partial-treemap-visual-detial }}
{{use: partial-treemap-prop-location-desc(name="colorSaturation")}}


#${prefix} colorMappingBy(string) = 'index'

表示同一层级节点，在颜色列表中（参见 `color` 属性）选择时，按照什么来选择。

**可选：**

* `'value'`：将节点的值（即 [series-treemap.data.value](~series-treemap.data.value)）映射到颜色列表中。

这样得到的颜色，反应了节点值的大小。

可以使用 [visualDimension](~series-treemap.levels.visualDimension) 属性来设置，用 [data](~series-treemap.data) 中哪个纬度的值来映射。

* `'index'`：将节点的 `index`（序号）映射到颜色列表中。即同一层级中，第一个节点取颜色列表中第一个颜色，第二个节点取第二个。

这样得到的颜色，便于区分相邻节点。

* `'id'`：将节点的 `id`（即 [series-treemap.data.id](~series-treemap.data.id)）映射到颜色列表中。`id` 是用户指定的，这样能够使得，在treemap 通过 setOption 变化数值时，同一 `id` 映射到同一颜色，保持一致性。参见 [例子](${galleryEditorPath}treemap-obama&edit=1&reset=1)。

{{ use: partial-treemap-visual-detial }}
{{use: partial-treemap-prop-location-desc(name="colorMappingBy")}}


#${prefix} visibleMin(number) = 10

如果某个节点的矩形的面积，小于这个数值（单位：px 平方），这个节点就不显示。

如果不加这个限制，很小的节点会影响显示效果。

{{ use: partial-treemap-visual-detial }}
{{use: partial-treemap-prop-location-desc(name="visibleMin")}}


#${prefix} childrenVisibleMin(number) = null

如果某个节点的矩形面积，小于这个数值（单位：px 平方），则不显示这个节点的子节点。

这能够在矩形面积不足够大时候，隐藏节点的细节。当用户用鼠标缩放节点时，如果面积大于此阈值，又会显示子节点。

{{ use: partial-treemap-visual-detial }}
{{use: partial-treemap-prop-location-desc(name="childrenVisibleMin")}}


#${prefix} label(Object)

`label` 描述了每个矩形中，文本标签的样式。

{{use: partial-treemap-prop-location-desc(name="label")}}

<br>

{{use:partial-label(
    prefix=${prefix} + "#",
    defaultPosition="'inside'",
    formatter=true,
    ellipsis=true
)}}

#${prefix} upperLabel(Object)

`upperLabel` 用于显示矩形的父节点的标签。当 [upperLabel.show](~series-treemap.upperLabel.show) 为 `true` 的时候，『显示父节点标签』功能开启。

同 [series-treemap.label](~series-treemap.label) 一样，`upperLabel` 可以存在于 [series-treemap](~series-treemap) 的根节点，或者 [series-treemap.level](~series-treemap.level) 中，或者 [series-treemap.data](~series-treemap.data) 的每个数据项中。

[series-treemap.label](~series-treemap.label) 描述的是，当前节点为叶节点时标签的样式；`upperLabel` 描述的是，当前节点为非叶节点（即含有子节点）时标签的样式，（此时标签一般会被显示在节点的最上部）。

**例如：**

~[700x500](${galleryViewPath}treemap-show-parent&edit=1&reset=1)


{{use: partial-treemap-prop-location-desc(name="label")}}

<br>

{{use:partial-label(
    prefix=${prefix} + "#",
    defaultPosition="'inside'",
    formatter=true,
    ellipsis=true
)}}

###${prefix} height(number) = 20

父节点标签区的高度。

#${prefix} itemStyle(Object)

{{use: partial-treemap-prop-location-desc(name="itemStyle")}}

<br>

{{use: partial-treemap-item-style(
    prefix=${prefix} + "#",
    galleryEditorPath=${galleryEditorPath},
    itemStyleType='normal'
)}}

#${prefix} emphasis(Object)
##${prefix} label(Object)
{{use:partial-label(
    prefix=${prefix} + "##",
    defaultPosition="'inside'",
    formatter=true,
    ellipsis=true
)}}
##${prefix} upperLabel(Object)
{{use:partial-label(
    prefix=${prefix} + "##",
    defaultPosition="'inside'",
    formatter=true,
    ellipsis=true
)}}
##${prefix} itemStyle(Object)
{{use: partial-treemap-item-style(
    prefix=${prefix} + "##",
    galleryEditorPath=${galleryEditorPath},
    itemStyleType='emphasis'
)}}






{{target: partial-treemap-prop-location-desc}}
<br>
> 注：treemap中 `${name}` 属性可能在多处地方存在：

{{ if: ${name} !== 'color' }}
> * 可以存在于 [sereis-treemap](~series-treemap) 根下，表示本系列全局的统一设置。

{{ /if }}
> * 可以存在于 [series-treemap.levels](~series-treemap.levels) 的每个数组元素中，表示树每个层级的统一设置。

> * 存在于 [series-treemap.data](~series-treemap.data) 的每个节点中，表示每个节点的特定设置。





{{target: partial-treemap-visual-detial}}

关于视觉设置，详见 [series-treemap.levels](~series-treemap.levels)。






{{target: partial-treemap-item-style}}

#${prefix} color(Color) =  null

矩形的颜色。默认从全局调色盘 [option.color](~color) 获取颜色。

{{if: ${itemStyleType} === 'normal' }}

#${prefix} colorAlpha(number) = null

矩形颜色的透明度。取值范围是 0 ~ 1 之间的浮点数。


#${prefix} colorSaturation(number) = null

矩形颜色的饱和度。取值范围是 0 ~ 1 之间的浮点数。


#${prefix} borderWidth(number) = 0

矩形边框线宽。为 0 时无边框。而矩形的内部子矩形（子节点）的间隔距离是由 [gapWidth](~series-treemap.levels.gapWidth) 指定的。


#${prefix} gapWidth(number) = 0

矩形内部子矩形（子节点）的间隔距离。

![700xauto](~treemap-border-gap.png)


#${prefix} borderColor(Color) = '#fff',

矩形边框 和 矩形间隔（gap）的颜色。


#${prefix} borderColorSaturation(Color) = null

矩形边框的颜色的饱和度。取值范围是 0 ~ 1 之间的浮点数。

**例如：**

如果设置此属性，则 `borderColor` 的设置无效，而是：取当前节点计算出的颜色（比如从父节点遗传而来），在此颜色值上设置 `borderColorSaturation` 得到最终颜色。这种方式，能够做出『不同区块有不同色调的矩形间隔线』的效果，能够便于区分层级。

<br>
{{ use: partial-treemap-borderColor-setting(galleryEditorPath=${galleryEditorPath}) }}

#${prefix} strokeColor(Color) = null

每个矩形的描边颜色。

#${prefix} strokeWidth(number) = null

每个矩形的描边宽度。

{{/if }}







{{ target: partial-treemap-borderColor-setting }}
**矩形边框（border）/缝隙（gap）设置如何避免混淆**

如果统一用一种颜色设置矩形的缝隙（gap），那么当不同层级的矩形同时展示时可能会出现混淆。

参见 [例子](${galleryEditorPath}doc-example/treemap-borderColor&edit=1&reset=1)，**注意：**其中红色的区块中的子矩形其实是更深层级，和其他用白色缝隙区分的矩形不是在一个层级。所以，红色区块中矩形的分割线的颜色，我们在 `borderColorSaturation` 中设置为『加了饱和度变化的红颜色』，以示区别。


