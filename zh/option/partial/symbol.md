{{target: partial-symbol}}

#${prefix} symbol(string{{ if: ${hasCallback} }}|Function{{ /if}}) = ${defaultSymbol}

${name}标记的图形。

{{ use: partial-icon }}

{{ if: ${hasCallback} }}
如果需要每个数据的图形不一样，可以设置为如下格式的回调函数：
```js
(value: Array|number, params: Object) => string
```
其中第一个参数 `value` 为 [data](~series-${seriesType}.data) 中的数据值。第二个参数 `params` 是其它的数据项参数。
{{ /if }}

#${prefix} symbolSize(number|Array{{ if: ${hasCallback} }}|Function{{ /if}}) = ${defaultSymbolSize}

${name}标记的大小，可以设置成诸如 `10` 这样单一的数字，也可以用数组分开表示宽和高，例如 `[20, 10]` 表示标记宽为 `20`，高为 `10`。

{{ if: ${hasCallback} }}
如果需要每个数据的图形大小不一样，可以设置为如下格式的回调函数：
```js
(value: Array|number, params: Object) => number|Array
```
其中第一个参数 `value` 为 [data](~series-${seriesType}.data) 中的数据值。第二个参数 `params` 是其它的数据项参数。
{{ /if }}

#${prefix} symbolRotate(number)

${name}标记的旋转角度。**注意:**在 `markLine` 中当 `symbol` 为 `'arrow'` 时会忽略 `symbolRotate` 强制设置为切线的角度。

#${prefix} symbolKeepAspect(boolean) = false

如果 `symbol` 是 `path://` 的形式，是否在缩放时保持该图形的长宽比。

#${prefix} symbolOffset(Array) = [0, 0]

${name}标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置，但是如果 symbol 是自定义的矢量路径或者图片，就有可能不希望 symbol 居中。这时候可以使用该配置项配置 symbol 相对于原本居中的偏移，可以是绝对的像素值，也可以是相对的百分比。

例如 `[0, '50%']` 就是把自己向上移动了一半的位置，在 symbol 图形是气泡的时候可以让图形下端的箭头对准数据点。
