
{{target: series-tree}}

# series.tree(Object)

**树图**

树图主要用来可视化树形数据结构，是一种特殊的层次类型，具有唯一的根节点，左子树，和右子树。

**注意：**目前不支持在单个 series 中直接绘制森林，可以通过在一个 option 中配置多个 series 实现。

**树图示例：**

~[900x780](${galleryViewPath}tree-vertical&edit=1&reset=1)

**多个 series 组合成森林示例：**

~[800x680](${galleryViewPath}tree-legend&edit=1&reset=1)

## type(string) = 'tree'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}

{{ use: partial-rect-layout-width-height(
    componentName='tree',
    defaultLeft: '12%',
    defaultRight: '12%',
    defaultTop: '12%',
    defaultBottom: '12%',
    defaultWidth: 'null',
    defaultHeight: 'null'
) }}

## layout(string) = 'orthogonal'

树图的布局，有 `正交` 和 `径向` 两种。这里的 `正交布局` 就是我们通常所说的 `水平` 和 `垂直` 方向，对应的参数取值为 `'orthogonal'` 。而 `径向布局` 是指以根节点为圆心，每一层节点为环，一层层向外发散绘制而成的布局，对应的参数取值为 `'radial'` 。

**正交布局示例：**

~[780x900](${galleryViewPath}tree-basic&edit=1&reset=1)


**径向布局示例：**

~[800x800](${galleryViewPath}tree-radial&edit=1&reset=1)


## orient(string) = 'LR'

树图中 `正交布局` 的方向，也就是说只有在 `layout = 'orthogonal'` 的时候，该配置项才生效。对应有 `水平` 方向的 `从左到右`，`从右到左`；以及垂直方向的 `从上到下`，`从下到上`。取值分别为 `'LR'` , `'RL'`, `'TB'`, `'BT'`。

**注意**，之前的配置项值 `'horizontal'` 等同于 `'LR'`， `'vertical'` 等同于 `'TB'`。


{{ use:partial-symbol(
    seriesType="tree",
    defaultSymbol="'emptyCircle'",
    defaultSymbolSize=7,
    prefix="#",
    hasCallback=true
) }}


## roam(boolean|string) = false
{{ use: partial-roam }}


## expandAndCollapse(boolean) = true

子树折叠和展开的交互，`默认打开` 。由于绘图区域是有限的，而通常一个树图的节点可能会比较多，这样就会出现节点之间相互遮盖的问题。为了避免这一问题，可以将暂时无关的子树折叠收起，等到需要时再将其展开。如上面径向布局树图示例，节点中心用蓝色填充的就是折叠收起的子树，可以点击将其展开。

**注意：**如果配置自定义的图片作为节点的标记，是无法通过填充色来区分当前节点是否有折叠的子树的。而目前暂不支持，上传两张图片分别表示节点折叠和展开两种状态。所以，如果想明确地显示节点的两种状态，建议使用 `ECharts` 常规的标记类型，如 `'emptyCircle'` 等。

## initialTreeDepth(number) = 2

树图初始展开的层级（深度）。根节点是第 0 层，然后是第 1 层、第 2 层，... ，直到叶子节点。该配置项主要和 `折叠展开` 交互一起使用，目的还是为了防止一次展示过多节点，节点之间发生遮盖。如果设置为 `-1` 或者 `null` 或者 `undefined`，所有节点都将展开。

## itemStyle(Object)

树图中每个节点的样式，其中 [itemStyle.color](~series-tree.itemStyle.color) 表示节点的填充色，用来区别当前节点所对应的子树折叠或展开的状态。

{{use: partial-item-style(
    prefix="##",
    useColorPalatte=true,
    defaultBorderWidth=1.5,
    defaultBorderColor="'#c23531'"
)}}


## label(Object)

`label` 描述了每个节点所对应的文本标签的样式。

{{use:partial-label(
    prefix="##",
    defaultShowLabel=true,
    formatter1d=true
)}}


## lineStyle(Object)

定义了树图边的样式。

{{use: partial-tree-line-style(prefix="##")}}


## emphasis(Object)

树图中个图形和标签高亮的样式。

### itemStyle(Object)
{{use: partial-item-style(prefix="###")}}
### lineStyle(Object)
{{use: partial-tree-line-style(
    prefix="###"
)}}
### label(Object)
{{use:partial-label(
    prefix="###",
    formatter1d=true
)}}


## leaves(Object)

叶子节点的特殊配置，如上面的树图实例中，叶子节点和非叶子节点的标签位置不同。

### label(Object)

描述了叶子节点所对应的文本标签的样式。

{{use:partial-label(
    prefix="###",
    defaultShowLabel=true,
    formatter1d=true
)}}

### itemStyle(Object)

树图中叶子节点的样式。

{{use: partial-item-style(
    prefix="###",
    useColorPalatte=true
)}}


### emphasis(Object)
叶子节点高亮的样式。
#### label(Object)
{{use:partial-label(
    prefix="####",
    formatter1d=true
)}}
#### itemStyle(Object)
{{use: partial-item-style(prefix="####")}}


## data(Object)

[series-tree.data](~series-tree.data) 的数据格式是树状结构的。

**例如：**

```javascript
{ // 注意，最外层是一个对象，代表树的根节点
    name: "flare",    // 节点的名称，当前节点 label 对应的文本
    label: {          // 此节点特殊的 label 配置（如果需要的话）。
        ...           // label的格式参见 series-tree.label。
    },
    itemStyle: {      // 此节点特殊的 itemStyle 配置（如果需要的话）。
        ...           // label的格式参见 series-tree.itemStyle。
    },
    children: [
        {
            name: "flex",
            value: 4116,    // value 值，只在 tooltip 中显示
            label: {
                ...
            },
            itemStyle: {
                ...
            },
            collapsed: null, // 如果为 true，表示此节点默认折叠。
            children: [...] // 叶子节点没有 children, 可以不写
        },
        ...
    ]
};
```

### name(string)

树节点的名称，用来标识每一个节点。

### value(number)

节点的值，在 tooltip 中显示。

### itemStyle(Object)

该节点的样式。

{{use:partial-item-style(prefix="###", useColorPalatte=true)}}

### label(Object)

该节点的标签。

{{ use:partial-label(
    prefix="###"
) }}


### emphasis(Object)
高亮的节点样式
#### label(Object)
{{ use:partial-label(
    prefix="####"
) }}
#### itemStyle(Object)
{{use:partial-item-style(prefix="####")}}


{{use: partial-tooltip-in-series-data(
    galleryViewPath=${galleryViewPath}
)}}


{{use: partial-animation(
    prefix="##",
    defaultAnimationEasing="'linear'",
    defaultAnimationDuration=1000,
    galleryEditorPath=${galleryEditorPath}
)}}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}


{{target: partial-tree-line-style}}

#${prefix} color(Color) = "'#ccc'"

树图边的颜色。

#${prefix} width(number) = 1.5

树图边的宽度。

#${prefix} curveness(number) = 0.5

树图边的曲度。

{{use: partial-style-shadow(prefix=${prefix})}}
