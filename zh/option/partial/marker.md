{{ target: partial-marker }}


{{use: partial-mark-point(
    prefix=${prefix},
    seriesType=${seriesType},
    hasCoord=${hasCoord},
    hasType=${hasType},
    galleryEditorPath=${galleryEditorPath}
)}}prefix
{{use: partial-mark-line(
    prefix=${prefix},
    seriesType=${seriesType},
    hasCoord=${hasCoord},
    hasType=${hasType},
    galleryEditorPath=${galleryEditorPath}
)}}
{{use: partial-mark-area(
    prefix=${prefix},
    seriesType=${seriesType},
    hasCoord=${hasCoord},
    hasType=${hasType},
    galleryEditorPath=${galleryEditorPath}
)}}




{{ target: marker-coord-explain }}

**注：**对于 [axis.type](~xAixs.type) 为 `'category'` 类型的轴

+ 如果 coord 值为 `number`，则表示 [axis.data](~xAxis.data) 的 index。
+ 如果 coord 值为 `string`，则表示 [axis.data](~xAxis.data) 中具体的值。注意使用这种方式时，xAxis.data 不能写成 [number, number, ...]，而只能写成 [string, string, ...]，否则不能被 markPoint / markLine 用『具体值』索引到。

 **例如：** 
```javascript
{
    xAxis: {
        type: 'category',
        data: ['5', '6', '9', '13', '19', '33']
        // 注意这里不建议写成 [5, 6, 9, 13, 19, 33]，否则不能被 markPoint / markLine 用『具体值』索引到。
    },
    series: {
        type: 'line',
        data: [11, 22, 33, 44, 55, 66],
        markPoint: { // markLine 也是同理
            data: [{
                coord: [5, 33.4], // 其中 5 表示 xAxis.data[5]，即 '33' 这个元素。
                // coord: ['5', 33.4] // 其中 '5' 表示 xAxis.data中的 '5' 这个元素。
                                      // 注意，使用这种方式时，xAxis.data 不能写成 [number, number, ...]
                                      // 而只能写成 [string, string, ...]
            }]
        }
    }
}
```