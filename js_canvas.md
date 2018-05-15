# Canvas

## 什么是Canvas

`<canvas>`是 HTML5 新增的元素，可使用JavaScript脚本来绘制图形。

`<canvas`是一个矩形区域，您可以控制其每一像素。

## 引入Canvas
```html
<canvas id="canvas" width="300" height="300"></canvas>
```

`<canvas>` 看起来和 `<img>` 元素很相像，唯一的不同就是它并没有 `src` 和 `alt` 属性。实际上，`<canvas>` 标签只有两个属性—— `width` 和 `height`，并且这些属性都是可选的。

#### width 和 height 属性
当没有设置宽度和高度的时候，`canvas` 会初始化宽度为300像素和高度为150像素。该元素可以使用CSS来定义大小，但在绘制时图像会伸缩以适应它的框架尺寸：如果CSS的尺寸与初始画布的比例不一致，它会出现扭曲。

	*注意*: 如果你绘制出来的图像是扭曲的, 尝试在<canvas>的属性中明确规定宽和高，而不是使用CSS。
	
#### 兼容性
某些较老的浏览器（尤其是IE9之前的IE浏览器）或者文本浏览器不支持HTML元素"canvas"，在这些浏览器上会把`<canvas>`标签内部的内容显示出来，因此我们可以在这些不支持`<canvas>`的浏览器上提供一些替代内容，而支持`<canvas>`的浏览器将会忽略在容器中包含的内容，并且只是正常渲染canvas。

```html
<canvas id="myCanvas" width="150" height="150">
  如果您的浏览器不支持Canvas，那么您将看到本行文字
</canvas>
```

####  </canvas> 标签不可省
与 `<img>` 元素不同，`<canvas>` 元素需要结束标签(`</canvas>`).如果结束标签不存在，则文档的其余部分会被认为是替代内容，将不会显示出来。

## 获取绘图上下文(the rendering context)
canvas起初是空白的.如果想要对canvas进行一些操作，那么则需要获取canvas的绘图上下文对象。`<canvas>` 元素有一个做 `getContext()` 的方法，这个方法是用来获得渲染上下文和它的绘画功能。`getContext()`只有一个参数，上下文的格式.对于2D图像而言，这个格式参数是`"2d"`。

```javascript
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');
```

如果在不支持`<canvas>`的浏览器中运行了上述代码，会抛出一个错误.所以在我们获取绘图上下文对象之前，应该先检查一下浏览器对该特性的支持情况。

```javascript
var canvas = document.getElementById('tutorial');

if (canvas.getContext){
  var ctx = canvas.getContext('2d');
  // drawing code here
} else {
  // canvas-unsupported code here
}
```

## 基本绘图操作
和Windows操作系统自带的画图程序一样，`Canvas`的两种基本绘图操作是填充和描边。填充，就是用指定的样式（颜色、渐变或图像）填充图形；描边，就是只在图形的边缘画线。填充和描边的样式分别取决于两个属性：`fillStyle`和`strokeStyle`。这两个属性的值可以是字符串、渐变对象或模式对象，而且它们的默认值都是`"#000000"`。如果为它们指定表示颜色的字符串值，可以使用 CSS 中指定颜色值的任何格式，包括颜色名、十六进制码、 rgb、rgba、hsl 或 hsla。

## 绘制矩形
矩形是唯一一种可以直接在 2D 上下文中绘制的形状.与矩形有关的方法包括 `fillRect()`、 `strokeRect()` 和 `clearRect()`。这三个方法都能接收 4 个参数：矩形的 x 坐标、矩形的 y 坐标、矩形宽度和矩形高度。这些参数的单位都是像素。

#### 填充矩形
`fillRect(x, y, width, height)`

#### 绘制矩形描边
`strokeRect(x, y, width, height)`

#### 清除矩形
	该方法的功能类似于Windows系统中画图程序的橡皮擦，会将指定矩形矩形区域中的所有内容全部清除。
	
`clearRect(x, y, width, height)`

## 绘制路径
如果要绘制矩形以外的形状，则需要自定义绘制路径。2D 绘制上下文支持很多在画布上绘制路径的方法。要绘制路径，首先必须调用 beginPath()方法，表示要开始绘制新路径。然后，再通过调用下列方法来实际地绘制路径。

### `arc(x, y, radius, startAngle, endAngle, counterclockwise)`

> 以`(x,y)`为圆心绘 制一条弧线，弧线半径为 `radius`，起始和结束角度（用弧度表示）分别为 `startAngle` 和 `endAngle`。最后一个参数表示 `startAngle` 和 `endAngle` 是否按逆时针方向计算，值为 `false` 表示按顺时针方向计算。

### `arcTo(x1, y1, x2, y2, radius)`
> 从上一点开始绘制一条弧线，到`(x2,y2)`为止，并且以 给定的半径 `radius` 穿过`(x1,y1)`。

### `lineTo(x, y)`
> 从上一点开始绘制一条直线，到`(x,y)`为止。

### `moveTo(x, y)`
> 将绘图游标移动到`(x,y)`，不画线。

### `rect(x, y, width, height)`
> 从点`(x,y)`开始绘制一个矩形，宽度和高度分别由 `width` 和 `height` 指定。这个方法绘制的是矩形路径，而不是 `strokeRect()` 和 `fillRect()` 所绘制的独立的形状。

创建了路径后，接下来有几种可能的选择。如果想绘制一条连接到路径起点的线条，可以调用 `closePath()`。如果路径已经完成，你想用 `fillStyle` 填充它，可以调用 `fill()` 方法。另外，还可 以调用 `stroke()` 方法对路径描边，描边使用的是 `strokeStyle`。最后还可以调用 `clip()`，这个方法可以在路径上创建一个剪切区域。

	绘制一个简易时钟

```javascript
var canvas = document.getElementById("canvas");
//确定浏览器支持元素 
if (canvas.getContext){
	var context = canvas.getContext("2d");

	//开始路径
	context.beginPath();
	
	//绘制外圆
	context.arc(100, 100, 99, 0, 2 * Math.PI, false);
	
	//绘制内圆
	context.moveTo(194, 100);
	context.arc(100, 100, 94, 0, 2 * Math.PI, false);
	
	//绘制分针
	context.moveTo(100, 100);
	context.lineTo(100, 15);
	
	//绘制时针
	context.moveTo(100, 100);
	context.lineTo(35, 100);
	
	//描边路径
	context.stroke();
}
```

## 绘制文本
绘制文本主要有两个方法：`fillText()` 和 `strokeText()`。这两个方法都可以接收 4 个参数：要绘制的文本字符串、`x` 坐标、`y` 坐标和可选的最大像素宽度。

而绘制出来文本的样式，由下面3个属性决定：

#### `font`
> 表示文本样式、大小及字体，用 CSS 中指定字体的格式来指定，例如`"10px Arial"`。

#### `textAlign`
> 表示文本对齐方式。可能的值有 `"start"`、`"end"`、`"left"`、`"right"` 和 `"center"`。建议使用 `"start"` 和 `"end"`，不要使用 `"left"` 和 `"right"`，因为前两者的意思更稳妥，能同时适合从左到右和从右到左显示（阅读）的语言。

#### `textBaseline`
> 表示文本的基线。可能的值有 `"top"`、`"hanging"`、`"middle"`、`"alphabetic"`、 `"ideographic"` 和 `"bottom"`。

```javascript
context.font = 'bold 14px Arial';
context.textAlign = 'center';
context.textBaseline = 'middle';
context.fillText('hello, world', 100, 100);
```
	


