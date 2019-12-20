{{ target: component-geo }}

# geo(Object)

地理坐标系组件。

地理坐标系组件用于地图的绘制，支持在地理坐标系上绘制[散点图](~series-scatter)、[线集](~series-lines)。

`3.1.10` 开始 geo 组件也支持鼠标事件。事件参数为
```js
{
    componentType: 'geo',
    // Geo 组件在 option 中的 index
    geoIndex: number,
    // 点击区域的名称，比如"上海"
    name: string,
    // 传入的点击区域的 region 对象，见 geo.regions
    region: Object
}
```

**Tip:**
geo 区域的颜色也可以被 map series 所控制，参见 [series-map.geoIndex](~series-map.geoIndex)。

{{use: partial-component-id(prefix="#")}}

## show(boolean) = true

是否显示地理坐标系组件。默认显示。

{{ use: geo-common(
    prefix='#',
    galleryEditorPath=${galleryEditorPath},
    galleryViewPath=${galleryViewPath}
) }}


## regions(Array)
在地图中对特定的区域配置样式。

**例如：**
```js
regions: [{
    name: '广东',
    itemStyle: {
        areaColor: 'red',
        color: 'red'
    }
}]
```
geo 区域的颜色也可以被 map series 所控制，参见 [series-map.geoIndex](~series-map.geoIndex)。

### name(string)
地图区域的名称，例如 `'广东'`，`'浙江'`。

### selected(boolean) = false
该区域是否选中。

### itemStyle(Object)
该区域的多边形样式设置
#### areaColor(Color)
地图区域的颜色。
{{ use: partial-item-style(prefix='###') }}

### label(Object)
{{use: partial-label-desc}}
{{use: partial-label(
    prefix="###",
    formatter=true
)}}



### emphasis(Object)
高亮的样式。
#### itemStyle(Object)
##### areaColor(Color)
地图区域的颜色。
{{ use: partial-item-style(prefix='####') }}
#### label(Object)
{{use: partial-label(
    prefix="####",
    formatter=true
)}}


{{ use:partial-silent(
    prefix="#"
) }}
