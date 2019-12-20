{{target: partial-axis-common-axis-line}}
#${prefix} silent(boolean) = false
坐标轴是否是静态无法交互。

#${prefix} triggerEvent(boolean) = false

坐标轴的标签是否响应和触发鼠标事件。默认不响应。

事件参数如下：

```js
{
    // 组件类型，xAxis, yAxis, radiusAxis, angleAxis
    // 对应组件类型都会有一个属性表示组件的 index，例如 xAxis 就是 xAxisIndex
    componentType: string,
    // 未格式化过的刻度值, 点击刻度标签有效
    value: '',
    // 坐标轴名称, 点击坐标轴名称有效
    name: ''
}
```

#${prefix} axisLine(Object)
坐标轴轴线相关设置。
##${prefix} show(boolean) = ${defaultShow|default(true)}
是否显示坐标轴轴线。

{{ if: ${componentType} == 'xAxis' || ${componentType} == 'yAxis' }}
##${prefix} onZero(boolean) = true
X 轴或者 Y 轴的轴线是否在另一个轴的 0 刻度上，只有在另一个轴为数值轴且包含 0 刻度时有效。

##${prefix} onZeroAxisIndex(number)
当有双轴时，可以用这个属性手动指定在哪个轴的 0 刻度上。
{{ /if }}

##${prefix} symbol(string|Array) = 'none'
轴线两端的图形。可以是字符串表示两端使用同样的图形，例如默认两端不显示图形，即 `'none'`，两端都显示为箭头可以设置为 `'arrow'`。也可以是长度为 2 的字符串数组，分别表示轴线两端的图形，例如只在末端显示箭头可以设置为 `['none', 'arrow']`。

##${prefix} symbolSize(Array) = [10, 15]
轴线两端的图形的大小，第一个数字表示宽度（垂直坐标轴方向），第二个数字表示高度（平行坐标轴方向）。

##${prefix} symbolOffset(Array|number) = [0, 0]

轴线两端的图形的偏移，如果是数组，第一个数字表示起始图形的偏移，第二个数字表示末端图形的偏移；如果是数字，表示这两个图形使用同样的偏移。

##${prefix} lineStyle(Object)
{{ use: partial-line-style(prefix='##' + ${prefix}, defaultColor="'#333'", defaultWidth=1, defaultType="'solid'", name="坐标轴线") }}


{{target: partial-axis-common-axis-label}}
#${prefix} axisLabel(Object)
坐标轴刻度标签的相关设置。

{{if: !${hideShow} }}
##${prefix} show(boolean) = ${defaultShow|default(true)}
是否显示刻度标签。
{{ /if }}

{{ if: ${hasLabelInterval|default(true)} }}
##${prefix} interval(number|Function) = 'auto'
{{ use: partial-axis-interval(
    name="坐标轴刻度标签",
    isAxisLabel=true,
    componentType=${componentType}
) }}
{{ /if }}

{{ if: ${hasInside|default(true)} }}
##${prefix} inside(boolean) = false
刻度标签是否朝内。默认朝外。
{{ /if }}

{{ if: ${componentType} !== 'angleAxis' }}
##${prefix} rotate(number) = 0
刻度标签旋转的角度。在类目轴的类目标签显示不下的时候可以通过旋转防止标签之间重叠。

旋转的角度从 -90 度到 90 度。
{{ /if }}

##${prefix} margin(number) = 8
刻度标签与轴线之间的距离。
##${prefix} formatter(string|Function) = null

{{use: axis-common-formatter-desc}}

##${prefix} showMinLabel(boolean) = null
是否显示最小 tick 的 label。默认自动判定（即如果标签重叠，不会显示最小 tick 的 label）。

**可选：** 
+ `true`
+ `false`
+ `null`

##${prefix} showMaxLabel(boolean) = null
是否显示最大 tick 的 label。默认自动判定（即如果标签重叠，不会显示最大 tick 的 label）。

**可选：** 
+ `true`
+ `false`
+ `null`


{{ use: partial-text-style(
    prefix='#' + ${prefix},
    defaultColor="'#333'"
)}}



<!-- Overwrite color -->
##${prefix} color(Color|Function)

