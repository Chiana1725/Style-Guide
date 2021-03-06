
# HTML 规范

## 空格

使用四个空格的缩进，这是保证代码在各种环境下显示一致的唯一方式。
嵌套的节点应该缩进（四个空格）。


```html
<ul>
    <li>first</li>
    <li>second</li>
</ul>
```
## 换行
> 每行不得超过 `120` 个字符。
* 过长的代码不容易阅读与维护。但是考虑到 HTML 的特殊性，不做硬性要求。
* 在属性上，使用双引号，不要使用单引号。
* 不要在自动闭合标签结尾处使用斜线 `/` - HTML5 规范 指出他们是可选的。

```html
<img src="images/logo.png" alt="Company">
```

> 不要忽略可选的关闭标签（例如，`</li>` 和 `</body>`）。

## HTML5 doctype

> 在每个 HTML 页面开头使用这个简单地 doctype 来启用标准模式，使其每个浏览器中尽可能一致的展现。虽然 doctype 不区分大小写，但是按照惯例，doctype 大写

```html
<!DOCTYPE html>
```

## 语言属性
> 必须添加语言属性，有助于提高页面的可访问性，如：让语音合成工具确定其所应该采用的发音，令翻译工具确定其翻译语言等。
```html
<html lang="en">
</html>
<html lang="zh-CN">
```


## 字符编码

> `HTML` 文件使用无 `BOM` 的 `UTF-8` 编码,`UTF-8` 编码具有更广泛的适应性。`BOM` 在使用程序或工具处理文件时可能造成不必要的干扰。

> 指定字符编码的 `meta` 必须是 `head` 的第一个直接子元素。能够确保浏览器快速并容易的判断页面内容的渲染方式。这样避免在 HTML 中使用字符实体标记

```html
<html>
    <head>
        <meta charset="UTF-8">
        ......
    </head>
    <body>
        ......
    </body>
</html>
```
> 。



## IE 兼容模式

> IE 支持通过特定的 <meta> 标签来确定绘制当前页面所应该采用的 IE 版本。除非有强烈的特殊需求，否则最好是设置为 edge mode，从而通知 IE 采用其所支持的最新的模
式。

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

## viewport

> 若页面欲对移动设备友好，需指定页面的 `viewport`。viewport meta tag 可以设置可视区域的宽度和初始缩放大小，避免在移动设备上出现页面展示不正常。比如，在页面宽度小于 `980px` 时，若需 iOS 设备友好，应当设置 viewport 的 `width` 值来适应你的页面宽度。同时因为不同移动设备分辨率不同，在设置时，应当使用 `device-width` 和 `device-height` 变量。另外，为了使 viewport 正常工作，在页面内容样式布局设计上也要做相应调整，如避免绝对定位等。

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

## 引入 CSS 和 JavaScript

>  根据 HTML5 规范, 通常在引入 CSS 和 JavaScript 时不需要指明 type，因为 text/css 和 text/javascript 分别是他们的默认值。引入 `CSS` 时必须指明 `rel="stylesheet"`

```html
<!-- External CSS -->
<link rel="stylesheet" href="code-guide.css">

<!-- In-document CSS -->
<style>
    /* ... */
</style>

<!-- JavaScript -->
<script src="code-guide.js"></script>
```

> 文件分离
* 展现定义放置于外部 `CSS` 中，行为定义放置于外部 `JavaScript` 中。结构-样式-行为的代码分离，对于提高代码的可阅读性和维护性都有好处。
> 引入位置
* 在 `head` 中引入页面需要的所有 `CSS` 资源。在页面渲染的过程中，新的CSS可能导致元素的样式重新计算和绘制，页面闪烁。
* `JavaScript` 应当放在页面末尾，或采用异步加载。将 `script` 放在页面中间将阻断页面的渲染。出于性能方面的考虑，如非必要，请遵守此条建议。

```html
<body>
    <!-- a lot of elements -->
    <script src="init-behavior.js"></script>
</body>
```


> 移动环境或只针对现代浏览器设计的 Web 应用，如果引用外部资源的 `URL` 协议部分与页面相同，建议省略协议前缀。使用 `protocol-relative URL` 引入 CSS，在 `IE7/8` 下，会发两次请求。是否使用 `protocol-relative URL` 应充分考虑页面针对的环境。

```html
<script src="//s1.bdstatic.com/cache/static/jquery-1.10.2.min_f2fb5194.js"></script>
```


## 实用高于完美
> 尽量遵循 HTML 标准和语义，但是不应该以浪费实用性作为代价。任何时候都要用尽量小的复杂度和尽量少的标签来解决问题。

## 减少标签数量
> 在编写 HTML 代码时，需要尽量避免多余的父节点。很多时候，需要通过迭代和重构来使 HTML 变得更少。 参考下面的示例:

