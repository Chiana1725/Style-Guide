# CSS 规范

## 空格
> 使用 `4` 个空格做为一个缩进层级，不允许使用 `2` 个空格 或 `tab` 字符,这是保证代码在各种环境下显示一致的唯一方式。

> `选择器` 与 `{` 之间必须包含1个空格，增加代码易读性



```css
.selector {
}
```

> `属性名` 与之后的 `:` 之间不允许包含空格， `:` 与 `属性值` 之间必须包含空格。
```css
margin: 0;
```

>  `列表型属性值` 书写在单行时，`,` 后必须跟一个空格。


```css
font-family: Arial, sans-serif;
```
> 小提示：解决css代码格式化问题，一般可以使用编辑器的插件完成空格和换行的处理,vscode 格式化插件beautify,prettier.

## 换行
> 声明块的右括号应该另起一行。
```css
/* bad */
.selector{
    line-height:1.5}

/* good */
.selector{
    line-height:1.5
}
```
> 每行不得超过 `120` 个字符，除非单行不可分割，如：超长URL。

> 对于超长的样式，在样式值的 `空格` 处或 `,` 后换行，建议按逻辑分组。

```css
{
    /* 不同属性值按逻辑分组 */
    background:
        transparent url(aVeryVeryVeryLongUrlIsPlacedHere)
        no-repeat 0 0;

    /* 可重复多次的属性，每次重复一行 */
    background-image:
        url(aVeryVeryVeryLongUrlIsPlacedHere)
        url(anotherVeryVeryVeryLongUrlIsPlacedHere);

    /* 类似函数的属性值可以根据函数调用的缩进进行 */
    background-image: -webkit-gradient(
        linear,
        left bottom,
        left top,
        color-stop(0.04, rgb(88,94,124)),
        color-stop(0.52, rgb(115,123,162))
    );
}
```
> 在一个声明块中只包含一条声明的情况下，为了易读性和快速编辑可以考虑移除其中的换行。所有包含多条声明的声明块应该分为多行。方便错误检测

```css
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }
```

## 符号 
> 所有声明应该以分号结尾,减少出错。
 
> 逗号分隔的取值，都应该在逗号之后增加一个空格。
```css
/* Bad CSS */
.selector {
    margin: 0px 0px 15px;
    background-color: rgba(0, 0, 0, 0.5);
    box-shadow: 0 1px 2px #CCC, inset 0 1px 0 #FFFFFF
}

/* Good CSS */
.selector {
    margin-bottom: 15px;
    background-color: rgba(0, 0, 0, .5);
    box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```


## 命名
> class的命名
* class 的命名应该尽量短，也要尽量明确。
* 全小写，使用中横线分割。单词间使用下横线。
* 命名时使用最近的父节点或者父 class 作为前缀。
* 使用有意义的名称；使用结构化或者作用目标相关，而不是抽象的名称。
* 使用 .js-* 来表示行为(相对于样式)，但是不要在 CSS 中包含这些 class。
* 避免过度使用简写。.btn 可以很好地描述 button，但是 .s 不能代表任何元素。
* 保持 class 命名为全小写，可以使用短划线（不要使用下划线和 camelCase 命名）。短划线应该作为相关类的自然间断。(例如，.btn 和 .btn-danger)。


```css
/* bad */
.header_left      { xxx }
.headerLeft       { xxx }
.HeaderLeft       { xxx }

/* good */
.header-left      { xxx }
.usa-main         { xxx }
.new_zealand-main { xxx }
```

> id命名 
小驼峰写法，中间无中横线或者下横线。

```css
/* bad */
#Logo             { xxx }
#header_logo      { xxx }
#header-logo      { xxx }
#HeaderLogo       { xxx }

/* good */
#logo             { xxx }
#headerLogo       { xxx }
#headerLogoWrap   { xxx }
```

## 选择器
> 当一个`规则`包含多个 `选择器` 时，每个选择器声明必须独占一行。

