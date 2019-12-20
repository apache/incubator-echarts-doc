
{{target: component-timeline}}

# timeline(Object)

`timeline` 组件，提供了在多个 ECharts `option` 间进行切换、播放等操作的功能。

示例效果如下：

~[600x400](${galleryViewPath}doc-example/mix-timeline-all&edit=1&reset=1)

`timeline` 和其他组件有些不同，它需要操作多个option。
假设，我们把 ECharts 的传统的 option 称为*原子option*，那么使用 `timeline` 时，传入 ECharts 的 option 就成为了一个集合多个原子option的*复合option*。

**例如：**
```javascript
// 如下，baseOption 是一个原子 option，options 数组中的每一项也是一个原子 option。
// 每个原子 option 中就是本文档中描述的各种配置项。
myChart.setOption(
    {
        baseOption: {
            timeline: {
                ...,
                data: ['2002-01-01', '2003-01-01', '2004-01-01']
            },
            title: {
                subtext: '数据来自国家统计局'
            },
            grid: {...},
            xAxis: [...],
            yAxis: [...],
            series: [
                { // 系列一的一些其他配置
                    type: 'bar',
                    ...
                },
                { // 系列二的一些其他配置
                    type: 'line',
                    ...
                },
                { // 系列三的一些其他配置
                    type: 'pie',
                    ...
                }
            ]
        },
        options: [
            { // 这是'2002-01-01' 对应的 option
                title: {
                    text: '2002 年统计值'
                },
                series: [
                    {data: []}, // 系列一的数据
                    {data: []}, // 系列二的数据
                    {data: []}  // 系列三的数据
                ]
            },
            { // 这是'2003-01-01' 对应的 option
                title: {
                    text: '2003 年统计值'
                },
                series: [
                    {data: []},
                    {data: []},
                    {data: []}
                ]
            },
            { // 这是'2004-01-01' 对应的 option
                title: {
                    text: '2004 年统计值'
                },
                series: [
                    {data: []},
                    {data: []},
                    {data: []}
                ]
            }
        ]
    }
);
```

在上例中，`timeline.data` 中的每一项，对应于 `options` 数组中的每个 `option`。

<br>
**使用注意与最佳实践：**

+ 公有的配置项，推荐配置在 `baseOption` 中。`timeline` 播放切换时，会把 `options` 数组中的对应的 `option`，与 `baseOption` 进行 merge 形成最终的 `option`。

+ `options` 数组中，如果某一数组项中配置了某个属性，那么其他数组项中也必须配置某个属性，而不能缺省。否则这个属性的执行效果会遗留。

+ *复合 option* 中的 `options` 不支持 merge。

    也就是说，当第二（或三、四、五 ...）次 `chart.setOption(rawOption)` 时，如果 `rawOption` 是*复合 option*（即包含 `options` 列表），那么新的 `rawOption.options` 列表不会和老的 `options` 列表进行 merge，而是简单替代。当然，`rawOption.baseOption` 仍然会正常和老的 option 进行 merge。


<br>
**与 ECharts 2 的兼容性：**

+ ECharts 3 中不再支持 timeline.notMerge 参数，也就是不支持 notMerge 模式。如果遇到这种场景需要使用，可在外部进行option管理，并用 setOption(option, true) 这样的notMerge方式设置。

+ ECharts 3 和 ECharts 2 相比，timeline 属性的定义位置有所不同，移到了 `baseOption` 中，统一作为一个普通的组件看待。但是，仍然兼容 ECharts 2 的 timeline 定义位置，只是不再推荐这样写。


## show(boolean) = true

是否显示 `timeline` 组件。默认显示。如果设置为`false` 则不会显示，但是功能还存在。


## type(string) = 'slider'

这个属性目前只支持为 `slider`，不需要更改。


## axisType(string) = 'time'

轴的类型。

**可选：**

+ `'value'`：数值轴，适用于连续数据。

+ `'category'`：类目轴，适用于离散的类目数据。

+ `'time'`：时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。


