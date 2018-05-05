# CANVAS

## 创建

- 在html中用`canvas`标签创建一块画布。
`<canvas id="canvas" width="600" height="600"></canvas>`
- 宽高限制画布大小，所有绘制在此范围内，不写会默认300x150。
- 在js中完成绘制功能。如下：
```javascript
var c=document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
var ctx=c.getContext("2d");
ctx.fillStyle="red";
ctx.fillRect(10,10,200,200);
}
```

- `fillStyle`定义了矩形当前的填充颜色。
- `fillRect(x,y,width,height)` 方法定义了矩形当前的填充位置和大小。
- `strokeStyle`定义了矩形当前的描边颜色。
- `strokeRect(x,y,width,height)` 方法定义了矩形当前的描边位置和大小。
- `clearRect(x,y,width,height)` 方法定义了矩形当前的清除位置和大小。

两个填充矩形重叠后重叠地方被清除，如下：
```javascript
var c=document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
var ctx=c.getContext("2d");
ctx.fillStyle="red";
ctx.fillRect(10,10,100,100);
ctx.fillStyle="blue";
ctx.fillRect(30,30,100,100);
ctx.clearRect(40,40,10,10);
}
```
### Test
* 当你输入一个`XXStyle`后你可以再次输入`XXStyle`会覆盖前面的颜色属性。
* `XXRect`只要出现，没有`XXStyle`会默认黑色；`XXStyle`必须在`XXRect`前面，不然会默认成黑色。
* `XXRect`只要在`XXStyle`后面出现，不论在哪个位置都会绘制，如下：
```javascript
var c=document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
var ctx=c.getContext("2d");
ctx.fillStyle="red";
ctx.fillStyle="green";
ctx.strokeStyle="yellow";
ctx.fillRect(10,10,100,100);
ctx.fillStyle="blue";
ctx.fillRect(30,130,100,100);
ctx.clearRect(40,40,10,10);
ctx.strokeRect(20,20,40,40);
}
```

## 路径

- 调用`beginPath()`开始绘制新路径。
- `moveTo(x,y)` 定义线条开始坐标。
- `arc(x,y,r,start,stop,counterclockwise)`以(x,y)为圆心r为半径画圆。`start`：起始角度，`stop`：结束角度。表示满圆，`start`为0、`stop`为`2*Math.PI`，`counterclockwise`：表示是否顺时针，默认true。
- `arcTo(x1,y1,x2,y2,stop)`从上一点开始到(x2,y2)为止以r为半径穿过(x1,y1)创建弧。
- `bezierCurveTo(c1x,c1y,c2x,c2y,x,y)`从上一点开始绘制曲线，到(x,y)为止并以(c1x,c1y)和(c2x,c2y)为控制点。
- `lineTo(x,y)` 定义线条结束坐标。
- `quadraticCurveTo(cx,cy,x,y)`从上一点开始绘制曲线，到(x,y)为止并以(cx,cy)为控制点。
- `rect(x,y,width,height)`从(x,y)开始绘制矩形。绘制的是矩形路径而非矩形，类似描边。 
- `stroke()`对路径描边，`fill()`填充路径，`clip()`剪切区域。

### 绘制一个时钟：

```javascript
var c=document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.arc(200,200,150,0,2*Math.PI);
ctx.moveTo(340,200);
ctx.arc(200,200,140,0,2*Math.PI);
ctx.moveTo(200,200);
ctx.lineTo(200,90);
ctx.moveTo(200,200);
ctx.lineTo(230,260);
ctx.stroke();
}
```

## 文本
- `font`：定义字体。
- `textAlign`：文本对齐方式，默认即可。
- `textBaseline`：文本基线，默认即可。
- `fillText(text,x,y)`：在 canvas 上绘制实心的文本，一般使用。
- `strokeText(text,x,y)`：在 canvas 上绘制空心的文本。

### 完善时钟

```javascript
var c=document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.arc(200,200,150,0,2*Math.PI);
ctx.moveTo(340,200);
ctx.arc(200,200,140,0,2*Math.PI);
ctx.moveTo(200,200);
ctx.lineTo(200,90);
ctx.moveTo(200,200);
ctx.lineTo(230,260);
ctx.font= "bold 16px Arial";
ctx.fillText('12',190,85);
ctx.fillText('3',320,200);
ctx.fillText('6',195,325);
ctx.fillText('9',80,200);
ctx.stroke();
}
```

## 变换



