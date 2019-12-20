
{{target: series-heatmap}}

# series.heatmap(Object)
**热力图**

热力图主要通过颜色去表现数值的大小，必须要配合 [visualMap](~visualMap) 组件使用。

可以应用在[直角坐标系](~grid)以及[地理坐标系](~geo)上，这两个坐标系上的表现形式相差很大，直角坐标系上必须要使用两个类目轴。

下面是在直角坐标系上应用的例子：

**直角坐标系：** 
~[600x400](${galleryViewPath}heatmap-cartesian&edit=1&reset=1)

## type(string) = 'heatmap'

{{use: partial-component-id(prefix="#")}}

{{ use: partial-series-name() }}

{{use: partial-coord-sys(
    seriesType="heatmap",
    coordSysDefault="'cartesian2d'",
    cartesian2d=true,
    polar=false,
    geo=true,
    calendar=true
)}}

## pointSize(number) = 20
每个点的大小，在地理坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'geo')上有效。

## blurSize(number) = 20
每个点模糊的大小，在地理坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'geo')上有效。

## minOpacity(number) = 0
最小的透明度，在地理坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'geo')上有效。

## maxOpacity(number) = 1
最大的透明度，在地理坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'geo')上有效。

{{ use:partial-progressive(
    prefix='#'
) }}

## label(Object)
在直角坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'cartesian2d')上有效。
{{ use:partial-label(
    prefix="##",
    defaultPosition="inside"
) }}

## itemStyle(Object)
样式设置，在直角坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'cartesian2d')上有效。
{{use:partial-item-style(prefix="##")}}


## emphasis(Object)

### itemStyle(Object)
{{use:partial-item-style(prefix="###")}}
### label(Object)
{{use:partial-label(prefix="###",
    defaultPosition="inside"
)}}

## data(Array)

{{ use: partial-2d-data-desc(
    galleryEditorPath = ${galleryEditorPath}
) }}

### name(string)
数据项名称。

### value(Array)
数据项值。

### label(Object)
在直角坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'cartesian2d')上有效。
{{ use:partial-label(
    prefix="###",
    defaultPosition="inside"
) }}

### itemStyle(Object)
单个数据点的样式设置，在直角坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'cartesian2d')上有效。
{{use:partial-item-style(prefix="###")}}


### emphasis(Object)

#### itemStyle(Object)
{{use:partial-item-style(prefix="####")}}

#### label(Object)
{{use:partial-label(prefix="####",
    defaultPosition="inside"
)}}

{{use: partial-marker(
    prefix="#",
    galleryEditorPath=${galleryEditorPath},
    seriesType="heatmap"
)}}

{{use:partial-z-zlevel(
    prefix="#",
    componentName="热力图"
) }}

{{ use:partial-silent(
    prefix="#"
) }}

{{use: partial-tooltip-in-series(
    galleryViewPath=${galleryViewPath}
)}}
