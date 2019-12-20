
{{target: series-funnel}}

# series.funnel(Object)

**漏斗图**

 **例如：** 
~[600x400](${galleryViewPath}funnel&reset=1&edit=1)

## type(string) = 'funnel'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}

## min(number) = 0
指定的数据最小值。

## max(number) = 100
指定的数据最大值。

## minSize(string) = '0%'
数据最小值 [min](~series-funnel.min) 映射的宽度。

可以是绝对的像素大小，也可以是相对[布局宽度](~series-funnel.width)的百分比，如果需要最小值的图形并不是尖端三角，可通过设置该属性实现。

## maxSize(string) = '100%'
数据最大值 [max](~series-funnel.max) 映射的宽度。

可以是绝对的像素大小，也可以是相对[布局宽度](~series-funnel.width)的百分比。

## sort(string) = 'descending'
数据排序， 可以取 `'ascending'`，`'descending'`，`'none'`（表示按 data 顺序），或者一个函数（即 `Array.prototype.sort(function (a, b) { ... })`）。

## gap(number) = 0
数据图形间距。

{{ use: partial-legend-hover-link }}

## funnelAlign(string) = 'center'
水平方向对齐布局类型，默认居中对齐，可用选项还有：'left' | 'right' | 'center'


## label(Object)
{{use:partial-label-desc(name="漏斗图")}}
{{use:partial-funnel-label(
    prefix="##",
    position=true,
    formatter=true
)}}

## labelLine(Object)
标签的视觉引导线样式，在 [label 位置](~series-funnel.label.position) 设置为`'left'`或者`'right'`的时候会显示视觉引导线。
{{ use: partial-funnel-label-line(
    prefix='##',
    length=true
)}}

## itemStyle(Object)
{{use:partial-item-style-desc}}
{{use:partial-item-style(
    prefix="##",
    useColorPalatte=true,
    hasCallback=true
)}}

## emphasis(Object)
高亮的标签和图形样式。

### label(Object)
{{use:partial-funnel-label(
    prefix="###",
    position=false,
    formatter=true
)}}

### labelLine(Object)
{{ use: partial-funnel-label-line(
    prefix='###',
    length=false
)}}

### itemStyle(Object)
{{use:partial-item-style(prefix="###")}}


{{ use: component-rect-layout-width-height(
    componentName="漏斗图",
    defaultLeft=80,
    defaultTop=60,
    defaultRight=80,
    defaultBottom=60
) }}

{{ use: partial-seriesLayoutBy }}

{{ use: partial-datasetIndex }}

{{use:partial-series-dimensions(
    prefix="#"
)}}

{{use:partial-series-encode(
    prefix="#"
)}}

## data(Array)
{{ use: partial-1d-data-desc }}
### name(string)
数据项名称。
### value(number)
数据值。
### itemStyle(Object)
{{use:partial-item-style-desc}}
{{use:partial-item-style(prefix="###")}}
#### height(string|number)
该数据项的高度。默认平均分配高度，如果需要修改，可以将其设为百分比（如：`'10%'`）或像素值（如：`20px`）。需要注意总和应为 100%。

### label(Object)
单个数据的标签配置。
{{use:partial-funnel-label(
    prefix="###",
    position=true,
    formatter=false
)}}


### labelLine(Object)
{{ use: partial-funnel-label-line(
    prefix='###',
    length=true
)}}

### itemStyle(Object)
{{use:partial-item-style-desc}}
{{use:partial-item-style(prefix="###")}}


### emphasis(Object)

#### itemStyle(Object)
{{use:partial-item-style(prefix="####")}}

#### label(Object)
{{use:partial-funnel-label(
    prefix="####",
    position=false,
    formatter=false
)}}

#### labelLine(Object)
{{use:partial-funnel-label-line(
    prefix="####",
    length=false
)}}



{{use: partial-tooltip-in-series-data(
    galleryViewPath=${galleryViewPath}
)}}

{{use: partial-marker(
    prefix="#",
    galleryEditorPath=${galleryEditorPath},
    seriesType="funnel"
)}}

{{ use:partial-silent(
    prefix="#"
) }}

{{use:partial-animation(
    prefix="#",
    galleryEditorPath=${galleryEditorPath}
)}}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}



{{ target: partial-funnel-label }}
#${prefix} show(boolean) = false
{{ if: ${position} }}
#${prefix} position(string) = 'outside'
标签的位置。

**可选：**
+ `'left'`

    漏斗图左侧，通过[视觉引导线](~series-funnel.labelLine)连到相应的梯形。

+ `'right'`

    漏斗图右侧，通过[视觉引导线](~series-funnel.labelLine)连到相应的梯形。

+ `'inside'`

    漏斗图梯形内部。

+ `'insideRight'`

    漏斗图梯形内部右侧。

+ `'insideLeft'`

    漏斗图梯形内部左侧。

+ `'leftTop'`

     漏斗图左侧上部。

 + `'leftBottom'`

     漏斗图左侧下部。

 + `'rightTop'`

     漏斗图右侧上部。

 + `'rightBottom'`

     漏斗图右侧下部。

+ `'inner'` 同 `'inside'`。
+ `'center'` 同 `'inside'`。

{{ /if }}
{{ if: ${formatter} }}
#${prefix} formatter(string|Function)
{{ use: partial-1d-data-label-formatter(extra = {
    percent: {
        desc: '百分比',
        type: 'number'
    }
}) }}
{{ /if }}

{{ use:partial-text-style(prefix=${prefix}) }}


{{ target: partial-funnel-label-line }}
#${prefix} show(boolean)
是否显示视觉引导线。
{{ if: ${length} }}
#${prefix} length(number)
视觉引导线的长度。
{{ /if }}
#${prefix} lineStyle(Object)
{{use:partial-line-style(prefix="#" + ${prefix})}}
