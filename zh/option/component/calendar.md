{{ target: component-calendar }}

# calendar(Object)

日历坐标系组件。

在 ECharts 中，我们非常有创意地实现了日历图，是通过使用日历坐标系组件来达到日历图效果的，如下方的几个示例图所示，我们可以在热力图、散点图、关系图中使用日历坐标系。

在日历坐标系中使用热力图的示例:
~[800x400](${galleryViewPath}calendar-heatmap&edit=1&reset=1)

在日历坐标系中使用散点图的示例:
~[800x600](${galleryViewPath}calendar-effectscatter&edit=1&reset=1)

在日历坐标系中使用关系图（以及混合图表）的示例:
~[600x600](${galleryViewPath}calendar-graph&edit=1&reset=1)

灵活利用 ECharts 图表和坐标系的组合，以及 API，可以实现更丰富的效果。
[在日历中使用文字](${galleryEditorPath}calendar-lunar&edit=1&reset=1)、
[在日历中放置饼图](${galleryEditorPath}calendar-pie&edit=1&reset=1)

---

**水平和垂直放置日历**

在日历坐标系可以水平放置，也可以垂直放置。如上面的例子，使用热力图时，经常是水平放置的。但是如果需要格子的尺寸大些，水平放置就过于宽了，于是也可以选择垂直放置。参见 [calendar.orient](~calendar.orient)。


---

**尺寸的自适应**

可以设置日历坐标系使他支持不同尺寸的容器（页面）大小变化的自适应。首先，和 ECharts 其他组件一样，日历坐标系可以选择使用 [left](~calendar.left) [right](~calendar.right) [top](~calendar.top) [bottom](bottom) [width](~calendar.width) [height](~calendar.height) 来描述尺寸和位置，从而将日历摆放在上下左右各种位置，并随着页面尺寸变动而改变自身尺寸。另外，也可以使用 [cellSize](~calendar.cellSize) 来固定日历格子的长宽。

---

**中西方日历习惯的支持**

中西方日历有所差别，西方常使用星期日作为一周的第一天，中国使用星期一为一周的第一天。日历坐标系做了这种切换的支持。参见 [calendar.dayLabel.firstDay](~calendar.dayLabel.firstDay)。

另外，日历上的月份和星期的文字，也可以较方便的切换中英文，甚至自定义。参见 [calendar.dayLabel.nameMap](~calendar.dayLabel.nameMap) [calendar.monthLabel.nameMap](~calendar.monthLabel.nameMap)。



---

{{use: partial-component-id(prefix="#")}}

{{ use: partial-rect-layout-width-height(
    componentName="calendar",
    defaultLeft="80",
    defaultTop="60"
) }}

## range(number|string|Array)
必填，日历坐标的范围 支持多种格式。

**例如：**
```js

// 某一年
range: 2017

// 某个月
range: '2017-02'

// 某个区间
range: ['2017-01-02', '2017-02-23']

// 注意：此写法会识别为['2017-01-01', '2017-02-01']
range: ['2017-01', '2017-02']

```


## cellSize(number|Array) = 20

日历每格框的大小，可设置单值 或数组  第一个元素是宽 第二个元素是高。
支持设置自适应：`auto`, 默认为高宽均为 20。

**例如：**
```js

// 设置宽高均为20
cellSize: 20

// 设置宽为20，高为40
cellSize: [20, 40]

// 设置宽高均为40
cellSize: [40]

// 设置宽高均自适应
cellSize: 'auto'

// 设置宽自适应，高为40
cellSize: ['auto', 40]

```

## width(number|string) = auto
日历坐标的整体宽度。

**注意:** 默认 cellSize 为 20，若设置了 `width` 的值, 则 `cellSize` 中的宽度强制转为 `auto`;

## height(number|string) = auto
日历坐标的整体高度，

**注意:** 默认 cellSize 为 20，若设置了 `height` 的值, 则 `cellSize` 中的高度强制转为 `auto`;


## orient(string) = 'horizontal'
日历坐标的布局朝向。

**可选：**
+ 'horizontal'
+ 'vertical'

## splitLine(Object)
设置日历坐标分隔线的样式。

### show(boolean) = ${defaultShow|default(true)}
是否显示分隔线。默认显示。

### lineStyle(Object)

{{ use: partial-line-style(
    prefix='###',
    defaultColor="#000",
    defaultWidth=1,
    defaultType="solid",
    name="分隔线"
) }}


**例如：**
```js
calendar: [{
    splitLine: {
        show: true,
        lineStyle: {
            color: '#000',
            width: 1,
            type: 'solid'
        }
    }
}]
```

## itemStyle(Object)
设置日历格的样式。
{{ use:partial-item-style(
    prefix="##",
    name="calendar",
    defaultColor="#fff",
    defaultBorderWidth=1,
    defaultBorderColor="'#ccc'"
) }}


**例如：**
```js
calendar: [{
    itemStyle: {
        color: '#fff',
        borderWidth: 1,
        borderColor: '#ccc'
    }
}]
```

