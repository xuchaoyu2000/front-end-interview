# 优雅的使用Markdownpad2
### 作者：black徐 
## 步骤1:下载
- 下载：点击蓝色按钮下载
[MP官网](http://markdownpad.com/)
![](https://i.imgur.com/YIWwhqQ.png)

- 查看版本
通过路径：`Help-About MarkdownPad`
![版本](https://i.imgur.com/nBW0kdp.png)
- 通过授权激活
- 邮箱：` Soar360@live.com `
- 授权密匙： `请通过下面链接原作者处获得，本人于18年4月27日测试可用。`

**简书上提供注册码的作者，原文：[注册码](https://www.jianshu.com/p/9e5cd946696d)**

## 步骤2:window10如果出现View Crashed Error
- win10安装会出现书写错误，请安装[awesomium](http://markdownpad.com/download/awesomium_v1.6.6_sdk_win.exe)

![Awesomium](https://i.imgur.com/rN8RiTJ.png)

## 技巧
### 中文模式
- tools->Options->editor->Application Language->中文
![Chinese](https://i.imgur.com/nVmb61b.png)
### 代码高亮设置
- tools->Options-Markdown->Markdown Processor->GitHub Flavored Markdown 
![HighLight](https://i.imgur.com/mfCsBg4.png)
- 需要登录GitHub账号 
- 连续三个反引号`，就是按键1前面的那个符号再加代码类型
- 如:三个\`后加javascript 写完再三个 \`，效果如下：
``` javascript
function great(){
	console.log("You're Great man.")
}
```

### 跳转锚点
`## <span id=a>next</span>`·
`跳转到[next](#a)`

跳转到[结束.](#end)
- 【注意】锚点跳转需要先导出成html格式的文件才行，在Markdownpad2使用在线预览功能不会触发锚点跳转哦

### 引用链接
`[example name](http://example.com/)"Title"`

### 图片
`![Alt text](/path/to/img.jpg "Optional title")`
- 图片链接Alt text可以省略不写。

### 代码换行
- 比上一行缩进两个tab位置或四个空格。
- tools->Options-Markdown->Markdown Processor->GitHub Flavored Markdown(Offline)（在线不在线都行）

## 快捷键
- ctrl+shift+o 有序列表
- ctrl+u 无序列表
- ctrl+g 插入图片
- ctrl+l 插入超链接
- ctrl+k 插入代码
- ctrl+b 加粗
- ctrl+i 斜体
- ctrl+1 插入H1
- ctrl+2 插入H2
- ctrl+q 插入引用

## 简写形式
#### 分隔线：
- 在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内除了空格不能有其他东西。
`---`
#### 强调：
- 被两个\*或者\_包裹起来。
`**强调**`
#### 斜体：
- 被一个\*或者\_包裹起来。
`*斜体*`
#### 转义字符：
- 需要转移的字符有
`\  *  _ { [ ( # + - ! .  反引号`
#### 标题：
- 一个#号后面空格接内容表示H1，两个H2，...H6
`# H1`
#### 引用：
- 行首使用 > 加上一个空格表示引用一个段落，可嵌套
- 从>>>退到>时，必须之间要加上一个空行作为过渡，否则默认为下一行和上一行是同一级别的引用
- 引用完之后，必须再空一行，重新一个新的开始，否则以后的文字都将在引用的范围内
` > 引用`
` >> 引用2`
` >>> 引用3 `
#### 自动链接:
- 使用尖括号<>包含住一段地址或者邮箱
`<www.qq.com>`
#### 列表：
- 无序列表用* + - 空格你的列表
`- 无序列表`
- 有序列表用数字1. 空格你的列表
`1. 有序列表`
#### 删除线：
- 有\~\~表示删除线，\~~和被删除的文字之间不能有空格
`~~删除线~~`
#### 注脚：
- 在需要添加注脚的文字后加上[^1]
`[^1]: 注脚解释文字 `






## <span id="end">结束.</span>