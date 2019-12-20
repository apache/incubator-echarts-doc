
{{target: component-parallel}}

# parallel(Object)

{{ use: partial-parallel-introduce(
    galleryViewPath=${galleryViewPath}
)}}

<br>
<br>

{{use: partial-component-id(prefix="#")}}

{{ use: partial-rect-layout-width-height(
    componentName='parallel ',
    defaultLeft: 80,
    defaultRight: 80,
    defaultTop: 60,
    defaultBottom: 60
) }}


## layout(string) = 'horizontal'

布局方式。

**可选：**

+ `'horizontal'`：水平排布各个坐标轴。

+ `'vertical'`：竖直排布各个坐标轴。

## axisExpandable(boolean) = false

{{use: partial-parallel-high-dim (
    galleryViewPath=${galleryViewPath}
)}}

是否允许点击展开折叠 axis。

## axisExpandCenter(number) = null

初始时，以哪个轴为中心展开，这里给出轴的 index。没有默认值，需要手动指定。

参见 [parallel.axisExpandable](parallel.axisExpandable)

## axisExpandCount(number) = 0

初始时，有多少个轴会处于展开状态。建议根据你的维度个数而手动指定。

参见 [parallel.axisExpandCenter](parallel.axisExpandCenter)
参见 [parallel.axisExpandable](parallel.axisExpandable)

## axisExpandWidth(number) = 50

在展开状态，轴的间距是多少，单位为像素。

参见 [parallel.axisExpandable](parallel.axisExpandable)

## axisExpandTriggerOn(string) = 'click'

可取值：
+ `'click'`：鼠标点击的时候 expand。
+ `'mousemove'`：鼠标悬浮的时候 expand。


## parallelAxisDefault(Object)

{{use: partial-parallel-axis-default}}

[参见示例](${galleryEditorPath}doc-example/parallel-all&edit=1&reset=1)

<br>

{{ use: axis-common(
    prefix='##',
    componentType='parallelAxis',
    noAxisPointer=true,
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
) }}