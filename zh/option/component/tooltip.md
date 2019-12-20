
{{target: component-tooltip}}

# tooltip(Object)

提示框组件。

---

{{use: partial-tooltip-introduction}}

{{use: partial-tooltip-coords-common(
    prefix='#',
    galleryViewPath=${galleryViewPath}
)}}

## showContent(boolean) = true

是否显示提示框浮层。默认显示。只需 tooltip 触发事件或显示 axisPointer ，而不需要显示内容时可设为 `false` 不显示。

## alwaysShowContent(boolean) = false

是否永远显示提示框内容。默认情况下在移出可触发提示框区域后 [一定时间](~tooltip.hideDelay) 后隐藏，设置为 `true` 可以保证一直显示提示框内容。


## triggerOn(string) = 'mousemove|click'

提示框触发的条件。

**可选：**

+ `'mousemove'`：鼠标移动时触发。

+ `'click'`：鼠标点击时触发。

+ `'mousemove|click'`：同时鼠标移动和点击时触发。

+ `'none'`：不在 `'mousemove'` 或 `'click'` 时触发，用户可以通过 [action.tooltip.showTip](api.html#action.tooltip.showTip) 和 [action.tooltip.hideTip](api.html#action.tooltip.hideTip) 来手动触发和隐藏。也可以通过 [axisPointer.handle](~xAxis.axisPointer.handle) 来触发或隐藏。


## showDelay(number) = 0

浮层显示的延迟。单位为 ms，默认为 0 即没有延迟。一般不建议设置延迟。只在 [triggerOn](~tooltip.triggerOn) 为 `'mousemove'` 时有效。

## hideDelay(number) = 100

浮层隐藏的延迟，单位为 ms，在 [alwaysShowContent](~tooltip.alwaysShowContent) 为 `true` 的时候无效。

## enterable(boolean) = false

鼠标是否可进入提示框浮层中，默认为false，如需详情内交互，如添加链接，按钮，可设置为 `true`。

## renderMode(string) = 'html'

浮层的渲染模式，默认以 `'html` 即额外的 DOM 节点展示 tooltip；此外还可以设置为 `'richText'` 表示以富文本的形式渲染，渲染的结果在图表对应的 Canvas 中（目前 SVG 尚未支持富文本），这对于一些没有 DOM 的环境（如微信小程序）有更好的支持。

## confine(boolean) = false

是否将 tooltip 框限制在图表的区域内。

当图表外层的 dom 被设置为 `'overflow: hidden'`，或者移动端窄屏，导致 tooltip 超出外界被截断时，此配置比较有用。

## transitionDuration(number) = 0.4

提示框浮层的移动动画过渡时间，单位是秒 (s)，设置为 0 的时候会紧跟着鼠标移动。


{{ use: partial-tooltip-common(scope='global', prefix='#') }}

