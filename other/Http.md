## Http几种请求方法的差别
### 作者：BlackXu 
## GET
- 它本质就是发送一个请求来取得服务器上的某一资源。资源通过一组HTTP头和呈现数据（如HTML文本，或者图片或者视频等）返回给客户端。  
- GET请求中，永远不会包含呈现数据。  

## POST
- 向URL指定的资源提交数据或附加新的数据。 
- 数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改。

## GET与POST区别
| 区别点        | GET           | POST        |
| ------------ |:-------------:| -----------:|
| 后退/刷新     |  无影响        | 重新提交数据 |
| 书签          | 可收藏         |   不可收藏  |
| 编码          | application/x-www-form-urlencoded | application/x-www-form-urlencoded或multipart/form-data |
| 历史          | 会保存        |   不会保存  |
| 长度限制      | 现在在2048字符内 |   无  |
| 类型限制      | 只允许ASCII字符 |   无  |
| 安全         | 安全性差，在URL中可见参数 | 安全，参数不会被保存  |
| 可见性       | 可见       | 不可见    |

## HEAD
- 只请求页面的首部。 
- 类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头。

## DELETE
- 删除服务器上的某资源。

## OPTIONS
- 允许客户端查看服务器的性能。
- 用于获取当前URL所支持的方法。如果请求成功，会有一个Allow的头包含类似“GET,POST”这样的信息。

## PUT
- 从客户端向服务器传送的数据取代指定的文档的内容。
- 跟POST方法很像，也是想服务器提交数据。但是，它们之间有不同。PUT指定了资源在服务器上的位置，而POST没有。PUT方法请求服务器去把请求里的实体存储在请求URI（Request-URI）标识下。如果请求URI（Request-URI）指定的的资源已经在源服务器上存在，那么此请求里的实体应该被当作是源服务器关于此URI所指定资源  实体的最新修改版本。如果请求RI（Request-URI）指定的资源不存在，并且此URI被用户代理定义为一个新资源，那么源服务器就应该根据请求里的实体创建一个此URI所标识下的资源。如果一个新的资源被创建了，源服务器必须能向用户代理（user agent）发送201（已创建）响应。如果已存在的资源被改变了，那么源服务器应该发送200（Ok）或者204（无内容）响应。如果资源不能根据请求URI创建或者改变，一个合适的错误响应应该给出以反应问题的性质。实体的接收者不能忽略任何它不理解和不能实现的Content-*（如：Content-Range）头域，并且必须返回501（没有被实现）响应。如果请求穿过一个缓存（cache），并且此请求URI（Request-URI）指示了一个或多个当前缓存的实体，那么这些实体应该被看作是旧的。PUT方法的响应是不可缓存的。POST方法和PUT方法请求最根本的区别是请求URI（Request-URI）的含义不同。POST请求里的URI 指示一个能处理请求实体的资源（译注：此资源可能是一段程序，如jsp 里的servlet） 。此资源可能是一个数据接收过程，一个网关（gateway，译注：网关和代理的区别是：网关可以进行协议转换，而代理不能，只是起代理的作用，比如缓存服务器其实就是一个代理），或者一个单独接收注释的实体。对比而言，PUT方法请求里的URI标识请求里封装的实体一一用户代理知道URI意指什么，并且服务器不能把此请求应用于其它资源（resource）。如果服务器期望请求被应用于一个不同的URI，那么它必须发送301（永久移动）响应；用户代理可以自己决定是否重定向请求。一个单独的资源可能会被许多不同的URI指定。如：一篇文章可能会有一个URI指定当前版本，而这个URI区别于这篇文章其它特殊版本的URI。这种情况下，对一个通用URI的PUT请求可能会导致其资源的其它URI请求被源服务器重定义。HTTP/1.1没有定义PUT方法对源服务器的状态影响。PUT请求必须遵循8.2节中的消息传送的要求。除非特别指出，PUT方法请求里的实体头域应该被用于资源的创建或修改。

## TRACE
- 回显服务器收到的请求，主要用于测试或诊断。
- TRACE方法被用于激发一个远程的，应用层的请求消息回路（译注：TRACE方法让客户端测试到服务器的网络通路，回路的意思如发送一个请返回一个响应，这就是一个请求响应回路）。最后的接收者也许是源服务器，也许是接收到包含Max-Forwards头域值为0请求的代理或网关。TRACE请求不能包含一个实体。TRACE方法允许客户端去了解数据被请求链的另一端接收的情况，并且利用那些数据信息去测试或诊断。Via头域值有特殊的用途，因为它可以作为请求链的跟踪信息。利用Max-Forwards头域允许客户端限制请求链的长度，这是非常有用的，因为可以利用此去测试代理链在无限循环里转发消息。如果请求是有效的，响应应该在实体主体里包含整个请求消息，并且响应应该包含一个Content-Type头域值为”message/http”的头域。此方法的响应不能被缓存。   

## CONNECT
- HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。
- 把请求连接转换到透明的TCP/IP通道。