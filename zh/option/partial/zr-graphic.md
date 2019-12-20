
{{target: partial-zr-graphic-elements}}

#${prefix} ${hostName}${symbolDeclare}group(Object)

group 是唯一的可以有子节点的容器。group 可以用来整体定位一组图形元素。

{{ use: partial-graphic-cpt-common-props(
    type='group',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} width(number) = 0

用于描述此 `group` 的宽。

这个宽只用于给子节点定位。

即便当宽度为零的时候，子节点也可以使用 `left: 'center'` 相对于父节点水平居中。


##${prefix} height(number) = 0

用于描述此 `group` 的高。

这个高只用于给子节点定位。

即便当高度为零的时候，子节点也可以使用 `top: 'middle'` 相对于父节点垂直居中。


##${prefix} diffChildrenByName(boolean) = false

在 [自定义系列](~series-custom) 中，当 `diffChildrenByName: true` 时，对于 [renderItem](~series-custom.renderItem) 返回值中的每一个 [group](~${optionPath}.${hostName}${symbolVisit}group)，会根据其 [children](~${optionPath}.${hostName}${symbolVisit}group.children) 中每个图形元素的 [name](~${optionPath}.${hostName}${symbolVisit}polygon.name) 属性进行 "diff"。在这里，"diff" 的意思是，重绘的时候，在已存在的图形元素和新的图形元素之间建立对应关系（依据 `name` 是否相同），从如果数据有更新，能够形成的过渡动画。

**注意：**这会有性能开销。如果数据量较大，不要开启这个功能。


##${prefix} children(Array)

子节点列表，其中项都是一个图形元素定义。

{{ use: partial-graphic-cpt-common-props(
    type='group',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}

) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}



{{ if: ${usageType} === 'customSeries' }}

#${prefix} ${hostName}${symbolDeclare}path(Object)

可使用 [SVG PathData](http://www.w3.org/TR/SVG/paths.html#PathData) 做路径。
可以用来画图标，或者其他各种图形，因为可以很便捷得缩放以适应给定尺寸。

**例如：**
[icons](${galleryEditorPath}custom-calendar-icon) 和 [shapes](${galleryEditorPath}custom-gantt-flight)。

关于制定尺寸、拉伸还是平铺，参见 [layout](~${optionPath}.${hostName}${symbolVisit}path.shape.layout)。


{{ use: partial-graphic-cpt-common-props(
    type='path',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} shape(Object)

###${prefix} pathData(string)

即 [SVG PathData](http://www.w3.org/TR/SVG/paths.html#PathData)。

**例如：**`'M0,0 L0,-20 L30,-20 C42,-20 38,-1 50,-1 L70,-1 L70,0 Z'`。

如果指定了 [width](~${optionPath}.${hostName}${symbolVisit}path.shape.width)、[height](~${optionPath}.${hostName}${symbolVisit}path.shape.height)、[x](~${optionPath}.${hostName}${symbolVisit}path.shape.x)、[y](~${optionPath}.${hostName}${symbolVisit}path.shape.y)，则会根据他们定义的矩形，缩放 PathData。如果没有指定这些，就不会缩放。

可使用 [layout](~${optionPath}.${hostName}${symbolVisit}path.shape.layout) 指定缩放策略。

**例如：**
[icons](${galleryEditorPath}custom-calendar-icon) 和 [shapes](${galleryEditorPath}custom-gantt-flight)。


###${prefix} d(string)

同 [pathData](~${optionPath}.${hostName}${symbolVisit}path.shape.pathData)，别名。


###${prefix} layout(string) = 'center'

如果指定了 [width](~${optionPath}.${hostName}${symbolVisit}path.shape.width)、[height](~${optionPath}.${hostName}${symbolVisit}path.shape.height)、[x](~${optionPath}.${hostName}${symbolVisit}path.shape.x)、[y](~${optionPath}.${hostName}${symbolVisit}path.shape.y)，则会根据他们定义的矩形，缩放 PathData。

`layout` 用于指定缩放策略。

**可选：**
+ `'center'`：保持原来的 PathData 的长宽比，居于矩形中，尽可能撑大但不会超出矩形。
+ `'cover'`：PathData 拉伸为矩形的长宽比，完全填满矩形，不会超出矩形。


{{ use: partial-graphic-cpt-sub-prop-xy(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-sub-prop-wh(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}



##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ /if }}




#${prefix} ${hostName}${symbolDeclare}image(Object)

{{ use: partial-graphic-cpt-common-props(
    type='image',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} style(Object)

###${prefix} image(string)

图片的内容，可以是图片的 URL，也可以是 [dataURI](https://tools.ietf.org/html/rfc2397).

{{ use: partial-graphic-cpt-sub-prop-xy(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-sub-prop-wh(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-style-prop-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}





#${prefix} ${hostName}${symbolDeclare}text(Object)

文本块。

{{ use: partial-graphic-cpt-common-props(
    type='text',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} style(Object)

###${prefix} text(string) = ''

文本块文字。可以使用 `\n` 来换行。

{{ use: partial-graphic-cpt-sub-prop-xy(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

###${prefix} font(string)

字体大小、字体类型、粗细、字体样式。格式参见 [css font](https://developer.mozilla.org/en-US/docs/Web/CSS/font)。

 **例如：** 
```
// size | family
font: '2em "STHeiti", sans-serif'

// style | weight | size | family
font: 'italic bolder 16px cursive'

// weight | size | family
font: 'bolder 2em "Microsoft YaHei", sans-serif'
```

###${prefix} textAlign(string) = 'left'

水平对齐方式，取值：`'left'`, `'center'`, `'right'`。

如果为 `'left'`，表示文本最左端在 `x` 值上。如果为 `'right'`，表示文本最右端在 `x` 值上。

###${prefix} textVerticalAlign(string)

垂直对齐方式，取值：`'top'`, `'middle'`, `'bottom'`。

{{ use: partial-graphic-cpt-style-prop-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}






#${prefix} ${hostName}${symbolDeclare}rect(Object)

矩形。

{{ use: partial-graphic-cpt-common-props(
    type='rect',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} shape(Object)

{{ use: partial-graphic-cpt-sub-prop-xy(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-sub-prop-wh(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

###${prefix} r(Array)

可以用于设置圆角矩形。`r: [r1, r2, r3, r4]`，左上、右上、右下、左下角的半径依次为r1、r2、r3、r4。

可以缩写。

**例如：**
+ `r` 缩写为 `1`         相当于 `[1, 1, 1, 1]`
+ `r` 缩写为 `[1]`       相当于 `[1, 1, 1, 1]`
+ `r` 缩写为 `[1, 2]`    相当于 `[1, 2, 1, 2]`
+ `r` 缩写为 `[1, 2, 3]1 相当于 `[1, 2, 3, 2]`


##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}




#${prefix} ${hostName}${symbolDeclare}circle(Object)

圆。

{{ use: partial-graphic-cpt-common-props(
    type='circle',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} shape(Object)

{{ use: partial-graphic-cpt-sub-prop-cxy(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-sub-prop-r(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}






#${prefix} ${hostName}${symbolDeclare}ring(Object)

圆环。

{{ use: partial-graphic-cpt-common-props(
    type='ring',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}


##${prefix} shape(Object)

{{ use: partial-graphic-cpt-sub-prop-cxy(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-sub-prop-rr0(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}


##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}







#${prefix} ${hostName}${symbolDeclare}sector(Object)

扇形。

{{ use: partial-graphic-cpt-common-props(
    type='sector',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} shape(Object)

{{ use: partial-graphic-cpt-sub-prop-cxy(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-sub-prop-rr0(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-sub-prop-angle(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}








#${prefix} ${hostName}${symbolDeclare}arc(Object)

圆弧。

{{ use: partial-graphic-cpt-common-props(
    type='arc',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} shape(Object)

{{ use: partial-graphic-cpt-sub-prop-cxy(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-sub-prop-rr0(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}
{{ use: partial-graphic-cpt-sub-prop-angle(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    fill = 'null',
    stroke = '"#000"',
    lineWidth = 1,
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}










#${prefix} ${hostName}${symbolDeclare}polygon(Object)

多边形。

{{ use: partial-graphic-cpt-common-props(
    type='polygon',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} shape(Object)

{{ use: partial-graphic-cpt-path-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}







#${prefix} ${hostName}${symbolDeclare}polyline(Object)

折线。

{{ use: partial-graphic-cpt-common-props(
    type='polyline',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} shape(Object)

{{ use: partial-graphic-cpt-path-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    fill = 'null',
    stroke = '"#000"',
    lineWidth = 5,
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}









#${prefix} ${hostName}${symbolDeclare}line(Object)

直线。

{{ use: partial-graphic-cpt-common-props(
    type='line',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} shape(Object)

{{ use: partial-graphic-cpt-sub-prop-x1y1x2y2(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

###${prefix} percent(number) = 1

线画到百分之多少就不画了。值的范围：[0, 1]。

##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    fill = 'null',
    stroke = '"#000"',
    lineWidth = 5,
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}








#${prefix} ${hostName}${symbolDeclare}bezierCurve(Object)

二次或三次贝塞尔曲线。

{{ use: partial-graphic-cpt-common-props(
    type='bezierCurve',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} shape(Object)

{{ use: partial-graphic-cpt-sub-prop-x1y1x2y2(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

###${prefix} cpx1(number) = 0

控制点 x 值。

###${prefix} cpy1(number) = 0

控制点 y 值。

###${prefix} cpx2(number) = null

第二个控制点 x 值。如果设置则开启三阶贝塞尔曲线。

###${prefix} cpy2(number) = null

第二个控制点 y 值。如果设置则开启三阶贝塞尔曲线。

###${prefix} percent(number) = 1

画到百分之多少就不画了。值的范围：[0, 1]。

##${prefix} style(Object)

{{ use: partial-graphic-cpt-style-prop-common(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-style-emphasis(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

{{ use: partial-graphic-cpt-event-handlers(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}














{{ target: partial-graphic-cpt-common-props }}

##${prefix} type(string) = ${type}

用 setOption 首次设定图形元素时必须指定。
可取值：

{{ use: partial-graphic-cpt-type-list(
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} id(string) = undefined

id 用于在更新或删除图形元素时指定更新哪个图形元素，如果不需要用可以忽略。


{{ if: ${usageType} === 'graphicComponent' }}

##${prefix} $action(string) = 'merge'

setOption 时指定本次对该图形元素的操作行为。

可取值：
+ `'merge'`：如果已有元素，则新的配置项和已有的设定进行 merge。如果没有则新建。
+ `'replace'`：如果已有元素，删除之，新建元素替代之。
+ `'remove'`：删除元素。

{{ /if }}


{{ use: partial-graphic-transform(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}


{{ if: ${usageType} === 'graphicComponent' }}

##${prefix} left(number|string) = undefined

{{ use: partial-graphic-cpt-location-prop-desc-common (
    hv = 'h',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} right(number|string) = undefined

{{ use: partial-graphic-cpt-location-prop-desc-common (
    hv = 'h',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} top(number|string) = undefined

{{ use: partial-graphic-cpt-location-prop-desc-common (
    hv = 'v',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} bottom(number|string) = undefined

{{ use: partial-graphic-cpt-location-prop-desc-common (
    hv = 'v',
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} bounding(strin) = 'all'

决定此图形元素在定位时，对自身的包围盒计算方式。

**例如：**
~[500x500](${galleryViewPath}doc-example/graphic-bounding&edit=1&reset=1)

**可选：**

+ `'all'`：（默认）
    表示用自身以及子节点整体的经过 transform 后的包围盒进行定位。
    这种方式易于使整体都限制在父元素范围中。

+ `'raw'`：
    表示仅仅用自身（不包括子节点）的没经过 tranform 的包围盒进行定位。
    这种方式易于内容超出父元素范围的定位方式。



##${prefix} z(number) = 0

z 方向的高度，决定层叠关系。

##${prefix} zlevel(number) = 0

决定此元素绘制在哪个 canvas 层中。
**注意：**越多 canvas 层会占用越多资源。

{{ /if }}


{{ if: ${usageType} === 'customSeries' }}

##${prefix} z2(number) = undefined

用于决定图形元素的覆盖关系。

##${prefix} name(string) = undefined

参见 [diffChildrenByName](~${optionPath}.${hostName}${symbolVisit}polygon.diffChildrenByName)。


{{ /if }}


##${prefix} info

用户定义的任意数据，可以在 event listener 中访问，

**例如：**

```js
chart.on('click', function (params) {
    console.log(params.info);
});
```

##${prefix} silent(boolean) = false

是否不响应鼠标以及触摸事件。

##${prefix} invisible(boolean) = false

节点是否可见。

##${prefix} ignore(boolean) = false

节点是否完全被忽略（既不渲染，也不响应事件）。



{{ if: ${usageType} === 'graphicComponent' }}

{{ use: partial-cursor(prefix="##") }}

##${prefix} draggable(boolean) = false

图形元素是否可以被拖拽。

##${prefix} progressive(boolean) = false

是否渐进式渲染。当图形元素过多时才使用。

{{ /if }}






{{ target: partial-graphic-cpt-style-prop-common }}

注：关于图形元素中更多的样式设置（例如 [富文本标签](http://echarts.baidu.com/tutorial.html#%E5%AF%8C%E6%96%87%E6%9C%AC%E6%A0%87%E7%AD%BE)），参见 [zrender/graphic/Displayable](https://ecomfe.github.io/zrender-doc/public/api.html#zrenderdisplayable) 中的 style 相关属性。

**注意：**这里图形元素的样式属性名称直接源于 zrender，和 `echarts label`、`echarts itemStyle` 等处同样含义的样式属性名称或有不同。例如，有如下对应：

+ [itemStyle.color](~series-scatter.label.color) => `style.fill`
+ [itemStyle.borderColor](~series-scatter.label.color) => `style.stroke`
+ [label.color](~series-scatter.label.color) => `style.textFill`
+ [label.textBorderColor](~series-scatter.label.textBorderColor) => `style.textStroke`
+ ...


###${prefix} fill(string) = ${fill|default("'#000'")}

填充色。

###${prefix} stroke(string) = ${stroke|default("null")}

笔画颜色。

###${prefix} lineWidth(number) = ${lineWidth|default("0")}

笔画宽度。

###${prefix} shadowBlur(number) = undefined

阴影宽度。

###${prefix} shadowOffsetX(number) = undefined

阴影 X 方向偏移。

###${prefix} shadowOffsetY(number) = undefined

阴影 Y 方向偏移。

###${prefix} shadowColor(number) = undefined

阴影颜色。








{{ target: partial-graphic-cpt-path-common }}

###${prefix} points(Array)

点列表，用于定义形状，如 `[[22, 44], [44, 55], [11, 44], ...]`

###${prefix} smooth(number|string) = undefined

是否平滑曲线。

+ 如果为 number：表示贝塞尔 (bezier) 差值平滑，smooth 指定了平滑等级，范围 `[0, 1]`。
+ 如果为 `'spline'`：表示 Catmull-Rom spline 差值平滑。

###${prefix} smoothConstraint(boolean) = false

是否将平滑曲线约束在包围盒中。`smooth` 为 `number`（bezier）时生效。









{{ target: partial-graphic-cpt-location-prop-desc-common }}

描述怎么根据父元素进行定位。

『父元素』是指：如果是顶层元素，父元素是 ECharts 图表容器。如果是 `group` 的子元素，父元素就是 `group` 元素。

值的类型可以是：

+ `number`：表示像素值。
+ 百分比值：如 '33%'，用父元素的{{ if: ${hv} === 'h' }}高{{ else }}宽{{ /if }}和此百分比计算出最终值。
+ {{ if: ${hv} === 'h' }}`'center'`{{ else }}`'middle'`{{ /if }}：表示自动居中。

{{ if: ${hv} === 'h' }}
[left](~${optionPath}.${hostName}${symbolVisit}polygon.left) 和 [right](~${optionPath}.${hostName}${symbolVisit}polygon.right) 只有一个可以生效。

如果指定 [left](~${optionPath}.${hostName}${symbolVisit}polygon.left) 或 [right](~${optionPath}.${hostName}${symbolVisit}polygon.right)，则 [shape](~${optionPath}.${hostName}${symbolVisit}polygon.shape) 里的 `x`、`cx` 等定位属性不再生效。
{{ else }}
[top](~${optionPath}.${hostName}${symbolVisit}polygon.top) 和 [bottom](~${optionPath}.${hostName}${symbolVisit}polygon.bottom) 只有一个可以生效。

如果指定 [top](~${optionPath}.${hostName}${symbolVisit}polygon.top) 或 [bottom](~${optionPath}.${hostName}${symbolVisit}polygon.bottom)，则 [shape](~${optionPath}.${hostName}${symbolVisit}polygon.shape) 里的 `y`、`cy` 等定位属性不再生效。
{{ /if }}





{{ target: partial-graphic-cpt-sub-prop-xy }}

###${prefix} x(number) = 0

图形元素的左上角在父节点坐标系（以父节点左上角为原点）中的横坐标值。

###${prefix} y(numbr) = 0

图形元素的左上角在父节点坐标系（以父节点左上角为原点）中的纵坐标值。


{{ target: partial-graphic-cpt-sub-prop-cxy }}

###${prefix} cx(number) = 0

图形元素的中心在父节点坐标系（以父节点左上角为原点）中的横坐标值。

###${prefix} cy(numbr) = 0

图形元素的中心在父节点坐标系（以父节点左上角为原点）中的纵坐标值。


{{ target: partial-graphic-cpt-sub-prop-wh }}

###${prefix} width(number) = 0

图形元素的宽度。

###${prefix} height(numbr) = 0

图形元素的高度。


{{ target: partial-graphic-cpt-sub-prop-r }}

###${prefix} r(number) = 0

外半径。


{{ target: partial-graphic-cpt-sub-prop-rr0 }}

{{ use: partial-graphic-cpt-sub-prop-r(
    prefix=${prefix},
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

###${prefix} r0(number) = 0

内半径。


{{ target: partial-graphic-cpt-sub-prop-x1y1x2y2 }}

###${prefix} x1(number) = 0

开始点的 x 值。

###${prefix} y1(number) = 0

开始点的 y 值。

###${prefix} x2(number) = 0

结束点的 x 值。

###${prefix} y2(number) = 0

结束点的 y 值。


{{ target: partial-graphic-cpt-sub-prop-angle }}

###${prefix} startAngle(number) = 0

开始弧度。

###${prefix} endAngle(number) = Math.PI * 2

结束弧度。

###${prefix} clockwise(boolean) = true

是否顺时针。







{{ target: partial-graphic-cpt-event-handlers }}

{{ if: ${usageType} === 'graphicComponent' }}

##${prefix} onclick(Function)

##${prefix} onmouseover(Function)

##${prefix} onmouseout(Function)

##${prefix} onmousemove(Function)

##${prefix} onmousewheel(Function)

##${prefix} onmousedown(Function)

##${prefix} onmouseup(Function)

##${prefix} ondrag(Function)

##${prefix} ondragstart(Function)

##${prefix} ondragend(Function)

##${prefix} ondragenter(Function)

##${prefix} ondragleave(Function)

##${prefix} ondragover(Function)

##${prefix} ondrop(Function)

{{ /if }}




{{ target: partial-graphic-transform }}

##${prefix} position(Array) = [0, 0]

{{ use: partial-graphic-transform-common-desc(
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} rotation(number) = 0

{{ use: partial-graphic-transform-common-desc(
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} scale(Array) = [1, 1]

{{ use: partial-graphic-transform-common-desc(
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}

##${prefix} origin(number) = [0, 0]

{{ use: partial-graphic-transform-common-desc(
    optionPath=${optionPath},
    usageType=${usageType},
    hostName=${hostName},
    symbolVisit=${symbolVisit},
    symbolDeclare=${symbolDeclare}
) }}


{{ target: partial-graphic-transform-common-desc }}

图形元素可以进行标准的 `2D transform`，其中包含：
+ [平移（position）](~${optionPath}.${hostName}${symbolVisit}polygon.position)：默认值是 `[0, 0]`。表示 `[横向平移的距离, 纵向平移的距离]`。右和下为正值。
+ [旋转（rotation）](~${optionPath}.${hostName}${symbolVisit}polygon.rotation)：默认值是 0。表示旋转的弧度值。正值表示逆时针旋转。
+ [缩放（scale）](~${optionPath}.${hostName}${symbolVisit}polygon.scale)：默认值是 `[1, 1]`。表示 `[横向缩放的倍数, 纵向缩放的倍数]`。

其中，[origin](~${optionPath}.${hostName}${symbolVisit}polygon.origin) 指定了旋转和缩放的中心点，默认值是 `[0, 0]`。

**注意：**
+ transform 中设定的坐标，都是相对于图形元素的父元素的（即 [group](~${optionPath}.${hostName}${symbolVisit}group) 元素或者顶层画布）的 `[0, 0]` 点。也就是说，我们可以使用 [group](~${optionPath}.${hostName}${symbolVisit}group) 来组织多个图形元素，并且 [group](~${optionPath}.${hostName}${symbolVisit}group) 可以嵌套。
+ 对于一个图形元素，`transform` 执行的顺序是：先缩放（scale），再旋转（rotation），再平移（position）。






{{ target: partial-graphic-cpt-style-emphasis }}

{{ if: ${usageType} === 'customSeries' }}

##${prefix} styleEmphasis(Object)

图形元素高亮时的样式。
结构同 [style](~${optionPath}.${hostName}${symbolVisit}polygon.style) 相同。

{{ /if }}



{{ target: partial-graphic-cpt-type-list }}

[image](~${optionPath}.${hostName}${symbolVisit}image),
[text](~${optionPath}.${hostName}${symbolVisit}text),
[circle](~${optionPath}.${hostName}${symbolVisit}circle),
[sector](~${optionPath}.${hostName}${symbolVisit}sector),
[ring](~${optionPath}.${hostName}${symbolVisit}ring),
[polygon](~${optionPath}.${hostName}${symbolVisit}polygon),
[polyline](~${optionPath}.${hostName}${symbolVisit}polyline),
[rect](~${optionPath}.${hostName}${symbolVisit}rect),
[line](~${optionPath}.${hostName}${symbolVisit}line),
[bezierCurve](~${optionPath}.${hostName}${symbolVisit}bezierCurve),
[arc](~${optionPath}.${hostName}${symbolVisit}arc),
[group](~${optionPath}.${hostName}${symbolVisit}group),



