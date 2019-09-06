The display interval of {{ target: component-axis3D-common-axis-interval }}
${name} is valid in the category axis. {{ if: !${isAxisLabel} }} defaults to the same as [axisLabel.interval](~${componentType}.axisLabel.interval). {{ /if }}

By default, `interval` is automatically calculated to ensure a good display.

Can be set to 0 to force all labels to be displayed.

If set to `1`, it means "displays a label every other label". If the value is `2`, it means "displays a label between two labels", and so on.

The interval data can be represented by a numerical value or by a callback function. The format of the callback function is as follows:

```js
(index:number, value: string) => boolean
```

The first parameter is the index of the class, the second value is the name of the class, and if it is skipped, it returns `false`.

{{target: component-axis3D-common-formatter-desc}}

The content formatter for tick labels. Supports both string templates and callback functions.

Example: 
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



{{ target: component-axis3D-common-axisLine }}

#${prefix|default('#')} axisLine(Object)
啊啊啊 坐标轴轴线相关设置。
##${prefix|default('#')} show(boolean) = ${defaultShow|default(true)}
是否显示坐标轴轴线。

{{ if: ${hasLabelInterval|default(true)} }}
##${prefix|default('#')} interval(number|Function) = 'auto'
{{ use: component-axis3D-common-axis-interval(
    name="坐标轴刻度标签",
    isAxisLabel=true,
    componentType=${componentType}
) }}
{{ /if }}

##${prefix|default('#')} lineStyle(Object)
{{ use: partial-line-style(prefix='##' + ${prefix|default('#')}, defaultColor="'#333'", defaultWidth=2, name="坐标轴线") }}




{{ target: component-axis3D-common-axisLabel }}

#${prefix|default('#')} axisLabel(Object)
坐标轴刻度标签的相关设置。
##${prefix|default('#')} show(boolean) = ${defaultShow|default(true)}
是否显示刻度标签。

##${prefix|default('#')} margin(number) = 8
刻度标签与轴线之间的距离。

**注意：** 这个距离是三维空间而非屏幕空间的。

{{ if: ${hasLabelInterval|default(true)} }}
##${prefix|default('#')} interval(number|Function) = 'auto'
{{ use: component-axis3D-common-axis-interval(
    name="坐标轴刻度标签",
    isAxisLabel=true,
    componentType=${componentType}
) }}
{{ /if }}

##${prefix|default('#')} formatter(string|Function) = null
{{use: axis-common-formatter-desc}}


##${prefix|default('#')} textStyle(Object)
{{ use: partial-text-style(
    prefix='##' + ${prefix|default('#')},
    defaultColor="'#333'"
)}}
<!-- Overwrite color -->
###${prefix|default('#')} color(Color|Function)

刻度标签文字的颜色，默认取 [axisLine.lineStyle.color](~${componentType}.axisLine.lineStyle.color)。支持回调函数，格式如下

```js
(val: string) => Color
```

参数是标签的文本，返回颜色值，如下示例：

```js
textStyle: {
    color: function (value, index) {
        return value >= 0 ? 'green' : 'red';
    }
}
```


{{ target: component-axis3D-common-axisTick }}

#${prefix|default('#')} axisTick(Object)
坐标轴刻度相关设置。
##${prefix|default('#')} show(boolean) = ${defaultShow|default(true)}
是否显示坐标轴刻度。

{{ if: ${hasLabelInterval|default(true)} }}
##${prefix|default('#')} interval(number|Function) = 'auto'
{{ use: component-axis3D-common-axis-interval(
    name="坐标轴刻度标签",
    componentType=${componentType}
) }}
{{ /if }}

##${prefix|default('#')} length(number) = 5
坐标轴刻度的长度。

##${prefix|default('#')} lineStyle(Object)
{{ use: partial-line-style(prefix='##' + ${prefix|default('#')}, defaultColor="'#333'", defaultWidth=1, name="坐标轴线") }}
<!-- Overwrite color -->
###${prefix|default('#')} color(Color)

刻度线的颜色，默认取 [axisLine.lineStyle.color](~${componentType}.axisLine.lineStyle.color)。



{{ target: component-axis3D-common-splitLine }}

#${prefix|default('#')} splitLine(Object)
坐标轴轴线相关设置。
##${prefix|default('#')} show(boolean) = ${defaultShow|default(true)}
是否显示坐标轴轴线。

{{ if: ${hasLabelInterval|default(true)} }}
##${prefix|default('#')} interval(number|Function) = 'auto'
{{ use: component-axis3D-common-axis-interval(
    name="坐标轴刻度标签",
    isAxisLabel=true,
    componentType=${componentType}
) }}
{{ /if }}

##${prefix|default('#')} lineStyle(Object)
{{ use: partial-line-style(prefix='##' + ${prefix|default('#')}, defaultColor="'#333'", defaultWidth=2, name="坐标轴线") }}



{{ target: component-axis3D-common-splitArea }}

#${prefix|default('#')} splitArea(Object)

坐标轴在 [grid3D](~grid3D) 的平面上的分隔区域。
##${prefix|default('#')} show(boolean) = ${defaultShow|default(true)}
是否显示分隔区域。

{{ if: ${hasLabelInterval|default(true)} }}
##${prefix|default('#')} interval(number|Function) = 'auto'
{{ use: component-axis3D-common-axis-interval(
    name="坐标轴分隔区域",
    componentType=${componentType}
) }}
{{ /if }}

##${prefix|default('#')} areaStyle(Object)
分隔区域的样式设置。
###${prefix|default('#')} color(Array) = ['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)']
分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
{{ use:partial-style-shadow-opacity(prefix='##' + ${prefix|default('#')}) }}




{{ target: component-axis3D-common-axisPointer }}

#${prefix|default('#')} axisPointer(Object)
坐标轴指示线。

##${prefix|default('#')} show(boolean) = ${defaultShow|default(true)}

是否显示坐标轴指示线。

##${prefix|default('#')} lineStyle(Object)

{{ use: partial-line-style(prefix='##' + ${prefix|default('#')}, defaultColor="'rgba(0, 0, 0, 0.8)'", defaultWidth=1, name="坐标轴指示线") }}

##${prefix|default('#')} label(Object)

指示线标签。

###${prefix|default('#')} show(boolean) = true

是否显示指示线标签。默认数值轴显示，类目轴不显示。

###${prefix|default('#')} formatter(Function)

标签格式器，函数第一个参数是当前坐标轴的数值，第二个参数是所有坐标轴的数值数组

```js
(value: number, valueAll: Array) => string
```

###${prefix|default('#')} margin(number)

标签距离坐标轴的距离。同刻度标签一样，这个距离是三维空间而非屏幕像素。

###${prefix|default('#')} textStyle(Object)

{{ use: partial-text-style(
    prefix='###' + ${prefix|default('#')},
    defaultFontSize=16
)}}




{{ target: component-axis3D-common }}

{{ use: component-axis3D-common-axisLine(
    prefix=${prefix|default('#')}
) }}

{{ use: component-axis3D-common-axisLabel(
    prefix=${prefix|default('#')}
) }}

{{ use: component-axis3D-common-axisTick(
    prefix=${prefix|default('#')}
) }}

{{ use: component-axis3D-common-splitLine(
    prefix=${prefix|default('#')}
) }}

{{ use: component-axis3D-common-splitArea(
    prefix=${prefix|default('#')}
) }}

{{ use: component-axis3D-common-axisPointer(
    prefix=${prefix|default('#')}
) }}