```css
/* good */
.post,
.page,
.comment {
    line-height: 1.5;
}

/* bad */
.post, .page, .comment {
    line-height: 1.5;
}
```

> `>`、`+`、`~` 选择器的两边各保留一个空格。

```css
/* good */
main > nav {
    padding: 10px;
}

label + input {
    margin-left: 5px;
}

input:checked ~ button {
    background-color: #69C;
}

/* bad */
main>nav {
    padding: 10px;
}

label+input {
    margin-left: 5px;
}

input:checked~button {
    background-color: #69C;
}
```

> 属性选择器中的值必须用双引号包围。

```css
/* good */
article[character="juliet"] {
    voice-family: "Vivien Leigh", victoria, female;
}

/* bad */
article[character='juliet'] {
    voice-family: "Vivien Leigh", victoria, female;
}
```
> 如无必要，不得为 `id`、`class` 选择器添加类型选择器进行限定。以免影响性能不好维护。


```css
/* good */
#error,
.danger-message {
    font-color: #c00;
}

/* bad */
dialog#error,
p.danger-message {
    font-color: #c00;
}
```

> 选择器的嵌套层级应不大于 `3` 级，位置靠后的限定条件应尽可能精确。

```css
/* good */
#username input {}
.comment .avatar {}

/* bad */
.page .header .login #username input {}
.comment div * {}
```
> 其他
* 只在必要的情况下使用后代选择器
* 减少选择器的长度，每个组合选择器的条目应该尽量控制在 3 个以内。
* 使用 class 而不是通用元素（p,div等）标签来优化渲染性能。
* 避免在经常出现的组件中使用一些属性选择器 (例如，[class^="..."])。浏览器性能会受到这些情况的影响。

## 属性
> 属性值如需引号，使用双引号
```css
/* good */
html[lang|="zh"] q:before {
    font-family: "Microsoft YaHei", sans-serif;
    content: "“";
}

html[lang|="zh"] q:after {
    font-family: "Microsoft YaHei", sans-serif;
    content: "”";
}

/* bad */
html[lang|=zh] q:before {
    font-family: 'Microsoft YaHei', sans-serif;
    content: '“';
}

html[lang|=zh] q:after {
    font-family: "Microsoft YaHei", sans-serif;
    content: "”";
}
```
> 属性定义必须另起一行。
```css
/* good */
.selector {
    margin: 0;
    padding: 0;
}

/* bad */
.selector { margin: 0; padding: 0; }
```
> 属性定义后必须以分号结尾。
```css
/* good */
.selector {
    margin: 0;
}

/* bad */
.selector {
    margin: 0
}
```
> 在可以使用缩写的情况下，尽量使用属性缩写。
```css
/* good */
.post {
    font: 12px/1.5 arial, sans-serif;
}

/* bad */
.post {
    font-family: arial, sans-serif;
    font-size: 12px;
    line-height: 1.5;
}
```
> 使用 `border` / `margin` / `padding` 等缩写时，应注意隐含值对实际数值的影响，确实需要设置多个方向的值时才使用缩写。以免覆盖不需要覆盖的设定。如某些方向需要继承其他声明的值，则应该分开设置。
```css
/* centering <article class="page"> horizontally and highlight featured ones */
article {
    margin: 5px;
    border: 1px solid #999;
}

/* good */
.page {
    margin-right: auto;
    margin-left: auto;
}

.featured {
    border-color: #69c;
}

/* bad */
.page {
    margin: 5px auto; /* introducing redundancy */
}

.featured {
    border: 1px solid #69c; /* introducing redundancy */
}
```
> 当使用厂商前缀属性时，通过缩进使取值垂直对齐以便多行编辑。

