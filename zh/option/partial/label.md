{{target:partial-label-desc}}

${name}图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等，`label`选项在 ECharts 2.x 中放置于`itemStyle`下，在 ECharts 3 中为了让整个配置项结构更扁平合理，`label` 被拿出来跟 `itemStyle` 平级，并且跟 `itemStyle` 一样拥有 `emphasis` 状态。


{{target:partial-label}}
#${prefix} show(boolean) = ${defaultShowLabel|default("false")}
是否显示标签。

{{ if: !${noPosition} }}
#${prefix} position(string|Array) = ${defaultPosition}
{{use:partial-label-position}}
{{ /if }}

#${prefix} distance(number) = 5
距离图形元素的距离。当 position 为字符描述值（如 `'top'`、`'insideRight'`）时候有效。

参见：[label position](${galleryEditorPath}doc-example/label-position)。


{{ if: !${noRotate} }}
#${prefix} rotate(number) = ${defaultRotate}
标签旋转。从 -90 度到 90 度。正值是逆时针。

参见：[label rotation](${galleryEditorPath}bar-label-rotation)。
{{ /if }}


#${prefix} offset(Array)
是否对文字进行偏移。默认不偏移。例如：`[30, 40]` 表示文字在横向上偏移 `30`，纵向上偏移 `40`。

{{ if: ${formatter} }}
#${prefix} formatter(string|Function)
{{use:partial-2d-data-label-formatter}}
{{ elif: ${formatter1d} }}
#${prefix} formatter(string|Function)
{{use:partial-1d-data-label-formatter}}
{{ /if }}


{{ if: !${noTextStyle} }}
{{ use:partial-text-style(
    prefix=${prefix},
    noAlign=${noAlign},
    noVerticalAlign=${noVerticalAlign},
    name=${name},
    defaultColor=${defaultColor},
    defaultFontSize=${defaultFontSize},
    noRich=${noRich},
    noBox=${noBox},
    enableAutoColor=true
) }}
{{ /if }}


{{ if: ${ellipsis} }}
#${prefix} ellipsis(boolean) = true

当文字超出的时候，是否超出部分替换为省略号。
{{ /if }}


{{ target:partial-label-position }}
标签的位置。

通过相对的百分比或者绝对像素值表示标签相对于图形包围盒左上角的位置。

 **例如：** 
```js
    // 绝对的像素值
    position: [10, 10],
    // 相对的百分比
    position: ['50%', '50%']
    ```

**可选：**

+ [x, y]
+ 'top'
+ 'left'
+ 'right'
+ 'bottom'
+ 'inside'
+ 'insideLeft'
+ 'insideRight'
+ 'insideTop'
+ 'insideBottom'
+ 'insideTopLeft'
+ 'insideBottomLeft'
+ 'insideTopRight'
+ 'insideBottomRight'

参见：[label position](${galleryViewPath}doc-example/label-position)。