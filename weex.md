# weex 
## weex problem
- `weex`中的样式不支持简写, 不支持`margin: 0 10px;background:url('..');border:1px solid;...`
- `android`下的view默认色是白色, `IOS`如果不设置没有默认颜色
- 只支持`px`长度单位
- `color`最好写成`#000，#000000，black`
- 默认盒模型为`flex`，`box-sizing` 默认为 `border-box`
- `<image>`组件暂不支持本地图片，需指明`width`和`height`否则无法显示
- `background-image` 优先级高于` background-color`
- 不支持`z-index`但靠后的元素层级更高
- Weex 支持四种伪类：`active`, `focus`, `disabled`, `enabled`，所有组件都支持 `active`, 但只有 `input` 组件和 `textarea` 组件支持 `focus`, `enabled`,` diabled`。
- `Android`：`font-weight`值仅支持 `400（normal）` 和 `700（bold）`
- `Android`：如果定位元素超过容器边界，在 `Android` 下，超出部分将不可见，原因在于 `Android` 端元素 `overflow` 默认值为 `hidden`，但目前 `Android `暂不支持设置 `overflow: visible`。