```css
/* Prefixed properties */
.selector {
    -webkit-box-shadow: 0 1px 2px rgba(0,0,0,.15);
            box-shadow: 0 1px 2px rgba(0,0,0,.15);
}
```
> 同一规则下的属性在书写时，应按功能进行分组，并以 `Formatting Model（布局方式、位置） > Box Model（尺寸） > Typographic（文本相关） > Visual（视觉效果）` 的顺序书写，以提高代码的可读性。如果包含 `content` 属性，应放在最前面。
- Formatting Model 相关属性包括：`position` / `top` / `right` / `bottom` / `left` / `float` / `display` / `overflow` 等
- Box Model 相关属性包括：`border` / `margin` / `padding` / `width` / `height` 等
- Typographic 相关属性包括：`font` / `line-height` / `text-align` / `word-wrap` 等
- Visual 相关属性包括：`background` / `color` / `transition` / `list-style` 等

```css
.sidebar {
    /* formatting model: positioning schemes / offsets / z-indexes / display / ...  */
    position: absolute;
    top: 50px;
    left: 0;
    overflow-x: hidden;

    /* box model: sizes / margins / paddings / borders / ...  */
    width: 200px;
    padding: 5px;
    border: 1px solid #ddd;

    /* typographic: font / aligns / text styles / ... */
    font-size: 14px;
    line-height: 20px;

    /* visual: colors / shadows / gradients / ... */
    background: #f5f5f5;
    color: #333;
    -webkit-transition: color 1s;
       -moz-transition: color 1s;
            transition: color 1s;
}
```

> 当数值为 0 - 1 之间的小数时，省略整数部分的 `0`。
```css
/* good */
panel {
    opacity: .8;
}

/* bad */
panel {
    opacity: 0.8;
}
```
## url()
> `url()` 函数中的路径不加引号。
```css
body {
    background: url(bg.png);
}
```
> `url()` 函数中的绝对路径可省去协议名。
```css
body {
    background: url(//baidu.com/img/bg.png) no-repeat 0 0;
}
```
## 长度
> 长度为 `0` 时须省略单位。 (也只有长度单位可省)
```css
/* good */
body {
    padding: 0 5px;
}

/* bad */
body {
    padding: 0px 5px;
}
```
## background-position
> 2D 位置必须同时给出水平和垂直方向的位置,2D 位置初始值为 `0% 0%`，但在只有一个方向的值时，另一个方向的值会被解析为 center。为避免理解上的困扰，应同时给出两个方向的值。
```css
/* good */
body {
    background-position: center top; /* 50% 0% */
}

/* bad */
body {
    background-position: top; /* 50% 0% */
}
```

## 颜色
>RGB颜色值必须使用十六进制记号形式 `#rrggbb`。不允许使用 `rgb()`。带有alpha的颜色信息可以使用 `rgba()`。使用 `rgba()` 时每个逗号后必须保留一个空格。
```css
/* good */
.success {
    box-shadow: 0 0 2px rgba(0, 128, 0, .3);
    border-color: #008000;
}

/* bad */
.success {
    box-shadow: 0 0 2px rgba(0,128,0,.3);
    border-color: rgb(0, 128, 0);
}
```

> 颜色值可以缩写时，必须使用缩写形式。
```css
/* good */
.success {
    background-color: #aca;
}

/* bad */
.success {
    background-color: #aaccaa;
}
```

> 颜色值不允许使用命名色值。
```css
/* good */
.success {
    color: #90ee90;
}

/* bad */
.success {
    color: lightgreen;
}
```

> 颜色值中的英文字符采用小写。如不用小写也需要保证同一项目内保持大小写一致。
```css
/* good */
.success {
    background-color: #aca;
    color: #90ee90;
}

/* good */
.success {
    background-color: #ACA;
    color: #90EE90;
}

/* bad */
.success {
    background-color: #ACA;
    color: #90ee90;
}
```

## 注释
> 使用/**/来注释

## 媒体查询

> 尽量将媒体查询的位置靠近他们相关的规则。不要将他们一起放到一个独立的样式文件中，或者丢在文档的最底部。这样做只会让大家以后更容易忘记他们。这里是一个典型的案例。

