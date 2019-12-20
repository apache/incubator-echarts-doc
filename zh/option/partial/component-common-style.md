
{{ target: partial-component-common-style }}

#${prefix} backgroundColor(Color) = 'transparent'

${componentName}背景色，默认透明。

> 颜色可以使用 RGB 表示，比如 `'rgb(128, 128, 128)'`   ，如果想要加上 alpha 通道，可以使用 RGBA，比如 `'rgba(128, 128, 128, 0.5)'`，也可以使用十六进制格式，比如 `'#ccc'`

{{if: ${needShow} }}
**注意:**此配置项生效的前提是，设置了 `show: true`。
{{/if}}

#${prefix} borderColor(Color) = '#ccc'

${componentName}的边框颜色。支持的颜色格式同 backgroundColor。

{{if: ${needShow} }}
**注意:**此配置项生效的前提是，设置了 `show: true`。
{{/if}}

#${prefix} borderWidth(number) = ${defaultBorderWidth|default(1)}

${componentName}的边框线宽。

{{if: ${needShow} }}
**注意:**此配置项生效的前提是，设置了 `show: true`。
{{/if}}

{{if: ${hasBorderRadius} }}
{{use: partial-border-radius(prefix=${prefix})}}
{{/if}}

{{ use:partial-style-shadow(prefix=${prefix}, needShow=true) }}






{{target: partial-border-radius}}

#${prefix} ${propName|default('borderRadius')}(number|Array) = 0
圆角半径，单位为 px，支持传入数组分别指定 4 个圆角半径。

**例如:**
```
${propName|default('borderRadius')}: 5, // 统一设置四个角的圆角大小
${propName|default('borderRadius')}: [5, 5, 0, 0] //（顺时针左上，右上，右下，左下）
```