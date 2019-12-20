{{target:partial-barGrid}}

## barWidth(number|string) = 自适应
柱条的宽度，不设时自适应。

{{use: partial-barGrid-value-absolute-or-percent}}

{{use:partial-barGrid-share-desc(seriesType=${seriesType})}}

## barMaxWidth(number|string) = null
柱条的最大宽度。

比 [barWidth](~series-bar.barWidth) 优先级高。

{{use: partial-barGrid-value-absolute-or-percent}}

{{use:partial-barGrid-share-desc(seriesType=${seriesType})}}

## barMinWidth(number|string)
柱条的最小宽度。在直角坐标系中，默认值是 `1`。否则默认值是 `null`。

比 [barWidth](~series-bar.barWidth) 优先级高。

{{use: partial-barGrid-value-absolute-or-percent}}

{{use:partial-barGrid-share-desc(seriesType=${seriesType})}}

## barMinHeight(number) = 0
柱条最小高度，可用于防止某数据项的值过小而影响交互。

## barGap(string) = ${barGapDefault|default('30%')}
不同系列的柱间距离，为百分比（如 `'30%'`，表示柱子宽度的 `30%`）。

如果想要两个系列的柱子重叠，可以设置 barGap 为 `'-100%'`。这在用柱子做背景的时候有用。

{{use:partial-barGrid-share-desc(seriesType=${seriesType})}}

**例如：**
~[600x400](${galleryViewPath}doc-example/barGrid-barGap&reset=1&edit=1)

## barCategoryGap(string) = '20%'
同一系列的柱间距离，默认为类目间距的20%，可设固定值

{{use:partial-barGrid-share-desc(seriesType=${seriesType})}}





{{target:partial-barGrid-share-desc}}

在同一坐标系上，此属性会被多个 `'${seriesType}'` 系列共享。此属性应设置于此坐标系中最后一个 `'${seriesType}'` 系列上才会生效，并且是对此坐标系中所有 `'${seriesType}'` 系列生效。


{{target: partial-barGrid-value-absolute-or-percent}}
可以是绝对值例如 `40` 或者百分数例如 `'60%'`。百分数基于自动计算出的每一类目的宽度。
