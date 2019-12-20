
{{target: component-visual-map-continuous}}

# visualMap.continuous(Object)

**连续型视觉映射组件（visualMapContinuous）**

（参考[视觉映射组件（visualMap）的介绍](~visualMap)）


`visualMapContinuous`中，可以通过 [visualMap.calculable](~visualMap.calculable) 来显示或隐藏手柄（手柄能拖拽改变值域）。

<br>
<br>


## type(string) = continuous

类型为连续型。

{{use: partial-component-id(prefix="#")}}

## min(number)

指定 visualMapContinuous 组件的允许的最小值。`'min'` 必须用户指定。`[visualMap.min, visualMax.max]` 形成了视觉映射的『定义域』。


## max(number)

指定 visualMapContinuous 组件的允许的最大值。`'max'` 必须用户指定。`[visualMap.min, visualMax.max]` 形成了视觉映射的『定义域』。


## range(Array)

指定手柄对应数值的位置。`range` 应在 `min` `max` 范围内。

**例如：**

```javascript
chart.setOption({
    visualMap: {
        min: 0,
        max: 100,
        // 两个手柄对应的数值是 4 和 15
        range: [4, 15],
        ...
    }
});
```

setOption 改变 min、max 时 range 的自适应。

如果 `range` 不设置（或设置为 null）。

**例如：**

```javascript
chart.setOption({visualMap: {min: 10, max: 300}}); // 不设置 range，则 range 默认为 [min, max]，即 [10, 300]。

chart.setOption({visualMap: {min: 0, max: 400}}); // 再次使用 setOption 改变 min、max。
// 此时 range 也自然会更新成改变过后的 [min, max]，即 [0, 400]。
```

如果 `range` 被以具体值设置了（如设置为 [10, 300]）。

**例如：**

```javascript

chart.setOption({visualMap: {min: 10, max: 300, range: [20, 80]}}); // 设置了 range

chart.setOption({visualMap: {min: 0, max: 400}}); // 再次使用 setOption 改变 min、max。
// 此时 range 不会改变而仍维持本来的数值，仍为 [20, 80]。

chart.setOption({visualMap: {range: null}}); // 再把 range 设为 null。
// 则 range 恢复为 [min, max]，即 [0, 400]，同时也恢复了自动随 min max 而改变的能力。

```

`getOption` 得到的 `range` 总是 `Array`，不会为 `null` 或 `undefined`。


## calculable(boolean) = false

是否显示拖拽用的手柄（手柄能拖拽调整选中范围）。

（注：为兼容 ECharts2，当 [visualMap.type](~visualMap.type) 未指定时，假如设置了 `'calculable'`，则`type`自动被设置为`'continuous'`，无视 [visualMap-piecewise.splitNumber](~visualMap-piecewise.splitNumber) 等设置。所以，建议使用者不要不指定 [visualMap.type](~visualMap.type)，否则表意不清晰。）


## realtime(boolean) = true

拖拽时，是否实时更新。

+ 如果为`ture`则拖拽手柄过程中实时更新图表视图。

+ 如果为`false`则拖拽结束时，才更新视图。


## inverse(boolean) = false

是否反转 visualMap 组件。

当`inverse`为`false`时，数据大小的位置规则，和直角坐标系相同，即：

+ 当 [visualMap.orient](~visualMap.orient) 为`'vertical'`时，数据上大下小。
+ 当 [visualMap.orient](~visualMap.orient) 为`'horizontal'`时，数据右大左小。

当`inverse`为`true`时，相反。


## precision(number) = 0

数据展示的小数精度，默认为0，无小数点。


## itemWidth(number) = 20

图形的宽度，即长条的宽度。


## itemHeight(number) = 140

图形的高度，即长条的高度。


## align(string) = 'auto'

指定组件中手柄和文字的摆放位置，可选值为：

+ `'auto'` 自动决定。
+ `'left'` 手柄和label在右，orient 为 horizontal 时有效。
+ `'right'` 手柄和label在左，orient 为 horizontal 时有效。
+ `'top'` 手柄和label在下，orient 为 vertical 时有效。
+ `'bottom'` 手柄和label在上，orient 为 vertical 时有效。


## text(Array) = null

两端的文本，如 `['High', 'Low']`。[参见例子](${galleryEditorPath}doc-example/map-visualMap-continuous-text&edit=1&reset=1)。

`text` 中的顺序，其实试试就知道。若要看详细的规则，参见 [visualMap.inverse](~visualMap.inverse)。


## textGap(Array) = 10

两端文字主体之间的距离，单位为px。参见 [visualMap-continuous.text](~visualMap-continuous.text)


{{ use: partial-visual-map-common(
    visualMapName='visualMap-continuous',
    galleryEditorPath=${galleryEditorPath}
) }}


## formatter(string|Function)

标签的格式化工具。

+ 如果为`string`，表示模板，例如：`aaaa{value}`。其中 `{value}` 是当前的范围边界值。
+ 如果为 `Function`，表示回调函数，形如：

```javascript
formatter: function (value) {
    return 'aaaa' + value; // 范围标签显示内容。
}
```