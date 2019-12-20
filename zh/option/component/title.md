
{{target: component-title}}


# title(Object)

图表的标题组件，包含主标题和副标题。

在 ECharts 中可以使用任意多个标题组件。在需要对标题进行排版，或者单个实例中的多个图表都需要使用标题时都会比较有用。（注意，在 ECharts 2.x 中，单个 ECharts 实例中最多只能有一个标题组件。）

**例如：**在下面不同缓动函数效果的示例中，每一个缓动效果的图表都带有一个标题组件：
~[700x400](${galleryViewPath}line-easing&edit=1&reset=1)

{{use: partial-component-id(prefix="#")}}

## show(boolean) = true

是否显示标题组件。默认为显示，若不想显示标题可将 show 设为 false。

## text(string) = ''

主标题文本。文本支持使用 `\n` 换行。

## link(string) = ''

主标题文本的超链接。

## target(string) = 'blank'

指定在哪个窗口打开主标题文本的超链接。

**可选：**

+ `'self'` 使用当前窗口打开链接。
+ `'blank'` 在新窗口中打开链接。

## textStyle

{{ use: partial-text-style(
    prefix="##",
    name="主标题",
    defaultFontSize=18,
    defaultFontWeight="'bolder'",
    defaultColor="'#333'",
    noAlign=true,
    noVerticalAlign=true,
    noBox=true
) }}


## subtext(string) = ''

副标题文本，支持使用 `\n` 换行。


## sublink(string) = ''

副标题文本的超链接。


## subtarget(string) = 'blank'

指定在哪个窗口打开副标题文本的超链接。

**可选：**

+ `'self'` 使用当前窗口打开链接。
+ `'blank'` 在新窗口中打开链接。


## subtextStyle

{{ use: partial-text-style(
    prefix='##',
    name="副标题",
    defaultColor="'#aaa'",
    noBox=true
) }}


## textAlign(string) = 'auto'

整体文本（包括 text 和 subtext）水平对齐。

**可选：**

`'auto'`、`'left'`、`'right'`、`'center'`。

## textVerticalAlign(string) = 'auto'

整体文本（包括 text 和 subtext）垂直对齐。

**可选：**

`'auto'`、`'top'`、`'bottom'`、`'middle'`。

## triggerEvent(boolean) = false

是否触发事件。

## padding(number) = 5

{{ use: partial-padding(componentName="标题")}}

## itemGap(number) = 10

主标题和副标题之间的间距。

{{use: partial-rect-layout(componentName="grid ")}}

{{ use: partial-component-common-style(
    componentName="标题",
    prefix='#',
    defaultBorderWidth="0",
    hasBorderRadius=true
) }}



