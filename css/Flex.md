# 浅入Flex布局
### 作者：BlackXu
### 参考： [阮一峰：Flex语法](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html/)
## 容器属性
### flex-direction
**主轴的方向。**

- `row（默认值）`：主轴为水平方向，起点在左端。
- `row-reverse`：主轴为水平方向，起点在右端。
- `column`：主轴为垂直方向，起点在上沿。
- `column-reverse`：主轴为垂直方向，起点在下沿。

### flex-wrap
**如果一条轴线排不下，如何换行。**

- `nowrap（默认）`：不换行。
- `wrap`：换行，第一行在上方。
- `wrap-reverse`：换行，第一行在下方。

### flex-flow
**是`flex-direction`和`flex-wrap`的简写形式，默认值为row nowrap。**

### justify-content
**在主轴上的对齐方式。**

- `flex-start`（默认值）：左对齐。
- `flex-end`：右对齐。
- `center`： 居中。
- `space-between`：两端对齐，项目之间的间隔都相等。
- `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### align-items
**在交叉轴上对齐方式。**

- `flex-start`：交叉轴的起点对齐。
- `flex-end`：交叉轴的终点对齐。
- `center`：交叉轴的中点对齐。
- `baseline`: 项目的第一行文字的基线对齐。
- `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

### align-content
**多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。**

- `flex-start`：与交叉轴的起点对齐。
- `flex-end`：与交叉轴的终点对齐。
- `center`：与交叉轴的中点对齐。
- `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
- `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- `stretch`（默认值）：轴线占满整个交叉轴。

## 元素属性
### order
**项目的排列顺序。数值越小，排列越靠前，默认为0。**

### flex-grow
**项目的放大比例，默认为0，即如果存在剩余空间，也不放大。**
**如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。**

### flex-shrink
**项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。**
**如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。**

### flex-basis
**在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。**
**它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。**

### flex
**`flex`是`flex-grow`、`flex-shrink`、`flex-basis`的缩写。**

- 假设以上三个属性同样取默认值，则`flex`的默认值是 0 1 auto。
- 当`flex`取值为 none，则计算值为 0 0 auto。
- 当`flex`取值为 auto，则计算值为 1 1 auto。
- 当`flex`取值为一个非负数字，则该数字为`flex-grow`值，`flex-shrink`取 1，`flex-basis`取 0%。
- 常用的是`flex:1`的属性，代表`flex-grow`取1，`flex-shrink`取1，`flex-basis`取0%。
- 当`flex`取值为一个长度px或百分比%，则视为`flex-basis`值，`flex-grow`取 1，`flex-shrink`取 1。
- 当`flex`取值为两个非负数字，则分别视为`flex-grow`和`flex-shrink`的值，`flex-basis`取 0%。
- 当`flex`取值为一个非负数字和一个长度或百分比，则分别视为`flex-grow`和`flex-basis`的值，`flex-shrink`取 1。

### align-self
**允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。**
**该属性可能取6个值，除了auto，其他都与align-items属性完全一致。**