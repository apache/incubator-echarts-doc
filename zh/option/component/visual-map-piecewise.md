
{{target: component-visual-map-piecewise}}

# visualMap.piecewise(Object)

**分段型视觉映射组件（visualMapPiecewise）**

（参考[视觉映射组件（visualMap）的介绍](~visualMap)）

展现形式如下图：
~[600x400](${galleryViewPath}doc-example/scatter-visualMap-piecewise&edit=1&reset=1)


分段型视觉映射组件，有三种模式：

+ **连续型数据平均分段**: 依据 [visualMap-piecewise.splitNumber](~visualMap-piecewise.splitNumber) 来自动平均分割成若干块。
+ **连续型数据自定义分段**: 依据 [visualMap-piecewise.pieces](~visualMap-piecewise.pieces) 来定义每块范围。
+ **离散数据根据类别分段**: 类别定义在 [visualMap-piecewise.categories](~visualMap-piecewise.categories) 中。


<br>
<br>

## type(string) = piecewise

类型为分段型。

{{use: partial-component-id(prefix="#")}}

## splitNumber(number) = 5

对于连续型数据，自动平均切分成几段。默认为 5 段。
连续数据的范围需要 [max](~visualMap-piecewise.max) 和 [min](~visualMap-piecewise.min) 来指定。

如果设置了 [visualMap-piecewise.pieces](~visualMap-piecewise.pieces) 或者 [visualMap-piecewise.categories](~visualMap-piecewise.categories)，则 `splitNumber` 无效。


## pieces(Array)

自定义『分段式视觉映射组件（visualMapPiecewise）』的每一段的范围，以及每一段的文字，以及每一段的特别的样式。

**例如：**

```javascript
pieces: [
    {min: 1500}, // 不指定 max，表示 max 为无限大（Infinity）。
    {min: 900, max: 1500},
    {min: 310, max: 1000},
    {min: 200, max: 300},
    {min: 10, max: 200, label: '10 到 200（自定义label）'},
    {value: 123, label: '123（自定义特殊颜色）', color: 'grey'}, // 表示 value 等于 123 的情况。
    {max: 5}     // 不指定 min，表示 min 为无限大（-Infinity）。
]
```

或者，更精确得，可以使用 `lt`（小于，little than），`gt`（大于，greater than），`lte`（小于等于 lettle than or equals），`gte`（大于等于，greater than or equals）来表达边界。

**例如：**

```javascript
pieces: [
    {gt: 1500},            // (1500, Infinity]
    {gt: 900, lte: 1500},  // (900, 1500]
    {gt: 310, lte: 1000},  // (310, 1000]
    {gt: 200, lte: 300},   // (200, 300]
    {gt: 10, lte: 200, label: '10 到 200（自定义label）'},       // (10, 200]
    {value: 123, label: '123（自定义特殊颜色）', color: 'grey'},  // [123, 123]
    {lt: 5}                 // (-Infinity, 5)
]
```

**注意：**如果两个 piece 的区间重叠，则会自动进行去重。


在每个 piece 中支持的 visualMap 属性有：

{{use: partial-visual-map-visual-type}}

[参见示例](${galleryEditorPath}doc-example/map-visualMap-pieces&edit=1&reset=1)

（注：在 ECharts 2 中，`pieces` 叫做 `splitList`。现在后者仍兼容，但推荐使用 `pieces`）

`pieces` 中的顺序，其实试试就知道。若要看详细的规则，参见 [visualMap.inverse](~visualMap.inverse)。


## categories(Array)

用于表示离散型数据（或可以称为类别型数据、枚举型数据）的全集。

当所指定的维度（[visualMap-piecewise.dimension](~visualMap-piecewise.dimension)）的数据为离散型数据时，例如数据值为优、良等，那么可如下配置：

```javascript
categories: ['严重污染', '重度污染', '中度污染', '轻度污染', '良', '优'],
```

[参见示例](${galleryEditorPath}doc-example/scatter-visualMap-categories&edit=1&reset=1)

`categories` 中的顺序，其实试试就知道。若要看详细的规则，参见 [visualMap.inverse](~visualMap.inverse)。


## min(number)

指定 visualMapPiecewise 组件的最小值。

在 **连续型数据自定义分段** 模式（即 [visualMap-piecewise.pieces](~visualMap-piecewise.pieces) 被使用）或 **离散数据根据类别分段** 模式（即 [visualMap-piecewise.categories](~visualMap-piecewise.categories) 被使用）时，`max` 和 `min` 不需指定。

