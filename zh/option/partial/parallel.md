{{target: partial-parallel-introduce}}

<br>

---

**平行坐标系介绍**

[平行坐标系（Parallel Coordinates）](https://en.wikipedia.org/wiki/Parallel_coordinates) 是一种常用的可视化高维数据的图表。

{{use: partial-parallel-data-example}}

平行坐标系适用于对这种多维数据进行可视化分析。每一个维度（每一列）对应一个坐标轴，每一个『数据项』是一条线，贯穿多个坐标轴。在坐标轴上，可以进行数据选取等操作。

 **例如：** 

~[600x400](${galleryViewPath}doc-example/parallel-all&edit=1&reset=1)

<br>

---

**配置方式概要**

『平行坐标系』的 `option` 基本配置。

 **例如：** 

```javascript
option = {
    parallelAxis: [                     // 这是一个个『坐标轴』的定义
        {dim: 0, name: schema[0].text}, // 每个『坐标轴』有个 'dim' 属性，表示坐标轴的维度号。
        {dim: 1, name: schema[1].text},
        {dim: 2, name: schema[2].text},
        {dim: 3, name: schema[3].text},
        {dim: 4, name: schema[4].text},
        {dim: 5, name: schema[5].text},
        {dim: 6, name: schema[6].text},
        {dim: 7, name: schema[7].text,
            type: 'category',           // 坐标轴也可以支持类别型数据
            data: ['优', '良', '轻度污染', '中度污染', '重度污染', '严重污染']
        }
    ],
    parallel: {                         // 这是『坐标系』的定义
        left: '5%',                     // 平行坐标系的位置设置
        right: '13%',
        bottom: '10%',
        top: '20%',
        parallelAxisDefault: {          // 『坐标轴』的公有属性可以配置在这里避免重复书写
            type: 'value',
            nameLocation: 'end',
            nameGap: 20
        }
    },
    series: [                           // 这里三个系列共用一个平行坐标系
        {
            name: '北京',
            type: 'parallel',           // 这个系列类型是 'parallel'
            data: [
                [1,  55,  9,   56,  0.46,  18,  6,  '良'],
                [2,  25,  11,  21,  0.65,  34,  9,  '优'],
                ...
            ]
        },
        {
            name: '上海',
            type: 'parallel',
            data: [
                [3,  56,  7,   63,  0.3,   14,  5,  '良'],
                [4,  33,  7,   29,  0.33,  16,  6,  '优'],
                ...
            ]
        },
        {
            name: '广州',
            type: 'parallel',
            data: [
                [4,  33,  7,   29,  0.33,  16,  6,  '优'],
                [5,  42,  24,  44,  0.76,  40,  16, '优'],
                ...
            ]
        }
    ]
};
```

需要涉及到三个组件：[parallel](~parallel)、[parallelAxis](~parallelAxis)、[series-parallel](~series-parallel)

+ [parallel](~parallel)

    这个配置项是平行坐标系的『坐标系』本身。一个系列（`series`）或多个系列（如上图中的『北京』、『上海』、『广州』分别各是一个系列）可以共用这个『坐标系』。

    和其他坐标系一样，坐标系也可以创建多个。

    位置设置，也是放在这里进行。

+ [parallelAxis](~parallelAxis)

    这个是『坐标系』中的坐标轴的配置。自然，需要有多个坐标轴。

    其中有 [parallelAxis.parallelIndex](~parallelAxis.parallelIndex) 属性，指定这个『坐标轴』在哪个『坐标系』中。默认使用第一个『坐标系』。

+ [series-parallel](~series-parallel)

    这个是『系列』的定义。系列被画到『坐标系』上。

    其中有 [series-parallel.parallelIndex](~series-parallel.parallelIndex) 属性，指定使用哪个『坐标系』。默认使用第一个『坐标系』。

<br>

---

**配置注意和最佳实践**

{{use: partial-parallel-axis-default}}

**如果数据量很大并且发生卡顿**

建议把 [series-parallel.lineStyle.width](~series-parallel.lineStyle.width) 设为 `0.5`（或更小），
可能显著改善性能。

<br>

---

**高维数据的显示**

{{use: partial-parallel-high-dim (galleryViewPath=${galleryViewPath})}}



{{target: partial-parallel-data-example}}
例如 [series-parallel.data](~series-parallel.data) 中有如下数据：

```javascript
[
    [1,  55,  9,   56,  0.46,  18,  6,  '良'],
    [2,  25,  11,  21,  0.65,  34,  9,  '优'],
    [3,  56,  7,   63,  0.3,   14,  5,  '良'],
    [4,  33,  7,   29,  0.33,  16,  6,  '优'],
    { // 数据项也可以是 Object，从而里面能含有对线条的特殊设置。
        value: [5,  42,  24,  44,  0.76,  40,  16, '优']
        lineStyle: {...},
    }
    ...
]
```
数据中，每一行是一个『数据项』，每一列属于一个『维度』。（例如上面数据每一列的含义分别是：『日期』,『AQI指数』, 『PM2.5』, 『PM10』, 『一氧化碳值』, 『二氧化氮值』, 『二氧化硫值』）。




{{target: partial-parallel-axis-default}}

配置多个 [parallelAxis](~parallelAxis) 时，有些值一样的属性，如果书写多遍则比较繁琐，那么可以放置在 [parallel.parallelAxisDefault](~parallel.parallelAxisDefault) 里。在坐标轴初始化前，[parallel.parallelAxisDefault](~parallel.parallelAxisDefault) 里的配置项，会分别融合进 [parallelAxis](~parallelAxis)，形成最终的坐标轴的配置。



{{target: partial-parallel-high-dim}}

维度比较多时，比如有 50+ 的维度，那么就会有 50+ 个轴。那么可能会页面显示不下。

可以通过 [parallel.axisExpandable](~parallel.axisExpandable) 来改善显示效果。
