{{target: component-data-zoom-inside}}

# dataZoom.inside(Object)

**内置型数据区域缩放组件（dataZoomInside）**

（参考[数据区域缩放组件（dataZoom）的介绍](~dataZoom)）

所谓内置，即内置在坐标系中。

+ 平移：在坐标系中滑动拖拽进行数据区域平移。
+ 缩放：
    + PC端：鼠标在坐标系范围内滚轮滚动（MAC触控板类同）
    + 移动端：在移动端触屏上，支持两指滑动缩放。


<br>
<br>


## type(string) = 'inside'

{{use: partial-component-id(prefix="#")}}

## disabled(boolean) = false

是否停止组件的功能。默认不停止。

{{ use: partial-data-zoom-common(
    dataZoomName='dataZoom-inside',
    galleryEditorPath=${galleryEditorPath},
    galleryViewPath=${galleryViewPath}
) }}

## zoomOnMouseWheel(boolean) = true

如何触发缩放。

**可选：**

+ `true`：表示不按任何功能键，鼠标滚轮能触发缩放。
+ `false`：表示鼠标滚轮不能触发缩放。
+ `'shift'`：表示按住 `shift` 和鼠标滚轮能触发缩放。
+ `'ctrl'`：表示按住 `ctrl` 和鼠标滚轮能触发缩放。
+ `'alt'`：表示按住 `alt` 和鼠标滚轮能触发缩放。

## moveOnMouseMove(boolean) = true

如何触发数据窗口平移。

**可选：**

+ `true`：表示不按任何功能键，鼠标移动能触发数据窗口平移。
+ `false`：表示鼠标移动不能触发平移。
+ `'shift'`：表示按住 `shift` 和鼠标移动能触发数据窗口平移。
+ `'ctrl'`：表示按住 `ctrl` 和鼠标移动能触发数据窗口平移。
+ `'alt'`：表示按住 `alt` 和鼠标移动能触发数据窗口平移。

## moveOnMouseWheel(boolean) = true

如何触发数据窗口平移。

**可选：**

+ `true`：表示不按任何功能键，鼠标滚轮能触发数据窗口平移。
+ `false`：表示鼠标滚轮不能触发平移。
+ `'shift'`：表示按住 `shift` 和鼠标滚轮能触发数据窗口平移。
+ `'ctrl'`：表示按住 `ctrl` 和鼠标滚轮能触发数据窗口平移。
+ `'alt'`：表示按住 `alt` 和鼠标滚轮能触发数据窗口平移。

## preventDefaultMouseMove(boolean) = true

是否阻止 mousemove 事件的默认行为。默认阻止。