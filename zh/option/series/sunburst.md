{{ target: partial-sunburst-label-helper }}

#${prefix} rotate(string|number) = 'radial'

如果是 `number` 类型，则表示标签的旋转角，从 -90 度到 90 度，正值是逆时针。

除此之外，还可以是字符串 `'radial'` 表示径向旋转、`'tangential'` 表示切向旋转。

默认径向旋转，如果不需要文字旋转，可以将其设为 `0`。

下面的例子展示了不同的 `rotate` 设置方法：

~[700x400](${galleryViewPath}sunburst-label-rotate&edit=1&reset=1)

#${prefix} align(string) = 'center'

文字对齐方式，可取值为：`'left'`、 `'center'`、 `'right'`。

**注意：**`'left'` 是指靠近内圈，而 `'right'` 是指靠近外圈。

~[700x400](${galleryViewPath}doc-example/sunburst-label-align&edit=1&reset=1)

#${prefix} minAngle(number) = null

当某个扇形块的角度小于该值（角度制）时，扇形块对应的文字不显示。该值用以隐藏过小扇形块中的文字。


{{use:partial-label(
    prefix=${prefix},
    defaultPosition="'inside'",
    formatter=true,
    defaultShowLabel="true",
    noRotate=true,
    noAlign=true
)}}



{{ target: partial-sunburst-label-props }}
${prefix} label(Object)

`label` 描述了每个扇形块中，文本标签的样式。

**优先级：[series.data.label](~series-sunburst.data.label) > [series.levels.label](~series-sunburst.levels.label) > [series.label](~series-sunburst.label)。**

{{ use: partial-label-desc }}

{{ use: partial-sunburst-label-helper(prefix=${prefix}) }}



{{ target: partial-sunburst-itemStyle-props }}

${prefix} itemStyle(Object)

旭日图扇形块的样式。

可以在 [series.itemStyle](~series-sunburst.itemStyle) 定义所有扇形块的样式，也可以在 [series.levels.itemStyle](~series-sunburst.levels.itemStyle) 定义每一层扇形块的样式，还可以在 [series.data.itemStyle](~series-sunburst.data.itemStyle) 定义每个扇形块单独的样式，这三者的优先级从低到高。也就是说，如果定义了 [series.data.itemStyle](~series-sunburst.data.itemStyle)，将会覆盖 [series.itemStyle](~series-sunburst.itemStyle) 和 [series.levels.itemStyle](~series-sunburst.levels.itemStyle)。

**优先级：[series.data.itemStyle](~series-sunburst.data.itemStyle) > [series.levels.itemStyle](~series-sunburst.levels.itemStyle) > [series.itemStyle](~series-sunburst.itemStyle)。**

ECharts 中，通常使用 *emphasis* 表示鼠标移动到图形上后的高亮状态。对于旭日图而言，我们引入了另两种状态：*highlight* 表示由于高亮了某个扇形块引起的其他相关扇形块的高亮；*downplay* 表示除了 highlight 扇形块之外的被淡化的扇形块。参见 [highlightPolicy](~series-sunburst.highlightPolicy)。

{{use: partial-item-style(
    prefix=${prefix},
    useColorPalatte=true,
    defaultBorderWidth=1,
    defaultBorderColor="'white'",
    defaultOpacity=1
)}}



{{ target: partial-sunburst-other-state }}

#${prefix} emphasis(Object)

鼠标悬停后的配置项。

{{use: partial-sunburst-label-props(
    prefix="##" + ${prefix}
)}}

{{use: partial-sunburst-itemStyle-props(
    prefix="##" + ${prefix}
)}}

#${prefix} highlight(Object)

鼠标悬停后相关扇形块的配置项。参见 [highlightPolicy](~series-sunburst.highlightPolicy)。

{{use: partial-sunburst-label-props(
    prefix="##" + ${prefix}
)}}

{{use: partial-sunburst-itemStyle-props(
    prefix="##" + ${prefix}
)}}

#${prefix} downplay(Object)

鼠标悬停后不相关扇形块的配置项。参见 [highlightPolicy](~series-sunburst.highlightPolicy)。

{{use: partial-sunburst-label-props(
    prefix="##" + ${prefix}
)}}

{{use: partial-sunburst-itemStyle-props(
    prefix="##" + ${prefix}
)}}



{{ target: series-sunburst }}

# series.sunburst(Object)