```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (min-width: 480px) {
    .element { ...}
    .element-avatar { ... }
    .element-selected { ... }
}
```
> `Media Query` 如果有多个逗号分隔的条件时，应将每个条件放在单独一行中。
```css
@media
(-webkit-min-device-pixel-ratio: 2), /* Webkit-based browsers */
(min--moz-device-pixel-ratio: 2),    /* Older Firefox browsers (prior to Firefox 16) */
(min-resolution: 2dppx),             /* The standard way */
(min-resolution: 192dpi) {           /* dppx fallback */
    /* Retina-specific stuff here */
}
```
> 尽可能给出在高分辨率设备下效果更佳的样式。

## 字体
> `font-family` 属性中的字体族名称应使用字体的英文 `Family Name`，其中如有空格，须放置在引号中。

解释：

所谓英文 Family Name，为字体文件的一个元数据，常见名称如下：

字体  | 操作系统 | Family Name
------|---------|------------
宋体 (中易宋体) | Windows | SimSun
黑体 (中易黑体) | Windows | SimHei
微软雅黑 | Windows | Microsoft YaHei
微软正黑 | Windows | Microsoft JhengHei
华文黑体 | Mac/iOS | STHeiti
冬青黑体 | Mac/iOS | Hiragino Sans GB
文泉驿正黑 | Linux | WenQuanYi Zen Hei
文泉驿微米黑 | Linux | WenQuanYi Micro Hei
```css
h1 {
    font-family: "Microsoft YaHei";
}
```


> `font-family` 按「西文字体在前、中文字体在后」、「效果佳 (质量高/更能满足需求) 的字体在前、效果一般的字体在后」的顺序编写，最后必须指定一个通用字体族( `serif` / `sans-serif` )。
```css
/* Display according to platform */
.article {
    font-family: Arial, sans-serif;
}

/* Specific for most platforms */
h1 {
    font-family: "Helvetica Neue", Arial, "Hiragino Sans GB", "WenQuanYi Micro Hei", "Microsoft YaHei", sans-serif;
}
```

> `font-family` 不区分大小写，但在同一个项目中，同样的 `Family Name` 大小写必须统一。



```css
/* good */
body {
    font-family: Arial, sans-serif;
}

h1 {
    font-family: Arial, "Microsoft YaHei", sans-serif;
}

/* bad */
body {
    font-family: arial, sans-serif;
}

h1 {
    font-family: Arial, "Microsoft YaHei", sans-serif;
}
```
> 需要在 Windows 平台显示的中文内容，其字号应不小于 `12px`。由于 Windows 的字体渲染机制，小于 `12px` 的文字显示效果极差、难以辨认。

> 需要在 Windows 平台显示的中文内容，不要使用除 `normal` 外的 `font-style`。其他平台也应慎用。由于中文字体没有 `italic` 风格的实现，所有浏览器下都会 fallback 到 `obilique` 实现 (自动拟合为斜体)，小字号下 (特别是 Windows 下会在小字号下使用点阵字体的情况下) 显示效果差，造成阅读困难。


>`font-weight` 属性必须使用数值方式描述。CSS 的字重分 100 – 900 共九档，但目前受字体本身质量和浏览器的限制，实际上支持 `400` 和 `700` 两档，分别等价于关键词 `normal` 和 `bold`。浏览器本身使用一系列启发式规则来进行匹配，在 `<700` 时一般匹配字体的 Regular 字重，`>=700` 时匹配 Bold 字重。但已有浏览器开始支持 `=600` 时匹配 Semibold 字重 故使用数值描述增加了灵活性，也更简短。

```css
/* good */
h1 {
    font-weight: 700;
}

/* bad */
h1 {
    font-weight: bold;
}
```

## 行高
> `line-height` 在定义文本段落时，应使用数值。将 `line-height` 设置为数值，浏览器会基于当前元素设置的 `font-size` 进行再次计算。在不同字号的文本段落组合中，能达到较为舒适的行间间隔效果，避免在每个设置了 `font-size` 都需要设置 `line-height`。当 `line-height` 用于控制垂直居中时，还是应该设置成与容器高度一致。
```css
.container {
    line-height: 1.5;
}
```