刻度标签文字的颜色。默认取 [axisLine.lineStyle.color](~${componentType}.axisLine.lineStyle.color)。支持回调函数，格式如下：

```js
(val: string) => Color
```

参数是标签的文本，返回颜色值。

**例如：**

```js
textStyle: {
    color: function (value, index) {
        return value >= 0 ? 'green' : 'red';
    }
}
```

{{target: partial-axis-common-axis-tick}}

#${prefix} axisTick(Object)
坐标轴刻度相关设置。
##${prefix} show(boolean) = ${defaultShow|default(true)}
是否显示坐标轴刻度。默认显示。

{{ if: ${hasAlignWithLabel|default(true)} }}
##${prefix} alignWithLabel(boolean) = false
类目轴中在 `boundaryGap` 为 `true` 的时候有效，可以保证刻度线和标签对齐。如下图：

![600xauto](~axis-align-with-label.png)
{{ /if }}

{{ if: ${hasLabelInterval|default(true)} }}
##${prefix} interval(number|Function) = 'auto'
{{ use: partial-axis-interval(
    name="坐标轴刻度",
    componentType=${componentType}
) }}
{{ /if }}

{{ if: ${hasInside|default(true)} }}
##${prefix} inside(boolean) = false
坐标轴刻度是否朝内。默认朝外。
{{ /if }}

##${prefix} length(number) = 5
坐标轴刻度的长度。
##${prefix} lineStyle(Object)
{{ use: partial-line-style(prefix='##' + ${prefix}, defaultColor="'#333'", defaultWidth=1, defaultType="'solid'", name="坐标轴刻度") }}
<!-- Overwrite color -->
###${prefix} color(Color)

刻度线的颜色。默认取 [axisLine.lineStyle.color](~${componentType}.axisLine.lineStyle.color)。





{{target: partial-axis-common-split-line}}

#${prefix} splitLine(Object)
坐标轴在 [grid](~grid) 区域中的分隔线。
##${prefix} show(boolean) = ${defaultShow|default(true)}
是否显示分隔线。默认数值轴显示分割线，类目轴不显示分割线。

{{ if: ${hasLabelInterval|default(true)} }}
##${prefix} interval(number|Function) = 'auto'
{{ use: partial-axis-interval(
    name="坐标轴分隔线",
    componentType=${componentType}
) }}
{{ /if }}
##${prefix} lineStyle(Object)

{{ use: partial-line-style(prefix='##' + ${prefix}, defaultColor="'#333'", defaultWidth=1, defaultType="'solid'", name="分隔线") }}

<!-- overwrite color -->
###${prefix} color(Array|string) = ['#ccc']
分隔线颜色。可以设置成单个颜色，也可以设置成颜色数组。分隔线会按数组中颜色的顺序依次循环设置颜色。

**例如：**
```
splitLine: {
    lineStyle: {
        // 使用深浅的间隔色
        color: ['#aaa', '#ddd']
    }
}
```





{{target: partial-axis-common-split-area}}

#${prefix} splitArea(Object)
坐标轴在 [grid](~grid) 区域中的分隔区域，默认不显示。


{{ if: ${hasLabelInterval|default(true)} }}
##${prefix} interval(number|Function) = 'auto'
{{ use: partial-axis-interval(
    name="坐标轴分隔区域",
    componentType=${componentType}
) }}
{{ /if }}

##${prefix} show(boolean) = ${defaultShow|default(false)}
是否显示分隔区域。
##${prefix} areaStyle(Object)
分隔区域的样式设置。
###${prefix} color(Array) = ['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)']
分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
{{ use:partial-style-shadow-opacity(prefix='##' + ${prefix}) }}



{{target: axis-common}}

#${prefix} type(string) = ${axisTypeDefault|default('value')}

坐标轴类型。

**可选：**
+ `'value'`
    数值轴，适用于连续数据。

+ `'category'`
    类目轴，适用于离散的类目数据，为该类型时必须通过 [data](~${componentType}.data) 设置类目数据。

+ `'time'`
    时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。

+ `'log'`
    对数轴。适用于对数数据。

{{ if: ${componentType} !== 'angleAxis' }}
#${prefix} name(string)

坐标轴名称。

#${prefix} nameLocation(string) = 'end'

坐标轴名称显示位置。