[旭日图（Sunburst）](https://en.wikipedia.org/wiki/Pie_chart#Ring_chart_/_Sunburst_chart_/_Multilevel_pie_chart)由多层的环形图组成，在数据结构上，内圈是外圈的父节点。因此，它既能像[饼图](~series-pie)一样表现局部和整体的占比，又能像[矩形树图](~series-treemap)一样表现层级关系。

**例如：**

~[700x500](${galleryViewPath}sunburst-monochrome&edit=1&reset=1)

~[700x700](${galleryViewPath}sunburst-drink&edit=1&reset=1)

**数据下钻**

旭日图默认支持数据下钻，也就是说，当用户点击了某个扇形块之后，将会以该节点作为根结点显示，并且在中间出现一个返回上层节点的圆。如果不希望有数据下钻功能，可以通过将 [series-sunburst.nodeClick](~series-treemap.nodeClick) 设置为 `false` 实现。


## type(string) = 'sunburst'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}

{{use: component-circular-layout(
    componentName="旭日图",
    defaultRadius="[0, '75%']"
)}}


## data(Array)

[series-sunburst.data](~series-sunburst.data) 的数据格式是树状的。

**例如：**

```js
[{
    name: 'parent1',
    value: 10,          // 可以不写父元素的 value，则为子元素之和；
                        // 如果写了，并且大于子元素之和，可以用来表示还有其他子元素未显示
    children: [{
        value: 5,
        name: 'child1',
        children: [{
            value: 2,
            name: 'grandchild1',
            itemStyle: {
                // 每个数据可以有自己的样式，覆盖 series.itemStyle 和 level.itemStyle
            },
            label: {
                // 标签样式，同上
            }
        }]
    }, {
        value: 3,
        name: 'child2'
    }],
    itemStyle: {
        // parent1 的图形样式，不会被后代继承
    },
    label: {
        // parent1 的标签样式，不会被后代继承
    }
}, {
    name: 'parent2',
    value: 4
}]
```

### value(number)

数据值，如果包含 children，则可以不写 value 值。这时，将使用子元素的 value 之和作为父元素的 value。如果 value 大于子元素之和，可以用来表示还有其他子元素未显示。

### name(string)

显示在扇形块中的描述文字。

### link(string)

点击此节点可跳转的超链接。须 [series-sunburst.nodeClick](~series-treemap.nodeClick) 值为 `'link'` 时才生效。

参见 [series-sunburst.data.target](~series-sunburst.data.target)。

### target(string) = 'blank'

意义同 HTML `<a>` 标签中的 `target`，参见 [series-sunburst.data.link](~series-sunburst.data.link)。可选值为：`'blank'` 或 `'self'`。


{{use: partial-sunburst-label-props(
    prefix="###"
)}}

{{use: partial-sunburst-itemStyle-props(
    prefix="###"
)}}

{{ use: partial-sunburst-other-state(prefix="##") }}

### children(Array)

子节点，递归定义，格式同 [series-sunburst.data](~series-sunburst.data)。

{{use: partial-sunburst-label-props(
    prefix="##"
)}}

{{use: partial-sunburst-itemStyle-props(
    prefix="##"
)}}

## highlightPolicy(string) = 'descendant'

当鼠标移动到一个扇形块时，可以高亮相关的扇形块。**如果其值为 `'descendant'`，则会高亮该扇形块和后代元素，其他元素将被淡化（*downplay*，参见 [itemStyle](~series-sunburst.itemStyle)）；如果其值为 `'ancestor'`，则会高亮该扇形块和祖先元素；如果其值为 `'self'` 则只高亮自身；`'none'` 则不会淡化其他元素。**

~[700x350](${galleryViewPath}doc-example/sunburst-highlight-descendant&edit=1&reset=1)

上面的例子 `highlightPolicy` 是默认值 `'descendant'`，我们通过 `dispatchAction` 触发了旭日图中某个数据块的高亮操作（相当于将鼠标移动到下图中的 `target` 扇形块中）。目标扇形块将采用 `emphasis` 的样式（在本例中是为红色），和目标扇形块相关的扇形块（由 `highlightPolicy` 决定哪些扇形块是相关的）采用 `highlight` 的样式（橙色），其他扇形块采用 `downplay` 的样式（灰色）。而如果没有高亮对象，则所有扇形块都采用默认的样式。样式定义是类似这样的：

```js
itemStyle: {
    color: 'yellow',
    borderWidth: 2
},
emphasis: {
    itemStyle: {
        color: 'red'
    }
},
highlight: {
    itemStyle: {
        color: 'orange'
    }
},
downplay: {
    itemStyle: {
        color: '#ccc'
    }
}
```

而如果将 `highlightPolicy` 设为 `'ancestor'`，则会得到这样的效果：

~[700x350](${galleryViewPath}doc-example/sunburst-highlight-ancestor&edit=1&reset=1)



## nodeClick(boolean|string) = 'rootToNode'

点击节点后的行为。可取值为：

+ `false`：节点点击无反应。
+ `'rootToNode'`：点击节点后以该节点为根结点。
+ `'link'`：如果节点数据中有 [link](~series-sunburst.data.link) 点击节点后会进行超链接跳转。



## sort(string|Function) = 'desc'

扇形块根据数据 [`value`](~series-sunburst.data.value) 的排序方式，如果未指定 `value`，则其值为子元素 `value` 之和。默认值 `'desc'` 表示降序排序；还可以设置为 `'asc'` 表示升序排序；`null` 表示不排序，使用原始数据的顺序；或者用回调函数进行排列。

**例如：**
```js
function(nodeA, nodeB) {
    return nodeA.getValue() - nodeB.getValue();
}
```



## renderLabelForZeroData(boolean) = false

如果数据没有 `name`，是否需要渲染文字。


{{use: partial-sunburst-label-props(
    prefix="##"
)}}

{{use: partial-sunburst-itemStyle-props(
    prefix="##"
)}}

{{ use: partial-sunburst-other-state(prefix="#") }}




## levels(Array) = []

**多层配置**

旭日图是一种有层次的结构，为了方便同一层样式的配置，我们提供了 levels 配置项。它是一个数组，其中的第 0 项表示数据下钻后返回上级的图形，其后的每一项分别表示从圆心向外层的层级。

假设我们没有数据下钻功能，并且希望将最内层的扇形块的颜色设为红色，文字设为蓝色，可以这样设置：

**例如：**

```js
series: {
    // ...
    levels: [
        {
            // 留给数据下钻点的空白配置
        },
        {
            // 最靠内测的第一层
            itemStyle: {
                color: 'red'
            },
            label: {
                color: 'blue'
            }
        },
        {
            // 第二层 ...
        }
    ]
}
```

{{use: partial-sunburst-label-props(
    prefix="###"
)}}

{{use: partial-sunburst-itemStyle-props(
    prefix="###"
)}}

{{ use: partial-sunburst-other-state(prefix="##") }}

{{use: partial-animation(
    prefix="#",
    defaultAnimationEasing="'cubicOut'",
    defaultAnimationDuration=1000,
    defaultAnimationDurationUpdate=500,
    galleryEditorPath=${galleryEditorPath}
)}}