在 **连续型数据平均分段** 模式（即 (that is, when [visualMap-piecewise.splitNumber](~visualMap-piecewise.splitNumber) 被使用时）需指定 `min`、`max`，如果不指定，则默认为 `[0, 200]`（注意并不是默认为
series.data 的 `dataMin` 和 `dataMax`）。

## max(number)

指定 visualMapPiecewise 组件的最大值。参见 [visualMap-piecewise.splitNumber](~visualMap-piecewise.splitNumber)

**连续型数据自定义分段** 模式（即 [visualMap-piecewise.pieces](~visualMap-piecewise.pieces) 被使用）或 **离散数据根据类别分段** 模式（即 [visualMap-piecewise.categories](~visualMap-piecewise.categories) 被使用），`max` 和 `min` 不需指定。

**连续型数据平均分段** 模式（即 (that is, when [visualMap-piecewise.splitNumber](~visualMap-piecewise.splitNumber) 被使用时）需指定 `min`、`max`，如果不指定，则默认为 `[0, 200]`（注意并不是默认为
series.data 的 `dataMin` 和 `dataMax`）。

## minOpen(boolean)

当 `type` 为 `piecewise` 且使用 `min`/`max`/`splitNumber` 时，此参数有效。当值为 `true` 时，界面上会额外多出一个『< min』的选块。

## maxOpen(boolean)

当 `type` 为 `piecewise` 且使用 `min`/`max`/`splitNumber` 时，此参数有效。当值为 `true` 时，界面上会额外多出一个『> max』的选块。

## selectedMode(string) = 'multiple'

选择模式，可以是：

+ `'multiple'`（多选）。
+ `'single'`（单选）。


## inverse(boolean) = false

是否反转。

+ **连续型数据平均分段** 模式（即 (that is, when [visualMap-piecewise.splitNumber](~visualMap-piecewise.splitNumber) 被使用时），数据排布规则，同 [visualMap-continuous.inverse](~visualMap-continuous.inverse)。

+ **连续型数据自定义分段** 模式（即 [visualMap-piecewise.pieces](~visualMap-piecewise.pieces) 被使用）或 **离散数据根据类别分段** 模式（即 [visualMap-piecewise.categories](~visualMap-piecewise.categories) 被使用），每个块的排布位置，取决于 `pieces` 或 `categories` 列表的定义顺序，即：

    + 当`inverse`为`false`时：

        * 当 [visualMap.orient](~visualMap.orient) 为 `'vertical'` 时，`pieces[0]` 或 `categories[0]`对应上方

        * 当 [visualMap.orient](~visualMap.orient) 为 `'horizontal'` 时，`pieces[0]` 或 `categories[0]` 对应左方。

    + 当 `inverse` 为 `true` 时，与上面相反。

其实没有那么复杂，使用时候，试试就知道了。


## precision(number) = null

数据展示的小数精度。

+ **连续型数据平均分段** 模式（即 (that is, when [visualMap-piecewise.splitNumber](~visualMap-piecewise.splitNumber) 被使用时），精度根据数据自动适应。

+ **连续型数据自定义分段** 模式（即 [visualMap-piecewise.pieces](~visualMap-piecewise.pieces) 被使用）或 **离散数据根据类别分段** 模式（即 [visualMap-piecewise.categories](~visualMap-piecewise.categories) 被使用），精度默认为0（没有小数）。


## itemWidth(number) = 20

图形的宽度，即每个小块的宽度。


## itemHeight(number) = 14

图形的高度，即每个小块的高度。


## align(string) = 'auto'

指定组件中图形（比如小方块）和文字的摆放关系。

**可选：**

+ `'auto'`：自动决定。
+ `'left'`：图形在左文字在右。
+ `'right'`：图形在右文字在左。


## text(Array) = null

两端的文本，如['High', 'Low']。[参见例子](${galleryEditorPath}doc-example/map-visualMap-piecewise-text&edit=1&reset=1)。

`text` 中的顺序，其实试试就知道。若要看详细的规则，参见 [visualMap.inverse](~visualMap.inverse)。

兼容 ECharts 2，当有 `text` 时，label 不显示。

## textGap(Array) = 10

两端文字主体之间的距离。单位为 px。参见 [visualMap-piecewise.text](~visualMap-piecewise.text)。

## showLabel(boolean)

是否显示每项的文本标签。默认显示。如果 [visualMap-piecewise.text](~visualMap-piecewise.text) 被使用则不显示文本标签。

## itemGap(number) = 10

每两个图元之间的间隔距离。单位为 px。


## itemSymbol(string) = 'roundRect'

默认的图形。可选值为：{{ import: partial-icon-buildin}}。

symbol的设置参见 [visualMap-piecewise.inRange](~visualMap-piecewise.inRange) 和 [visualMap-piecewise.outOfRange](~visualMap-piecewise.outOfRange)。

当他们没有进行指定时，取此 `itemSymbol` 为默认值（但是只在 visualMap 组件上使用，不在 chart 中使用）。


{{ use: partial-visual-map-common(
    visualMapName='visualMap-piecewise',
    galleryEditorPath=${galleryEditorPath}
) }}


## formatter(string|Function)

标签的格式化工具。

+ 如果为`string`，表示模板，如：`aaaa{value}bbbb{value2}`。其中 `{value}` 和 `{value2}` 是当前的范围边界值。
+ 如果为 `Function`，表示回调函数，形如：

```javascript
formatter: function (value, value2) {
    return 'aaaa' + value + 'bbbb' + value2; // 范围标签显示内容。
}
```