**可选：**
+ `'start'`
+ `'middle'` 或者 `'center'`
+ `'end'`

#${prefix} nameTextStyle(Object)

坐标轴名称的文字样式。

{{use: partial-text-style(prefix='#' + ${prefix}, name="坐标轴名称")}}
<!-- Overwrite color -->
##${prefix} color(Color)

坐标轴名称的颜色。默认取 [axisLine.lineStyle.color](~${componentType}.axisLine.lineStyle.color)。


#${prefix} nameGap(number) = 15

坐标轴名称与轴线之间的距离。

#${prefix} nameRotate(number) = null

坐标轴名字旋转的角度值。

#${prefix} inverse(boolean) = false

是否是反向坐标轴。

{{/if}}

#${prefix} boundaryGap(boolean|Array)
坐标轴两边留白策略，类目轴和非类目轴的设置和表现不一样。

类目轴中 `boundaryGap` 可以配置为 `true` 和 `false`。默认为 `true`，这时候[刻度](~${componentType}.axisTick)只是作为分隔线，标签和数据点都会在两个[刻度](~${componentType}.axisTick)之间的带(band)中间。

非类目轴，包括时间，数值，对数轴，`boundaryGap`是一个两个值的数组，分别表示数据最小值和最大值的延伸范围，可以直接设置数值或者相对的百分比，在设置 [min](~${componentType}.min) 和 [max](~${componentType}.max) 后无效。

**例如：**
```js
boundaryGap: ['20%', '20%']
```

#${prefix} min(number|string|function) = null

坐标轴刻度最小值。

可以设置成特殊值 `'dataMin'`，此时取数据在该轴上的最小值作为最小刻度。不设置时会自动计算最小值保证坐标轴刻度的均匀分布。

在类目轴中，也可以设置为类目的序数（如类目轴 `data: ['类A', '类B', '类C']` 中，序数 `2` 表示 `'类C'`。也可以设置为负数，如 `-3`）。

当设置成 `function` 形式时，可以根据计算得出的数据最大最小值设定坐标轴的最小值。

**例如：**

```
min: function(value) {
    return value.min - 20;
}
```

其中 `value` 是一个包含 `min` 和 `max` 的对象，分别表示数据的最大最小值，这个函数应该返回坐标轴的最小值。

#${prefix} max(number|string) = null

坐标轴刻度最大值。

可以设置成特殊值 `'dataMax'`，此时取数据在该轴上的最大值作为最大刻度。不设置时会自动计算最大值保证坐标轴刻度的均匀分布。

在类目轴中，也可以设置为类目的序数（如类目轴 `data: ['类A', '类B', '类C']` 中，序数 `2` 表示 `'类C'`。也可以设置为负数，如 `-3`）。

当设置成 `function` 形式时，可以根据计算得出的数据最大最小值设定坐标轴的最小值。

**例如：**

```
max: function(value) {
    return value.max - 20;
}
```

其中 `value` 是一个包含 `min` 和 `max` 的对象，分别表示数据的最大最小值，这个函数应该返回坐标轴的最大值。

#${prefix} scale(boolean) = false

只在数值轴中（[type](~${componentType}.type): 'value'）有效。

是否是脱离 0 值比例。设置成 `true` 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。

在设置 [min](~${componentType}.min) 和 [max](~${componentType}.max) 之后该配置项无效。

#${prefix} splitNumber(number) = 5

坐标轴的分割段数，需要注意的是这个分割段数只是个预估值，最后实际显示的段数会在这个基础上根据分割后坐标轴刻度显示的易读程度作调整。

在类目轴中无效。

#${prefix} minInterval(number) = 0

自动计算的坐标轴最小间隔大小。

例如可以设置成 `1` 保证坐标轴分割刻度显示成整数。

```js
{
    minInterval: 1
}
```

只在数值轴或时间轴中（[type](~${componentType}.type): 'value' 或 'time'）有效。

#${prefix} maxInterval(number)

自动计算的坐标轴最大间隔大小。

例如，在时间轴（（[type](~${componentType}.type): 'time'））可以设置成 `3600 * 24 * 1000` 保证坐标轴分割刻度最大为一天。

```js
{
    maxInterval: 3600 * 24 * 1000
}
```

