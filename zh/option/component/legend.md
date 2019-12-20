
{{target: component-legend}}

# legend(Object)

图表的图例组件。图表的每个系列都对应一个图例，图例组件中包含标记 (symbol)、颜色和系列名称。可以通过点击图例来控制系列是否在图表中显示。

单个 ECharts 实例中可以存在多个图例组件，会方便多个图例的布局。
当图例数量过多时，可以使用 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)，参见：[legend.type](~legend.type)


## type(string)

图例的类型。

**可选：**

+ `'plain'`：普通图例。默认类型。
+ `'scroll'`：可滚动翻页的图例。当图例数量较多时使用。

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

当使用 `'scroll'` 时，可以使用以下配置项来设置更多细节：
+ [legend.scrollDataIndex](~legend.scrollDataIndex)
+ [legend.pageButtonItemGap](~legend.pageButtonItemGap)
+ [legend.pageButtonGap](~legend.pageButtonGap)
+ [legend.pageButtonPosition](~legend.pageButtonPosition)
+ [legend.pageFormatter](~legend.pageFormatter)
+ [legend.pageIcons](~legend.pageIcons)
+ [legend.pageIconColor](~legend.pageIconColor)
+ [legend.pageIconInactiveColor](~legend.pageIconInactiveColor)
+ [legend.pageIconSize](~legend.pageIconSize)
+ [legend.pageTextStyle](~legend.pageTextStyle)
+ [legend.animation](~legend.animation)
+ [legend.animationDurationUpdate](~legend.animationDurationUpdate)

{{use: partial-component-id(prefix="#")}}

## show(boolean) = true

是否显示图例组件。


{{use: partial-rect-layout-width-height(componentName="图例")}}

## orient(string) = 'horizontal'

图例组件的布局朝向。

**可选：**
+ `'horizontal'`：水平布局。
+ `'vertical'`：垂直布局。

## align(string) = 'auto'

图例和文本的对齐。默认自动，根据组件的位置和 [orient](~legend.orient) 决定。当组件的 [right](~legend.right) 值为 `'right'` 并且图例组件为纵向布局（[orient](~legend.orient) 为 `'vertical'`）的时候，图例和文本为右对齐，即为 `'right'`。

**可选：**
+ `'auto'`：元素自动对齐。
+ `'left'`：元素左边缘对齐。
+ `'right'`：元素右边缘对齐。

## padding(number) = 5

{{ use: partial-padding(componentName="图例")}}

## itemGap(number) = 10

每项图例之间的间隔。单位为 px。图例横向布局时为水平间隔，纵向布局时为纵向间隔。

## itemWidth(number) = 25

图例标记的图形宽度。单位为 px。

## itemHeight(number) = 14

图例标记的图形高度。单位为 px。

## symbolKeepAspect(boolean) = true

如果图标（可能来自系列的 `symbol` 或用户自定义的 `legend.data.icon`）是 `path://` 的形式，是否在缩放时保持该图形的长宽比。默认为保持，可以设成 `false` 关闭。

## formatter(string|Function) = null

用来格式化图例文本，支持字符串模板和回调函数两种形式。

**示例：**
```js
// 使用字符串模板，模板变量为图例名称 {name}
formatter: 'Legend {name}'
// 使用回调函数
formatter: function (name) {
    return 'Legend ' + name;
}
```

## selectedMode(string|boolean) = true

图例选择的模式，控制是否可以通过点击图例改变系列的显示状态。默认开启图例选择，可以设成 `false` 关闭。

除此之外，也可以选择图例使用单选或者多选模式。

**可选：**
+ `'single'` 单选模式
+ `'multiple'` 多选模式


## inactiveColor(Color) = '#ccc'

图例关闭的颜色。

## selected(Object)

图例选中的状态表。

**示例：**
```
selected: {
    // 选中'系列1'
    '系列1': true,
    // 不选中'系列2'
    '系列2': false
}
```

## textStyle(Object)

图例的文本样式。

{{ use: partial-text-style(
    componentName='图例',
    prefix='##',
    defaultColor="#333",
    noAlign=true,
    noVerticalAlign=true
) }}

## tooltip(Object)

图例的 tooltip 配置，配置项同 [tooltip](~tooltip)。默认不显示，可以在 legend 文字很多的时候对文字做裁剪并且开启 tooltip。

**示例：**

```js
legend: {
    formatter: function (name) {
        return echarts.format.truncateText(name, 40, '14px Microsoft Yahei', '…');
    },
    tooltip: {
        show: true
    }
}
```

## icon(string)

图例项的 icon。

{{ use: partial-icon }}

## data(Array)

图例的数据数组。数组项通常为一个字符串，每一项代表一个系列的 `name`（如果是[饼图](~series-pie)，也可以是饼图单个数据的 `name`）。图例组件会自动根据对应系列的图形标记（symbol）来绘制自己的标记和颜色，特殊字符串 `''`（空字符串）或者 `'\n'`（换行字符串）用于图例的换行。

如果 `data` 没有被指定，会自动从当前系列中获取。多数系列会取自 [series.name](~series.name) 或者 [series.encode](~series.encode) 的 `seriesName` 所指定的维度。如 [饼图](~series-pie) and [漏斗图](~series-funnel) 等会取自 series.data 中的 name。

