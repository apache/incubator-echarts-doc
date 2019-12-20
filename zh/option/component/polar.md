
{{target: component-polar}}

# polar(Object)

极坐标系，可以用于散点图和折线图。每个极坐标系拥有一个[角度轴](~angleAxis)和一个[半径轴](~radiusAxis)。

**例如：**

~[600x400](${galleryViewPath}scatter-polar-punchCard&edit=1&reset=1)

{{use: partial-component-id(prefix="#")}}

{{use: component-circular-layout(
    componentName="极坐标系",
    disableArray=false
)}}


{{use: partial-tooltip-in-coords(
    galleryViewPath=${galleryViewPath},
    galleryEditorPath=${galleryEditorPath}
)}}