```html
<!-- Not so great -->
<span class="avatar">
    <img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">
```

## 属性
> HTML 属性应该按照特定的顺序出现以保证易读性。class 是为高可复用组件设计的，理论上他们应处在第一位。id 更加具体而且应该尽量少使用（例如, 页内书签），所以他们处在第二位。
1. class
2. id
3. name
4. data-*
5. src, for, type, href, value , max-length, max, min, pattern
6. placeholder, title, alt
7. aria-*, role
8. required, readonly, disabled

> Boolean 属性指不需要声明取值的属性。XHTML 需要每个属性声明取值，但是 HTML5 并不需要。一个元素中 Boolean 属性的存在表示取值 true，不存在则表示取值 false。简而言之，不要为 Boolean 属性添加取值。

```html
<input type="text" disabled>
```

> 在 JavaScript 文件中生成标签让内容变得更难查找，更难编辑，性能更差。应该尽量避免这种情况的出现。


>  属性名必须使用小写字母。
```html
<!-- good -->
<table cellspacing="0">...</table>

<!-- bad -->
<table cellSpacing="0">...</table>
```
>  属性值必须用双引号包围。

```html
<!-- good -->
<script src="esl.js"></script>

<!-- bad -->
<script src='esl.js'></script>
<script src=esl.js></script>
```

> 布尔类型的属性，建议不添加属性值。
```html
<input type="text" disabled>
<input type="checkbox" value="1" checked>
```


> 自定义属性建议以 `xxx-` 为前缀，推荐使用 `data-`。使用前缀有助于区分自定义属性和标准定义的属性。

```html
<ol data-ui-type="Select"></ol>
```




## id class 命名
>  `class` 必须单词全字母小写，单词间以 `-` 分隔。

>  `class` 必须代表相应模块或部件的内容或功能，不得以样式信息进行命名。公用类除外
```html
<!-- good -->
<div class="sidebar"></div>

<!-- bad -->
<div class="left"></div>
```

> * 元素 `id` 必须保证页面唯一。同一个页面中，不同的元素包含相同的 `id`，不符合 `id` 的属性含义。并且使用 `document.getElementById` 时可能导致难以追查的问题。
> * `id` 建议单词小驼峰式命名或者全小写，单词间以 `-` 分隔。但是同项目必须保持风格一致。
> * `id`、`class` 命名，在避免冲突并描述清楚的前提下尽可能短。

```html
<!-- good -->
<div id="nav"></div>
<!-- bad -->
<div id="navigation"></div>

<!-- good -->
<p class="comment"></p>
<!-- bad -->
<p class="com"></p>

<!-- good -->
<span class="author"></span>
<!-- bad -->
<span class="red"></span>
```

>  * 禁止为了 `hook 脚本`，创建无样式信息的 `class`。使用 `id`、属性选择作为 hook 是更好的方式。不允许 `class` 只用于让 JavaScript 选择某些元素，`class` 应该具有明确的语义和样式。否则容易导致 CSS class 泛滥。
>  * 同一页面，应避免使用相同的 `name` 与 `id`。IE 浏览器会混淆元素的 `id` 和 `name` 属性， `document.getElementById` 可能获得不期望的元素。所以在对元素的 `id` 与 `name` 属性的命名需要非常小心。一个比较好的实践是，为 `id` 和 `name` 使用不同的命名法。
```html
<input name="foo">
<div id="foo"></div>
<script>
// IE6 将显示 INPUT
alert(document.getElementById('foo').tagName);
</script>
```


## 标签
>  标签名必须使用小写字母。
```html
<!-- good -->
<p>Hello StyleGuide!</p>

<!-- bad -->
<P>Hello StyleGuide!</P>
```

>  对于无需自闭合的标签，不允许自闭合。常见无需自闭合标签有 `input`、`br`、`img`、`hr` 等。
```html
<!-- good -->
<input type="text" name="title">

<!-- bad -->
<input type="text" name="title" />
```

>  对 `HTML5` 中规定允许省略的闭合标签，不允许省略闭合标签。对代码体积要求非常严苛的场景，可以例外。比如：第三方页面使用的投放系统。
```html
<!-- good -->
<ul>
    <li>first</li>
    <li>second</li>
</ul>

<!-- bad -->
<ul>
    <li>first
    <li>second
</ul>
```

