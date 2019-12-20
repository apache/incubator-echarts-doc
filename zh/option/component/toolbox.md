{{ target: feature-icon-style }}

#${prefix} iconStyle(Object)
${name} icon 样式设置。由于 icon 的文本信息只在 icon hover 时候才显示，所以文字相关的配置项请在 `emphasis` 下设置。
{{ use: partial-item-style(
    defaultBorderColor = '#666',
    defualtColor = 'none',
    defaultBorderWidth = 1,
    prefix="#" + ${prefix}
) }}


#${prefix} emphasis(Object)
##${prefix} iconStyle(Object)
{{ use: partial-item-style(prefix="##" + ${prefix}) }}
###${prefix} textPosition(string) = 'bottom'
文本位置，`'left'` / `'right'` / `'top'` / `'bottom'`。
###${prefix} textFill(string) = '#000'
文本颜色，如果未设定，则依次取图标 emphasis 时候的填充色、描边色，如果都不存在，则为 `'#000'`。
###${prefix} textAlign(string) = 'center'
文本对齐方式，`'left'` / `'center'` / `'right'`。
###${prefix} textBackgroundColor(string)
文本区域填充色。
###${prefix} textBorderRadius(number)
文本区域圆角大小。
###${prefix} textPadding(number)
文本区域内边距。


{{ target: feature-common}}

#### show(boolean) = true
是否显示该工具。默认显示。

#### title(boolean) = '${title}'

#### icon
{{ use: partial-icon-image-path }}

{{ use: feature-icon-style(name=${title}, prefix="###") }}



{{ target: component-toolbox }}

# toolbox(Object)

工具栏。内置有[导出图片](~toolbox.feature.saveAsImage)、[数据视图](~toolbox.feature.dataView)、[动态类型切换](~toolbox.feature.magicType)、[数据区域缩放](~toolbox.feature.dataZoom)、[重置](~toolbox.feature.reset)五个工具。

**例如：**

~[600x400](${galleryViewPath}line-marker&reset=1&edit=1)

{{use: partial-component-id(prefix="#")}}

## show(boolean) = true

是否显示工具栏组件。默认显示。

## orient(string) = 'horizontal'

工具栏 icon 的布局朝向。

**可选：**
+ 'horizontal'
+ 'vertical'

## itemSize(number) = 15

工具栏 icon 的大小。

## itemGap(number) = 10

工具栏 icon 每项之间的间隔。横向布局时为水平间隔，纵向布局时为纵向间隔。

## showTitle(boolean) = true

是否在鼠标 hover 的时候显示每个工具 icon 的标题。默认显示。

## feature(Object)
各工具配置项。

除了各个内置的工具按钮外，还可以自定义工具按钮。

**注意：**自定义的工具名字，只能以 `my` 开头，如 `myTool1`，`myTool2`。
**例如：**

```javascript
{
    toolbox: {
        feature: {
            myTool1: {
                show: true,
                title: '自定义扩展方法1',
                icon: 'path://M432.45,595.444c0,2.177-4.661,6.82-11.305,6.82c-6.475,0-11.306-4.567-11.306-6.82s4.852-6.812,11.306-6.812C427.841,588.632,432.452,593.191,432.45,595.444L432.45,595.444z M421.155,589.876c-3.009,0-5.448,2.495-5.448,5.572s2.439,5.572,5.448,5.572c3.01,0,5.449-2.495,5.449-5.572C426.604,592.371,424.165,589.876,421.155,589.876L421.155,589.876z M421.146,591.891c-1.916,0-3.47,1.589-3.47,3.549c0,1.959,1.554,3.548,3.47,3.548s3.469-1.589,3.469-3.548C424.614,593.479,423.062,591.891,421.146,591.891L421.146,591.891zM421.146,591.891',
                onclick: function (){
                    alert('myToolHandler1')
                }
            },
            myTool2: {
                show: true,
                title: '自定义扩展方法',
                icon: 'image://http://echarts.baidu.com/images/favicon.png',
                onclick: function (){
                    alert('myToolHandler2')
                }
            }
        }
    }
}
```

