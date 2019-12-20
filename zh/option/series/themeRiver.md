
{{target: series-themeRiver}}

# series.themeRiver(Object)

** 主题河流 **

是一种特殊的流图, 它主要用来表示事件或主题等在一段时间内的变化。

**例如：**

~[700x580](${galleryViewPath}themeRiver-lastfm&edit=1&reset=1)


<br>
**可视编码：**

主题河流中不同颜色的条带状河流分支编码了不同的事件或主题，河流分支的宽度编码了原数据集中的value值。

此外，原数据集中的时间属性，映射到单个时间轴上。


## type(string) = 'themeRiver'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-rect-layout-width-height(
    componentName='thmemRiver',
    defaultLeft: '5%',
    defaultRight: '5%',
    defaultTop: '5%',
    defaultBottom: '5%',
    defaultWidth: 'null',
    defaultHeight: 'null'
) }}

**注意：**
整个主题河流view的位置信息复用了单个时间轴的位置信息，即left，top，right，bottom。


## coordinateSystem(string) = "single"

坐标系统，主题河流用的是单个的时间轴。


## boundaryGap(Array) = ["10%", "10%"]

图中与坐标轴正交的方向的边界间隙，设置该值是为了调整图的位置，使其尽量处于屏幕的正中间，避免处于屏幕的上方或下方。


## singleAxisIndex(number) = 0

单个时间轴的index，默认值为0，因为只有单个轴。


## label(Object)

`label` 描述了主题河流中每个带状河流分支对应的文本标签的样式。

{{use:partial-label(
    prefix="##",
    defaultShowLabel=true,
    defaultPosition="'left'",
    defaultMargin=4,
    noAlign=true,
    noVerticalAlign=true,
    defaultColor="'#000'",
    defaultFontSize=11,
)}}

## itemStyle(Object)

主题河流中每个带状河流分支的样式。

{{use: partial-item-style(
    prefix="##"
)}}

## emphasis(Object)

高亮的图形和标签样式。

### label(Object)
{{use:partial-label(
    prefix="###",
    defaultPosition="'left'",
    defaultMargin=4,
    noAlign=true,
    noVerticalAlign=true,
    defaultColor="'#000'",
    defaultFontSize=11,
)}}

### itemStyle(Object)
{{use: partial-item-style(
    prefix="###",
    defaultShadowBlur=20,
    defaultShadowColor="'rgba(0,0,0,0.8)'"
)}}


## data(Array)
{{ use: partial-2d-data-desc() }}
### date(string)
时间或主题的时间属性。
### value(number)
事件或主题在某个时间点的值。
### name(string)
事件或主题的名称。

```js
data: [
    ["2015/11/09",10,"DQ"],
    ["2015/11/10",10,"DQ"],
    ["2015/11/11",10,"DQ"],
    ["2015/11/08",10,"SS"],
    ["2015/11/09",10,"SS"],
    ["2015/11/10",10,"SS"],
    ["2015/11/11",10,"SS"],
    ["2015/11/12",10,"SS"],
    ["2015/11/13",10,"QG"],
    ["2015/11/08",10,"QG"],
    ["2015/11/11",10,"QG"],
    ["2015/11/13",10,"QG"],
]
```
**数据说明：**

如上所示，主题河流的数据格式是二维数组的形式，里层数组的每一项由事件或主题的时间属性、事件或主题在某个时间点的值，以及事件或主题的名称组成。值得注意的是，一定要提供一个具有完整时间段的事件或主题作为主干河流，其他事件或主题以该主干河流为依据，将缺省的时间点上的值补为0，也就是说其他事件或主题的时间段是包含在主干河流内的，如果超出，布局会出错，这么做的原因是，在计算整个图的布局的时候要计算一条baseline，以便将每个事情画成流带状。如上图中的"SS"这一事件就是一个主干河流，经过处理，我们会将"DQ"中缺省的三个时间点以["2015/11/08",0,"DQ"]，["2015/11/12",0,"DQ"]，［"2015/11/13",0,"DQ"］的格式补齐，使其与主干河流对其。从中还可以看出，我们可以在完整时间段的任意位置缺省。


{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}
