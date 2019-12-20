{{target:partial-line-style}}

#${prefix} color(Color)={{ if: !${useColorPalatte} }} ${defaultColor|default('"#000"')} {{ else }}'自适应'{{ /if }}

${name}线的颜色。{{ if: ${useColorPalatte} }} 默认从[option.color 调色盘](~color) 获取颜色{{/if}}

{{ if: ${hasCallback} }}
支持使用回调函数。回调函数格式如下：
```js
(params: Object) => Color
```
传入的是数据项 `seriesIndex`, `dataIndex`, `data`, `value` 等各个参数。
{{ /if }}

{{ use: partial-color-desc }}

#${prefix} width(number) = ${defaultWidth|default(1)}

${name}线宽。

#${prefix} type(string) = ${defaultType|default('solid')}

${name}线的类型。

**可选：**
+ `'solid'`
+ `'dashed'`
+ `'dotted'`

{{ use:partial-style-shadow-opacity(
    prefix=${prefix},
    defaultOpacity=${defaultOpacity},
    defaultShadowBlur=${defaultShadowBlur},
    defaultShadowColor=${defaultShadowColor}
) }}
{{ if: ${hasCurveness} }}
#${prefix} curveness(number) = 0
边的曲度。支持从 0 到 1 的值，值越大曲度越大。
{{ /if }}