## transition
>使用 `transition` 时应指定 `transition-property`。
```css
/* good */
.box {
    transition: color 1s, border-color 1s;
}

/* bad */
.box {
    transition: all 1s;
}
```

> [建议] 尽可能在浏览器能高效实现的属性上添加过渡和动画，在可能的情况下应选择这样四种变换，可以使用 `translate` 来代替 `left` 作为动画属性。
* `transform: translate(npx, npx);`
* `transform: scale(n);`
* `transform: rotate(ndeg);`
* `opacity: 0..1;`

```css
/* good */
.box {
    transition: transform 1s;
}
.box:hover {
    transform: translate(20px); /* move right for 20px */
}

/* bad */
.box {
    left: 0;
    transition: left 1s;
}
.box:hover {
    left: 20px; /* move right for 20px */
}
```



## 代码组织

以组件为单位组织代码。

制定一个一致的注释层级结构。

使用一致的空白来分割代码块，这样做在查看大的文档时更有优势。

当使用多个 CSS 文件时，通过组件而不是页面来区分他们。页面会被重新排列，而组件移动就可以了。


## !important
> 尽量不使用 `!important` 声明。

> 当需要强制指定样式且不允许任何场景覆盖时，通过标签内联和 `!important` 定义样式。必须注意的是，仅在设计上 `确实不允许任何其它场景覆盖样式` 时，才使用内联的 `!important` 样式。通常在第三方环境的应用中使用这种方案。



## z-index
> 将 `z-index` 进行分层，对文档流外绝对定位元素的视觉层级关系进行管理。同层的多个元素，如多个由用户输入触发的 Dialog，在该层级内使用相同的 `z-index` 或递增 `z-index`。

建议每层包含100个 `z-index` 来容纳足够的元素，如果每层元素较多，可以调整这个数值。


>在可控环境下，期望显示在最上层的元素，`z-index` 指定为 `999999`。可控环境分成两种，一种是自身产品线环境；还有一种是可能会被其他产品线引用，但是不会被外部第三方的产品引用。

不建议取值为 `2147483647`。以便于自身产品线被其他产品线引用时，当遇到层级覆盖冲突的情况，留出向上调整的空间。


> 在第三方环境下，期望显示在最上层的元素，通过标签内联和 `!important`，将 `z-index` 指定为 `2147483647`。第三方环境对于开发者来说完全不可控。在第三方环境下的元素，为了保证元素不被其页面其他样式定义覆盖，需要采用此做法。

## 兼容性
>   属性前缀带私有前缀的属性由长到短排列，按冒号位置对齐。方便阅读，也便于在编辑器内进行多行编辑

```css
.box {
    -webkit-box-sizing: border-box;
       -moz-box-sizing: border-box;
            box-sizing: border-box;
}
```
> Hack
* 非必要时不使用hack，应尽可能考虑是否可以采用其他方式解决。如果能通过合理的 HTML 结构或使用其他的 CSS 定义达到理想的样式，则不应该使用 hack 手段解决问题。通常 hack 会导致维护成本的增加。
* 尽量使用 `选择器 hack` 处理兼容性，而非 `属性 hack`，可以避免一些第三方库无法识别 hack 语法的问题。
```css
/* IE 7 */
*:first-child + html #header {
    margin-top: 3px;
    padding: 5px;
}

/* IE 6 */
* html #header {
    margin-top: 5px;
    padding: 4px;
}
```
* 如果使用了属性hack，尽量使用简单的 `属性 hack`。
```css
.box {
    _display: inline; /* fix double margin */
    float: left;
    margin-left: 20px;
}

.container {
    overflow: hidden;
    *zoom: 1; /* triggering hasLayout */
}
```
* 禁止使用无样式class来hook脚本,以免造成页面class定义冗余以及增加维护难度请使用元素自带属性或自定义属性实现。

```javascript
// bad
<div class="click-alert"></div>
$('.click-alert').click(function() {});

// good
<div data-action="clickAlert"></div>
$('div[data-action="clickAlert"]').click(function() {});
```
## css 引入
> 不使用 @import，与`<link>`相比，`@import`较慢，增加额外的页面请求，并可能导致其他不可预见的问题。

