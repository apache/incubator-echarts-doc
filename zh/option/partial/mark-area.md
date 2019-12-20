{{ target: partial-mark-area }}

#${prefix} markArea(Object)
图表标域，常用于标记图表中某个范围的数据，例如标出某段时间投放了广告。

{{ use: partial-silent(prefix="#" + ${prefix}) }}

##${prefix} label(Object)
标域文本配置。
{{ use: partial-label(
    prefix=${prefix} + '##'
) }}

##${prefix} itemStyle(Object)
该标域的样式。
{{ use: partial-item-style(prefix="##" + ${prefix}) }}

##${prefix} emphasis(Object)
高亮的标域样式
###${prefix} label(Object)
{{ use: partial-label(
    prefix=${prefix} + '###'
) }}
###${prefix} itemStyle
{{ use: partial-item-style(prefix="###" + ${prefix}) }}


##${prefix} data
标域的数据数组。每个数组项是一个两个项的数组，分别表示标域左上角和右下角的位置，每个项支持通过下面几种方式指定自己的位置。

1. 通过 [x](~series-${seriesType}.markArea.data.0.x), [y](~series-${seriesType}.markArea.data.0.y) 属性指定相对容器的屏幕坐标，单位像素，支持百分比。
{{ if: ${hasCoord} }}
2. 用 [coord](~series-${seriesType}.markArea.data.0.coord) 属性指定数据在相应坐标系上的坐标位置，单个维度支持设置 `'min'`, `'max'`, `'average'`。
{{ /if }}{{ if: ${hasType} }}
3. 直接用 [type](~series-${seriesType}.markArea.data.0.type) 属性标注系列中的最大值，最小值。这时候可以使用 [valueIndex](~series-${seriesType}.markArea.data.0.valueIndex) 或者 [valueDim](~series-${seriesType}.markPoint.data.0.valueDim) 指定是在哪个维度上的最大值、最小值、平均值。

4. 如果是笛卡尔坐标系的话，也可以通过只指定 `xAxis` 或者 `yAxis` 来实现 X 轴或者 Y 轴为某值的标域，见示例 [scatter-weight](${galleryEditorPath}scatter-weight)
{{ /if }}
当多个属性同时存在时，优先级按上述的顺序。

{{if: ${hasType} }}

{{ /if }}
```
data: [
    {{if: ${hasType} }}
    [
        {
            name: '平均值到最大值',
            type: 'average'
        },
        {
            type: 'max'
        }
    ],
    {{/if}}{{if: ${hasCoord} }}
    [
        {
            name: '两个坐标之间的标域',
            coord: [10, 20]
        },
        {
            coord: [20, 30]
        }
    ], [
        {
            name: '60分到80分',
            yAxis: 60
        },
        {
            yAxis: 80
        }
    ], [
        {
            name: '所有数据范围区间',
            coord: ['min', 'min']
        },
        {
            coord: ['max', 'max']
        }
    ],
    {{/if}}[
        {
            name: '两个屏幕坐标之间的标域',
            x: 100,
            y: 100
        }, {
            x: '90%',
            y: '10%'
        }
    ]
]
```

###${prefix} 0(Object)
标域左上角的数据
{{ use: mark-area-data-item-item(
    name="起点",
    prefix="###"+${prefix},
    hasCoord=${hasCoord},
    hasType=${hasType},
    index=0
) }}

###${prefix} 1(Object)
标域右下角的数据
{{ use: mark-area-data-item-item(
    name="终点",
    prefix="###"+${prefix},
    hasCoord=${hasCoord},
    hasType=${hasType},
    index=1
) }}

{{ use: partial-animation(
    prefix="#" + ${prefix},
    defaultAnimation='false',
    galleryEditorPath=${galleryEditorPath},
) }}


{{ target: mark-area-data-item-item }}
{{ if: ${hasType} }}
#${prefix} type(string)
特殊的标注类型，用于标注最大值最小值等。

**可选:**
+ `'min'` 最大值。
+ `'max'` 最大值。
+ `'average'` 平均值。
{{ /if }}
{{ if: ${hasCoord} }}
#${prefix} valueIndex(number)
在使用 [type](~series-${seriesType}.markArea.data.type) 时有效，用于指定在哪个维度上指定最大值最小值，可以是 `0`（xAxis, radiusAxis），`1`（yAxis, angleAxis），默认使用第一个数值轴所在的维度。

#${prefix} valueDim(string)
在使用 [type](~series-${seriesType}.markArea.data.type) 时有效，用于指定在哪个维度上指定最大值最小值。这可以是维度的直接名称，例如折线图时可以是`x`、`angle`等、candlestick 图时可以是`open`、`close`等维度名称。

#${prefix} coord(Array)
起点或终点的坐标。坐标格式视系列的坐标系而定，可以是[直角坐标系](~grid)上的 `x`, `y`，也可以是[极坐标系](~polar)上的 `radius`, `angle`。

{{ /if }}

#${prefix} name(string) = '${name}'
标注名称，将会作为文字显示。

#${prefix} x(number)
相对容器的屏幕 x 坐标，单位像素，支持百分比形式，例如 `'20%'`。

#${prefix} y(number)
相对容器的屏幕 y 坐标，单位像素，支持百分比形式，例如 `'20%'`。

#${prefix} value(number)
标域值，可以不设。

#${prefix} itemStyle(Object)
该数据项区域的样式，起点和终点项的`itemStyle`会合并到一起。
{{ use: partial-item-style(
    prefix="#"+${prefix}
) }}

#${prefix} label(Object)
该数据项标签的样式，起点和终点项的`label`会合并到一起。

{{ use: partial-label(
    prefix='#'+${prefix}
) }}

#${prefix} emphasis(Object)
##${prefix} itemStyle(Object)
{{ use: partial-item-style(
    prefix="##"+${prefix}
) }}
##${prefix} label(Object)
{{ use: partial-label(
    prefix='##'+${prefix}
) }}
