
{{ target: series-heatmap }}

# series.heatmap(Object)

**热力图**

热力图主要通过颜色去表现数值的大小，必须要配合 [visualMap](~visualMap) 组件使用。

可以应用在[直角坐标系](~grid)以及[地理坐标系](~geo)上，这两个坐标系上的表现形式相差很大，直角坐标系上必须要使用两个类目轴。

下面是在直角坐标系上应用的例子：

**直角坐标系：**
~[600x400](${galleryViewPath}heatmap-cartesian&edit=1&reset=1)

<ExampleBaseOption name="heatmap" title="直角坐标系热力图" title-en="Heatmap on Cartesian">
const hours = ['12a', '1a', '2a', '3a', '4a', '5a', '6a',
        '7a', '8a', '9a','10a','11a',
        '12p', '1p', '2p', '3p', '4p', '5p',
        '6p', '7p', '8p', '9p', '10p', '11p'];
const days = ['Saturday', 'Friday', 'Thursday',
        'Wednesday', 'Tuesday', 'Monday', 'Sunday'];

const data = [[0,0,5],[0,1,1],[0,2,0],[0,3,0],[0,4,0],[0,5,0],[0,6,0],[0,7,0],[0,8,0],[0,9,0],[0,10,0],[0,11,2],[0,12,4],[0,13,1],[0,14,1],[0,15,3],[0,16,4],[0,17,6],[0,18,4],[0,19,4],[0,20,3],[0,21,3],[0,22,2],[0,23,5],[1,0,7],[1,1,0],[1,2,0],[1,3,0],[1,4,0],[1,5,0],[1,6,0],[1,7,0],[1,8,0],[1,9,0],[1,10,5],[1,11,2],[1,12,2],[1,13,6],[1,14,9],[1,15,11],[1,16,6],[1,17,7],[1,18,8],[1,19,12],[1,20,5],[1,21,5],[1,22,7],[1,23,2],[2,0,1],[2,1,1],[2,2,0],[2,3,0],[2,4,0],[2,5,0],[2,6,0],[2,7,0],[2,8,0],[2,9,0],[2,10,3],[2,11,2],[2,12,1],[2,13,9],[2,14,8],[2,15,10],[2,16,6],[2,17,5],[2,18,5],[2,19,5],[2,20,7],[2,21,4],[2,22,2],[2,23,4],[3,0,7],[3,1,3],[3,2,0],[3,3,0],[3,4,0],[3,5,0],[3,6,0],[3,7,0],[3,8,1],[3,9,0],[3,10,5],[3,11,4],[3,12,7],[3,13,14],[3,14,13],[3,15,12],[3,16,9],[3,17,5],[3,18,5],[3,19,10],[3,20,6],[3,21,4],[3,22,4],[3,23,1],[4,0,1],[4,1,3],[4,2,0],[4,3,0],[4,4,0],[4,5,1],[4,6,0],[4,7,0],[4,8,0],[4,9,2],[4,10,4],[4,11,4],[4,12,2],[4,13,4],[4,14,4],[4,15,14],[4,16,12],[4,17,1],[4,18,8],[4,19,5],[4,20,3],[4,21,7],[4,22,3],[4,23,0],[5,0,2],[5,1,1],[5,2,0],[5,3,3],[5,4,0],[5,5,0],[5,6,0],[5,7,0],[5,8,2],[5,9,0],[5,10,4],[5,11,1],[5,12,5],[5,13,10],[5,14,5],[5,15,7],[5,16,11],[5,17,6],[5,18,0],[5,19,5],[5,20,3],[5,21,4],[5,22,2],[5,23,0],[6,0,1],[6,1,0],[6,2,0],[6,3,0],[6,4,0],[6,5,0],[6,6,0],[6,7,0],[6,8,0],[6,9,0],[6,10,1],[6,11,0],[6,12,2],[6,13,1],[6,14,3],[6,15,4],[6,16,0],[6,17,0],[6,18,0],[6,19,0],[6,20,1],[6,21,2],[6,22,2],[6,23,6]].map(function (item) {
    return [item[1], item[0], item[2] || '-'];
});

