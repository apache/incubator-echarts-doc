{{target: component-data-zoom-slider}}

# dataZoom.slider(Object)

**滑动条型数据区域缩放组件（dataZoomSlider）**

（参考[数据区域缩放组件（dataZoom）的介绍](~dataZoom)）


<br>
<br>


## type(string) = 'slider'

{{use: partial-component-id(prefix="#")}}

## show(boolean) = true

是否显示 ${dataZoomName} 组件。默认显示。如果设置为 `false`，则不会显示，但是数据过滤的功能还存在。


## backgroundColor(Color) = 'rgba(47,69,84,0)'

组件的背景颜色。


## dataBackground(Object)

数据阴影的样式。

### lineStyle(Object)

阴影的线条样式

{{use:partial-line-style(
    prefix="###",
    defaultWidth=0.5,
    defaultOpacity=0.3,
    defaultColor='#2f4554'
)}}

### areaStyle(Object)

阴影的填充样式

{{use:partial-area-style(
    prefix="###",
    defaultOpacity=0.3,
    defaultColor='rgba(47,69,84,0.3)'
)}}


## fillerColor(Color) = 'rgba(167,183,204,0.4)'

选中范围的填充颜色。

## borderColor(Color) = '#ddd'

边框颜色。


## handleIcon(string)

手柄的 icon 形状，支持路径字符串，默认为：
```js
'M8.2,13.6V3.9H6.3v9.7H3.1v14.9h3.3v9.7h1.8v-9.7h3.3V13.6H8.2z M9.7,24.4H4.8v-1.4h4.9V24.4z M9.7,19.1H4.8v-1.4h4.9V19.1z'
```

{{ use: partial-icon-image-path }}

自定义 icon 见 [示例 area-simple](${galleryEditorPath}area-simple)

## handleSize(number) = '100%'

控制手柄的尺寸，可以是像素大小，也可以是相对于 dataZoom 组件宽度的百分比，默认跟 dataZoom 宽度相同。

## handleStyle(Object)

手柄的样式配置，见 [示例 area-simple](${galleryEditorPath}area-simple)

{{use: partial-item-style(
    prefix="##",
    defaultColor="#a7b7cc"
)}}


## labelPrecision(number) = 'auto'

显示label的小数精度。默认根据数据自动决定。


## labelFormatter(string|Function) = null

显示的label的格式化器。

+ 如果为 `string`，表示模板，例如：`aaaa{value}bbbb`，其中`{value}`会被替换为实际的数值。

+ 如果为 `Function`，表示回调函数，例如：

```javascript
/**
 * @param {*} value 如果 axis.type 为 'category'，则 `value` 为 axis.data 的 index。
 *                  否则 `value` 是当前值。
 * @param {strign} valueStr 内部格式化的结果。
 * @return {string} 返回最终的label内容。
 */
labelFormatter: function (value) {
    return 'aaa' + value + 'bbb';
}
```


## showDetail(boolean) = true

是否显示 detail，即拖拽时候显示详细数值信息。


## showDataShadow(string) = 'auto'

是否在 `dataZoom-silder` 组件中显示数据阴影。默认显示。数据阴影可以简单地反应数据走势。


## realtime(boolean) = true

拖动时，是否实时更新系列的视图。如果设置为 `false`，则只在拖拽结束的时候更新。


## textStyle

{{ use:partial-simple-text-style(
    prefix='##',
    name='dataZoom ',
    defaultColor='#333'
) }}





{{ use: partial-data-zoom-common(
    dataZoomName='dataZoom-slider',
    galleryEditorPath=${galleryEditorPath},
    galleryViewPath=${galleryViewPath}
) }}

{{ use: partial-rect-layout(
    componentName='dataZoom-slider'
) }}
