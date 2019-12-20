
{{target: series-sankey}}

# series.sankey(Object)

** 桑基图 **

是一种特殊的流图（可以看作是有向无环图）。 它主要用来表示原材料、能量等如何从最初形式经过中间过程的加工或转化达到最终状态。

**例如：**

~[700x580](${galleryViewPath}sankey-energy&edit=1&reset=1)

<br>
**可视编码：**

桑基图将原数据中的每个 `node` 编码成一个小矩形，不同的节点尽量用不同的颜色展示，小矩形旁边的 `label` 编码的是节点的名称。

此外，图中每两个小矩形之间的边编码的是原数据中的 `link`，边的粗细编码的是 `link` 中的 `value`。

<br>

**排序：**
如果想指定结果的纵向顺序，那么可以把 [layoutIterations](~series-sankey.layoutIterations) 设为 `0`，此时纵向的顺序依照数据在 [links](~series-sankey.links) 中出现的顺序。

## type(string) = 'sankey'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-rect-layout-width-height(
    componentName='sankey',
    defaultLeft: '5%',
    defaultRight: '20%',
    defaultTop: '5%',
    defaultBottom: '5%',
    defaultWidth: 'null',
    defaultHeight: 'null'
) }}

## nodeWidth(number) = 20

桑基图中每个矩形节点的宽度。

## nodeGap(number) = 8

桑基图中每一列任意两个矩形节点之间的间隔。

## nodeAlign(string) = 'justify'

桑基图中节点的对齐方式，默认是双端对齐，可以设置为左对齐或右对齐，对应的值分别是：

+ `justify`: 节点双端对齐。
+ `left`: 节点左对齐。
+ `right`: 节点右对齐。

## layoutIterations(number) = 32

布局的迭代次数，用来不断优化图中节点的位置，以减少节点和边之间的相互遮盖。

默认布局迭代次数：`32`。

经测试，布局迭代次数不要低于默认值。

## orient(string) = 'horizontal'

桑基图中节点的布局方向，可以是水平的从左往右，也可以是垂直的从上往下，对应的参数值分别是 `horizontal`, `vertical`。

## draggable(boolean) = true

控制节点拖拽的交互，默认开启。开启后，用户可以将图中任意节点拖拽到任意位置。若想关闭此交互，只需将值设为 `false` 就行了。

## focusNodeAdjacency(boolean|string) = false

鼠标 hover 到节点或边上，相邻接的节点和边高亮的交互，默认关闭，可手动开启。

**可选：**

+ `false`：hover 到节点或边时，只有被 hover 的节点或边高亮。
+ `true`：同 `'allEdges'`。
+ `'allEdges'`：hover 到节点时，与节点邻接的所有边以及边对应的节点全部高亮。hover 到边时，边和相邻节点高亮。
+ `'outEdges'`：hover 的节点、节点的出边、出边邻接的另一节点 会被高亮。hover 到边时，边和相邻节点高亮。
+ `'inEdges'`：hover 的节点、节点的入边、入边邻接的另一节点 会被高亮。hover 到边时，边和相邻节点高亮。

## levels(Array)

桑基图每一层的设置。可以逐层设置。

**例如：**

```js
levels: [{
    depth: 0,
    itemStyle: {
        color: '#fbb4ae'
    },
    lineStyle: {
        color: 'source',
        opacity: 0.6
    }
}, {
    depth: 1,
    itemStyle: {
        color: '#b3cde3'
    },
    lineStyle: {
        color: 'source',
        opacity: 0.6
    }
}]
```

也可以只设置某一层：

```js
levels: [{
    depth: 3,
    itemStyle: {
        color: '#fbb4ae'
    },
    lineStyle: {
        color: 'source',
        opacity: 0.6
    }
}]
```

### depth(number)

指定设置的是桑基图哪一层，取值从 0 开始。

### itemStyle(Object)

桑基图指定层节点的样式。

{{use:partial-item-style(prefix="###", useColorPalatte=true)}}

### lineStyle(Object)

桑基图指定层出边的样式。其中 [lineStyle.color](~series-sankey.lineStyle.color) 支持设置为 `'source'` 或者 `'target'` 特殊值，此时出边会自动取源节点或目标节点的颜色作为自己的颜色。

{{use: partial-sankey-line-style(prefix="###")}}


## label(Object)

`label` 描述了每个矩形节点中文本标签的样式。

{{use:partial-label(
    prefix="##",
    defaultShowLabel=true,
    defaultPosition="'right'",
    formatter1d=true
)}}

## itemStyle(Object)

桑基图节点矩形的样式。

{{use: partial-item-style(
    prefix="##",
    useColorPalatte=true,
    defaultBorderWidth=1,
    defaultBorderColor="'#aaa'"
)}}

## lineStyle(Object)

桑基图边的样式，其中 [lineStyle.color](~series-sankey.lineStyle.color) 支持设置为 `'source'` 或者 `'target'` 特殊值，此时边会自动取源节点或目标节点的颜色作为自己的颜色。

{{use: partial-sankey-line-style(prefix="##")}}

## emphasis(Object)

桑基图的高亮样式设置。

### label(Object)

{{use:partial-label(
    prefix="###",
    formatter1d=true
)}}

### itemStyle(Object)

{{use: partial-item-style(prefix="###")}}

### lineStyle(Object)

{{use: partial-sankey-line-style(
    prefix="###"
)}}

## data(Array)

桑基图节点数据列表。

```js
data: [{
    name: 'node1',
    // This attribute decides the layer of the current node.
    depth: 0
}, {
    name: 'node2',
    depth: 1
}]
```

**注意:** 节点的 `name` 不能重复。

### name(string)

节点的名称。

### depth(number)

节点所在的层，取值从 0 开始。

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

同 [data](~series-sankey.data)

## links(Array)

节点间的边。**注意:** 桑基图理论上只支持有向无环图（DAG, Directed Acyclic Graph），所以请确保输入的边是无环的.

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

### source(string)

边的[源节点名称](~series-sankey.data.name)

### target(string)

边的[目标节点名称](~series-sankey.data.name)

### value(number)

边的数值，决定边的宽度。

### lineStyle(Object)

关系边的线条样式。
{{use:partial-sankey-line-style(
    prefix="###"
)}}

### emphasis(Object)

#### lineStyle(Object)

{{ use:partial-sankey-line-style(
    prefix="####"
) }}

## edges(Array)

同 [links](~series-sankey.links)

{{ use:partial-silent(
    prefix="#"
) }}

{{use: partial-animation(
    prefix="#",
    defaultAnimationEasing="'linear'",
    defaultAnimationDuration=1000,
    galleryEditorPath=${galleryEditorPath}
)}}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}



{{target: partial-sankey-line-style}}

#${prefix} color(Color) = "'#314656'"

桑基图边的颜色。

#${prefix} opacity(number) = 0.2

桑基图边的透明度。

#${prefix} curveness(number) = 0.5

桑基图边的曲度。

{{use: partial-style-shadow(prefix=${prefix})}}