### saveAsImage(Object)
保存为图片。
#### type(string) = 'png'
保存的图片格式。支持 `'png'` 和 `'jpeg'`。
#### name(string)
保存的文件名称，默认使用 [title.text](~title.text) 作为名称。
#### backgroundColor(Color) = 'auto'
保存的图片背景色，默认使用 [backgroundColor](~backgroundColor)，如果 `backgroundColor` 不存在的话会取白色。
#### connectedBackgroundColor(Color) = '#fff'
如果图表使用了 [echarts.connect](api.html#echarts.connect) 对多个图表进行联动，则在导出图片时会导出这些联动的图表。该配置项决定了图表与图表之间间隙处的填充色。
#### excludeComponents(Array) = ['toolbox']
保存为图片时忽略的组件列表，默认忽略工具栏。
{{ use: feature-common(title="保存为图片") }}
#### pixelRatio(number) = 1
保存图片的分辨率比例，默认跟容器相同大小，如果需要保存更高分辨率的，可以设置为大于 1 的值，例如 2。

### restore(Object)
配置项还原。
{{ use: feature-common(title="还原") }}

### dataView(Object)
数据视图工具，可以展现当前图表所用的数据，编辑后可以动态更新。
{{ use: feature-common(title="数据视图") }}
#### readOnly(boolean) = false
是否不可编辑（只读）。
#### optionToContent(Function)
```js
(option:Object) => HTMLDomElement|string
```

自定义 dataView 展现函数，用以取代默认的 textarea 使用更丰富的数据编辑。可以返回 dom 对象或者 html 字符串。

如下示例使用表格展现数据值：
```js
optionToContent: function(opt) {
    var axisData = opt.xAxis[0].data;
    var series = opt.series;
    var table = '<table style="width:100%;text-align:center"><tbody><tr>'
                 + '<td>时间</td>'
                 + '<td>' + series[0].name + '</td>'
                 + '<td>' + series[1].name + '</td>'
                 + '</tr>';
    for (var i = 0, l = axisData.length; i < l; i++) {
        table += '<tr>'
                 + '<td>' + axisData[i] + '</td>'
                 + '<td>' + series[0].data[i] + '</td>'
                 + '<td>' + series[1].data[i] + '</td>'
                 + '</tr>';
    }
    table += '</tbody></table>';
    return table;
}
```

#### contentToOption(Function)
```js
(container:HTMLDomElement, option:Object) => Object
```

在使用 optionToContent 的情况下，如果支持数据编辑后的刷新，需要自行通过该函数实现组装 option 的逻辑。

#### lang(Array) = ['数据视图', '关闭', '刷新']
数据视图上有三个话术，默认是`['数据视图', '关闭', '刷新']`。
#### backgroundColor(string) = '#fff'
数据视图浮层背景色。
#### textareaColor(string) = '#fff'
数据视图浮层文本输入区背景色。
#### textareaBorderColor(string) = '#333'
数据视图浮层文本输入区边框颜色。
#### textColor(string) = '#000'
文本颜色。
#### buttonColor(string) = '#c23531'
按钮颜色。
#### buttonTextColor(string) = '#fff'
按钮文本颜色。

### dataZoom(Object)
数据区域缩放。目前只支持直角坐标系的缩放。
{{ use: feature-common(title="数据区域缩放") }}

#### xAxisIndex(number|Array|boolean)
指定哪些 [xAxis](~xAxis) 被控制。如果缺省则控制所有的x轴。如果设置为 `false` 则不控制任何x轴。如果设置成 `3` 则控制 axisIndex 为 `3` 的x轴。如果设置为 `[0, 3]` 则控制 axisIndex 为 `0` 和 `3` 的x轴。
#### yAxisIndex(number|Array|boolean)
指定哪些 [yAxis](~yAxis) 被控制。如果缺省则控制所有的y轴。如果设置为 `false` 则不控制任何y轴。如果设置成 `3` 则控制 axisIndex 为 `3` 的y轴。如果设置为 `[0, 3]` 则控制 axisIndex 为 `0` 和 `3` 的y轴。
#### icon(Object)
缩放和还原的 icon path。
##### zoom(string)
{{ use: partial-icon-image-path }}
##### back(string)
{{ use: partial-icon-image-path }}
#### title(Object)
缩放和还原的标题文本。
##### zoom(string) = '区域缩放'
##### back(string) = '区域缩放还原'


### magicType(Object)
动态类型切换。

**例如：**
```js
feature: {
    magicType: {
        type: ['line', 'bar', 'stack', 'tiled']
    }
}
```
#### show(boolean) = true
是否显示该动态类型切换。默认显示。
#### type(Array)
启用的动态类型，包括`'line'`（切换为折线图）、 `'bar'`（切换为柱状图）、 `'stack'`（切换为堆叠模式）、 `'tiled'`（切换为平铺模式）。
{{ use: feature-common(title="动态类型切换") }}
#### icon(Object)
各个类型的 icon path，可以分别配置。
##### line(string)
{{ use: partial-icon-image-path }}
##### bar(string)
{{ use: partial-icon-image-path }}
##### stack(string)
{{ use: partial-icon-image-path }}
##### tiled(string)
{{ use: partial-icon-image-path }}
#### title(Object)
各个类型的标题文本，可以分别配置。
##### line(string) = '切换为折线图'
##### bar(string) = '切换为柱状图'
##### stack(string) = '切换为堆叠'
##### tiled(string) = '切换为平铺'
#### option(Object)
各个类型的专有配置项。在切换到某类型的时候会合并相应的配置项。
##### line(Object)
##### bar(Object)
##### stack(Object)
##### tiled(Object)
#### seriesIndex(Object)
各个类型对应的系列的列表。
##### line(Array)
##### bar(Array)
##### stack(Array)
##### tiled(Array)


### brush(Object)
选框组件的控制按钮。

也可以不在这里指定，而是在 [brush.toolbox](~brush.toolbox) 中指定。

#### type(Array)
使用的按钮。

**可选：**

+ `'rect'`：开启矩形选框选择功能。
+ `'polygon'`：开启任意形状选框选择功能。
+ `'lineX'`：开启横向选择功能。
+ `'lineY'`：开启纵向选择功能。
+ `'keep'`：切换单选和多选模式。后者可支持同时画多个选框。前者支持单击清除所有选框。
+ `'clear'`：清空所有选框。


#### icon(Object)
每个按钮的 icon path。
##### rect(string)
{{ use: partial-icon-image-path }}
##### polygon(string)
{{ use: partial-icon-image-path }}
##### lineX(string)
{{ use: partial-icon-image-path }}
##### lineY(string)
{{ use: partial-icon-image-path }}
##### keep(string)
{{ use: partial-icon-image-path }}
##### clear(string)
{{ use: partial-icon-image-path }}
#### title(Object)
标题文本。
##### rect(string) = '矩形选择'
##### polygon(string) = '圈选'
##### lineX(string) = '横向选择'
##### lineY(string) = '纵向选择'
##### keep(string) = '保持选择'
##### clear(string) = '清除选择'


{{ use: feature-icon-style(name="公用的", prefix="#") }}

{{ use: partial-rect-layout-width-height(componentName="工具栏") }}


## tooltip(Object)

工具箱的 tooltip 配置，配置项同 [tooltip](~tooltip)。默认不显示，可以在需要特殊定制文字样式（尤其是想用自定义 CSS 控制文字样式）的时候开启 tooltip。

**例如：**

```js
option = {
    tooltip: {
        show: true // 必须引入 tooltip 组件
    },
    toolbox: {
        show: true,
        showTitle: false, // 隐藏默认文字，否则两者位置会重叠
        feature: {
            saveAsImage: {
                show: true,
                title: 'Save As Image'
            },
            dataView: {
                show: true,
                title: 'Data View'
            },
        },
        tooltip: { // 和 option.tooltip 的配置项相同
            show: true,
            formatter: function (param) {
                return return '<div>' + param.title + '</div>'; // 自定义的 DOM 结构
            },
            backgroundColor: '#222',
            textStyle: {
                fontSize: 12,
            },
            extraCssText: 'box-shadow: 0 0 3px rgba(0, 0, 0, 0.3);' // 自定义的 CSS 样式
        }
    },
    ...
}
```