## dayLabel(Object)
设置日历坐标中 星期轴的样式。

### show(boolean) = true
是否在普通状态下显示标签。默认显示。

### firstDay(number) = 0
一周从周几开始，默认从周日开始。

**例如：**

```js

calendar: [{
    dayLabel: {
        firstDay: 1 // 从周一开始
    }
}]

```

### margin(number) = 0
星期标签与轴线之间的距离。

### position(string) = 'start'
星期的位置 在星期轴的开头还是结尾。

**可选：**
+ 'start'
+ 'end'

### nameMap(string|Array) = 'en'
星期显示的效果，默认为'en'。
可设置中英文以及自定义。下标 0 为对应星期天的文字显示。

**例如：**
```js
// 快捷设置英文 ['S', 'M', 'T', 'W', 'T', 'F', 'S'],
nameMap: 'en'
// 快捷设置中文 ['日', '一', '二', '三', '四', '五', '六']
nameMap: 'cn'
// 自定义设置： 中英文混杂 或者不显示
nameMap: ['S', '一', 'T', '三', '', '五', 'S'],

calendar: [{
    dayLabel: {
        nameMap: 'en'
    }
}]
```

{{ use: partial-text-style(prefix='##', defaultColor="#000",) }}


## monthLabel(Object)
设置日历坐标中月份轴的样式。

### show(boolean) = true
是否在普通状态下显示标签。默认显示。

### align(string) = 'center'
设置月份区间内的月份文字位置。

**可选：**
+ 'center'： 区间内的中间。
+ 'left'： 区间内的左边。

### margin(number) = 5
月份标签与轴线之间的距离。

### position(string) = 'start'
月份的位置 在开头还是结尾。

**可选：**
+ 'start'
+ 'end'

### nameMap(string|Array) = 'en'
月份显示的效果，默认为'en'。
可设置中英文以及自定义。下标 0 为对应一月的文字显示。

**例如：**
```js
// 快捷设置英文 [
                'Jan', 'Feb', 'Mar',
                'Apr', 'May', 'Jun',
                'Jul', 'Aug', 'Sep',
                'Oct', 'Nov', 'Dec'
            ],
nameMap: 'en'
// 快捷设置中文 [
                '一月', '二月', '三月',
                '四月', '五月', '六月',
                '七月', '八月', '九月',
                '十月', '十一月', '十二月'
            ]
nameMap: 'cn'
// 自定义设置： 中英文混杂 或者不显示
nameMap: [
            '一月', 'Feb', '三月',
            '四月', 'May', '六月',
            '七月', '八月', '',
            '十月', 'Nov', '十二月'
        ],

calendar: [{
    monthLabel: {
        nameMap: 'en'
    }
}]
```

### formatter(string|Function) = null

用来格式化月份文本，支持字符串模板和回调函数两种形式。

**例如：**
```js
// 使用字符串模板，例如：2017-02
/*
    模板变量{nameMap} 月份原本名称 eg：'Feb'
    模板变量{yyyy}   四位数年份 eg: 2017
    模板变量{yy}   后两位数年份 eg: 17
    模板变量{MM}   两位数月份 eg: 02
    模板变量{M}   一位数月份 eg: 2
*/
formatter: '{yyyy}-{MM}'
// 使用回调函数
/*
    param.nameMap 月份原本名称 eg：'Feb'
    param.yyyy   四位数年份 eg: 2017
    param.yy   后两位数年份 eg: 17
    param.MM   两位数月份 eg: 02
    param.M   一位数月份 eg: 2
*/
formatter: function (param) {
    // ...
    return param.MM;
}
```

{{ use: partial-text-style(prefix='##', defaultColor="#000") }}

## yearLabel(Object)
设置日历坐标中年的样式。

### show(boolean) = true
是否在普通状态下显示标签。默认显示。

### margin(number) = 30
年份与轴线之间的距离。

### position(string)
年份的位置。
默认为横向是 'left' ，竖向是 'top'。

**可选：**
+ 'top'
+ 'bottom'
+ 'left'
+ 'right'

### formatter(string|Function) = null

用来格式化年份文本，支持字符串模板和回调函数两种形式。
默认显示当前范围的年，若区间跨年 显示 ('start-end')。

**示例：**
```js
// 使用字符串模板，例如：['2017-10-11', '2018-01-21']
/*
    模板变量{nameMap} 年份原本名称 eg：'2017-2018'
    模板变量{start}   开始年份 eg: 2017
    模板变量{end}   结束年份 eg: 2018
*/

formatter: '{start}-{end}'
// 使用回调函数
/*
    param.nameMap 年份原本名称 eg：'2017-2018'
    param.start   开始年份 eg: 2017
    param.end   结束年份 eg: 2018
*/
formatter: function (param) {
    // ...
    return param.end;
}
```

{{ use: partial-text-style(prefix='##') }}


{{ use:partial-silent(
    prefix="#",
    defaultFontWeight="bolder",
    defaultFontSize="20"
) }}
