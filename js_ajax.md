# AJAX(Asynchronous JavaScript and XML) #

- ajax

**什么是 AJAX？**

> - AJAX = 异步 JavaScript 和 XML。
> - AJAX 是一种用于创建快速动态网页的技术。
> - 通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。
> - 这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
> - 传统的网页（不使用 AJAX）如果需要更新内容，必需重载整个网页面。


Google Suggest

在 2005 年，Google 通过其 Google Suggest 使 AJAX 变得流行起来。
Google Suggest 使用 AJAX 创造出动态性极强的 
web 界面：当您在谷歌的搜索框输入关键字时，JavaScript 会把这些字符发送到服务器，然后服务器会返回一个搜索建议的列表。


## XMLHttpRequest ##


创建 XMLHttpRequest 对象的语法：

    variable=new XMLHttpRequest();

老版本的 Internet Explorer （IE5 和 IE6）使用 ActiveX 对象：

    variable=new ActiveXObject("Microsoft.XMLHTTP");
为了应对所有的现代浏览器，包括 IE5 和 IE6，请检查浏览器是否支持 XMLHttpRequest 对象。
如果支持，则创建 XMLHttpRequest 对象。如果不支持，则创建 ActiveXObject ：

    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }

**XMLHttpRequest 对象用于和服务器交换数据**

    xmlhttp.open("GET","test.asp",true);
    xmlhttp.send();

    open(method,url,async)	
    	规定请求的类型、URL 以及是否异步处理请求。
    	method：请求的类型；GET 或 POST
    	url：文件在服务器上的位置
    	async：true（异步）或 false（同步）

    send(string)	
	    将请求发送到服务器。
	    string：仅用于POST请求


**GET 还是 POST？**

与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。
然而，在以下情况中，请使用 POST 请求：

- 无法使用缓存文件（更新服务器上的文件或数据库）
- 向服务器发送大量数据（POST 没有数据量限制）
- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠



> GET

    xmlhttp.open("GET","test_get.asp",true);
    xmlhttp.send();

参数：url ? key=value & key2=value2

> POST

	xmlhttp.open("POST","test_post.asp",true);
	xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
	xmlhttp.send("account=mly&pwd=123456&email=test@163.com");

> setRequestHeader(header,value)	
> 
- > 向请求添加 HTTP 头。
- > header: 规定头的名称
- > value: 规定头的值


**异步 - True 或 False？**

AJAX 指的是异步 JavaScript 和 XML（Asynchronous JavaScript and XML）。
XMLHttpRequest 对象如果要用于 AJAX 的话，其 open() 方法的 async 参数必须设置为 true;

	xmlhttp.open("GET","ajax_test.asp",true);

对于 web 开发人员来说，发送异步请求是一个巨大的进步。很多在服务器执行的任务都相当费时。AJAX 出现之前，这可能会引起应用程序挂起或停止。
通过 AJAX，JavaScript 无需等待服务器的响应，而是：

- 在等待服务器响应时执行其他脚本
- 当响应就绪后对响应进行处理


**Async = true**

**获取服务器响应**
> xmlhttp.onreadystatechange = 方法


	xmlhttp.onreadystatechange=function(){
	  if (xmlhttp.readyState==4 && xmlhttp.status==200){
			xmlhttp.responseText;	获得字符串形式的响应数据。
			xmlhttp.responseXML;	获得 XML 形式的响应数据。
	    }
	  }

	xmlhttp.open("GET","test1.txt",true);
	xmlhttp.send();
![](images/onready_img.png)
