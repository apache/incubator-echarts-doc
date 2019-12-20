{{target:partial-area-style}}

#${prefix} color(Color)={{ if: !${useColorPalatte} }} ${defaultColor|default('"#000"')} {{ else }}'自适应'{{ /if }}

填充的颜色。{{ if: ${useColorPalatte} }} 默认从[option.color 调色盘](~color)获取颜色 {{/if}}

{{ use: partial-color-desc }}

{{ if: ${hasCallback} }}
支持使用回调函数。回调函数格式如下：
```js
(params: Object) => Color
```
传入的是数据项 `seriesIndex`, `dataIndex`, `data`, `value` 等各个参数。
{{ /if}}

{{if: ${hasOrigin} }}
#${prefix|default('##')} origin(string) = 'auto'

图形区域的起始位置。

默认情况下，图形会从坐标轴轴线到数据间进行填充。如果需要填充的区域是坐标轴最大值到数据间，或者坐标轴最小值到数据间，则可以通过这个配置项进行设置。

**可选：**

- `'auto'` 填充坐标轴轴线到数据间的区域。此为默认值。
- `'start'` 填充坐标轴底部（非 `inverse` 情况是最小值）到数据间的区域；
- `'end'` 填充坐标轴顶部（非 `inverse` 情况是最大值）到数据间的区域。
{{/if}}



{{ use:partial-style-shadow-opacity(
    prefix=${prefix},
    defaultOpacity=${defaultOpacity},
    defaultShadowBlur=${defaultShadowBlur},
    defaultShadowColor=${defaultShadowColor}
) }}