如果要设置单独一项的样式，也可以把该项写成配置项对象。此时必须使用 `name` 属性对应表示系列的 `name`。

示例
```
data: [{
    name: '系列1',
    // 强制设置图形为圆。
    icon: 'circle',
    // 设置文本为红色
    textStyle: {
        color: 'red'
    }
}]
```

### name(string)
图例项的名称，相当于某系列的`name`值（如果是饼图，也可以是饼图单个数据的 `name`）。

### icon(string)

图例项的 icon。

{{ use: partial-icon }}

### textStyle(Object)

图例项的文本样式。

{{ use: partial-component-common-style(
    componentName='图例',
    prefix='#',
    defaultBorderColor="'#ccc'",
    hasBorderRadius=true
) }}



## scrollDataIndex(number) = 0

[legend.type](~legend.type) 为 `'scroll'` 时有效。

图例当前最左上显示项的 `dataIndex`。

在 `setOption` 模式时指定此项的话，可决定当前图例滚动到哪里。

但是，如果仅仅想改变图例翻页，一般并不调用 `setOption`（因为这太重量了），仅仅使用 action [legendScroll](api.html#action.legend.legendScroll) 即可。

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

## pageButtonItemGap(number) = 5

[legend.type](~legend.type) 为 `'scroll'` 时有效。

图例控制块中，按钮和页信息之间的间隔。

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

## pageButtonGap(number) = null

[legend.type](~legend.type) 为 `'scroll'` 时有效。

图例控制块和图例项之间的间隔。

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

## pageButtonPosition(string) = 'end'

[legend.type](~legend.type) 为 `'scroll'` 时有效。

图例控制块的位置。

**可选：**

+ `'start'`：控制块在左或上。
+ `'end'`：控制块在右或下。

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

## pageFormatter(string|Function) = '{current}/{total}'

[legend.type](~legend.type) 为 `'scroll'` 时有效。

图例控制块中，页信息的显示格式。默认为 `'{current}/{total}'`，其中 `{current}` 是当前页号（从 1 开始计数），`{total}` 是总页数。

如果 `pageFormatter` 使用函数，须返回字符串，参数为：
```js
{
    current: number
    total: number
}
```

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

## pageIcons(Object)

[legend.type](~legend.type) 为 `'scroll'` 时有效。

图例控制块的图标。

### horizontal(Array)

[legend.orient](~legend.orient) 为 `'horizontal'` 时的翻页按钮图标。

是一个数组，表示 `[previous page button, next page button]`。默认值为 `['M0,0L12,-10L12,10z', 'M0,0L-12,-10L-12,10z']`。

数组中每项，{{ use: partial-icon-image-path }}

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

### vertical(Array)

[legend.orient](~legend.orient) 为 `'vertical'` 时的翻页按钮图标。

是一个数组，表示 `[previous page button, next page button]`。默认值为 `['M0,0L20,0L10,-20z', 'M0,0L20,0L10,20z']`，。

数组中每项，{{ use: partial-icon-image-path }}

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

## pageIconColor(string) = '#2f4554'

[legend.type](~legend.type) 为 `'scroll'` 时有效。

翻页按钮的颜色。

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

## pageIconInactiveColor(string) = '#aaa'

[legend.type](~legend.type) 为 `'scroll'` 时有效。

翻页按钮不激活时（即翻页到头无法再翻页时）的颜色。

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

## pageIconSize(number|Array) = 15

[legend.type](~legend.type) 为 `'scroll'` 时有效。

翻页按钮的大小。可以是数字，也可以是数组，如 `[10, 3]`，分别表示宽和高。单位为 px。

参见 [滚动图例（垂直）](${galleryEditorPath}pie-legend&edit=1&reset=1) 或 [滚动图例（水平）](${galleryEditorPath}radar2&edit=1&reset=1)。

## pageTextStyle(Object)

[legend.type](~legend.type) 为 `'scroll'` 时有效。

图例页信息的文字样式。

{{ use: partial-simple-text-style(componentName='图例页信息', prefix='##', defaultColor="#333") }}

## animation(boolean)

图例翻页是否使用动画。

## animationDurationUpdate(number) = 800

图例翻页动画的时长。单位为 ms。

## selector(boolean|Array) = false

图例组件中的选择器按钮，目前包括全选和反选两种功能。默认不显示，用户可手动开启，也可以手动配置每个按钮的标题。

**例如：**

```js
selector: [
    {
        type: 'all or inverse',
        // 可以是任意你喜欢的 title
        title: '全选'
    },
    {
        type: 'inverse',
        title: '反选'
    }
]

// 或
selector: true

// 或
selector: ['all', 'inverse']
```

## selectorLabel(Object)

选择器按钮的文本标签样式，默认显示。

{{use:partial-label(
    prefix='##',
    defaultShowLabel=true,
    noPosition=true,
    formatter=false,
    formatter1d=false
)}}

## selectorPosition(string) = 'auto'

选择器的位置，可以放在图例的尾部或者头部，对应的值分别为 `'end'` 和 `'start'`。默认情况下，图例横向布局的时候，选择器放在图例的尾部；图例纵向布局的时候，选择器放在图例的头部。

## selectorItemGap(number) = 7

选择器按钮之间的间隔。单位为 px。

## selectorButtonGap(number) = 10

选择器按钮与图例组件之间的间隔。单位为 px。
