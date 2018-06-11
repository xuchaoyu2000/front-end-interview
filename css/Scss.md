## 初入Scss/Sass
### 作者：black徐
## linux版本安装
- 通过安装ruby来安装Sass
- `sudo apt-get install ruby-dev`
- `gem install sass`

## 异同
- Scss更接近于Css的语法，需要`{}`和`;`，但对空白符号不敏感。
- Sass更简洁，但对排版有严格要求，可以直接用回车来结束一个属性，或者一个选择器。

```css
//sass
div  
  background-color: #ccc
  color: red
//scss
div { background-color: #ccc; color: red; }
```

## 引入
- 原生Css引入`@import`会产生新的Http请求，而Sass不会。
- 可以在首页引入一个Sass文件，在Sass文件中引入各种分支，如样式重置。

```css
//reset.scss
a { text-decoration: none; }
ul { list-style: none; }
```
```css
@import 'reset.css'; //引入css
@import 'reset','header'; //引入scss，可多个
div { color: red; }
```

## 变量
- 通过`$`符号去声明一个变量。然后通过`$`去引用。

```css
$back-color: #ccc;

div {
  background-color:$back-color;
}
```

## 嵌套
- 类似于js的语法，有包含嵌套的关系。实际上很少用这个，因为难以维护。

```css
div {
  ul {
	list-style: none;
  }
  a {
    text-decoration: none;
  }
}
```
### 嵌套规则
- 可以在父子关系中使用选择器。如下面其实指的`body`下的`.yellow`选择器。

```css
body{
  font-size: 18px;
  color: red;
  
  .yellow{
	color: yellow;
  }
}

```

### 嵌套时可简写引用父级选择器
- 使用`&`来简写。

```css
#span{
  display: block;
  &:hover{ background-color: red;}
  & ul{ list-style: none;}
  &-img{ width: 100%;} //表示#span-img选择器
}
```

### 属性也可以嵌套
- 某些有相同字段的属性可以用`:`来代替原来中间的`-`。

```css
div{
  font: {
    size: 18px;
	weight: bolder;
  }
}
```

## 混合
- 多存放复用的Css用于解决浏览器兼容性。
- 以`@mixin`声明,`@include`复用。

```css
@mixin border-radius($r){
  border-radius: $r;
  -ms-border-radius: $r;
  -moz-border-radius: $r;
  -webkit-border-radius: $r;
}
div{
  @include border-radius(50%);
}
```

## 继承
-以`%参数名`声明，以`@extend %参数名`来复用Css代码段。

```css
%border-bottom{
  border-bottom: 1px solid #ccc; 
}
div{ 
  @extend %border-bottom;
  color: red;
}
```

## 操作符
- 可以在Css中使用算术运算符计算，多用于计算百分比，或rem。

```css
div{ width: 500px / 1200px * 100%;}
```