>  标签使用必须符合标签嵌套规则。
* 比如 `div` 不得置于 `p` 中，`tbody` 必须置于 `table` 中。详细的标签嵌套规则参见[HTML DTD](http://www.cs.tut.fi/~jkorpela/html5.dtd)中的 `Elements` 定义部分。
* html标签包含块级元素、内联元素，元素的类型决定嵌套的规则。常见块元素：div、section、ul、li、p、h1~h6等。常见内联元素：span、a、i、input、label、img等。

```html
<!-- right：块级元素可以内嵌其他块级元素或者内联元素 -->
<div><h1><span></span></h1></div>

<!-- right：内联元素可以内嵌其他内联元素 -->
<a href=""><span></span></a>

<!-- wrong：内联元素不能嵌套其他块级元素 -->
<span><div></div></span>

<!-- wrong：p元素不能内嵌块级元素，类似元素有h1、h2、h3、h4、h5、h6、p、dt -->
<p><div></div></p>
<h1><div></div></h1>
...
<h6><div></div></h6>

<!-- wrong：a标签不能内嵌a标签，这个错误会经常发生，值得重视 -->
<a href="a.html"><a href="a.html"></a></a>
 
<!-- right：内联元素内嵌块级元素 -->
<a style="display: block;" href=""><div></div></a>
```

> HTML 标签的使用应该遵循标签的语义。
下面是常见标签语义
- p - 段落
- h1,h2,h3,h4,h5,h6 - 层级标题
- strong,em - 强调
- ins - 插入
- del - 删除
- abbr - 缩写
- code - 代码标识
- cite - 引述来源作品的标题
- q - 引用
- blockquote - 一段或长篇引用
- ul - 无序列表
- ol - 有序列表
- dl,dt,dd - 定义列表
```html
<!-- good -->
<p>Esprima serves as an important <strong>building block</strong> for some JavaScript language tools.</p>

<!-- bad -->
<div>Esprima serves as an important <span class="strong">building block</span> for some JavaScript language tools.</div>
使用html5的语义化标签。针对旧版浏览器，引用html5shiv.js进行兼容调整。

<!-- bad -->
<div class="header"></div>
<div class="nav"></div>
<div class="section"></div>
<div class="article"></div>
<div class="footer"></div>

<!-- good -->
<header class="header"></header>
<nav class="nav"></nav>
<section class="content-section"></section>
<article class="article"></article>
<footer class="footer"></footer>
```
> 一个页面只能有一个h1标签，具体与seo有关。

```html
<!-- bad -->
<h1>我是标题一</h1>
<h1>我是标题二</h1>

<!-- good -->
<h1>我是标题一</h1>
<h2>我是标题二</h2>
...
<h6>我是标题六</h6>
```

> * 在 CSS 可以实现相同需求的情况下不得使用表格进行布局。在兼容性允许的情况下应尽量保持语义正确性。对网格对齐和拉伸性有严格要求的场景允许例外，如多列复杂表单。
> * 标签的使用应尽量简洁，减少不必要的标签。

```html
<!-- good -->
<img class="avatar" src="image.png">

<!-- bad -->
<span class="avatar">
    <img src="image.png">
</span>
```

## title
>  * 页面必须包含 `title` 标签声明标题。
>  * `title` 必须作为 `head` 的直接子元素，并紧随 `charset` 声明之后。
>  * `title` 中如果包含 ASCII 之外的字符，浏览器需要知道字符编码类型才能进行解码，否则可能导致乱码。
```html
<head>
    <meta charset="UTF-8">
    <title>页面标题</title>
</head>
```

## favicon
>  * 保证 `favicon` 可访问。
>  * 在未指定 favicon 时，大多数浏览器会请求 Web Server 根目录下的 `favicon.ico` 。为了保证 favicon 可访问，避免 404，必须遵循以下两种方法之一：
>     1. 在 Web Server 根目录放置 `favicon.ico` 文件。
>     2. 使用 `link` 指定 favicon。
```html
<link rel="shortcut icon" href="path/to/favicon.ico">
```

##  图片
>  * 禁止 `img` 的 `src` 取值为空。延迟加载的图片也要增加默认的 `src`。`src` 取值为空，会导致部分浏览器重新加载一次当前页面
>  * 避免为 `img` 添加不必要的 `title` 属性。多余的 `title` 影响看图体验，并且增加了页面尺寸。
>  * 为重要图片添加 `alt` 属性。可以提高图片加载失败时的用户体验。
>  * 添加 `width` 和 `height` 属性，以避免页面抖动。有下载需求的图片采用 `img` 标签实现，无下载需求的图片采用 CSS 背景图实现。
>       1. 产品 logo、用户头像、用户产生的图片等有潜在下载需求的图片，以 `img` 形式实现，能方便用户下载。
>       2. 无下载需求的图片，比如：icon、背景、代码使用的图片等，尽可能采用 CSS 背景图实现。


>   图像压缩
* 所有图片必须经过一定的压缩和优化才能发布

 
>   背景图
* 使用PNG格式而不是GIF格式，因为PNG格式色彩更丰富，还能提供更好的压缩比；
 
>   前景图
* 内容图片建议使用JPG，可以拥有更好地显示效果；装饰性图片使用PNG。


>   精灵图Sprite
CSS Sprite是一种将数个图片合成为一张大图的技术（既可以是背景图也可以是前景图），然后通过偏移来进行图像位置选取；CSS Sprite可以减少http请求。


##  表单

>  * 有文本标题的控件必须使用 `label` 标签将其与其标题相关联。
>  * 有两种方式：1. 将控件置于 `label` 内。2. `label` 的 `for` 属性指向控件的 `id`。推荐使用第一种，减少不必要的 `id`。如果 DOM 结构不允许直接嵌套，则应使用第二种。
```html
<label><input type="checkbox" name="confirm" value="on"> 我已确认上述条款</label>

<label for="username">用户名：</label> <input type="textbox" name="username" id="username">
```

>  使用 `button` 元素时必须指明 `type` 属性值。`button` 元素的默认 `type` 为 `submit`，如果被置于 `form` 元素中，点击后将导致表单提交。为显示区分其作用方便理解，必须给出 `type` 属性。
```html
<button type="submit">提交</button>
<button type="button">取消</button>
```

> 尽量不要使用按钮类元素的 `name` 属性。由于浏览器兼容性问题，使用按钮的 `name` 属性会带来许多难以发现的问题。


> 负责主要功能的按钮在 DOM 中的顺序应靠前。以提高可访问性。如果在 CSS 中指定了 `float: right` 则可能导致视觉上主按钮在前，而 DOM 中主按钮靠后的情况。


```html
<!-- good -->
<style>
.buttons .button-group {
    float: right;
}
</style>

<div class="buttons">
    <div class="button-group">
        <button type="submit">提交</button>
        <button type="button">取消</button>
    </div>
</div>

<!-- bad -->
<style>
.buttons button {
    float: right;
}
</style>

<div class="buttons">
    <button type="button">取消</button>
    <button type="submit">提交</button>
</div>
```



> 在针对移动设备开发的页面时，根据内容类型指定`input`输入框的 `type` 属性。根据内容类型指定输入框类型，能获得能友好的输入体验。

```html
<input type="date">
```


##  多媒体
> 当在现代浏览器中使用 `audio` 以及 `video` 标签来播放音频、视频时，应当注意格式。

* 音频应尽可能覆盖到如下格式：
    * MP3
    * WAV
    * Ogg

* 视频应尽可能覆盖到如下格式：
    * MP4
    * WebM
    * Ogg

> 在支持 `HTML5` 的浏览器中优先使用 `audio` 和 `video` 标签来定义音视频元素。

> 使用退化到插件的方式来对多浏览器进行支持。
```html
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    <object width="100" height="50" data="audio.mp3">
        <embed width="100" height="50" src="audio.swf">
    </object>
</audio>

<video width="100" height="50" controls>
    <source src="video.mp4" type="video/mp4">
    <source src="video.ogg" type="video/ogg">
    <object width="100" height="50" data="video.mp4">
        <embed width="100" height="50" src="video.swf">
    </object>
</video>
```

> 只在必要的时候开启音视频的自动播放。


> 在 `object` 标签内部提供指示浏览器不支持该标签的说明。

```html
<object width="100" height="50" data="something.swf">DO NOT SUPPORT THIS TAG</object>
```

##  模板中的 HTML

> 模板代码的缩进优先保证 HTML 代码的缩进规则。

```html
<!-- good -->
{if $display == true}
<div>
    <ul>
    {foreach $item_list as $item}
        <li>{$item.name}<li>
    {/foreach}
    </ul>
</div>
{/if}

<!-- bad -->
{if $display == true}
    <div>
        <ul>
    {foreach $item_list as $item}
        <li>{$item.name}<li>
    {/foreach}
        </ul>
    </div>
{/if}
```

> 模板代码应以保证 HTML 单个标签语法的正确性为基本原则。



```html
<!-- good -->
<li class="{if $item.type_id == $current_type}focus{/if}">{ $item.type_name }</li>

<!-- bad -->
<li {if $item.type_id == $current_type} class="focus"{/if}>{ $item.type_name }</li>
```

> 在循环处理模板数据构造表格时，若要求每行输出固定的个数，建议先将数据分组，之后再循环输出。



```html
<!-- good -->
<table>
    {foreach $item_list as $item_group}
    <tr>
        {foreach $item_group as $item}
        <td>{ $item.name }</td>
        {/foreach}
    <tr>
    {/foreach}
</table>

<!-- bad -->
<table>
<tr>
    {foreach $item_list as $item}
    <td>{ $item.name }</td>
        {if $item@iteration is div by 5}
    </tr>
    <tr>
        {/if}
    {/foreach}
</tr>
</table>
```

