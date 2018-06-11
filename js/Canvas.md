# 初入Canvas
### 作者：BlackXu   
### 参考：`<<JS高级程序设计>>`
## 创建
- 在html中用`canvas`标签创建一块画布。
`<canvas id="canvas" width="600" height="600"></canvas>`
- 宽高限制画布大小，所有绘制在此范围内，不写会默认300x150。
- 在js中完成绘制功能。如下：

```javascript
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.fillStyle = "red";
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
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.fillStyle = "red";
  ctx.fillRect(10,10,100,100);
  ctx.fillStyle = "blue";
  ctx.fillRect(30,30,100,100);
  ctx.clearRect(40,40,10,10);
}
```
### 练习
* 当你输入一个`XXStyle`后你可以再次输入`XXStyle`会覆盖前面的颜色属性。
* `XXRect`只要出现，没有`XXStyle`会默认黑色；`XXStyle`必须在`XXRect`前面，不然会默认成黑色。
* `XXRect`只要在`XXStyle`后面出现，不论在哪个位置都会绘制，如下：

```javascript
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.fillStyle = "red";
  ctx.fillStyle = "green";
  ctx.strokeStyle = "yellow";
  ctx.fillRect(10,10,100,100);
  ctx.fillStyle = "blue";
  ctx.fillRect(30,130,100,100);
  ctx.clearRect(40,40,10,10);
  ctx.strokeRect(20,20,40,40);
}
```
## 路径
- 调用`beginPath()`：开始绘制新路径。
- `moveTo(x,y)`：定义线条开始坐标。
- `arc(x,y,r,start,stop,counterclockwise)`：以(x,y)为圆心r为半径画圆。`start`：起始角度，`stop`：结束角度。表示满圆，`start`为0、`stop`为`2*Math.PI`，`counterclockwise`：表示是否顺时针，默认true。
- `arcTo(x1,y1,x2,y2,stop)`：从上一点开始到(x2,y2)为止以r为半径穿过(x1,y1)创建弧。
- `bezierCurveTo(c1x,c1y,c2x,c2y,x,y)`：从上一点开始绘制曲线，到(x,y)为止并以(c1x,c1y)和(c2x,c2y)为控制点。
- `lineTo(x,y)`：定义线条结束坐标。
- `quadraticCurveTo(cx,cy,x,y)`：从上一点开始绘制曲线，到(x,y)为止并以(cx,cy)为控制点。
- `rect(x,y,width,height)`：从(x,y)开始绘制矩形。绘制的是矩形路径而非矩形，类似描边。 
- `stroke()`：对路径描边，`fill()`：填充路径，`clip()`：剪切区域。
- `closePath()`：创建从当前点到开始点的路径。
- `isPointInPath(x,y)`：判断(x,y)是否位于当前路径中，是返回true，否则返回false。
 
