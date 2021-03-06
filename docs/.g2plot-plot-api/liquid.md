### 图表容器

#### width

<description>**optional** _number_ _default:_ `400`</description>

设置图表宽度。

#### height

<description>**optional** _number_ _default:_ `400`</description>

设置图表高度。

#### autoFit

<description>**optional** _boolean_ _default:_ `true`</description>

图表是否自适应容器宽高。当 `autoFit` 设置为 true 时，`width` 和 `height` 的设置将失效。

#### padding

<description>**optional** _number\[] | number | 'auto'_</description>

画布的 `padding` 值，代表图表在上右下左的间距，可以为单个数字 `16`，或者数组 `[16, 8, 16, 8]` 代表四个方向，或者开启 `auto`，由底层自动计算间距。

#### appendPadding

<description>**optional** _number\[] | number_</description>

额外增加的 `appendPadding` 值，在 `padding` 的基础上，设置额外的 padding 数值，可以是单个数字 `16`，或者数组 `[16, 8, 16, 8]` 代表四个方向。

#### renderer

<description>**optional** _string_ _default:_ `canvas`</description>

设置图表渲染方式为 `canvas` 或 `svg`。

#### pixelRatio

<description>**optional** _number_ _default:_ `window.devicePixelRatio`</description>

设置图表渲染的像素比，和底层的 devicePixelRatio 含义一致，一般不用设置，除非在页面有整体 scale 的情况下，可以自定义。

### 数据映射

#### percent

<description>**required** _number_</description>

指标比例数据 \[0-1]。

#### radius

<description>**optional** _number_ _default:_ `0.9`</description>

外环的半径 \[0-1]，相对于画布宽高的最小值来计算的。

### 图形样式

#### liquidStyle

<description>**optional** _StyleAttr | Function_</description>

水波图的样式。

<!--图形样式-->

| 属性名 | 类型 | 介绍 |
| --- | --- | --- |
| fill | string | 图形的填充色 |
| fillOpacity | number | 图形的填充透明度 |
| stroke | string | 图形的描边 |
| lineWidth | number | 图形描边的宽度 |
| lineDash | \[number,number] | 描边的虚线配置，第一个值为虚线每个分段的长度，第二个值为分段间隔的距离。lineDash 设为\[0,0]的效果为没有描边。 |
| lineOpacity | number | 描边透明度 |
| opacity | number | 图形的整体透明度 |
| shadowColor | string | 图形阴影颜色 |
| strokeOpacity | number | 图形边框透明度 |
| shadowBlur | number | 图形阴影的高斯模糊系数 |
| shadowOffsetX | number | 设置阴影距图形的水平距离 |
| shadowOffsetY | number | 设置阴影距图形的垂直距离 |
| cursor | string | 鼠标样式。同 css 的鼠标样式，默认 'default'。 |

示例代码：

```ts
{
  style: {
    fill: 'red',
    fillOpacity: 0.5,
    stroke: 'black',
    lineWidth: 1,
    lineDash: [4, 5],
    strokeOpacity: 0.7,
    shadowColor: 'black',
    shadowBlur: 10,
    shadowOffsetX: 5,
    shadowOffsetY: 5,
    cursor: 'pointer'
  }
}
```

关于 ShapeStyle 更加详细的文档参考 [绘图属性](/guide/graphic-style)。

#### color

<description>**optional** _string | string\[] | Function_</description>

指定点的颜色。如没有配置 colorField，指定一个单值即可。对 colorFiled 进行了配置的情况下，即可以指定一系列色值，也可以通过回调函数的方法根据对应数值进行设置。

默认配置：采用 theme 中的色板。

```ts
// 设置单一颜色
{
  color: '#a8ddb5'
}
// 设置多色
{
  colorField: 'type', // 部分图表使用 seriesField
  color: ['#d62728', '#2ca02c', '#000000'],
}
// Function
{
  colorField: 'type', // 部分图表使用 seriesField
  color: ({ type }) => {
    if(type === 'male'){
      return 'red';
    }
    return 'yellow';
  }
}
```

### 图表组件

#### statistic ✨

<description>**optional** _object_</description>

指标中心文本组件。

| 配置项  | 类型  | 描述          |
| ------- | ----- | ------------- |
| title   | false | StatisticText | 标题 |
| content | false | StatisticText | 主体内容 |

StatisticText

| 配置项 | 类型 | 描述 |
| --- | --- | --- |
| style | CSSStyleDeclaration | 统计文本的样式 (css 样式) |
| customHtml | `(container: HTMLElement, view: View, datum: object, data: object[]) => string;` | 自定义主体文本的 html，优先级高于 formatter |
| formatter | Function | 主体文本的格式化内容 |
| rotate | number | 旋转角度 |
| offsetX | number | X 偏移值 |
| offsetY | number | Y 偏移值 |
