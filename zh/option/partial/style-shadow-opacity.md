{{target:partial-style-shadow}}

#${prefix} shadowBlur(number) = ${defaultShadowBlur}

整个图例区域阴影的模糊大小。该属性配合 `shadowColor`,`shadowOffsetX`, `shadowOffsetY` 一起设置图形的阴影效果。

**例如：**
```js
{
    shadowColor: 'rgba(0, 0, 0, 0.5)',
    shadowBlur: 10
}
```

{{if: ${needShow} }}
**注意:**此配置项生效的前提是设置了 `show: true` 以及值不为 `transparent` 的背景色 [backgroundColor](~legend.backgroundColor)。
{{/if}}


#${prefix} shadowColor(Color) = ${defaultShadowColor}

整个图例区域阴影的颜色。支持的格式同 `color`。

{{if: ${needShow} }}
**注意:**此配置项生效的前提是设置了 `show: true` 以及值不为 `transparent` 的背景色 [backgroundColor](~legend.backgroundColor)。
{{/if}}


#${prefix} shadowOffsetX(number) = ${defaultShadowOffsetX|default(0)}

整个图例区域阴影在水平方向上的偏移距离。

{{if: ${needShow} }}
**注意:**此配置项生效的前提是设置了 `show: true` 以及值不为 `transparent` 的背景色 [backgroundColor](~legend.backgroundColor)。
{{/if}}


#${prefix} shadowOffsetY(number) = ${defaultShadowOffsetY|default(0)}

整个图例区域阴影在垂直方向上的偏移距离。

{{if: ${needShow} }}
**注意:**此配置项生效的前提是设置了 `show: true` 以及值不为 `transparent` 的背景色 [backgroundColor](~legend.backgroundColor)。
{{/if}}


{{target:partial-style-opacity}}

#${prefix} opacity(number) = ${defaultOpacity}

图形的透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。


{{target:partial-style-shadow-opacity}}

{{use: partial-style-shadow(
    prefix=${prefix},
    defaultOpacity=${defaultOpacity},
    defaultShadowColor=${defaultShadowColor},
    defaultShadowBlur=${defaultShadowBlur},
    defaultShadowOffsetX=${defaultShadowOffsetX},
    defaultShadowOffsetY=${defaultShadowOffsetY}
)}}
{{use: partial-style-opacity(
    prefix=${prefix},
    defaultOpacity=${defaultOpacity},
    defaultShadowColor=${defaultShadowColor},
    defaultShadowBlur=${defaultShadowBlur},
    defaultShadowOffsetX=${defaultShadowOffsetX},
    defaultShadowOffsetY=${defaultShadowOffsetY}
)}}