```html
<!-- Use link elements -->
<link rel="stylesheet" href="core.css">

<!-- Avoid @imports -->
<style>
    @import url("more.css");
</style>
```


### 清除浮动
> 当元素需要撑起高度以包含内部的浮动元素时，通过对伪类设置 `clear` 或触发 `BFC` 的方式进行 `clearfix`。尽量不使用增加空标签的方式。

> 对已经触发 BFC 的元素不需要再进行 clearfix. 触发 BFC 的方式很多，常见的有：

* float 非 none
* position 非 static
* overflow 非 visible
## 编码
>  `CSS` 文件使用无 `BOM` 的 `UTF-8` 编码。UTF-8 编码具有更广泛的适应性。BOM 在使用程序或工具处理文件时可能造成不必要的干扰。

## Less 和 Sass 中的嵌套

避免不必要的嵌套。可以进行嵌套，不意味着你应该这样做。只有在需要给父元素增加样式并且同时存在多个子元素时才需要考虑嵌套。

```less
// Without nesting
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// With nesting
.table > thead > tr {
    > th { … }
    > td { … }
}
```

## 编辑器配置

根据以下的设置来配置你的编辑器，将这些设置应用到项目的 .editorconfig 文件，来避免常见的代码不一致和丑陋的 diffs。

- 使用四个空格的缩进。
- 在保存时删除尾部的空白字符。
- 设置文件编码为 UTF-8。
- 在文件结尾添加一个空白行。


## 页面结构:  
　　头：header  
　　内容：content/container  
　　尾：footer  
　　导航：nav  
　　侧栏：sidebar  
　　栏目：column  
　　页面外围控制整体佈局宽度：wrapper  
　　左右中：left right center  
　　登录条：loginbar  
　　标志：logo  
　　广告：banner  
　　页面主体：main  
　　热点：hot  
　　新闻：news  
　　下载：download  
　　子导航：subnav  
　　菜单：menu  
　　子菜单：submenu  
　　搜索：search  
　　友情链接：friendlink  
　　页脚：footer  
　　版权：copyright  
　　滚动：scroll  
　　内容：content  
　　标签：tags  
　　文章列表：list  
　　提示信息：msg  
　　小技巧：tips  
　　栏目标题：title  
　　加入：joinus  
　　指南：guide  
　　服务：service  
　　注册：regsiter  
　　状态：status  
　　投票：vote  
　　合作伙伴：partner

## 导航  
　　导航：nav  
　　主导航：mainnav  
　　子导航：subnav  
　　顶导航：topnav  
　　边导航：sidebar  
　　左导航：leftsidebar  
　　右导航：rightsidebar  
　　菜单：menu  
　　子菜单：submenu  
　　标题: title  
　　摘要: summary  
## 功能  
　　标志：logo  
　　广告：banner  
　　登陆：login  
　　登录条：loginbar  
　　注册：register  
　　搜索：search  
　　功能区：shop  
　　标题：title  
　　加入：joinus  
　　状态：status  
　　按钮：btn  
　　滚动：scroll  
　　标签页：tab  
　　文章列表：list  
　　提示信息：msg  
　　当前的: current  
　　小技巧：tips  
　　图标: icon  
　　注释：note  
　　指南：guild  
　　服务：service  
　　热点：hot  
　　新闻：news  
　　下载：download  
　　投票：vote  
　　合作伙伴：partner  
　　友情链接：link  
　　版权：copyright  

## 注意事项::  
　　1.一律小写;  
　　2.尽量用英文;  
　　3.不加中杠和下划线;  
　　4.尽量不缩写，除非一看就明白的单词。
  
## CSS样式表文件命名  
　　主要的 master.css  
　　模块 module.css  
　　基本共用 base.css  
　　布局、版面 layout.css  
　　主题 themes.css    
　　专栏 columns.css  
　　文字 font.css  
　　表单 forms.css  
　　补丁 mend.css  
　　打印 print.css  