## currentIndex(number) = 0

表示当前选中项是哪项。比如，`currentIndex` 为 `0` 时，表示当前选中项为 `timeline.data[0]`（即使用 `options[0]`）。


## autoPlay(boolean) = false

表示是否自动播放。


## rewind(boolean) = false

表示是否反向播放。


## loop(boolean) = true

表示是否循环播放。


## playInterval(number) = 2000

表示播放的速度（跳动的间隔），单位毫秒（ms）。


## realtime(boolean) = true

拖动圆点的时候，是否实时更新视图。


## controlPosition(string) = 'left'

表示播放按钮的位置。

**可选：**

+`'left'`
+`'right'`

{{ use: partial-rect-layout(
    componentName='timeline'
) }}


## padding(number|Array) = 5

{{ use: partial-padding(componentName='timeline')}}


## orient(string) = 'horizontal'

摆放方式。

**可选：**

+ `'vertical'`：竖直放置。
+ `'horizontal'`：水平放置。


## inverse(boolean) = false

+ 是否反向放置 `timeline`，反向则首尾颠倒过来。


{{ use: partial-symbol(
    prefix='#',
    defaultSymbol="'emptyCircle'",
    defaultSymbolSize=10,
    name='timeline'
) }}


## lineStyle(Object)


### show(boolean) = true

是否显示轴线。默认显示。可以设置为 `false` 不显示轴线，实现不同的样式效果。

{{ use:partial-line-style(
    prefix="##",
    name="timeline ",
    defaultWidth=2,
    defaultColor="'#304654'"
)}}


## label(Object)

轴的文本标签。`emphasis` 是文本高亮的样式，比如鼠标悬浮或者图例联动高亮的时候会使用 `emphasis` 作为文本的样式。

### position(string|number) = 'auto'

轴的文本标签放置的位置。

**可选：**

+ `'auto'`：完全自动决定。
+ `'left'`：贴左边界放置。当 [timline.orient](~timeline.orient) 为 `'vertical'` 时有效。

+ `'right'`：贴右边界放置。当 [timline.orient](~timeline.orient) 为 `'vertical'` 时有效。

+ `'top'`：贴上边界放置。当 [timline.orient](~timeline.orient) 为 `'horizontal'` 时有效。

+ `'bottom'`：贴下边界放置。当 [timline.orient](~timeline.orient) 为 `'horizontal'` 时有效。

+ `number`：指定某个数值时，表示 `label` 和轴的距离。为 `0` 时则和坐标轴重合，可以为正负值，决定 `label` 在坐标轴的哪一边。


{{ use: partial-timeline-label(
    prefix="##",
    textStyleDefaultColor="'#304654'"
) }}


## itemStyle(Object)

{{use:partial-item-style-desc(
    name="timeline "
) }}



{{ use:partial-item-style(
    prefix="##",
    name="timeline ",
    defaultColor="'#304654'",
    defaultBorderWidth=1
) }}



## checkpointStyle(Object)

当前项（`checkpoint`）的图形样式。

{{ use: partial-symbol(
    prefix='##',
    defaultSymbol="'circle'",
    defaultSymbolSize=13,
    name='timeline.checkpointStyle '
) }}


### color(Color) = '#c23531'

`timeline`组件中当前项（`checkpoint`）的颜色。


### borderWidth(number) = 5

`timeline`组件中当前项（`checkpoint`）的边框宽度。


### borderColor(Color) = 'rgba(194,53,49, 0.5)'

`timeline`组件中当前项（`checkpoint`）的边框颜色。


### animation(boolean) = true

`timeline`组件中当前项（`checkpoint`）在 `timeline` 播放切换中的移动，是否有动画。


### animationDuration(number) = 300

`timeline`组件中当前项（`checkpoint`）的动画时长。


### animationEasing(string) = 'quinticInOut'

`timeline`组件中当前项（`checkpoint`）的动画的缓动效果。不同的缓动效果可以参考 [缓动示例](${galleryViewPath}line-easing)。