### 绘制一个时钟：
```javascript
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.beginPath();
  ctx.arc(200,200,150,0,2 * Math.PI);
  ctx.moveTo(340,200);
  ctx.arc(200,200,140,0,2 * Math.PI);
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
- `measureText(text)`：检查text的宽度，返回一个带有width的对象。

### 完善时钟
```javascript
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.beginPath();
  ctx.arc(200,200,150,0,2 * Math.PI);
  ctx.moveTo(340,200);
  ctx.arc(200,200,140,0,2 * Math.PI);
  ctx.moveTo(200,200);
  ctx.lineTo(200,90);
  ctx.moveTo(200,200);
  ctx.lineTo(230,260);
  ctx.font = "bold 16px Arial";
  ctx.fillText('12',190,85);
  ctx.fillText('3',320,200);
  ctx.fillText('6',195,325);
  ctx.fillText('9',80,200);
  ctx.stroke();
}
```
## 变换
- `scale(x,y)`：缩放当前绘图，x方向乘以x，y方向乘以y。
- `rotate(x)`：旋转当前绘图。
- `translate(x,y)`：重新映射画布上的 (0,0) 位置。
- `transform(m1x,m1y,m2x,m2y,dx,dy)`：替换绘图的当前转换矩阵。
- `setTransform(m1x,m1y,m2x,m2y,dx,dy)`：将当前转换重置为单位矩阵。然后运行 transform()。

直接修改时钟原点再绘制表针更简单。
```javascript
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.beginPath();
  ctx.arc(200,200,150,0,2 * Math.PI);
  ctx.moveTo(340,200);
  ctx.arc(200,200,140,0,2 * Math.PI);
  ctx.translate(200,200);
  ctx.moveTo(0,0);
  ctx.lineTo(0,-110);
  ctx.moveTo(0,0);
  ctx.lineTo(30,60);
  ctx.stroke();
}
```
## 其他方面
- `save()`：保存当前所有设置，对上下文进行其他修改，可连续使用，只会保存设置和变换，不会保存内容。
- `restore()`：回到保存时的状态，可连续返回。

```js
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.fillStyle = "red";
  ctx.save();
  ctx.fillStyle = "green";
  ctx.strokeStyle = "yellow";
  ctx.fillRect(10,10,100,100);
  ctx.restore(); //不会保有strokeStyle为黄色了
  ctx.fillRect(100,100,200,200);
  ctx.fillStyle = "blue";
  ctx.fillRect(30,130,100,100);
  ctx.clearRect(40,40,10,10);
  ctx.strokeRect(20,20,40,40);
}
```
## 绘制图像
- `drawImage(img,sx,sy,swidth,sheight,x,y,width,height)`：img表示图片、画布或视频（在某标签中引用后用dom操作），中间四个数据表示剪切的图像位置和大小，后四个表示要绘制到的位置和大小。中间四个和最后的大小都可以省略。

```js
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  var img = new Image();
  img.src = 'img/doubleOne.png';
  img.onload = function(){
    ctx.drawImage(img,0,0,100,100,10,10,210,210);
  }
}
```
## 阴影
- `shadowColor`：设置或返回用于阴影的颜色。
- `shadowBlur`：设置或返回用于阴影的模糊级别。
- `shadowOffsetX`：设置或返回阴影与形状的水平距离。
- `shadowOffsetY`：设置或返回阴影与形状的垂直距离。

```js
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.shadowOffsetX = 5;
  ctx.shadowOffsetY = 5;
  ctx.shadowBlur = 4;
  ctx.shadowColor = "rgba(0,0,0,.5)";
  ctx.fillStyle = "red";
  ctx.fillRect(100,100,200,200);
  ctx.fillStyle = "blue";
  ctx.fillRect(30,130,100,100);
}
```
## 渐变
- `createLinearGradient(x,y,x1,y1)`：创建线条渐变。
- `createRadialGradient(x,y,r,x1,y1,r1)`：创建一个径向/圆渐变。
- `addColorStop()`：指定颜色。0-1分别表示开始到结束的颜色。

```js
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  var grd = ctx.createLinearGradient(20,20,150,100);
  grd.addColorStop(0,'white');
  grd.addColorStop(.5,"blue");
  grd.addColorStop(1,'black');
  ctx.fillStyle = grd;
  ctx.fillRect(20,20,150,100);
}
```
## 模式
- `createPattern(img,rep)`：img表示图片、视频或其他canvas元素，rep表示重复的方向和次数。 

```js
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.rect(0,0,600,600);
  var img = new Image();
  img.src = 'img/doubleOne.png';
  img.onload = function(){
    var pat = ctx.createPattern(img,"repeat");
    ctx.fillStyle = pat;
    ctx.fill();
  }
}
```
## 使用图像数据
- `getImageData(x,y,width,height)`：返回包含width、height、data的对象，data里存储的是rgba的四个元素，该对象拷贝了画布指定矩形的像素数据。
- `putImageData(imgData,x,y,dirtyX,dirtyY,dirtyWidth,dirtyHeight)`：前三个表示放回画布的imageData对象和坐标，后四个可选，表示放置图像的位置水平值、垂直值、宽高。
- `createImageData(width,height)、(imageData)`：创建一个定宽高的空白ImageData对象，参数可以是一个imageData，就会创建一个与之宽高相同的空白ImageData对象。

实现图像的灰阶过滤(用getImageData会引起跨域问题)：
```js
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  var img = new Image();
  img.src = 'img/new_pic03.jpg';
  img.onload = function(){
    ctx.drawImage(img,0,0,150,150,10,10,210,210);
  }
  var i,len,avg,r,g,b,a;
  var imgData = ctx.getImageData(0,0,200,200);
  var data = imgData.data;
  for(i = 0,len = data.length;i < len;i += 4){
    r = data[i];
    g = data[i + 1];
    b = data[i + 2];
    a = data[i + 3];
    avg = Math.floor((r + g + b) / 3);
    data[i] = data[i + 1] = data[i + 2] = avg;
  }
  imgData.data = data;
  ctx.putImageData(imgData,0,0);
}
```
## 合成
- `globalAlpha = x`：设置或返回绘图的当前透明值为x。
- `globalCompositeOperation = x`：设置或返回新图像如何绘制到已有的图像上。`source-over`默认，在目标图像上显示源图像。`source-atop`在目标图像顶部显示源图像。源图像位于目标图像之外的部分是不可见的。`source-in`在目标图像中显示源图像。只有目标图像之内的源图像部分会显示，目标图像是透明的。`source-out`在目标图像之外显示源图像。只有目标图像之外的源图像部分会显示，目标图像是透明的。`destination-over`在源图像上显示目标图像。`destination-atop`在源图像顶部显示目标图像。目标图像位于源图像之外的部分是不可见的。`destination-in`在源图像中显示目标图像。只有源图像之内的目标图像部分会被显示，源图像是透明的。`destination-out`在源图像之外显示目标图像。只有源图像之外的目标图像部分会被显示，源图像是透明的。`lighter`显示源图像 + 目标图像。`copy`显示源图像。忽略目标图像。`xor`使用异或操作对源图像与目标图像进行组合。

```js
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.fillStyle="red";
  ctx.fillRect(20,20,75,50);
  ctx.globalAlpha=0.2;
  ctx.fillStyle="blue"; 
  ctx.fillRect(50,50,75,50); 
  ctx.fillStyle="green"; 
  ctx.fillRect(80,80,75,50);
}
```
```js
var c = document.getElementById("canvas");
if(c.getContext){//确认是否支持canvas
  var ctx = c.getContext("2d");
  ctx.fillStyle="red";
  ctx.fillRect(20,20,75,50);
  ctx.globalCompositeOperation="source-over";
  ctx.fillStyle="blue"; 
  ctx.fillRect(50,50,75,50); 
  ctx.fillStyle="red";
  ctx.fillRect(150,20,75,50);
  ctx.globalCompositeOperation="destination-over";
  ctx.fillStyle="blue"; 
  ctx.fillRect(180,50,75,50);
}
```