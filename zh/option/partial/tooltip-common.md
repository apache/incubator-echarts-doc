
{{target: partial-tooltip-introduction}}

**提示框组件的通用介绍：**

提示框组件可以设置在多种地方：

+ 可以设置在全局，即 [tooltip](~tooltip)

+ 可以设置在坐标系中，即 [grid.tooltip](~grid.tooltip)、[polar.tooltip](~polar.tooltip)、[single.tooltip](~single.tooltip)

+ 可以设置在系列中，即 [series.tooltip](~series.tooltip)

+ 可以设置在系列的每个数据项中，即 [series.data.tooltip](~series.data.tooltip)


---







{{target: partial-tooltip-in-coords}}

## tooltip

本坐标系特定的 tooltip 设定。

---

{{use: partial-tooltip-introduction}}

{{use: partial-tooltip-coords-common(
    prefix='##',
    galleryViewPath=${galleryViewPath}
)}}

{{ use: partial-tooltip-common(scope='coordSys', prefix='##') }}













{{target: partial-tooltip-in-series}}

## tooltip

本系列特定的 tooltip 设定。

{{ use: partial-tooltip-common(scope='series', prefix='##') }}








{{target: partial-tooltip-in-series-data}}

### tooltip

本系列每个数据项中特定的 tooltip 设定。

{{ use: partial-tooltip-common(scope='seriesData', prefix='###') }}








{{target: partial-tooltip-scope-tip}}

{{if: ${scope} === 'series' }}
<br>
> **注意：**`series.tooltip` 仅在 [tooltip.trigger](~tooltip.trigger) 为 `'item'` 时有效。<br>
{{elif: ${scope} === 'seriesData' }}
> **注意：**`series.data.tooltip` 仅在 [tooltip.trigger](~tooltip.trigger) 为 `'item'` 时有效。<br>
{{/if}}









{{target: partial-tooltip-coords-common}}


#${prefix} show(boolean) = true

是否显示提示框组件，包括提示框浮层和 [axisPointer](~tooltip.axisPointer)。


#${prefix} trigger(string) = 'item'

触发类型。

**可选：**
+ `'item'`：数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。

+ `'axis'`：坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用。

    在 ECharts 2.x 中只支持类目轴上使用 axis trigger，在 ECharts 3 中支持在[直角坐标系](~grid)和[极坐标系](~polar)上的所有类型的轴。并且可以通过 [axisPointer.axis](~tooltip.axisPointer.axis) 指定坐标轴。

+ `'none'`：什么都不触发。

#${prefix} axisPointer(Object)

坐标轴指示器配置项。

`tooltip.axisPointer` 是配置坐标轴指示器的快捷方式。实际上坐标轴指示器的全部功能，都可以通过轴上的 axisPointer 配置项完成（例如 [xAxis.axisPointer](~xAxis.axisPointer) 或 [angleAxis.axisPointer](~angleAxis.axisPointer)）。但是使用 `tooltip.axisPinter` 在简单场景下会更方便一些。

> **注意：** `tooltip.axisPointer` 中诸配置项的优先级低于轴上的 axisPointer 的配置项。

---

{{ use: partial-axisPointer-introduction(
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
) }}


##${prefix} type(string) = 'line'

指示器类型。

**可选：**
+ `'line'`：直线指示器

+ `'shadow'`：阴影指示器

+ `'none'`：无指示器

+ `'cross'`：十字准星指示器。其实是种简写，表示启用两个正交的轴的 axisPointer。


##${prefix} axis(string) = 'auto'

指示器的坐标轴。

默认情况，坐标系会自动选择显示哪个轴的 axisPointer（默认取类目轴或者时间轴）。

可以是 `'x'`, `'y'`, `'radius'`, `'angle'`。

{{ use: partial-axisPointer-tooltip-shared(
    prefix="#" + ${prefix},
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
) }}

##${prefix} crossStyle(Object)

[axisPointer.type](~tooltip.axisPointer.type) 为 `'cross'` 时有效。

{{ use: partial-line-style(prefix="##" + ${prefix}, defaultColor="#555", defaultWidth=1, defaultType="dashed") }}


{{ use: partial-animation(
    prefix='#' + ${prefix},
    defaultAnimationEasingUpdate='exponentialOut',
    defaultAnimationDurationUpdate=200
) }}







{{target: partial-tooltip-common}}

#${prefix} position(string|Array|Function)

{{use: partial-tooltip-scope-tip(scope=${scope})}}

提示框浮层的位置，默认不设置时位置会跟随鼠标的位置。

**可选：**

+ `Array`：通过数组表示提示框浮层的位置，支持数字设置绝对位置，百分比设置相对位置。

     **例如：** 

    ```js
    // 绝对位置，相对于容器左侧 10px, 上侧 10 px
    position: [10, 10]
    // 相对位置，放置在容器正中间
    position: ['50%', '50%']
    ```

