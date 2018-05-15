
# DOM对象(文档对象模型) #
HTML DOM 是 W3C 标准（是 HTML 文档对象模型的英文缩写，Document Object Model for HTML）。HTML DOM 定义了用于 HTML 的一系列标准的对象，以及访问和处理 HTML 文档的标准方法。通过 DOM，可以访问所有的 HTML 元素，连同它们所包含的文本和属性。可以对其中的内容进行修改和删除，同时也可以创建新的元素。

###1. 属性###
<table style='width:800px;font-size:14px;text-align:center;'><tr><th>属性</th><th>描述</th></tr><tr><td>document.title</td><td>返回当前文档的标题</td></tr><tr><td>document.URL</td><td>返回文档完整的URL</td></tr><tr><td>document.bgColor</td><td>背景色</td></tr><tr><td>document.fgColor</td><td>前景色</td></tr></table>
###2. 方法###
**2.1 document.getElementById("elementID");**

定义和用法:
- 返回对拥有指定 ID 的第一个对象的引用
- 如果没有指定 ID 的元素返回 null

**2.2 document.getElementsByTagName("tagname");**

定义和用法:
- 返回带有指定标签名的对象的集合
- 参数值 "*" 返回文档的所有元素
- 返回的集合对象拥有 length 属性,并且可以通过 Index 来访问集合中的元素

**2.3 document.getElementsByName("name");**

定义和用法:
- 返回带有指定名称的对象的集合
- 返回的集合对象拥有 length 属性,并且可以通过 Index 来访问集合中的元素
- 存在兼容性问题(该方法适用于表单操作)
>IE 浏览器中,如果name存在于form表单中,可以正常使用,但是如果出现在例如div元素中,则不能正常返回值,原因是name并不是div的标准属性
>CHROM, FIREFOX 均正常

**2.4 document.getElementsByClassName("classname");**

定义和用法:
- 返回文档中所有指定类名的元素集合
- 返回的集合对象拥有 length 属性,并且可以通过 Index 来访问集合中的元素
- 存在兼容性问题(FF,CHROM 支持该方法,IE不支持)
解决办法:
```
function getElesByClassName(className) {
    var arr = [];
    if(document.getElementsByClassName) {
        return document.getElementsByClassName(className);
    } else {
        var tags = document.getElementsByTagName("*");
        for(var i = 0; i < tags.length; i++) {
            if(tags[i].className == className) {
                arr.push(tags[i]);
            }
        }
        return arr;
    }
}
```

###3. 对象集合###
**3.1 all**
所有对象的集合,常用来做兼容性判断
**3.2 forms**
所有form表单集合
```
console.log(document.forms.length);
```
- 通过 index 来访问表单对象
```
document.forms[0];
``` 
- 通过表单的 name 属性来访问表单对象
```
document.forms["name"];
```

###4. 操作元素内容###
**4.1 innerHTML: 设置或获取标签对中的内容( 识别HTML )**
**4.2 innerText: 获取文字内容( IE ) textContent: 获取文字内容(FF,chrom)**
```
function getContent(obj, val) {
    if(document.all) {
        if(val) {
            obj.innerText = val;
        } else {
            return obj.innerText;
        }
    } else {
        if(val) {
            obj.textContent = val;
        } else {
            return obj.textContent;
        }
    }
}
```
###5. 属性操作###
**5.1 直接操作**
object.attr = value ( 获取和设置 )
**5.2 方法**
获取: object.getAttribute("attr") 
设置: 对象.setAttribute("attr", "value")

###6. 样式操作###
**6.1 行内样式**
设置和获取: object.style.attr 示例: hover
```
html:
<a id="one" href="#" style="color: red;background-color: blue; padding: 3px;">跳转</a>
javascript:
(function() {
    var one = document.getElementById("one");
    one.onmouseover = function() {
        this.style.color = "blue";
        this.style.backgroundColor = "red";
    };
    one.onmouseout = function() {
        this.style.color = "red";
        this.style.backgroundColor = "blue";
    };
}());
```
**6.2 css层叠样式**
- **通过 className 修改样式**
- **获取或修改某个属性的值(兼容性问题)**
<table style='width:800px;font-size:14px;text-align:center;'><tr><th>属性</th><th>描述</th></tr><tr><td>document.styleSheets</td><td>返回样式表的集合</td></tr><tr><td>document.styleSheets[index].rules / document.styleSheets[index].cssRules</td><td>返回样式表中选择器的集合</td></tr><tr><td>document.styleSheets[index].rules[index].style.attr</td><td>查找样式表中的样式属性(**ie chrom**)</td></tr><tr><td>document.styleSheets[index].cssRules[index].style.attr</td><td>查找样式表中的样式属性(**firefox**)</td></table>
- **动态添加或删除**
document.styleSheets[index].insertRule("selector{attr:value}", index);
document.styleSheets[index].deleteRule(index);
document.styleSheets[index].addRule("selector","attr:value", index);
document.styleSheets[index].removeRule(index);

**6.3 获取最终样式(只能获取,不能操作)**
object.currentStyle.attr ( IE )
window.getComputedStyle(object,null).attr ( W3C )
**6.4 获得元素尺寸(可直接运算)	**
clientWidth/clientHeight: 元素可视部分的高度和宽度(width + padding)
offsetWidth/offsetHeight: 元素实际的高度和宽度(width+padding+border)