只在数值轴或时间轴中（[type](~${componentType}.type): 'value' 或 'time'）有效。

#${prefix} interval(number)

强制设置坐标轴分割间隔。

因为 [splitNumber](~${componentType}.splitNumber) 是预估的值，实际根据策略计算出来的刻度可能无法达到想要的效果，这时候可以使用 interval 配合 [min](~${componentType}.min)、[max](~${componentType}.max) 强制设定刻度划分，一般不建议使用。

无法在类目轴中使用。在时间轴（[type](~${componentType}.type): 'time'）中需要传时间戳，在对数轴（[type](~${componentType}.type): 'log'）中需要传指数值。

#${prefix} logBase(number) = 10

对数轴的底数。只在对数轴中（[type](~${componentType}.type): 'log'）有效。


{{ use: partial-axis-common-axis-line(
    prefix=${prefix},
    componentType=${componentType}
) }}

{{ use: partial-axis-common-axis-tick(
    prefix=${prefix},
    componentType=${componentType}
) }}

{{ use: partial-axis-common-axis-label(
    prefix=${prefix},
    componentType=${componentType}
) }}

{{ if: ${hasSplitLineAndArea} }}

{{ use: partial-axis-common-split-line(
    prefix=${prefix},
    componentType=${componentType}
) }}

{{ use: partial-axis-common-split-area(
    prefix=${prefix},
    componentType=${componentType}
) }}

{{ /if }}



#${prefix} data(Array)

类目数据。在类目轴（[type](~${componentType}.type): `'category'`）中有效。

如果没有设置 [type](~${componentType}.type)，但是设置了 `axis.data`，则认为 `type` 是 `'category'`。

如果设置了 [type](~${componentType}.type) 是 `'category'`，但没有设置 `axis.data`，则 `axis.data` 的内容会自动从 [series.data](~series.data) 中获取，这会比较方便。不过注意，`axis.data` 指明的是 `'category'` 轴的取值范围。如果不指定而是从 [series.data](~series.data) 中获取，那么只能获取到 [series.data](~series.data) 中出现的值。比如说，假如 [series.data](~series.data) 为空时，就什么也获取不到。

**例如：**

```js
// 所有类目名称列表
data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
// 每一项也可以是具体的配置项，此时取配置项中的 `value` 为类目名
data: [{
    value: '周一',
    // 突出周一
    textStyle: {
        fontSize: 20,
        color: 'red'
    }
}, '周二', '周三', '周四', '周五', '周六', '周日']
```

##${prefix} value(string)

单个类目名称。

##${prefix} textStyle(Object)

类目标签的文字样式。

{{ use:partial-text-style(
    prefix='##' + ${prefix}
) }}

{{if: !${noAxisPointer} }}
#${prefix} axisPointer(Object)

axisPointer settings on axis.

{{ use: partial-axisPointer-common(
    prefix="#" + ${prefix},
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
)}}
{{/if}}



{{ target: partial-axis-interval }}
${name}的显示间隔，在类目轴中有效。{{ if: !${isAxisLabel} }}默认同 [axisLabel.interval](~${componentType}.axisLabel.interval) 一样。{{ /if }}

默认会采用标签不重叠的策略间隔显示标签。

可以设置成 0 强制显示所有标签。如果设置为 `1`，表示『隔一个标签显示一个标签』，如果值为 `2`，表示隔两个标签显示一个标签，以此类推。

可以用数值表示间隔的数据，也可以通过回调函数控制。回调函数格式如下：
```js
(index:number, value: string) => boolean
```
第一个参数是类目的 index，第二个值是类目名称，如果跳过则返回 `false`。



{{target: axis-common-formatter-desc}}

刻度标签的内容格式器，支持字符串模板和回调函数两种形式。

**例如：**
```js
// 使用字符串模板，模板变量为刻度默认标签 {value}
formatter: '{value} kg'

// 使用函数模板，函数参数分别为刻度数值（类目），刻度的索引
formatter: function (value, index) {
    // 格式化成月/日，只在第一个刻度显示年份
    var date = new Date(value);
    var texts = [(date.getMonth() + 1), date.getDate()];
    if (index === 0) {
        texts.unshift(date.getYear());
    }
    return texts.join('/');
}
```
