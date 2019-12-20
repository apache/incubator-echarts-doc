{{target: partial-z-zlevel}}

#${prefix|default("#")} zlevel(number) = ${defaultZLevel|default(0)}

${componentName}所有图形的 zlevel 值。

`zlevel` 用于 Canvas 分层，不同 zlevel 值的图形会放置在不同的 Canvas 中，`zlevel` 大的 Canvas 会放在 `zlevel` 小的 Canvas 的上面。Canvas 分层是一种常见的优化手段解决图形之间重叠的问题。我们可以把一些图形变化频繁（例如有动画）的组件设置成一个单独的 `zlevel`。

**注意：**过多的 Canvas 会引起内存开销的增大，在手机端上需要谨慎使用以防崩溃。

#${prefix|default("#")} z(number) = ${defaultZ|default(2)}

${componentName}组件的所有图形的 `z` 值。控制图形的前后顺序。`z` 值小的图形会被 `z` 值大的图形覆盖。

`z` 相比 `zlevel` 优先级更低，而且不会创建新的 Canvas。