option = {
    tooltip: {
        position: 'top'
    },
    animation: false,
    grid: {
        height: '50%',
        top: '10%'
    },
    xAxis: {
        type: 'category',
        data: hours,
        splitArea: {
            show: true
        }
    },
    yAxis: {
        type: 'category',
        data: days,
        splitArea: {
            show: true
        }
    },
    visualMap: {
        min: 0,
        max: 10,
        calculable: true,
        orient: 'horizontal',
        left: 'center',
        bottom: '15%'
    },
    series: [{
        name: 'Punch Card',
        type: 'heatmap',
        data: data
    }]
};
</ExampleBaseOption>

## type(string) = 'heatmap'

{{ use: partial-component-id(
    prefix = "#"
) }}

{{ use: partial-series-name() }}

{{ use: partial-coord-sys(
    seriesType = "heatmap",
    coordSysDefault = "'cartesian2d'",
    cartesian2d = true,
    polar = false,
    geo = true,
    calendar = true
) }}

## pointSize(number) = 20

每个点的大小，在地理坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'geo')上有效。

## blurSize(number) = 20

每个点模糊的大小，在地理坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'geo')上有效。

## minOpacity(number) = 0

最小的透明度，在地理坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'geo')上有效。

## maxOpacity(number) = 1

最大的透明度，在地理坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'geo')上有效。

{{ use: partial-progressive(
    prefix = '#'
) }}

## label(Object)

在直角坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'cartesian2d')上有效。

{{ use: partial-label(
    prefix = "##",
    defaultPosition = "inside"
) }}

## labelLayout(Object|Function)

{{ use: partial-label-layout(
    prefix = "##"
) }}

## itemStyle(Object)

样式设置，在直角坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'cartesian2d')上有效。

{{ use: partial-item-style(
    prefix = "##"
) }}

## emphasis(Object)

高亮状态的图形样式。

{{ use: partial-focus-blur-scope() }}

{{ use: heatmap-state(
    prefix = "##"
) }}

## blur(Object)

{{ use: partial-version(
    version = "5.0.0"
) }}

淡出状态的图形样式。开启 [emphasis.focus](~series-heatmap.emphasis.focus) 后有效。

{{ use: heatmap-state(
    prefix = "##"
) }}

## select(Object)

{{ use: partial-version(
    version = "5.0.0"
) }}

选中状态的图形样式。开启 [selectedMode](~series-heatmap.selectedMode) 后有效。

{{ use: heatmap-state(
    prefix = "##"
) }}

{{ use: partial-selected-mode(
    version = '5.0.0'
) }}

## strictlyAligned(boolean) = false

{{ use: partial-strictly-aligned }}

## data(Array)

{{ use: partial-2d-data-desc() }}

### name(string)

数据项名称。

### value(Array)

数据项值。

### label(Object)

在直角坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'cartesian2d')上有效。

{{ use: partial-label(
    prefix = "###",
    defaultPosition = "inside"
) }}

### itemStyle(Object)

单个数据点的样式设置，在直角坐标系([coordinateSystem](~series-heatmap.coordinateSystem): 'cartesian2d')上有效。

{{ use: partial-item-style(
    prefix = "###"
) }}

### emphasis(Object)

#### itemStyle(Object)

{{ use: partial-item-style(
    prefix = "####"
) }}

#### label(Object)

{{ use: partial-label(
    prefix = "####",
    defaultPosition = "inside"
) }}

{{ use: partial-marker(
    prefix = "#",
    seriesType = "heatmap"
) }}

{{ use: partial-z-zlevel(
    prefix = "#",
    componentName = "热力图"
) }}

{{ use: partial-silent(
    prefix = "#"
) }}

{{ use: partial-tooltip-in-series() }}



{{ target: heatmap-state }}

#${prefix} itemStyle(Object)

{{ use: partial-item-style(
    prefix = "#" + ${prefix}
) }}

#${prefix} label(Object)

{{ use: partial-label(
    prefix = "#" + ${prefix},
    defaultPosition = "inside"
) }}