+ `Function`：回调函数，格式如下
    ```js
    (point: Array, params: Object|Array.<Object>, dom: HTMLDomElement, rect: Object, size: Object) => Array
    ```

    **参数：**<br>
    point: 鼠标位置，如 [20, 40]。<br>
    params: 同 formatter 的参数相同。<br>
    dom: tooltip 的 dom 对象。<br>
    rect: 只有鼠标在图形上时有效，是一个用`x`, `y`, `width`, `height`四个属性表达的图形包围盒。<br>
    size: 包括 dom 的尺寸和 ECharts 容器的当前尺寸，例如：`{contentSize: [width, height], viewSize: [width, height]}`。<br>

    **返回值：**<br>
    可以是一个表示 tooltip 位置的数组，数组值可以是绝对的像素值，也可以是相  百分比。<br>
    也可以是一个对象，如：`{left: 10, top: 30}`，或者 `{right: '20%', bottom: 40}`。<br>

     **例如：** 
    ```js
    position: function (point, params, dom, rect, size) {
        // 固定在顶部
        return [point[0], '10%'];
    }
    ```
    或者：
    ```js
    position: function (pos, params, dom, rect, size) {
        // 鼠标在左侧时 tooltip 显示到右侧，鼠标在右侧时 tooltip 显示到左侧。
        var obj = {top: 60};
        obj[['left', 'right'][+(pos[0] < size.viewSize[0] / 2)]] = 5;
        return obj;
    }
    ```


+ `'inside'`：鼠标所在图形的内部中心位置，只在 [trigger](~tooltip.trigger) 为`'item'`的时候有效。

+ `'top'`：鼠标所在图形上侧，只在 [trigger](~tooltip.trigger) 为`'item'`的时候有效。

+ `'left'`：鼠标所在图形左侧，只在 [trigger](~tooltip.trigger) 为`'item'`的时候有效。

+ `'right'`：鼠标所在图形右侧，只在 [trigger](~tooltip.trigger) 为`'item'`的时候有效。

+ `'bottom'`：鼠标所在图形底侧，只在 [trigger](~tooltip.trigger) 为`'item'`的时候有效。


#${prefix} formatter(string|Function)

{{use: partial-tooltip-scope-tip(scope=${scope})}}

提示框浮层内容格式器，支持字符串模板和回调函数两种形式。

**1, 字符串模板**

模板变量有 `{a}`, `{b}`，`{c}`，`{d}`，`{e}`，分别表示系列名，数据名，数据值等。
在 [trigger](~tooltip.trigger) 为 `'axis'` 的时候，会有多个系列的数据，此时可以通过 `{a0}`, `{a1}`, `{a2}` 这种后面加索引的方式表示系列的索引。
不同图表类型下的 `{a}`，`{b}`，`{c}`，`{d}` 含义不一样。
其中变量`{a}`, `{b}`, `{c}`, `{d}`在不同图表类型下代表数据含义为：

+ 折线（区域）图、柱状（条形）图、K线图 : `{a}`（系列名称），`{b}`（类目值），`{c}`（数值）, `{d}`（无）

+ 散点图（气泡）图 : `{a}`（系列名称），`{b}`（数据名称），`{c}`（数值数组）, `{d}`（无）

+ 地图 : `{a}`（系列名称），`{b}`（区域名称），`{c}`（合并数值）, `{d}`（无）

+ 饼图、仪表盘、漏斗图: `{a}`（系列名称），`{b}`（数据项名称），`{c}`（数值）, `{d}`（百分比）

更多其它图表模板变量的含义可以见相应的图表的 label.formatter 配置项。

 **例如：** 
```js
formatter: '{b0}: {c0}<br />{b1}: {c1}'
```


**2, 回调函数**

回调函数格式：

```js
(params: Object|Array, ticket: string, callback: (ticket: string, html: string)) => string
```

第一个参数 `params` 是 formatter 需要的数据集。格式如下：
{{ use: partial-formatter-params-structure(extra = {
    percent: {
        desc: '饼图的百分比',
        type: 'number'
    }
}) }}

在 [trigger](~tooltip.trigger) 为 `'axis'` 的时候，或者 tooltip 被 [axisPointer](~xAxis.axisPointer) 触发的时候，`params` 是多个系列的数据数组。其中每项内容格式同上，并且，

{{ use: partial-formatter-params-structure}}

**注：** ECharts 2.x 使用数组表示各参数的方式不再支持。

第二个参数 `ticket` 是异步回调标识，配合第三个参数 `callback` 使用。
第三个参数 `callback` 是异步回调，在提示框浮层内容是异步获取的时候，可以通过 callback 传入上述的 `ticket` 和 `html` 更新提示框浮层内容。

 **例如：** 
```js
formatter: function (params, ticket, callback) {
    $.get('detail?name=' + params.name, function (content) {
        callback(ticket, toHTML(content));
    });
    return 'Loading';
}
```

#${prefix} backgroundColor(Color) = 'rgba(50,50,50,0.7)'

{{use: partial-tooltip-scope-tip(scope=${scope})}}

提示框浮层的背景颜色。

#${prefix} borderColor(Color) = '#333'

{{use: partial-tooltip-scope-tip(scope=${scope})}}

提示框浮层的边框颜色。

#${prefix} borderWidth(number) = 0

{{use: partial-tooltip-scope-tip(scope=${scope})}}

提示框浮层的边框宽。

#${prefix} padding(number) = 5

{{use: partial-tooltip-scope-tip(scope=${scope})}}

{{ use: partial-padding(componentName='提示框浮层') }}

#${prefix} textStyle(Object)

{{use: partial-tooltip-scope-tip(scope=${scope})}}

提示框浮层的文本样式。

{{ use: partial-simple-text-style(prefix="#" + ${prefix}, defaultColor="'#fff'", defaultFontSize=14) }}

#${prefix} extraCssText(string)

{{use: partial-tooltip-scope-tip(scope=${scope})}}

额外附加到浮层的 css 样式。如下为浮层添加阴影的示例：

```js
extraCssText: 'box-shadow: 0 0 3px rgba(0, 0, 0, 0.3);'
```







