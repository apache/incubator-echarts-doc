
{{target: component-x-axis}}

# xAxis(Object)

直角坐标系 grid 中的 X 轴。一般情况下单个 grid 组件最多只能放上下两个 X 轴，多于两个 X 轴时需要通过配置 [offset](~xAxis.offset) 属性以防止同个位置多个 X 轴的重叠。

{{use: partial-component-id(prefix="#")}}

## show(boolean) = true

是否显示 X 轴。默认显示。

## gridIndex(number) = 0

X 轴所在的 grid 的索引，默认位于第一个 grid。

## position(string)

X 轴的位置。

**可选：**
+ `'top'`
+ `'bottom'`

默认 grid 中的第一个 X 轴在 grid 的下方（`'bottom'`），第二个 X 轴放在第一个 X 轴位置的另一侧。

## offset(number) = 0

X 轴相对于默认位置的偏移，在相同的 `position` 上有多个 X 轴的时候有用。

{{ use: axis-common(
    prefix='#',
    componentType='xAxis',
    axisTypeDefault="'category'",
    hasSplitLineAndArea=true,
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
)}}


{{use:partial-z-zlevel(
    prefix="#",
    componentName="X 轴",
    defaultZ=0
) }}
