{{ target: partial-progressive}}

#${prefix} progressive(number) = ${defaultProgressive|default(400)}

渐进式渲染时每一帧绘制图形数量，设为 0 时不启用渐进式渲染，支持每个系列单独配置。


在图中有数千到几千万图形元素的时候，一下子把图形绘制出来，或者交互重绘的时候可能会造成界面的卡顿甚至假死。ECharts 4 开始全流程支持渐进渲染（progressive rendering），渲染的时候会把创建好的图形分到数帧中渲染，每一帧渲染只渲染指定数量的图形。

该配置项就是用于配置该系列每一帧渲染的图形数，可以根据图表图形复杂度的需要适当调整这个数字使得在不影响交互流畅性的前提下达到绘制速度的最大化。比如在 lines 图或者平行坐标中线宽大于 1 的 polyline 绘制会很慢，这个数字就可以设置小一点，而线宽小于等于 1 的 polyline 绘制非常快，该配置项就可以相对调得比较大。

#${prefix} progressiveThreshold(number) = ${defaultProgressiveThreshold|default(3000)}

启用渐进式渲染的图形数量阈值，在单个系列的图形数量超过该阈值时启用渐进式渲染。

{{ if: ${supportProgressiveChunkMode} }}
#${prefix} progressiveChunkMode(string) = ${defaultProgressiveChunkMode|default('sequential')}
分片的方式。

**可选：**
+ `'sequential'`：按照数据的顺序分片。缺点是渲染过程不自然。
+ `'mod'`：取模分片，即每个片段中的点会遍布于整个数据，从而能够视觉上均匀得渲染。

{{ /if }}