## controlStyle(Object)

控制按钮的样式。控制按钮包括：播放按钮、前进按钮、后退按钮。


### show(boolean) = true

是否显示控制按钮。默认显示。设置为 `false` 则全不显示。


### showPlayBtn(boolean) = true

是否显示播放按钮。默认显示。


### showPrevBtn(boolean) = true

是否显示后退按钮。默认显示。


### showNextBtn(boolean) = true

是否显示前进按钮。默认显示。


### itemSize(number) = 22

控制按钮的尺寸，单位为 px。


### itemGap(number) = 12

控制按钮的间隔，单位为 px。


### position(string) = 'left'

控制按钮的位置。

+ 当 [timeline.orient](~timeline.orient) 为 `'horizontal'`时，`'left'`、`'right'`有效。

+ 当 [timeline.orient](~timeline.orient) 为 `'vertical'`时，`'top'`、`'bottom'`有效。


### playIcon(string)

控制按钮的可播放状态的图形。

{{ use: partial-icon-image-path }}


### stopIcon(string)

播放按钮的可停止状态的图形。

{{ use: partial-icon-image-path }}


### prevIcon(string)

后退按钮的图形。

{{ use: partial-icon-image-path }}


### nextIcon(string)

前进按钮的图形。

{{ use: partial-icon-image-path }}


### color(Color) = '#304654'

按钮颜色。


### borderColor(Color) = '#304654'

按钮边框颜色。


### borderWidth(number) = 1

按钮边框线宽。



## emphasis(Object)

### label(Object)
{{ use: partial-timeline-label(
    prefix="###",
    state="emphasis",
    textStyleDefaultColor="'#c23531'"
) }}

### itemStyle(Object)
{{ use:partial-item-style(
    prefix="###",
    name="timeline ",
    defaultColor="'#c23531'",
    defaultBorderWidth=1
) }}

### checkpointStyle(Object)
当前项高亮状态的样式（hover时）。

### controlStyle(Object)
控制按钮的高亮状态的样式（hover时）。


## data(Array)

`timeline` 数据。`Array` 的每一项，可以是直接的数值。
如果需要对每个数据项单独进行样式定义，则数据项写成 `Object`。`Object` 中，`value` 属性为数值。其他属性如下例子，可以覆盖 `timeline` 中的属性配置。

**例如：**

```javascript
[
    '2002-01-01',
    '2003-01-01',
    '2004-01-01',
    {
        value: '2005-01-01',
        tooltip: {          // 让鼠标悬浮到此项时能够显示 `tooltip`。
            formatter: '{b} xxxx'
        },
        symbol: 'diamond',  // 此项的图形的特别设置。
        symbolSize: 16      // 此项的图形大小的特别设置。
    },
    '2006-01-01',
    '2007-01-01',
    '2008-01-01',
    '2009-01-01',
    '2010-01-01',
    {
        value: '2011-01-01',
        tooltip: {          // 让鼠标悬浮到此项时能够显示 `tooltip`。
            formatter: function (params) {
                return params.name + 'xxxx';
            }
        },
        symbol: 'diamond',
        symbolSize: 18
    },
]
```





{{target: partial-timeline-label}}

#${prefix} show(boolean) = true

是否显示 label。默认显示。


#${prefix} interval(string|number) = 'auto'

`label` 的间隔。当指定为数值时，例如指定为 `2`，则每隔两个显示一个 label。


#${prefix} rotate(prefix) = 0

`label` 的旋转角度。正值表示逆时针旋转。

#${prefix} formatter(string|Function) = null

{{use: axis-common-formatter-desc}}

{{ if: ${state} }}
{{ use: partial-text-style(
    prefix=${prefix},
    name="timeline.lable." + ${state},
    defaultColor=${textStyleDefaultColor}
) }}
{{ else }}
{{ use: partial-text-style(
    prefix=${prefix},
    name="timeline.lable",
    defaultColor=${textStyleDefaultColor}
) }}
{{ /if }}
