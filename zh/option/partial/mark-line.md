{{ target: partial-mark-line }}

#${prefix} markLine
图表标线。

{{ use: partial-silent(prefix="#" + ${prefix}) }}

##${prefix} symbol(string|Array)
标线两端的标记类型，可以是一个数组分别指定两端，也可以是单个统一指定，具体格式见 [data.symbol](~series-${seriesType}.markLine.data.0.symbol)。
##${prefix} symbolSize(number|Array)
标线两端的标记大小，可以是一个数组分别指定两端，也可以是单个统一指定。

**注意：** 这里无法像一般的 `symbolSize` 那样通过数组分别指定高宽。

##${prefix} precision(number) = 2
标线数值的精度，在显示平均值线的时候有用。

##${prefix} label(Object)
标线的文本。
{{ use: mark-line-label(
    prefix=${prefix} + '##'
) }}

##${prefix} lineStyle(Object)
标线的样式
{{ use: partial-line-style(
    prefix="##" + ${prefix},
    defaultColor='自适应',
    defaultLineType='dashed',
    hasCurveness=true
) }}

##${prefix} emphasis(Object)

标线的高亮样式。

###${prefix} label(Object)
{{ use: mark-line-label(
    prefix=${prefix} + '###'
) }}
###${prefix} lineStyle(Object)
{{ use: partial-line-style(
    prefix="###" + ${prefix}
) }}

##${prefix} data
标线的数据数组。每个数组项可以是一个两个值的数组，分别表示线的起点和终点，每一项是一个对象，有下面几种方式指定起点或终点的位置。
1. 通过 [x](~series-${seriesType}.markLine.data.0.x), [y](~series-${seriesType}.markLine.data.0.y) 属性指定相对容器的屏幕坐标，单位像素，支持百分比。
{{ if: ${hasCoord} }}
2. 用 [coord](~series-${seriesType}.markLine.data.0.coord) 属性指定数据在相应坐标系上的坐标位置，单个维度支持设置 `'min'`, `'max'`, `'average'`。
{{ /if }}{{ if: ${hasType} }}
3. 直接用 [type](~series-${seriesType}.markLine.data.0.type) 属性标注系列中的最大值，最小值。这时候可以使用 [valueIndex](~series-${seriesType}.markLine.data.0.valueIndex) 或者 [valueDim](~series-${seriesType}.markLine.data.0.valueDim) 指定是在哪个维度上的最大值、最小值、平均值。

4. 如果是笛卡尔坐标系的话，也可以通过只指定 `xAxis` 或者 `yAxis` 来实现 X 轴或者 Y 轴为某值的标线，见示例 [scatter-weight](${galleryEditorPath}scatter-weight)
{{ /if }}
当多个属性同时存在时，优先级按上述的顺序。

{{if: ${hasType} }}
也可以是直接通过 `type` 设置该标线的类型，是最大值的线还是平均线。同样的，这时候可以通过使用 `valueIndex` 指定维度。
{{ /if }}
```
data: [
    {{if: ${hasType} }}{
        name: '平均线',
        // 支持 'average', 'min', 'max'
        type: 'average'
    },
    {
        name: 'Y 轴值为 100 的水平线',
        yAxis: 100
    },
    [
        {
            // 起点和终点的项会共用一个 name
            name: '最小值到最大值',
            type: 'min'
        },
        {
            type: 'max'
        }
    ],
    {{/if}}{{if: ${hasCoord} }}[
        {
            name: '两个坐标之间的标线',
            coord: [10, 20]
        },
        {
            coord: [20, 30]
        }
    ], [{
        // 固定起点的 x 像素位置，用于模拟一条指向最大值的水平线
        yAxis: 'max',
        x: '90%'
    }, {
        type: 'max'
    }],
    {{/if}}[
        {
            name: '两个屏幕坐标之间的标线',
            x: 100,
            y: 100
        },
        {
            x: 500,
            y: 200
        }
    ]
]
```

###${prefix} 0(Object)
起点的数据。
{{ use: mark-line-data-item-item(
    name="起点",
    prefix="###"+${prefix},
    hasCoord=${hasCoord},
    hasType=${hasType},
    index=0
) }}

###${prefix} 1(Object)
终点的数据。
{{ use: mark-line-data-item-item(
    name="终点",
    prefix="###"+${prefix},
    hasCoord=${hasCoord},
    hasType=${hasType},
    index=1
) }}

{{ use: partial-animation(
    prefix="#" + ${prefix},
    galleryEditorPath=${galleryEditorPath},
) }}


{{ target: mark-line-label }}
#${prefix} show(boolean) = ${defaultShowLabel|default(true)}
是否显示标签。
#${prefix} position(string) = 'end'
标签位置。

**可选:**
+ `'start'` 线的起始点。
+ `'middle'` 线的中点。
+ `'end'`   线的结束点。
#${prefix} formatter(string|Function)
{{ use: partial-1d-data-label-formatter }}



{{ target: mark-line-data-item-item }}
{{ if: ${hasType} }}
#${prefix} type(string)
特殊的标注类型，用于标注最大值最小值等。

**可选:**
+ `'min'` 最小值。
+ `'max'` 最大值。
+ `'average'` 平均值。
{{ /if }}
{{ if: ${hasCoord} }}
#${prefix} valueIndex(number)
在使用 [type](~series-${seriesType}.markLine.data.type) 时有效，用于指定在哪个维度上指定最大值最小值，可以是 `0`（xAxis, radiusAxis），`1`（yAxis, angleAxis），默认使用第一个数值轴所在的维度。

#${prefix} valueDim(string)
在使用 [type](~series-${seriesType}.markLine.data.type) 时有效，用于指定在哪个维度上指定最大值最小值。这可以是维度的直接名称，例如折线图时可以是`x`、`angle`等、candlestick 图时可以是`open`、`close`等维度名称。

#${prefix} coord(Array)
起点或终点的坐标。坐标格式视系列的坐标系而定，可以是[直角坐标系](~grid)上的 `x`, `y`，也可以是[极坐标系](~polar)上的 `radius`, `angle`。

{{ use: marker-coord-explain }}

{{ /if }}

#${prefix} name(string) = '${name}'
标注名称，将会作为文字显示。

#${prefix} x(number)
相对容器的屏幕 x 坐标，单位像素。

#${prefix} y(number)
相对容器的屏幕 y 坐标，单位像素。

#${prefix} value(number)
标注值，可以不设。

{{ use:partial-symbol(
    prefix=${prefix},
    name=${index} === 0 ? '起点' : '终点'
) }}

#${prefix} lineStyle(Object)
该数据项线的样式，起点和终点项的 `lineStyle` 会合并到一起。
{{ use: partial-line-style(
    prefix="#"+${prefix},
    hasCurveness=true
) }}

#${prefix} label(Object)
该数据项标签的样式，起点和终点项的 `label` 会合并到一起。
{{ use: mark-line-label(
    prefix='#'+${prefix}
) }}

#${prefix} emphasis(Object)
##${prefix} lineStyle(Object)
{{ use: partial-line-style(
    prefix="##"+${prefix},
    hasCurveness=true
) }}
##${prefix} label(Object)
{{ use: mark-line-label(
    prefix='##'+${prefix}
) }}