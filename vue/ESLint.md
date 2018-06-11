# ESLint规范问题
### 作者：black徐 

### 1.vue报错 `Do not use built-in or reserved HTML elements as component id:header`
- 组件，不能和html标签重复。
- header组件，h5新标签重复。
- 由于在模板需要插入到 DOM 中，所以模板中的标签名必须能够被 DOM 正确地解析。主要有三种情况：
    一是完全不合法的标签名，例如 </>；
    二是与 HTML 元素重名会产生不确定的行为，例如使用 input 做组件名不会解析到自定义组件，使用 button 在 Chrome 上正常但在 IE 上不正常；
    三是与 Vue 保留的 slot、partial、component 重名，因为会优先以本身的意义解析，从而产生非预期的结果。

### 2.eslint: `Expected indentation of 2 spaces but found 4`
- 缩进报错 ，所有缩进只能用两个空格。

### 3. `Newline required at end of file but not found`  
- 需要在最后的</style>后面再加一行!

### 4.`Missing space before value for key 'name'`  
- 在关键字“值”之前缺少空格。

### 5.`A space is required after ','`
- 在，后面要加空格。

### 6.`space-before-blocks`
- 关键字后面要空一格。

### 7.`key-spacing`
- 对象字面量中冒号的前后空格。

### 8.`no-unused-vars`
- 不能有声明后未被使用的变量或参数。

### 9.所有`.vue`里面的，`style`和`script`属性都顶格。