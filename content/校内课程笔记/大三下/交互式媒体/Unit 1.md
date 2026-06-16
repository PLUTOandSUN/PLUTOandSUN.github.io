---
title: Unit 1 - Coding & Development
date: 2026-06-14
tags:
  - course/interactive-media-design
  - html
  - css
  - css-animation
  - javascript
  - vanilla-js
  - canvas
  - web-development
  - lecture-note
source:
  - "[[附件/Unit 1 - Coding & Development/Lecture 1. HTML Basics.pdf|Lecture 1. HTML Basics.pdf]]"
  - "[[附件/Unit 1 - Coding & Development/Lecture 2. CSS Basics and Animations.pdf|Lecture 2. CSS Basics and Animations.pdf]]"
  - "[[附件/Unit 1 - Coding & Development/Lecture 3. JavaScript Basics.pdf|Lecture 3. JavaScript Basics.pdf]]"
  - "[[附件/Unit 1 - Coding & Development/Lecture 4. Production and Management.pdf|Lecture 4. Production and Management.pdf]]"
  - "[[附件/Unit 1 - Coding & Development/Lecture 5. AI-Led Development.pdf|Lecture 5. AI-Led Development.pdf]]"
---

# Unit 1 - HTML Basics 讲解

> [!info] 来源
> 本笔记讲解的是 EBU6305 Interactive Media Design and Production 的 **Lecture 1: HTML Basics**，原课件见：[[附件/Unit 1 - Coding & Development/Lecture 1. HTML Basics.pdf|Lecture 1. HTML Basics.pdf]]。

## 1. 本章在讲什么？

这一章是交互式媒体设计里“网页开发基础”的第一讲，核心目标是让你理解 **HTML 是什么、HTML 文件如何组织、常见标签如何使用、为什么要写语义化结构，以及如何用 SVG 在网页里画图**。

课件的学习目标包括：

- 理解 HTML 的基本语法。
- 描述一个 HTML 文档的整体结构。
- 理解语义化结构的重要性。
- 能够写出基本的 HTML 页面。

整章可以概括为一句话：

> HTML 负责网页的“内容和结构”，CSS 负责“外观表现”，JavaScript 负责“行为交互”。本章主要讲 HTML 这一层。

---

## 2. Website layers：网页的三层结构

课件先把网站拆成三层：

1. **Content / HTML**：内容层，负责页面里有什么，例如标题、段落、图片、链接、表格、表单等。
2. **Presentation / CSS**：表现层，负责页面长什么样，例如颜色、字体、布局、动画等。
3. **Behaviour / JavaScript**：行为层，负责页面怎么动、怎么响应用户操作，例如点击按钮、表单验证、动态更新内容等。

理解这三层很重要，因为之后写网页时要避免把所有东西混在一起：

- HTML 重点写结构和语义。
- CSS 重点写样式。
- JavaScript 重点写交互逻辑。

---

## 3. HTML Document Structure：HTML 文档结构

### 3.1 一个 HTML 文档由什么组成？

课件指出 HTML 文档由 **文本内容** 和 **HTML elements** 组成。一个标准网页通常分成两大区域：

- `<head>`：头部信息区。
  - 放页面的元信息，例如标题、字符编码、CSS 链接、脚本引用等。
  - 这里的内容通常不会直接显示在页面正文中。
- `<body>`：页面主体内容区。
  - 放用户真正看到的内容，例如文字、图片、链接、表格、表单等。

基本结构如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Hello World</title>
</head>
<body>
  <p>Hello HTML5 World EBU6305!</p>
</body>
</html>
```

### 3.2 `<!DOCTYPE html>` 的作用

`<!DOCTYPE html>` 用来声明文档类型，告诉浏览器：这个文件应该按照 HTML5 标准来解析。

它不是普通 HTML 标签，而是一个声明。一般写在 HTML 文件第一行。

### 3.3 标签大小写

课件提到：标准 HTML 标签本身不区分大小写，例如 `<HEAD>`、`<Head>` 和 `<head>` 理论上都能被识别。

但是实际开发中建议统一使用小写：

```html
<head></head>
<body></body>
<p></p>
```

这样更规范、更易读，也和现代 HTML/CSS/JavaScript 习惯一致。

---

## 4. Elements and Attributes：元素和属性

### 4.1 Element 是什么？

一个 HTML element 通常由三部分组成：

1. 起始标签 opening tag。
2. 内容 content。
3. 结束标签 closing tag。

例如：

```html
<p id="intro">Welcome</p>
```

这里：

- `<p id="intro">` 是起始标签。
- `Welcome` 是内容。
- `</p>` 是结束标签。
- 整体 `<p id="intro">Welcome</p>` 是一个 HTML element。

### 4.2 Tag 和 Element 的区别

课件强调了 tag 和 element 的区别：

- **Tag**：标签本身，例如 `<p>` 或 `</p>`。
- **Element**：由起始标签、内容、结束标签组成的整体。

例如：

```html
<h1>This is a heading</h1>
```

其中 `<h1>` 和 `</h1>` 是 tags，整个 `<h1>This is a heading</h1>` 是 element。

### 4.3 Attribute 是什么？

Attribute 是写在起始标签里的额外信息，通常是 `name="value"` 的形式。

例如：

```html
<img src="img_girl.jpg" width="500" height="600" alt="A girl">
<a href="https://www.qmul.ac.uk">QMUL Homepage</a>
<p style="color:red">I am a paragraph</p>
```

属性的作用：

- 给元素补充信息。
- 控制元素行为或显示。
- 为 CSS 和 JavaScript 提供定位依据。

常见属性包括：

- `id`：元素的唯一标识。
- `class`：元素类别，常用于 CSS 批量设置样式。
- `title`：鼠标悬停时可能显示的提示文字。
- `style`：直接写内联样式。
- `lang`：语言。
- `href`：链接地址，常用于 `<a>`。
- `src`：资源地址，常用于 `<img>`、`<script>`、`video source` 等。
- `alt`：图片无法显示时的替代文本，也有助于无障碍访问。

> [!tip] 实际开发建议
> HTML5 中属性值有时可以不加引号，但建议始终写成 `name="value"`，这样更清晰，也能减少错误。

### 4.4 Attribute 的类型

课件把 attributes 分成三类：

1. **Optional attributes**：可选属性，不同元素可用的可选属性不同。
2. **Standard attributes**：标准属性，例如 `id`、`class`、`title`、`style`、`dir`、`lang`。
3. **Event attributes**：事件属性，例如 `onclick`、`onmouseover`、`onkeydown` 等，主要用于脚本交互。

现代开发中，虽然可以直接写：

```html
<button onclick="alert('Hello')">Click</button>
```

但更推荐把交互逻辑放在 JavaScript 文件中，保持 HTML 结构清晰。

---

## 5. HTML Tags：标签和嵌套

### 5.1 标签的基本形式

大多数 HTML 标签成对出现：

```html
<tag_name>content</tag_name>
```

例如：

```html
<p>This is a paragraph.</p>
```

有些标签没有结束标签，称为 **empty elements**，例如：

```html
<img src="photo.jpg" alt="Photo">
<br>
<hr>
<link rel="stylesheet" href="main.css">
```

它们没有包裹文本内容，而是通过属性或自身位置发挥作用。

### 5.2 标签嵌套

HTML 元素可以嵌套在其他元素内部，例如：

```html
<div>
  <p>Content</p>
</div>
```

嵌套时要注意顺序正确：

```html
<!-- 正确 -->
<p><strong>Important</strong></p>

<!-- 错误：结束顺序乱了 -->
<p><strong>Important</p></strong>
```

---

## 6. Browser 会忽略什么？

课件提到浏览器通常会忽略：

- HTML 注释。
- 无法识别的标签。
- 普通文本中的换行。
- 多个连续空格。
- tab 缩进。

例如：

```html
<p>Hello        world</p>
```

浏览器通常只显示成类似：

```text
Hello world
```

如果要控制页面排版，应该使用 HTML 结构和 CSS，而不是依赖大量空格或换行。

---

## 7. HTML Comments：HTML 注释

HTML 注释写法如下：

```html
<!-- Write your comments here -->
```

注释用于解释代码，浏览器不会把注释内容显示在页面中。

使用场景：

- 标记某一段代码的作用。
- 临时隐藏一小段 HTML。
- 给团队成员留下说明。

不要在注释里写密码、密钥或隐私信息，因为前端源码仍然可能被用户查看。

---

## 8. HTML DOM：文档对象模型

### 8.1 DOM 是什么？

当浏览器加载网页时，会把 HTML 文档解析成一个树状结构，称为 **Document Object Model**，简称 **DOM**。

例如这个 HTML：

```html
<!DOCTYPE html>
<html>
<head>
  <title>Page Title</title>
</head>
<body>
  <h1>This is a Heading</h1>
  <p>This is a paragraph.</p>
</body>
</html>
```

可以理解成一棵树：

- `html` 是根元素。
- `head` 和 `body` 是 `html` 的子节点。
- `title` 是 `head` 的子节点。
- `h1` 和 `p` 是 `body` 的子节点。

### 8.2 DOM 关系

课件展示了 DOM Tree 里的关系，包括：

- **Parent**：父节点。
- **Child**：子节点。
- **Sibling**：兄弟节点。
- **Ancestor**：祖先节点。

为什么 DOM 重要？因为 CSS 和 JavaScript 都经常通过 DOM 找到页面元素：

- CSS 根据选择器给某些节点加样式。
- JavaScript 读取、修改、添加、删除 DOM 节点。

所以 HTML 不只是“显示文本”，它也是后续样式和交互的基础结构。

---

## 9. Essential HTML Elements：必要元素

课件列出了构成有效 HTML 页面的一些核心元素。

### 9.1 `<html>`

`<html>` 是整个 HTML 文档的根元素，所有其他 HTML 标签都应该放在它里面。

```html
<html>
  ...
</html>
```

### 9.2 `<head>`

`<head>` 包含页面元数据，例如：

- `<title>` 页面标题。
- `<meta>` 字符编码、页面描述、关键词、作者、viewport 等。
- `<link>` 外部资源，例如 CSS 文件。
- `<style>` 当前页面内部 CSS。
- `<script>` JavaScript 脚本。

### 9.3 `<title>`

`<title>` 定义页面标题。它会出现在：

- 浏览器标签页。
- 收藏夹标题。
- 搜索结果标题中。

例如：

```html
<title>My First Web Page</title>
```

### 9.4 `<body>`

`<body>` 里放页面实际显示内容，例如：

- 标题。
- 段落。
- 图片。
- 链接。
- 表格。
- 表单。
- 视频。
- SVG 图形。

---

## 10. `<head>` 中的常见元素

### 10.1 `<style>`：内部 CSS

`<style>` 用来在 HTML 文件内部写 CSS：

```html
<style>
  h1 {
    color: red;
  }
</style>
```

适合小页面或课堂演示。实际项目中通常会把 CSS 单独放到 `.css` 文件里。

### 10.2 `<link>`：链接外部样式表

`<link>` 常用于引用外部 CSS：

```html
<link rel="stylesheet" href="style.css">
```

这样可以让 HTML 只负责结构，CSS 文件负责样式。

### 10.3 `<meta>`：元数据

`<meta>` 可以设置字符编码、页面描述、关键词、作者、viewport 等。

常见写法：

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

`viewport` 很重要，尤其是移动端网页。没有 viewport 设置时，手机浏览器可能会按桌面宽度缩放页面，导致内容显示很小或布局异常。

### 10.4 `<script>`：客户端脚本

`<script>` 用来引入或书写 JavaScript：

```html
<script src="main.js"></script>
```

它让网页可以响应用户操作、更新内容、进行计算或与服务器通信。

---

## 11. 常见 Body 元素

### 11.1 Headings：标题 `<h1>` 到 `<h6>`

HTML 有六级标题：

```html
<h1>Main heading</h1>
<h2>Section heading</h2>
<h3>Subsection heading</h3>
```

- `<h1>` 最重要，通常一个页面主标题只用一个。
- `<h6>` 最不重要。
- 标题不仅影响视觉大小，也影响页面结构和语义。

`<hr>` 表示内容主题的分隔线：

```html
<hr>
```

### 11.2 Paragraphs：段落 `<p>` 和换行 `<br>`

`<p>` 表示段落：

```html
<p>This is a paragraph.</p>
```

`<br>` 表示强制换行：

```html
<p>Line one<br>Line two</p>
```

一般不要用很多 `<br>` 来做布局，布局应该交给 CSS。

### 11.3 Links：链接 `<a>`

链接的基本形式：

```html
<a href="https://www.qmul.ac.uk">QMUL Homepage</a>
```

说明：

- `href` 是目标地址。
- 链接文本是用户能点击的部分。
- 链接不一定只能包文字，也可以包图片或其他元素。

### 11.4 Images：图片 `<img>`

图片基本形式：

```html
<img src="queen-building.jpg" alt="QMUL Queen's Building">
```

关键属性：

- `src`：图片路径。
- `alt`：替代文本。图片加载失败时会显示，也能帮助屏幕阅读器理解图片内容。

> [!important] `alt` 很重要
> `alt` 不只是“图片加载失败时显示的字”，还是网页无障碍访问和搜索引擎理解图片内容的重要信息。

### 11.5 Tables：表格

表格相关标签：

```html
<table>
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Alice</td>
    <td>20</td>
  </tr>
</table>
```

含义：

- `<table>`：表格。
- `<tr>`：table row，表格行。
- `<th>`：table header，表头单元格。
- `<td>`：table data，普通数据单元格。

表格适合展示二维数据，不建议用表格来做整体页面布局。

### 11.6 iframes：嵌入网页

`iframe` 可以在一个网页中嵌入另一个网页：

```html
<iframe src="https://example.com"></iframe>
```

课件举例是把 Google Map 嵌入到网页中。

使用 iframe 时要注意：

- 有些网站禁止被 iframe 嵌入。
- iframe 会影响性能。
- 嵌入第三方内容时要注意安全和隐私。

### 11.7 Forms：表单

表单用于收集用户输入：

```html
<form>
  <label for="name">Name:</label>
  <input id="name" type="text" name="name">

  <input type="submit" value="Submit">
</form>
```

常见输入控件：

- text fields：文本框。
- checkboxes：复选框。
- radio buttons：单选按钮。
- submit buttons：提交按钮。

表单是网页交互的重要基础，之后通常会和 JavaScript 或后端服务配合使用。

---

## 12. Block and Inline Elements：块级元素和行内元素

HTML 元素有默认显示方式，常见分为 **block-level** 和 **inline**。

### 12.1 Block-level elements

块级元素特点：

- 通常从新的一行开始。
- 默认占据可用宽度。
- 常用于页面结构分区。

课件重点讲了 `<div>`：

```html
<div class="section">
  <h2>London</h2>
  <p>London is the capital city of England.</p>
</div>
```

`<div>` 本身没有具体语义，它只是一个通用容器。和 CSS 搭配时可以用来控制一整块内容的样式或布局。

### 12.2 Inline elements

行内元素特点：

- 不会自动另起一行。
- 只占据自身内容需要的宽度。
- 常用于修饰一小段文本。

课件重点讲了 `<span>`：

```html
<h1>My <span style="color:red">Important</span> Heading</h1>
```

`<span>` 本身也没有具体语义，常用于给文本中的某一小部分加样式。

### 12.3 `<div>` 和 `<span>` 的区别

| 元素 | 类型 | 用途 |
|---|---|---|
| `<div>` | block | 包住一整块内容，常用于布局或分区 |
| `<span>` | inline | 包住一小段文字，常用于局部样式 |

---

## 13. Semantic Markup：语义化标记

### 13.1 什么是语义化？

课件说：semantic element 会清楚描述自己的意义，让浏览器和开发者都知道它代表什么。

例如：

```html
<nav>
  <ul>
    <li><a href="/home">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>
```

这里 `<nav>` 明确表示“导航区域”。相比之下：

```html
<div class="nav">
  ...
</div>
```

虽然也能显示，但语义不如 `<nav>` 清楚。

### 13.2 为什么语义化重要？

语义化的好处：

1. **代码更易读**：开发者一看标签就知道内容作用。
2. **利于可访问性**：屏幕阅读器能更好理解页面结构。
3. **利于搜索引擎**：搜索引擎能更准确判断页面内容层级。
4. **利于维护**：结构清楚，后期改 CSS 或 JS 更方便。

课件中举的语义结构包括：

- articles。
- headings。
- lists。
- paragraphs。
- links。
- navigation。
- footers。

### 13.3 Semantic vs Non-Semantic

语义化元素例子：

- `<table>`：表示表格数据。
- `<form>`：表示用户输入表单。
- `<nav>`：表示导航。
- `<article>`：表示独立文章内容。
- `<footer>`：表示页脚。

非语义化元素例子：

- `<div>`：通用块级容器。
- `<span>`：通用行内容器。

它们不是不能用，而是不要在有更准确语义标签时滥用。

---

## 14. Lists：列表

课件详细讲了无序列表、有序列表和嵌套列表。

### 14.1 Unordered List：无序列表 `<ul>`

无序列表用项目符号显示：

```html
<ul>
  <li>Apple</li>
  <li>Pear</li>
  <li>Kiwi</li>
</ul>
```

逐行解释：

| 代码 | 解释 |
|---|---|
| `<ul>` | 开始一个 **unordered list**，也就是无序列表。浏览器通常会用项目符号 bullet points 显示它。 |
| `  <li>Apple</li>` | 列表里的第一个项目。`<li>` 表示 **list item**，这里的内容是 `Apple`。 |
| `  <li>Pear</li>` | 列表里的第二个项目，内容是 `Pear`。 |
| `  <li>Kiwi</li>` | 列表里的第三个项目，内容是 `Kiwi`。 |
| `</ul>` | 结束这个无序列表。所有属于这个列表的 `<li>` 都应该放在 `<ul>` 和 `</ul>` 之间。 |

可以通过 CSS 改变项目符号样式，例如：

```html
<ul style="list-style-type: square">
  <li>Apple</li>
  <li>Pear</li>
</ul>
```

常见样式：

- `disc`
- `circle`
- `square`

### 14.2 Ordered List：有序列表 `<ol>`

有序列表带编号：

```html
<ol>
  <li>Apple</li>
  <li>Pear</li>
  <li>Kiwi</li>
</ol>
```

可以通过 CSS 改变编号类型：

```html
<ol style="list-style-type: upper-roman">
  <li>Step one</li>
  <li>Step two</li>
</ol>
```

常见样式：

- `decimal`
- `lower-alpha`
- `upper-roman`

### 14.3 List Item：列表项 `<li>`

`<li>` 必须放在 `<ul>` 或 `<ol>` 内部：

```html
<ul>
  <li>List item</li>
</ul>
```

### 14.4 Nested Lists：嵌套列表

列表可以嵌套：

```html
<ul>
  <li>NFC North
    <ul>
      <li>Packers</li>
      <li>Vikings</li>
      <li>Lions</li>
      <li>Bears</li>
    </ul>
  </li>
  <li>NFC East
    <ul>
      <li>Cowboys</li>
      <li>Giants</li>
      <li>Redskins</li>
      <li>Eagles</li>
    </ul>
  </li>
</ul>
```

也可以混合无序和有序列表：外层用 `<ul>`，内层用 `<ol>`。

> [!warning] 嵌套列表的易错点
> 内层列表最好放在外层某个 `<li>` 的内部，而不是直接和 `<li>` 平级乱放。这样 DOM 结构更清楚，也更符合语义。

---

## 15. Examples of HTML Pages：课件中的页面例子

### 15.1 Image loading：图片加载

课件用一个例子展示如何加载 QMUL Queen's Building 的图片。核心思想是：

- 页面有标题 `<h1>`。
- 页面有说明段落 `<p>`。
- 用 `<figure>` 组织图片和说明。
- 用 `<img>` 加载图片。
- 用 `alt` 写替代文本。

更现代、常见的写法可以是：

```html
<figure>
  <img src="queensBuilding.jpg" alt="QMUL Queen's Building">
  <figcaption>Figure: Queen's Building</figcaption>
</figure>
```

`figure` 适合包裹图片、图表、代码片段等独立内容，`figcaption` 是它的说明文字。

### 15.2 Navigation：导航

课件用 `<nav>`、`<ul>`、`<li>` 和 `<a>` 做导航栏：

```html
<nav id="mainNav">
  <ul>
    <li><a href="https://www.qmul.ac.uk">Home</a></li>
    <li><a href="https://www.qmul.ac.uk/about/">About</a></li>
    <li><a href="https://www.qmul.ac.uk/research/">Research</a></li>
    <li><a href="https://www.qmul.ac.uk/contact/">Contact</a></li>
  </ul>
</nav>
```

这个例子体现了语义化：导航区域用 `<nav>`，链接列表用 `<ul>` 和 `<li>`，每个具体链接用 `<a>`。

### 15.3 Video：视频

课件展示了 HTML5 视频标签：

```html
<video width="600" controls>
  <source src="video.mp4" type="video/mp4">
  <strong>HTML5 video element not supported</strong>
</video>
```

说明：

- `<video>` 表示视频播放器。
- `controls` 显示播放、暂停、音量等控制条。
- `<source>` 指定视频文件和 MIME 类型。
- 如果浏览器不支持 video，会显示备用文字。

---

## 16. SVG Drawing：SVG 绘图

### 16.1 SVG 是什么？

SVG 全称是 **Scalable Vector Graphics**，即可缩放矢量图形。

它可以直接写在 HTML 中，用来画：

- 圆形。
- 矩形。
- 椭圆。
- 直线。
- 多边形。
- 折线。
- 任意路径。
- 文字。

SVG 的特点：

- 是矢量图，放大后不会像普通位图那样模糊。
- 每个 SVG 元素和属性都可以被 CSS 或 JavaScript 控制。
- 可以做动画和交互效果。
- 是 W3C 推荐标准。

### 16.2 SVG 基本元素

课件列出的基本元素包括：

| SVG 元素       | 作用                       |
| ------------ | ------------------------ |
| `<g>`        | 分组，类似 HTML 里的 `<div>` 概念 |
| `<circle>`   | 圆                        |
| `<rect>`     | 矩形                       |
| `<ellipse>`  | 椭圆                       |
| `<line>`     | 直线                       |
| `<polygon>`  | 多边形，至少三条直边围成             |
| `<polyline>` | 折线，由多段直线连接但不一定闭合         |
| `<path>`     | 路径，可画复杂线条和形状             |
| `<text>`     | 文本                       |

### 16.3 常见 SVG 属性

常见属性包括：

- `width` / `height`：SVG 画布显示尺寸。
- `viewBox`：定义内部坐标系统。
- `cx` / `cy`：圆心坐标。
- `r`：圆半径。
- `x` / `y`：矩形起点坐标。
- `width` / `height`：矩形宽高。
- `rx` / `ry`：椭圆的横向、纵向半径。
- `fill`：填充颜色。
- `stroke`：描边颜色。
- `stroke-width`：描边宽度。
- `opacity` 或 `fill-opacity`：透明度。
- `transform`：变换，例如平移、旋转、缩放。

例如：

```html
<svg width="300" height="200">
  <circle cx="60" cy="60" r="30" fill="green" />
  <rect x="120" y="30" width="50" height="50" fill="red" />
  <ellipse cx="160" cy="140" rx="80" ry="40" fill="purple" />
</svg>
```

### 16.4 课件中的 SVG 例子

课件后面展示了几个 SVG 例子：

1. 用 `<circle>`、`<rect>`、`<ellipse>` 画圆、正方形和椭圆。
2. 用多个不同半径、不同颜色的圆叠加出彩虹效果。
3. 用矩形、圆形、多边形组合出房子、烟囱、烟雾等图形，并通过 CSS hover 改变颜色，实现简单交互。

这些例子想说明：SVG 图形不是图片文件，而是由标签和属性组成的结构化图形。也就是说，你可以像操作 HTML 元素一样操作 SVG 图形。

### 16.5 SVG 考试题思路

课件最后有 past exam paper question，要求根据图形选择合适的 SVG 元素。解题思路是：

- 雪花：可以用 `<line>` 或 `<path>` 画线段组合。
- 圣诞树：树冠可用 `<polygon>`，树干可用 `<rect>`。
- 姜饼人：头和身体可用 `<circle>` / `<ellipse>`，手脚和纽扣可用 `<circle>`、`<line>`、`<path>` 等。

这种题不一定要求写完整 SVG 代码，重点是能根据图形判断应该使用哪些 SVG 元素。

---

## 17. 本章重点总结

### 17.1 必须掌握的概念

- HTML 是网页内容和结构层。
- HTML 文档主要由 `<head>` 和 `<body>` 构成。
- Element = 起始标签 + 内容 + 结束标签。
- Attribute 写在起始标签中，形式通常是 `name="value"`。
- DOM 是浏览器把 HTML 解析出来的树状结构。
- 语义化 HTML 能提高可读性、可访问性和可维护性。
- `<div>` 和 `<span>` 是通用容器，但没有具体语义。
- `<ul>`、`<ol>`、`<li>` 用来创建列表。
- SVG 可以在网页中直接绘制矢量图形。

### 17.2 常见易错点

1. **把 tag 和 element 混为一谈**：tag 是标签，element 是完整元素。
2. **忘记写 `<!DOCTYPE html>`**：可能导致浏览器解析模式不一致。
3. **把所有内容都写进 `<div>`**：能显示，但语义差。
4. **图片不写 `alt`**：影响可访问性，也不利于错误提示。
5. **用表格做页面布局**：现代网页应主要用 CSS 布局，表格用于数据。
6. **滥用 `<br>` 控制排版**：排版应该交给 CSS。
7. **嵌套标签不正确闭合**：会导致 DOM 结构混乱。
8. **忽视 viewport meta**：移动端显示可能异常。
9. **把 CSS/JS/HTML 职责混在一起**：小例子可以，项目中应分层。
10. **只关注显示效果，不关注语义结构**：考试和实际开发都会看结构是否合理。

---

## 18. 推荐记忆模板

### 18.1 HTML 页面基本模板

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>Main Title</h1>
  </header>

  <nav>
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#about">About</a></li>
    </ul>
  </nav>

  <main>
    <section>
      <h2>Section Title</h2>
      <p>This is a paragraph.</p>
    </section>
  </main>

  <footer>
    <p>Footer information</p>
  </footer>

  <script src="main.js"></script>
</body>
</html>
```

### 18.2 SVG 基本模板

```html
<svg width="300" height="200" viewBox="0 0 300 200">
  <rect x="10" y="10" width="100" height="60" fill="skyblue" />
  <circle cx="180" cy="60" r="30" fill="orange" />
  <line x1="20" y1="150" x2="260" y2="150" stroke="black" stroke-width="2" />
</svg>
```

---

## 19. 如果要复习考试，优先看这些

1. 写出一个完整 HTML5 页面骨架。
2. 解释 `<head>` 和 `<body>` 的区别。
3. 解释 element、tag、attribute 的区别。
4. 说明 DOM Tree 中 parent、child、sibling、ancestor 的关系。
5. 判断哪些标签是语义化标签，哪些只是通用容器。
6. 正确写出 `<a>`、`<img>`、`table`、`form`、`ul/ol/li` 的基本用法。
7. 区分 block 和 inline 元素，尤其是 `<div>` 与 `<span>`。
8. 能根据图形选择合适的 SVG 元素，例如 circle、rect、polygon、path 等。

---

## 20. 一句话结尾

本章不是只让你“背标签”，而是让你建立网页结构思维：先用 HTML 把内容组织成清晰、语义明确的结构，再用 CSS 美化，用 JavaScript 增加交互。HTML 写得好，后面的样式、动画和交互才会更容易实现。
---

# Unit 1 - Lecture 2: CSS Basics & Animations 讲解

> [!info] 来源
> 本部分讲解的是 EBU6305 Interactive Media Design and Production 的 **Lecture 2: CSS Basics & Animations**，原课件见：[[附件/Unit 1 - Coding & Development/Lecture 2. CSS Basics and Animations.pdf|Lecture 2. CSS Basics and Animations.pdf]]。

## 1. 这一讲整体在讲什么？

Lecture 1 主要讲 HTML：网页有什么内容、结构怎么写。Lecture 2 开始讲 CSS：网页内容应该长什么样、元素应该怎么排版、怎么做动画和视觉效果。

这一讲的核心目标是：

- 理解 CSS 的基本语法和结构。
- 知道 CSS 如何影响 HTML 元素的显示方式。
- 掌握 CSS 选择器、class、id、盒模型、常用属性和单位。
- 理解 CSS 动画的基本机制，例如 `@keyframes`、`transition`、`transform`、`opacity`。
- 理解如何用多层动画和视觉技巧做出类似 2.5D 的深度错觉。

一句话概括：

> HTML 负责“页面里有什么”，CSS 负责“这些东西看起来是什么样、怎么移动、怎么变化”。

---

## 2. What is CSS：CSS 是什么？

CSS 全称是 **Cascading Style Sheets**，中文通常叫“层叠样式表”。

课件里说 CSS 的作用是描述 HTML 元素应该如何显示在：

- 屏幕上。
- 纸张上。
- 其他媒体中。

例如 HTML 写的是：

```html
<p>This is a paragraph.</p>
```

它只说明“这是一个段落”。但是它没有详细说明这个段落应该是什么颜色、字体多大、是否居中、背景是什么颜色。

CSS 可以写成：

```css
p {
  color: red;
  font-size: 20px;
  text-align: center;
}
```

这就告诉浏览器：所有 `<p>` 段落文字变红、字号为 `20px`、居中显示。

CSS 的优点：

1. **节省工作量**：一个 CSS 规则可以同时控制很多 HTML 元素。
2. **方便统一风格**：整个网站可以共享同一个样式文件。
3. **内容和表现分离**：HTML 写结构，CSS 写样式，代码更清楚。
4. **便于维护**：改一个 CSS 文件，就可能影响多个页面。

---

## 3. A Style：CSS 样式的基本组成

课件用这个例子解释 CSS 样式：

```css
p {
  font-family: times;
}
```

它可以拆成三部分：

| 部分 | 例子 | 意思 |
|---|---|---|
| Selector | `p` | 选择要设置样式的 HTML 元素 |
| Property | `font-family` | 要修改的样式属性 |
| Value | `times` | 这个属性的具体值 |

逐行解释：

```css
p {
```

选择所有 `<p>` 元素。大括号 `{` 表示样式声明开始。

```css
  font-family: times;
```

设置字体为 `times`。`font-family` 是属性，`times` 是值。属性和值之间用冒号 `:`，这一条声明用分号 `;` 结束。

```css
}
```

样式声明结束。

> [!important] 标点很重要
> CSS 中 `:`、`;`、`{}` 都很重要。少写分号或括号，样式可能失效。

---

## 4. CSS Rule：CSS 规则集

一个 CSS rule-set 通常由两部分组成：

1. **selector**：选择器，指出要给哪些 HTML 元素加样式。
2. **declaration block**：声明块，包含一条或多条样式声明。

例如：

```css
h1 {
  color: red;
  font-size: xx-large;
  text-align: center;
}
```

逐行解释：

| 代码 | 解释 |
|---|---|
| `h1 {` | 选择所有 `<h1>` 标题，开始写样式规则。 |
| `color: red;` | 设置文字颜色为红色。 |
| `font-size: xx-large;` | 设置字体大小为很大。 |
| `text-align: center;` | 设置文字居中对齐。 |
| `}` | 结束这组 CSS 规则。 |

所以 CSS 规则可以理解成：

> 选择谁 selector，然后告诉它应该变成什么样 declaration。

---

## 5. CSS Syntax and Selectors：选择器

选择器决定 CSS 要作用到哪些 HTML 元素上。课件讲了几种基础选择器。

### 5.1 Element selector：元素选择器

根据 HTML 标签名选择元素。

```css
p {
  text-align: center;
}
```

意思是：所有 `<p>` 段落都居中。

适合用于统一设置某类标签的默认样式，例如所有段落、所有标题、所有链接。

### 5.2 ID selector：ID 选择器

ID 选择器用 `#`，对应 HTML 里的 `id` 属性。

HTML：

```html
<p id="para1">Hello</p>
```

CSS：

```css
#para1 {
  text-align: center;
}
```

意思是：只选择 `id="para1"` 的那个元素。

特点：

- 一个页面中同一个 `id` 应该只出现一次。
- `id` 适合定位唯一元素。
- JavaScript 也经常通过 `id` 找元素。

### 5.3 Class selector：类选择器

Class 选择器用 `.`，对应 HTML 里的 `class` 属性。

HTML：

```html
<p class="center">Hello</p>
<h2 class="center">Title</h2>
```

CSS：

```css
.center {
  text-align: center;
}
```

意思是：所有 `class="center"` 的元素都居中。

特点：

- 同一个 class 可以被很多元素共用。
- 一个元素可以有多个 class。
- class 是 CSS 里最常用的样式组织方式。

### 5.4 Grouping selectors：分组选择器

如果多个选择器使用相同样式，可以用逗号合并：

```css
h1, h2, p {
  text-align: center;
}
```

意思是：`h1`、`h2` 和 `p` 都居中。

这样可以减少重复代码。

---

## 6. Cascading：为什么叫“层叠”？

CSS 里的 cascading 指的是：当多个样式同时作用到同一个元素，并且它们之间发生冲突时，浏览器会根据优先级决定最终使用哪一个。

课件给出的优先级顺序是：

1. **Inline style**：内联样式，优先级最高。
2. **Internal style sheet**：内部样式表，第二优先级。
3. **External style sheet**：外部样式表，第三优先级。
4. **Browser default**：浏览器默认样式，最低优先级。

例如：

```html
<h1 style="color: red;">Title</h1>
```

如果外部 CSS 写：

```css
h1 {
  color: blue;
}
```

因为内联样式优先级更高，最终标题会显示红色。

课件还提醒：如果在同一个样式表中写了多条冲突规则，通常后面的规则会覆盖前面的规则。

```css
p {
  color: red;
}

p {
  color: blue;
}
```

最终 `<p>` 通常会显示蓝色，因为后面的规则覆盖前面的规则。

---

## 7. Three Ways to Use CSS：使用 CSS 的三种方式

### 7.1 Inline Style：内联样式

内联样式直接写在 HTML 标签的 `style` 属性里：

```html
<h2 style="color:red;">CAUTION: Icy Road Conditions</h2>
<h2>Please Slow Down!</h2>
```

解释：

- 第一行 `<h2>` 有 `style="color:red;"`，所以变红。
- 第二行 `<h2>` 没有这个 style，所以不会被这条内联样式影响。

优点：写起来直接，适合临时测试。

缺点：

- 只能影响一个元素。
- 样式和内容混在一起。
- 不利于维护。

所以课件说，内联样式一般不推荐大量使用。

### 7.2 Internal Style Sheet：内部样式表

内部样式表写在 HTML 的 `<head>` 里的 `<style>` 标签中：

```html
<head>
  <style type="text/css">
    h2 {
      color: red;
    }
  </style>
</head>
<body>
  <h2>CAUTION: Icy Road Conditions</h2>
  <h2>Please Slow Down!</h2>
</body>
```

解释：

- CSS 写在 `<style>` 里。
- 选择器是 `h2`，所以页面上所有 `<h2>` 都会变红。
- 样式放在 `<head>`，页面内容放在 `<body>`，比内联样式更清楚。

适合单个页面的小项目或课堂练习。

### 7.3 External Style Sheet：外部样式表

外部样式表是把 CSS 写到单独的 `.css` 文件中，再在 HTML 里用 `<link>` 引入。

`style.css`：

```css
h2 {
  color: red;
}
```

`example.html`：

```html
<head>
  <link rel="stylesheet" type="text/css" href="style.css">
</head>
<body>
  <h2>CAUTION: Icy Road Conditions</h2>
  <h2>Please Slow Down!</h2>
</body>
```

`<link>` 的作用是告诉浏览器：加载 `style.css`，并把里面的 CSS 应用到当前 HTML 页面。

外部 CSS 的好处：

- **Re-usability**：一个 CSS 文件可以被多个页面共用。
- **Redundancy reduction**：减少重复代码。
- **Separation of concerns**：HTML 管结构，CSS 管样式。
- **更适合真实网站**：大多数网站都会使用外部 CSS。

---

## 8. HTML Class：class 的作用

`class` 属性用于给一组元素定义相同样式。

例如：

```html
<div class="city">
  <h2>London</h2>
  <p>London is the capital of England.</p>
</div>

<div class="city">
  <h2>Paris</h2>
  <p>Paris is the capital of France.</p>
</div>
```

CSS：

```css
.city {
  background-color: black;
  color: white;
  padding: 20px;
}
```

解释：

- 两个 `<div>` 都有 `class="city"`。
- `.city` 选择器会选中它们两个。
- 所以 London 和 Paris 两块内容会有相同样式。

### 8.1 一个元素可以有多个 class

课件提到：多个 class 名之间用空格分开。

```html
<div class="city main important">London</div>
```

这表示这个元素同时属于三个 class：

- `city`
- `main`
- `important`

CSS 可以分别写：

```css
.city {
  padding: 20px;
}

.main {
  background-color: tomato;
}

.important {
  font-weight: bold;
}
```

这个元素会同时受到这三组样式影响。

> [!tip] class 怎么记？
> class 像“分类标签”。很多元素可以属于同一个 class，一个元素也可以同时属于多个 class。

---

## 9. HTML ID：id 的作用

`id` 属性用于给某一个 HTML 元素设置唯一标识。

HTML：

```html
<h1 id="myHeader">My Header</h1>
```

CSS：

```css
#myHeader {
  background-color: lightblue;
  color: black;
  padding: 40px;
  text-align: center;
}
```

解释：

- `id="myHeader"` 表示这个元素的唯一名字是 `myHeader`。
- CSS 中用 `#myHeader` 选择这个元素。
- `#` 是 id selector 的标志。

### 9.1 Class 和 ID 的区别

| 对比 | class | id |
|---|---|---|
| CSS 符号 | `.` | `#` |
| 是否唯一 | 不唯一，可重复 | 应该唯一 |
| 一个元素能有几个 | 可以有多个 class | 通常只能有一个 id |
| 常见用途 | 批量设置样式 | 定位唯一元素，配合 JS 操作 |

例子：

```html
<p class="city">London</p>
<p class="city">Paris</p>
<p id="main-title">Main Title</p>
```

- `city` 可以给多个元素使用。
- `main-title` 应该只给一个元素使用。

---

## 10. Pseudo-class：伪类

伪类用于表示元素的某种特殊状态。

课件给出的语法：

```css
selector:pseudo-class {
  property: value;
}
```

常见场景：

- 鼠标悬停时改变样式。
- 已访问和未访问链接使用不同样式。
- 输入框获得焦点时改变样式。

例子：

```css
a:hover {
  color: red;
}
```

意思是：当鼠标悬停在链接上时，链接文字变红。

再比如：

```css
input:focus {
  border: 2px solid blue;
}
```

意思是：当输入框被点击并处于输入状态时，边框变蓝。

> [!note] 伪类的重点
> 伪类不是 HTML 里真实写出来的 class，而是浏览器根据元素状态“临时匹配”的样式条件。

---

## 11. Pseudo-element：伪元素

伪元素用于选择元素中的某一部分，例如第一个字母、第一行等。

课件给出的语法：

```css
selector:pseudo-element {
  property: value;
}
```

现代 CSS 更常见的写法是双冒号：

```css
p::first-letter {
  color: red;
  font-size: xx-large;
}
```

意思是：每个 `<p>` 段落的第一个字母变红，并且变大。

再比如：

```css
p::first-line {
  font-weight: bold;
}
```

意思是：段落第一行加粗。

伪类和伪元素的区别：

| 类型 | 作用 | 例子 |
|---|---|---|
| pseudo-class | 选择某种状态 | `a:hover`、`input:focus` |
| pseudo-element | 选择元素的一部分 | `p::first-letter`、`p::first-line` |

---

## 12. CSS Comments：CSS 注释

CSS 注释用：

```css
/* This is a comment */
```

也可以跨多行：

```css
/*
  This is a multi-line comment.
  Browser will ignore it.
*/
```

注释的作用：

- 解释某段样式的用途。
- 临时禁用某段 CSS。
- 给自己或团队成员留下说明。

浏览器不会把注释当成样式执行。

---

## 13. CSS Combinator Selectors：组合选择器

课件只把这一部分作为 background reading，但它很重要。组合选择器用于根据元素之间的关系选择元素。

常见组合选择器：

| 选择器 | 名称 | 作用 |
|---|---|---|
| `div p` | 后代选择器 | 选择 `div` 里面所有 `p` |
| `div > p` | 子元素选择器 | 只选择直接子级 `p` |
| `div + p` | 相邻兄弟选择器 | 选择紧跟在 `div` 后面的第一个 `p` |
| `div ~ p` | 通用兄弟选择器 | 选择 `div` 后面的所有兄弟 `p` |

例子：

```css
.card p {
  color: gray;
}
```

意思是：选择 `.card` 里面所有段落。

```css
.card > p {
  color: gray;
}
```

意思是：只选择 `.card` 的直接子级段落，不包括更深层嵌套的段落。

---

## 14. CSS Box Model：盒模型

### 14.1 盒模型是什么？

课件说：所有 HTML 元素都可以看作盒子。

CSS box model 包括四层：

1. **Content**：内容区域，显示文字或图片。
2. **Padding**：内边距，内容和边框之间的透明区域。
3. **Border**：边框，围绕 padding 和 content。
4. **Margin**：外边距，元素边框外面的透明区域，用来和其他元素保持距离。

可以想象成：

```text
Margin
  Border
    Padding
      Content
```

### 14.2 Content

Content 是元素真正的内容区域，例如文字、图片等。

```css
div {
  width: 320px;
}
```

这里的 `width: 320px` 默认设置的是 content 区域宽度。

### 14.3 Padding

Padding 是内容和边框之间的空间。

```css
div {
  padding: 10px;
}
```

表示上下左右内边距都是 `10px`。

Padding 是透明的，但它会增加元素占用空间。

### 14.4 Border

Border 是边框。

```css
div {
  border: 5px solid green;
}
```

意思是：边框宽度 `5px`，样式为实线 `solid`，颜色是绿色。

### 14.5 Margin

Margin 是边框外面的空间。

```css
div {
  margin: 20px;
}
```

表示这个元素和周围元素之间留出 `20px` 距离。

### 14.6 元素实际宽度怎么算？

课件给了这个例子：

```css
div {
  width: 320px;
  padding: 10px;
  border: 5px solid green;
  margin: 0;
}
```

总宽度计算：

```text
320px 内容宽度
+ 20px 左右 padding：10px + 10px
+ 10px 左右 border：5px + 5px
+ 0px 左右 margin
= 350px
```

所以虽然 `width` 写的是 `320px`，但元素实际占据的水平空间是 `350px`。

> [!important] 盒模型是 CSS 布局的基础
> 很多布局问题都和 `width`、`padding`、`border`、`margin` 的计算有关。

---

## 15. CSS Properties：常用 CSS 属性

课件列出了一批常见 CSS 属性，可以分成三类。

### 15.1 Colours & Borders：颜色和边框

```css
color: red;
```

设置文字颜色。

```css
background-color: white;
```

设置背景颜色。

```css
background-image: url(image.gif);
```

设置背景图片。

```css
border-color: yellow;
```

设置边框颜色。

```css
border: 1px solid blue;
```

一次性设置边框宽度、样式和颜色。

### 15.2 Text Styles：文字样式

```css
text-align: left;
```

设置水平对齐方式，可以是 `left`、`center`、`right`。

```css
text-decoration: underline;
```

设置文字装饰，例如下划线、删除线等。

```css
font-family: Arial, Helvetica, sans-serif;
```

设置字体。

```css
font-size: 16pt;
```

设置字号。

```css
font-weight: bold;
```

设置字体粗细。

### 15.3 Size and Layout：尺寸和布局

```css
width: 400px;
```

设置元素宽度。

```css
height: 100%;
```

设置元素高度。

```css
margin: 5px;
```

设置外边距。

```css
margin-top: 1px;
```

单独设置顶部外边距。类似的还有 `margin-bottom`、`margin-left`、`margin-right`。

```css
padding: 5px;
```

设置内边距。

```css
padding-top: 1px;
```

单独设置顶部内边距。类似的还有 `padding-bottom`、`padding-left`、`padding-right`。

---

## 16. CSS Units：CSS 单位

CSS 中很多属性都需要单位，比如宽度、高度、字号、边距等。

### 16.1 Absolute length units：绝对单位

课件列出的绝对单位：

| 单位 | 含义 |
|---|---|
| `cm` | 厘米 |
| `mm` | 毫米 |
| `in` | 英寸，`1in = 96px = 2.54cm` |
| `px` | 像素，屏幕设计最常见 |
| `pt` | 点，`1pt = 1/72in` |
| `pc` | pica，`1pc = 12pt` |

课件提醒：绝对单位是固定长度，但屏幕尺寸差异很大，所以不一定适合响应式网页。它们更适合输出媒介已知的场景，例如打印。

### 16.2 Relative length units：相对单位

相对单位会根据其他东西变化，更适合不同屏幕和响应式布局。

| 单位 | 相对于什么 |
|---|---|
| `em` | 当前元素字体大小，`2em` 是当前字体的 2 倍 |
| `rem` | 根元素字体大小，通常相对于 `<html>` |
| `%` | 父元素尺寸 |
| `vw` | 视口宽度的 1% |
| `vh` | 视口高度的 1% |
| `vmin` | 视口较短边的 1% |
| `vmax` | 视口较长边的 1% |
| `ch` | 字符 `0` 的宽度 |
| `ex` | 当前字体 x-height，较少使用 |

例子：

```css
.container {
  width: 80%;
}
```

意思是容器宽度为父元素的 80%。

```css
.hero {
  height: 100vh;
}
```

意思是这个区域高度等于整个浏览器视口高度。

---

## 17. CSS Animation：CSS 动画

课件从 falling animation 和 bike animation 引入：很多动画可以完全用 HTML 和 CSS 完成，不一定需要 JavaScript。

它说动画的关键材料是：

- 一部分 HTML 或 SVG：用来画出图形结构。
- 一部分 CSS：用来定义图形的样式和行为。
- `@keyframes`：定义动画过程中样式如何变化。
- styles：普通样式规则。

---

## 18. `@keyframes`：关键帧动画

### 18.1 `@keyframes` 是什么？

`@keyframes` 用来定义动画代码。动画的本质是：元素从一组 CSS 样式逐渐变化到另一组 CSS 样式。

课件提到两种写法：

1. 用 `from` 和 `to` 表示开始和结束。
2. 用百分比 `0%`、`25%`、`50%`、`100%` 表示不同时间点。

### 18.2 From and To 写法

```html
<html>
<head>
<style>
div {
  width: 100px;
  height: 100px;
  background: red;
  position: relative;
  animation: fall 5s infinite;
}

@keyframes fall {
  from {
    top: 0px;
  }
  to {
    top: 200px;
  }
}
</style>
</head>
<body>
  <div></div>
</body>
</html>
```

逐行解释重点：

| 代码 | 解释 |
|---|---|
| `width: 100px;` | 设置 div 宽度为 100px。 |
| `height: 100px;` | 设置 div 高度为 100px。 |
| `background: red;` | 设置 div 背景为红色，所以它看起来是红色方块。 |
| `position: relative;` | 让元素可以相对自身正常位置移动。没有定位时，`top` 不会按预期工作。 |
| `animation: fall 5s infinite;` | 使用名为 `fall` 的动画，持续 5 秒，并无限循环。 |
| `@keyframes fall` | 定义名为 `fall` 的动画。名字必须和 `animation` 中的名字对应。 |
| `from { top: 0px; }` | 动画开始时，元素在原始垂直位置。 |
| `to { top: 200px; }` | 动画结束时，元素向下移动 200px。 |

所以这个动画的效果是：红色方块不断向下移动。

### 18.3 Percentages 写法

```css
@keyframes changeBG {
  0% {
    background-color: red;
  }
  25% {
    background-color: yellow;
  }
  50% {
    background-color: blue;
  }
  100% {
    background-color: green;
  }
}

div {
  width: 100px;
  height: 100px;
  position: relative;
  background-color: red;
  animation-name: changeBG;
  animation-duration: 4s;
}
```

解释：

- `0%`：动画刚开始，背景是红色。
- `25%`：动画进行到四分之一，背景变黄色。
- `50%`：动画进行到一半，背景变蓝色。
- `100%`：动画结束，背景变绿色。
- `animation-name` 指定动画名字。
- `animation-duration` 指定动画持续时间。

百分比写法比 `from/to` 更灵活，因为可以定义中间过程。

---

## 19. Relative vs Absolute：相对定位和绝对定位

课件对比了两种定位：

- **Relative**：相对于元素自己的正常位置移动。
- **Absolute**：相对于它的定位父元素移动。

### 19.1 `position: relative`

```css
.red {
  position: relative;
  top: 16px;
  left: 10px;
}
```

意思是：元素原本在正常文档流中的位置不变，但是视觉上从原位置向下移动 `16px`，向右移动 `10px`。

可以理解成：

> 先站在原来的位置，再从原位置偏移。

### 19.2 `position: absolute`

```css
.red {
  position: absolute;
  top: 16px;
  left: 10px;
}
```

意思是：元素脱离正常文档流，根据最近的定位父元素来确定位置。

可以理解成：

> 不再按原来的排队位置站，而是按照父容器的坐标直接放到指定位置。

### 19.3 为什么动画常用 position？

如果动画里要改变 `top`、`left`，元素通常需要设置 `position`。否则这些属性可能不会产生移动效果。

---

## 20. 2.5D：什么是 2.5D？

课件说 2.5D 是一种视觉风格：它使用平面的 2D 元素，但通过阴影、渐变、层叠、透视、视差等方式模拟 3D 深度。

它不是完整的 3D 建模，而是制造“看起来有深度”的错觉。

常见特点：

- 使用 shadows 阴影暗示高度。
- 使用 gradients 渐变暗示光照。
- 使用 layering 层叠制造前后关系。
- 使用 perspective 透视制造空间感。
- 使用 parallax 视差让不同层移动速度不同。

常见应用：

- UI 设计。
- 游戏。
- 动画。
- 信息图。
- 等距视角 isometric games。
- 视差网页 parallax websites。

### 20.1 为什么叫 2.5D？

因为它介于 2D 和 3D 之间：

- 素材本质上还是二维平面。
- 视觉上却让人感觉有三维空间。

---

## 21. Perspectives for Illusion：用多种动画制造错觉

课件指出：你可以用多个动画叠加出不同透视效果，让用户产生 illusion。

比如一个画面中可能同时有：

- 背景缓慢移动。
- 前景快速移动。
- 物体从远到近变大。
- 阴影跟着移动。
- 透明度变化。
- 元素旋转或缩放。

这些效果组合起来，就会让平面网页有空间深度。

---

## 22. Transition：过渡效果

`transition` 用来让 CSS 属性变化时不要突然改变，而是平滑过渡。

例如：

```html
<style>
div {
  width: 100px;
  height: 100px;
  background: blue;
  transition: all 0.5s linear;
}

div:hover {
  width: 150px;
  height: 150px;
}
</style>

<div></div>
```

解释：

- 初始时 `div` 是 `100px × 100px` 的蓝色方块。
- `transition: all 0.5s linear;` 表示所有可变化属性用 0.5 秒线性过渡。
- 鼠标悬停时，宽高变成 `150px × 150px`。
- 因为有 transition，所以方块会平滑变大，而不是瞬间变大。

---

## 23. Transform：变换效果

`transform` 可以让元素移动、旋转、缩放、倾斜等。

课件的 Example 2 是 transition 和 transform 结合。

例如：

```css
div {
  width: 100px;
  height: 100px;
  background: blue;
  transition: all 0.5s linear;
}

div:hover {
  transform: rotate(45deg) scale(1.2);
}
```

解释：

- 鼠标不悬停时，是普通蓝色方块。
- 鼠标悬停时，方块旋转 `45deg`，并放大到 `1.2` 倍。
- 因为有 `transition`，旋转和放大过程是平滑的。

常见 transform 函数：

| 函数 | 作用 |
|---|---|
| `translate(x, y)` | 平移 |
| `rotate(deg)` | 旋转 |
| `scale(n)` | 缩放 |
| `skew(deg)` | 倾斜 |

---

## 24. Opacity：透明度

`opacity` 控制元素透明度：

```css
opacity: 0;
```

完全透明，看不见。

```css
opacity: 1;
```

完全不透明，正常显示。

课件 Example 3 的思路是：

1. 创建两个大小一样的 `<div>` 盒子。
2. 其中一个开始时透明。
3. 鼠标悬停时，让透明的盒子显示出来，并覆盖另一个盒子。

示例：

```css
.box {
  width: 300px;
  height: 200px;
  position: relative;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 300px;
  height: 200px;
  background-color: rgba(0, 255, 0, 0.7);
  opacity: 0;
  transition: opacity 0.5s ease-in-out;
}

.box:hover .overlay {
  opacity: 1;
}
```

解释：

- `.overlay` 是覆盖层。
- 初始 `opacity: 0`，看不见。
- 鼠标悬停 `.box` 时，`.overlay` 变成 `opacity: 1`。
- `transition` 让出现过程变得平滑。

课件问 random text generator 的意义：它可以快速生成占位文字，用来测试网页排版、文字覆盖、布局空间是否合理。

---

## 25. Polish it：让效果更精致

课件 Example 4 说：加入更多 hover 效果，合理混合可以制造更强的透视感。

可以逐步加入：

- `opacity`：透明度变化。
- `transform: scale()`：放大缩小。
- `transform: translate()`：移动。
- `transition-delay`：延迟出现。
- `transition-timing-function`：控制速度曲线。
- `box-shadow`：增加阴影。
- `overflow: hidden`：隐藏超出容器的内容。

关键方法是：

> 一次只加一个效果，测试没问题后再加下一个。

这样更容易定位错误，也能避免动画效果过度混乱。

---

## 26. 本讲重点总结

### 26.1 必须掌握

- CSS 是 Cascading Style Sheets，用来控制 HTML 的视觉表现。
- CSS 规则由 selector 和 declaration block 组成。
- 每条声明由 property 和 value 组成。
- CSS 可以通过 inline、internal、external 三种方式使用。
- `class` 用 `.` 选择，可以重复使用。
- `id` 用 `#` 选择，应该唯一。
- 伪类用于状态，例如 `:hover`。
- 伪元素用于元素的一部分，例如 `::first-letter`。
- 盒模型包括 content、padding、border、margin。
- `width` 默认只是 content 宽度，不包括 padding、border、margin。
- CSS 单位分绝对单位和相对单位。
- `@keyframes` 用来定义动画过程。
- `transition` 控制平滑过渡。
- `transform` 控制移动、旋转、缩放等变换。
- `opacity` 控制透明度。
- 2.5D 是用 2D 元素模拟 3D 深度的视觉方法。

### 26.2 常见易错点

1. 忘记 CSS 声明末尾的分号 `;`。
2. 忘记 declaration block 的 `{}`。
3. 混淆 class 和 id：class 用 `.`，id 用 `#`。
4. 在一个页面里重复使用同一个 id。
5. 大量使用 inline style，导致样式难以维护。
6. 不理解 cascading，导致样式被覆盖却不知道原因。
7. 忘记 padding 和 border 会增加元素实际尺寸。
8. 改 `top` / `left` 却没有设置 `position`。
9. 用动画堆太多效果，导致页面混乱或性能下降。
10. 只看动画效果，不理解 HTML/SVG 结构和 CSS 行为之间的关系。

---

## 27. 推荐记忆模板

### 27.1 CSS 基本规则模板

```css
selector {
  property: value;
}
```

### 27.2 外部 CSS 引入模板

```html
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

### 27.3 class 和 id 模板

```html
<div class="card important" id="main-card">
  Content
</div>
```

```css
.card {
  padding: 20px;
}

.important {
  font-weight: bold;
}

#main-card {
  background-color: lightblue;
}
```

### 27.4 盒模型模板

```css
.box {
  width: 320px;
  padding: 10px;
  border: 5px solid green;
  margin: 20px;
}
```

实际占用宽度：

```text
320 + 10 + 10 + 5 + 5 + 20 + 20 = 390px
```

### 27.5 动画模板

```css
.square {
  width: 100px;
  height: 100px;
  background: red;
  position: relative;
  animation: fall 5s infinite;
}

@keyframes fall {
  from {
    top: 0;
  }
  to {
    top: 200px;
  }
}
```

### 27.6 hover + transition 模板

```css
.card {
  transition: all 0.3s ease;
}

.card:hover {
  transform: scale(1.05);
  opacity: 0.8;
}
```

---

## 28. 如果要复习考试，优先看这些

1. 写出 CSS rule-set，并指出 selector、property、value。
2. 解释 CSS 为什么叫 cascading。
3. 比较 inline、internal、external CSS 的区别和优先级。
4. 正确使用 element selector、class selector、id selector。
5. 解释 class 和 id 的区别。
6. 解释 `:hover` 这种 pseudo-class 的作用。
7. 解释 `::first-letter` 这种 pseudo-element 的作用。
8. 画出或解释 CSS box model 的四层：content、padding、border、margin。
9. 计算元素实际宽度。
10. 区分 absolute units 和 relative units。
11. 写出基本 `@keyframes` 动画。
12. 解释 `transition` 和 `transform` 的区别。
13. 解释 `opacity` 如何做覆盖层效果。
14. 解释 2.5D 如何用 2D 元素制造 3D 错觉。

---

## 29. 一句话结尾

Lecture 2 的重点不是单纯背 CSS 属性，而是理解“选择谁、改什么、如何层叠、如何布局、如何变化”。只要掌握 selector、box model、class/id 和 animation 这几块，后面做网页视觉设计和交互动画就有了基础。
---

# Unit 1 - Lecture 3: JavaScript Basics 讲解

> [!info] 来源
> 本部分讲解的是 EBU6305 Interactive Media Design and Production 的 **Lecture 3: JavaScript Basics**，原课件见：[[附件/Unit 1 - Coding & Development/Lecture 3. JavaScript Basics.pdf|Lecture 3. JavaScript Basics.pdf]]。

## 1. 这一讲整体在讲什么？

前两讲分别讲了：

- **HTML**：网页的内容和结构。
- **CSS**：网页的视觉样式和动画表现。

Lecture 3 进入第三层：**JavaScript**。

JavaScript 主要负责网页的 **行为 behaviour**，也就是让网页能够响应用户操作、改变页面内容、处理数据、运行逻辑、制作小应用。

这一讲的学习目标包括：

- 理解 JavaScript 的基本语法。
- 能够用 JavaScript 写简单程序。
- 理解如何在 HTML 文档中使用 JavaScript。
- 用 JavaScript 创建简单应用，例如拖拽图片和时钟。

课件主题包括：

1. Structure：JavaScript 的基本结构。
2. Data Types：数据类型。
3. Program Control：程序控制，包括条件、循环、函数。
4. Event Listener：事件监听器。
5. A Simple Clock：用 Canvas 和 JavaScript 做一个简单时钟。

一句话概括：

> JavaScript 是网页的“动作和逻辑层”：HTML 放内容，CSS 做样式，JavaScript 让网页能动、能判断、能响应用户。

---

## 2. JavaScript as a Language：JavaScript 是什么语言？

课件说 JavaScript 是一种 **scripting language**，也就是脚本语言。

### 2.1 脚本语言是什么意思？

脚本语言通常通过 **解释器 interpreter** 运行，而不是像某些语言那样先整体编译成机器码再运行。

在网页里，JavaScript 通常由浏览器解释执行。

例如你在 HTML 里写：

```html
<script>
  alert("Hello JavaScript");
</script>
```

浏览器加载页面时会执行这段脚本。

### 2.2 JavaScript 是动态语言

课件说 JavaScript 是 dynamic programming language。这里的 dynamic 可以理解为：

- 变量的数据类型可以变化。
- 很多事情在运行时才确定。
- 写法相对灵活。

例如：

```javascript
var myValue;
myValue = 10;
myValue = "My Name";
```

同一个变量 `myValue` 一开始可以存数字，后面又可以存字符串。

### 2.3 JavaScript 不是 Java

课件特别提醒：**JavaScript is NOT Java**。

它们名字像，但不是同一种语言。

区别可以简单理解为：

| 对比     | JavaScript  | Java        |
| ------ | ----------- | ----------- |
| 常见运行环境 | 浏览器、Node.js | JVM、服务器、安卓等 |
| 类型系统   | 动态类型        | 静态类型        |
| 网页中的作用 | 前端交互核心语言    | 不是浏览器原生脚本语言 |
| 语法关系   | 有 C 风格语法    | 也有 C 风格语法   |

JavaScript 和 Java 都有 `if`、`switch`、`while` 等结构，但语义和运行方式不同。

---

## 3. JavaScript Structure：JavaScript 在 HTML 中的结构

### 3.1 `<script>` 标签

JavaScript 写在 HTML 中时，通常放在 `<script>` 和 `</script>` 之间。

```html
<script>
  document.getElementById("demo").innerHTML = "My JavaScript Programme";
</script>
```

逐行解释：

| 代码 | 解释 |
|---|---|
| `<script>` | 告诉浏览器：这里开始是 JavaScript 代码。 |
| `document.getElementById("demo")` | 在 HTML 文档中寻找 `id="demo"` 的元素。 |
| `.innerHTML` | 修改这个元素内部的 HTML 内容。 |
| `= "My JavaScript Programme";` | 把元素内容设置成这段文字。 |
| `</script>` | JavaScript 代码结束。 |

### 3.2 JavaScript 可以放在哪里？

课件说 JavaScript 可以嵌入在：

- `<head>` 中。
- `<body>` 中。

例如放在 `<body>` 中：

```html
<html>
<body>
  <p id="myJavaScript"></p>

  <script>
    document.getElementById("myJavaScript").innerHTML = "My JavaScript Programme";
  </script>
</body>
</html>
```

这种写法的好处是：当脚本执行时，`<p id="myJavaScript"></p>` 已经存在了，所以 JavaScript 能找到它。

如果脚本放在 `<head>` 里，但页面元素还没被浏览器加载出来，直接查找元素可能失败。因此实际开发中常见做法是：

- 把 `<script>` 放在 `body` 结尾。
- 或者使用 `defer`。
- 或者等 DOM 加载完成后再执行代码。

---

## 4. JS Syntax：JavaScript 语法基础

### 4.1 Expression：表达式

课件说 expression 是变量或常量的组合，它本身不能独立构成完整程序句子。

例子：

```javascript
10 + 7
10 - 7
10 / 7
```

这些表达式会产生一个值，例如 `10 + 7` 的结果是 `17`。

### 4.2 Statement：语句

Statement 是程序里的完整句子，可以执行一个动作。

例如：

```javascript
var mySum = 10 + 7;
var mySub = 10 - 7;
var myDiv = 10 / 7;
document.getElementById("myJavaScript").innerHTML = "My JavaScript Programme";
```

解释：

- `var mySum = 10 + 7;` 是完整语句：声明变量并赋值。
- `10 + 7` 只是表达式。
- 语句通常以分号 `;` 结束。

> [!tip] 简单记法
> Expression 像“一个计算片段”；Statement 像“完整的一句话/命令”。

---

## 5. JS Assignment：赋值

课件说变量用等号 `=` 赋值。

```javascript
myAge = 35;
```

意思是把数字 `35` 存进变量 `myAge`。

再看课件例子：

```javascript
var thisYear;      // variable declaration
thisYear = "2020"; // assignment
```

逐行解释：

| 代码 | 解释 |
|---|---|
| `var thisYear;` | 声明一个变量，名字叫 `thisYear`。此时还没有具体值。 |
| `thisYear = "2020";` | 把字符串 `"2020"` 赋值给 `thisYear`。 |

注意：

```javascript
=
```

在 JavaScript 中主要是 **赋值**，不是数学意义上的“相等判断”。

相等判断常用：

```javascript
==
===
```

初学阶段先记住：

> 单个 `=` 是把右边的值放进左边的变量。

---

## 6. JS Operators：运算符

课件把运算符分为三类。

### 6.1 Arithmetic operators：算术运算符

| 运算符 | 作用 |
|---|---|
| `+` | 加法，也可用于字符串拼接 |
| `-` | 减法 |
| `*` | 乘法 |
| `/` | 除法 |
| `%` | 取余数 |
| `++` | 自增 1 |
| `--` | 自减 1 |

例子：

```javascript
var a = 10;
var b = 3;
var sum = a + b;      // 13
var remainder = a % b; // 1
```

### 6.2 Comparison operators：比较运算符

| 运算符 | 作用 |
|---|---|
| `<` | 小于 |
| `>` | 大于 |
| `==` | 等于，允许类型转换 |
| `<=` | 小于等于 |
| `>=` | 大于等于 |
| `!=` | 不等于 |

例子：

```javascript
var myAge = 18;
var canDrive = myAge >= 17;
```

如果 `myAge` 是 18，那么 `canDrive` 的值是 `true`。

### 6.3 Logical operators：逻辑运算符

课件列了：

```javascript
&, |, ~, &&, ||, !
```

初学网页编程时最常用的是：

| 运算符 | 作用 |
|---|---|
| `&&` | 逻辑与，两个条件都真才真 |
| `||` | 逻辑或，有一个条件为真就真 |
| `!` | 逻辑非，取反 |

例子：

```javascript
var age = 20;
var hasLicense = true;

if (age >= 17 && hasLicense) {
  console.log("Can drive");
}
```

意思是：年龄至少 17，并且有驾照，才输出 `Can drive`。

---

## 7. JS Variables：变量

变量用来存储值。

课件中的写法：

```javascript
var myAge;
myAge = 35;
```

解释：

- `var myAge;`：声明变量。
- `myAge = 35;`：给变量赋值。

也可以合起来写：

```javascript
var myAge = 35;
```

### 7.1 变量像什么？

可以把变量理解为一个有名字的盒子：

```javascript
var myName = "Wang";
```

意思是有一个盒子叫 `myName`，里面放着字符串 `"Wang"`。

### 7.2 关于 `var` 的补充

课件使用的是 `var`，这是早期 JavaScript 常用的变量声明方式。

现代 JavaScript 更常用：

```javascript
let age = 20;
const name = "Wang";
```

简单区别：

- `let`：变量后面可以改。
- `const`：常量，声明后不应重新赋值。
- `var`：老写法，仍然能用，但作用域规则更容易让初学者混淆。

课程代码用 `var` 是为了基础教学，但你以后可以逐渐学习 `let` 和 `const`。

---

## 8. JS Comments：注释

JavaScript 注释不会被解释器执行，主要用于解释代码。

单行注释：

```javascript
// This is the beginning of the programme
// var y = 30;
```

解释：

- `//` 后面的内容是注释。
- `// var y = 30;` 不会真的声明变量，因为这一行被注释掉了。

注释的用途：

1. 解释代码为什么这样写。
2. 临时禁用某行代码。
3. 帮助别人或未来的自己理解程序。

---

## 9. JS Data Types：数据类型

JavaScript 是动态类型语言，同一个变量可以在不同时间存不同类型的值。

```javascript
var myValue;
myValue = 10;
myValue = "My Name";
```

这里 `myValue` 先是数字，后是字符串。

### 9.1 Numbers：数字

数字可以是整数，也可以是小数，也可以用科学计数法。

```javascript
60
100
56.89
569e7
567e-9
```

例子：

```javascript
var score = 95;
var temperature = 36.5;
```

### 9.2 Strings：字符串

字符串是文本，用单引号或双引号包起来。

```javascript
"my Name"
'Her Name'
"23"
"24.7"
```

注意：

```javascript
23
```

是数字。

```javascript
"23"
```

是字符串，因为它被引号包住了。

### 9.3 Arrays：数组

数组用来存一组值，用方括号 `[]` 表示。

```javascript
var myIntArray = [4, 8, 200, 50];
var myStringArray = ["Name", "StudID", "Degree"];
```

数组的 index 默认从 0 开始。

```javascript
myIntArray[0] = 4;
myStringArray[2] = "Degree";
```

解释：

| 表达式 | 结果 |
|---|---|
| `myIntArray[0]` | 第 1 个元素，值是 `4` |
| `myIntArray[1]` | 第 2 个元素，值是 `8` |
| `myStringArray[2]` | 第 3 个元素，值是 `"Degree"` |

> [!warning] 数组从 0 开始
> 初学者常错把第一个元素写成 `[1]`。在 JavaScript 中，第一个元素是 `[0]`。

### 9.4 Objects：对象

对象用来描述一个有多个属性的东西，用大括号 `{}` 表示。

课件例子：

```javascript
var student = {
  surName: "Wang",
  firstName: "Liu",
  age: 20
};
```

对象结构是 name-value pairs：

| 属性名 | 值 |
|---|---|
| `surName` | `"Wang"` |
| `firstName` | `"Liu"` |
| `age` | `20` |

访问对象属性：

```javascript
student.firstName
```

结果是：

```text
Liu
```

### 9.5 使用 `new` 创建对象

课件介绍了 `new` 关键字。

```javascript
var person = new Object();
person.firstName = "Wang";
person.lastName = "Zhang";
person.age = 18;
```

意思是：

1. 创建一个空对象 `person`。
2. 给它添加 `firstName` 属性。
3. 给它添加 `lastName` 属性。
4. 给它添加 `age` 属性。

然后可以写：

```javascript
document.getElementById("newExample").innerHTML =
  person.firstName + " is " + person.age + " years old.";
```

输出类似：

```text
Wang is 18 years old.
```

### 9.6 Boolean：布尔值

Boolean 只有两个值：

```javascript
true
false
```

例子：

```javascript
var myBooleanValue1 = true;
var myBooleanValue2 = false;
```

Boolean 常用于条件判断：

```javascript
var isLoggedIn = true;

if (isLoggedIn) {
  console.log("Welcome");
}
```

### 9.7 `typeof`：查看数据类型

`typeof` 可以查看一个值的数据类型。

```javascript
typeof 23;       // "number"
typeof "Wang";   // "string"
typeof false;    // "boolean"
```

它适合用来检查变量当前到底是什么类型。

---

## 10. DOM 操作：`getElementById()` 和 `innerHTML`

### 10.1 `document.getElementById()`

课件解释：`getElementById()` 会返回指定 id 对应的元素对象。

HTML：

```html
<p id="demo">Hello</p>
```

JavaScript：

```javascript
const myElement = document.getElementById("demo");
myElement.style.color = "red";
```

解释：

| 代码 | 解释 |
|---|---|
| `document` | 当前 HTML 文档。 |
| `.getElementById("demo")` | 找到 `id="demo"` 的元素。 |
| `const myElement = ...` | 把这个元素保存到变量 `myElement` 中。 |
| `myElement.style.color = "red";` | 把该元素文字颜色改成红色。 |

### 10.2 `innerHTML`

`innerHTML` 用来设置或读取一个元素内部的 HTML 内容。

```javascript
document.getElementById("demo").innerHTML = "Hello";
```

意思是：找到 `id="demo"` 的元素，并把它里面的内容改成 `Hello`。

例如原来是：

```html
<p id="demo"></p>
```

运行后页面变成：

```html
<p id="demo">Hello</p>
```

> [!important] `innerHTML` 的作用
> 它不是改 CSS，而是改元素里面的 HTML 内容。它常用于动态显示文字、结果、提示信息等。

---

## 11. Program Control：程序控制

程序控制就是让程序不只是从上到下执行，还能判断、循环、封装功能。

本讲包括：

- 条件语句。
- switch 语句。
- 循环语句。
- 函数。

---

## 12. Conditional Statements：条件语句

### 12.1 `if` 语句

结构：

```javascript
if (condition) {
  // execute the code here if the condition is true
}
```

意思是：如果条件为真，就执行大括号里的代码。

课件例子：

```javascript
if (myAge < 16) {
  driving = "I cannot drive!";
}
```

解释：如果 `myAge` 小于 16，就把 `driving` 设置成 `"I cannot drive!"`。

### 12.2 `if...else` 语句

```javascript
if (myAge < 16) {
  driving = "I cannot drive!";
} else {
  driving = "I can drive!";
}
```

意思是：

- 如果 `myAge < 16` 为真，执行第一块。
- 否则执行 `else` 里的代码。

可以理解为程序里的“如果……否则……”。

### 12.3 `switch` 语句

当一个表达式有多个可能值时，可以用 `switch`。

```javascript
switch (expression) {
  case 1:
    // code block
    break;
  case 2:
    // code block
    break;
  default:
    // default code block
}
```

解释：

| 代码 | 解释 |
|---|---|
| `switch (expression)` | 检查表达式的值。 |
| `case 1:` | 如果值是 1，执行这里。 |
| `break;` | 跳出 switch，避免继续执行下面的 case。 |
| `default:` | 如果没有任何 case 匹配，就执行默认代码。 |

例子：

```javascript
var day = 1;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  default:
    console.log("Other day");
}
```

---

## 13. Loop Statements：循环语句

循环用于重复执行代码。

### 13.1 `for` 循环

课件例子：

```javascript
for (i = 0; i < 5; i++) {
  myNumbers += "My number is " + i + "<br>";
}
```

逐行解释：

| 代码 | 解释 |
|---|---|
| `i = 0` | 循环开始前，设置计数器 i 为 0。 |
| `i < 5` | 只要 i 小于 5，就继续循环。 |
| `i++` | 每次循环结束后，i 增加 1。 |
| `myNumbers += ...` | 把新的文字追加到 `myNumbers` 里。 |
| `"<br>"` | HTML 换行标签，让每一行分开显示。 |

这个循环会执行 5 次，`i` 分别是：

```text
0, 1, 2, 3, 4
```

### 13.2 `while` 循环

结构：

```javascript
while (condition) {
  // Execute code block if condition is true
}
```

意思是：只要条件为真，就一直执行。

例子：

```javascript
var i = 0;

while (i < 5) {
  console.log(i);
  i++;
}
```

注意：while 循环一定要让条件最终变成 false，否则可能形成死循环。

---

## 14. JS Functions：函数

函数是一段可以重复调用的代码块，用来完成某个功能。

基本结构：

```javascript
function functionName(para1, para2) {
  return returnValue;
}
```

解释：

| 部分 | 意思 |
|---|---|
| `function` | 声明函数的关键字。 |
| `functionName` | 函数名。 |
| `para1, para2` | 参数，可以没有，也可以有多个。 |
| `return` | 返回结果。 |
| `returnValue` | 函数调用后得到的值。 |

课件例子：

```javascript
var mySum = myAddFunction(4, 3);

function myAddFunction(a, b) {
  return a + b;
}
```

解释：

1. `myAddFunction(4, 3)` 调用函数。
2. `a` 收到 `4`。
3. `b` 收到 `3`。
4. `return a + b;` 返回 `7`。
5. `mySum` 最终得到 `7`。

函数的意义：

- 避免重复代码。
- 把复杂程序拆成小块。
- 让代码更清晰、更容易调试。

---

## 15. Event Listener：事件监听器

事件监听器是 JavaScript 做交互的核心。

### 15.1 什么是事件？

事件就是用户或浏览器发生的动作，例如：

- 鼠标按下 `mousedown`。
- 鼠标移动 `mousemove`。
- 鼠标松开 `mouseup`。
- 点击 `click`。
- 键盘按下 `keydown`。
- 页面加载完成 `load`。

### 15.2 什么是 event listener？

Event listener 可以理解为：

> 让 JavaScript 监听某个动作，一旦这个动作发生，就执行某个函数。

基本写法：

```javascript
element.addEventListener("eventName", functionName, false);
```

例如：

```javascript
apple.addEventListener("mousedown", initialClick, false);
```

意思是：当用户在 `apple` 这个元素上按下鼠标时，执行 `initialClick` 函数。

---

## 16. 拖拽图片示例

课件用一个苹果图片演示如何拖拽元素。

### 16.1 Step 1：添加图片

第一步是先把图片放到页面中。

课件思路类似：

```html
<div id="apple" style="top:100px; left:100px;"></div>
```

然后用 CSS 给它设置图片背景：

```css
#apple {
  width: 100px;
  height: 100px;
  position: absolute;
  background-image: url(images/apple.png);
  background-size: contain;
}
```

解释：

- `width` / `height` 设置盒子大小。
- `position: absolute` 让图片可以通过 `top` 和 `left` 定位。
- `background-image` 设置苹果图片。
- `background-size: contain` 让图片完整显示在盒子里。

### 16.2 Step 2：鼠标按下后开始拖拽

课件代码的核心是：

```javascript
var apple = document.getElementById("apple");
apple.addEventListener("mousedown", initialClick, false);

function initialClick(e) {
  image = this;
  document.addEventListener("mousemove", move, false);
}

function move(e) {
  var newX = e.clientX - 10;
  var newY = e.clientY - 10;
  image.style.left = newX + "px";
  image.style.top = newY + "px";
}
```

逐行解释：

| 代码 | 解释 |
|---|---|
| `var apple = document.getElementById("apple");` | 找到页面中 `id="apple"` 的元素。 |
| `apple.addEventListener("mousedown", initialClick, false);` | 给苹果添加鼠标按下事件。按下时执行 `initialClick`。 |
| `function initialClick(e) { ... }` | 定义鼠标按下后要执行的函数。 |
| `image = this;` | `this` 指当前被按下的元素，也就是苹果。把它保存到 `image`。 |
| `document.addEventListener("mousemove", move, false);` | 开始监听鼠标移动。鼠标一动就执行 `move`。 |
| `function move(e) { ... }` | 定义鼠标移动时要执行的函数。 |
| `e.clientX` | 鼠标当前相对于浏览器窗口左侧的 x 坐标。 |
| `e.clientY` | 鼠标当前相对于浏览器窗口顶部的 y 坐标。 |
| `image.style.left = newX + "px";` | 改变图片左侧位置。 |
| `image.style.top = newY + "px";` | 改变图片顶部位置。 |

这一步的问题是：图片会一直粘着鼠标，因为还没有停止监听 `mousemove`。

### 16.3 Step 3：鼠标松开后停止拖拽

课件接着加入 `mouseup`：

```javascript
apple.addEventListener("mouseup", releaseClick, false);

function releaseClick(e) {
  document.removeEventListener("mousemove", move);
}
```

解释：

- `mouseup` 表示鼠标松开。
- 松开后执行 `releaseClick`。
- `removeEventListener("mousemove", move)` 会取消鼠标移动监听。
- 取消后，图片就不会继续跟着鼠标移动。

### 16.4 Step 4：拖拽多个图片

如果页面有多个苹果：

```html
<div id="apple1"></div>
<div id="apple2"></div>
```

就需要分别获取它们，并分别添加事件监听：

```javascript
var apple1 = document.getElementById("apple1");
var apple2 = document.getElementById("apple2");

apple1.addEventListener("mousedown", initialClick, false);
apple1.addEventListener("mouseup", releaseClick, false);

apple2.addEventListener("mousedown", initialClick, false);
apple2.addEventListener("mouseup", releaseClick, false);
```

关键是 `image = this;`，它能让程序知道当前拖的是哪一个元素。

---

## 17. DIY Jigsaw Game：拼图游戏思路

课件提出 DIY 拼图游戏：把分散的图片碎片拖动组合成完整图片。

它本质上就是前面拖拽图片技术的扩展：

1. 准备多张图片碎片。
2. 每张碎片都是一个可拖动元素。
3. 给每个碎片添加 `mousedown`、`mousemove`、`mouseup` 相关事件。
4. 用户拖动碎片到正确位置。
5. 可以进一步判断是否拼对。

### 17.1 图片素材注意事项

课件强调：透明背景图片更适合重叠和拼图。

原因：

- 非透明背景会带白色方块，看起来不自然。
- 透明 PNG 更容易叠放在其他图片上。
- 做拼图、贴纸、拖拽物体时更美观。

搜索图片时也要注意版权，尽量使用 royalty-free 或课程提供素材。

---

## 18. A Simple Clock：简单时钟应用

后半部分课件讲一个简单时钟，用到：

- HTML Canvas。
- JavaScript 绘图。
- Date 对象获取时间。
- `setInterval()` 定时刷新。

### 18.1 Canvas 是什么？

Canvas 是 HTML5 提供的画布，可以用 JavaScript 在上面画图形。

```html
<canvas id="canvas" width="400" height="400"></canvas>
```

JavaScript 获取 canvas：

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");
```

解释：

- `canvas` 是画布元素。
- `ctx` 是 2D 绘图上下文，可以理解为“画笔”。

### 18.2 Step 1：画钟面

课件说需要：

- 一个黑色 canvas box。
- 一个白色圆。
- 中心一个黑点。

常见画法：

```javascript
ctx.beginPath();
ctx.arc(200, 200, 180, 0, 2 * Math.PI);
ctx.fillStyle = "white";
ctx.fill();

ctx.beginPath();
ctx.arc(200, 200, 5, 0, 2 * Math.PI);
ctx.fillStyle = "black";
ctx.fill();
```

解释：

| 代码 | 解释 |
|---|---|
| `ctx.beginPath();` | 开始一条新路径。 |
| `ctx.arc(200, 200, 180, 0, 2 * Math.PI);` | 画一个圆，圆心 `(200, 200)`，半径 `180`。 |
| `ctx.fillStyle = "white";` | 填充颜色设置成白色。 |
| `ctx.fill();` | 填充这个圆。 |
| 第二个 `arc` | 画中心小圆点。 |

### 18.3 Step 2：画数字

课件说：旋转 Canvas 画笔到指定角度，画数字，然后恢复状态。用循环重复这个过程。

基本思路：

```javascript
for (var num = 1; num < 13; num++) {
  var ang = num * Math.PI / 6;
  ctx.rotate(ang);
  ctx.translate(0, -radius * 0.85);
  ctx.rotate(-ang);
  ctx.fillText(num.toString(), 0, 0);
  ctx.rotate(ang);
  ctx.translate(0, radius * 0.85);
  ctx.rotate(-ang);
}
```

这段看起来复杂，但核心逻辑是：

1. 一圈是 360 度，也就是 `2 * Math.PI` 弧度。
2. 时钟有 12 个数字，所以每个数字间隔 30 度。
3. 用 `rotate()` 把画笔转到对应方向。
4. 用 `translate()` 移动到数字应该出现的位置。
5. 用 `fillText()` 写数字。
6. 再把画布状态转回去。

### 18.4 Step 3：画时间

课件说画时间步骤：

1. 获取当前时间。
2. 用数学公式计算时针、分针、秒针角度。
3. 画出指针。

获取时间：

```javascript
var now = new Date();
var hour = now.getHours();
var minute = now.getMinutes();
var second = now.getSeconds();
```

解释：

- `new Date()` 创建当前时间对象。
- `getHours()` 获取小时。
- `getMinutes()` 获取分钟。
- `getSeconds()` 获取秒。

指针本质上就是从中心点画到某个方向的一条线。

### 18.5 Step 4：刷新时间

课件最后说：每 1000 ms 重新画一次整个时钟。

```javascript
setInterval(drawClock, 1000);
```

解释：

- `setInterval` 会重复调用函数。
- `drawClock` 是要重复执行的函数。
- `1000` 表示 1000 毫秒，也就是 1 秒。

所以每一秒重新绘制一次，时钟就会动起来。

> [!important] 为什么要重画整个时钟？
> Canvas 画上去的图形不像 DOM 元素那样可以单独更新。通常做动画时，会清空画布，然后重新画背景、数字和指针。

---

## 19. Vanilla JavaScript：原生 JavaScript

课件最后强调 Vanilla JavaScript。

### 19.1 什么是 Vanilla JavaScript？

Vanilla JavaScript 指的是：

> 不使用 React、jQuery、Vue、Angular 等外部库或框架，直接使用浏览器原生 JavaScript。

例如：

```javascript
document.getElementById("demo").innerHTML = "Hello";
```

这就是原生 JavaScript。

### 19.2 为什么要学原生 JavaScript？

课件列出好处：

- **Lightweight**：没有额外依赖，加载更快。
- **Zero setup**：浏览器直接运行，不需要复杂工具链。
- **Good for learning**：有助于理解基础。
- **Sufficient for many small projects**：很多小项目不需要复杂框架。

### 19.3 长期职业现实

课件强调：框架会变化，但 JavaScript 基础不会很快过时。

只会框架但不懂原生基础的人，在这些场景容易遇到困难：

- 框架更新或变化。
- 调试底层问题。
- 跨生态迁移。
- 做性能敏感项目。

理解 vanilla fundamentals 的人可以：

- 更快学习新框架。
- 更深入地调试问题。
- 更容易适应变化。
- 写出更清晰的架构。

课件最后的观点很直接：

> “I know React but not JavaScript” 并不值得骄傲。很多面试依然会考察原生 JavaScript 概念。

---

## 20. 本讲重点总结

### 20.1 必须掌握

- JavaScript 是网页行为层，用来实现交互和逻辑。
- JavaScript 可以写在 `<script>` 标签中。
- 表达式 expression 是计算片段，语句 statement 是完整命令。
- `=` 是赋值，不是相等判断。
- 变量可以用 `var` 声明，现代 JS 也常用 `let` 和 `const`。
- 常见数据类型包括 number、string、array、object、boolean。
- 数组 index 从 0 开始。
- 对象用 `{}`，内部是 name-value pairs。
- `typeof` 可以查看数据类型。
- `getElementById()` 用 id 找 DOM 元素。
- `innerHTML` 可以修改元素内部内容。
- `if` / `else` / `switch` 用于条件判断。
- `for` / `while` 用于循环。
- function 用来封装可重复使用的代码。
- event listener 用来响应用户事件。
- Canvas 可以用 JavaScript 绘图。
- `setInterval()` 可以定时重复执行函数。
- Vanilla JavaScript 是不依赖框架的原生 JavaScript。

### 20.2 常见易错点

1. 把 JavaScript 和 Java 混为一谈。
2. 忘记 `<script>` 标签闭合。
3. 在元素还没加载出来前就调用 `getElementById()`。
4. 把 `=` 当成相等判断。
5. 忘记字符串要加引号。
6. 数组下标从 0 开始，不是从 1 开始。
7. 忘记 `break`，导致 `switch` 继续执行后面的 case。
8. while 循环条件永远为 true，造成死循环。
9. 拖拽时只添加 `mousemove`，忘记在 `mouseup` 后移除。
10. Canvas 动画中忘记清空和重画画布。
11. 只学框架，不理解 JavaScript 基础。

---

## 21. 推荐记忆模板

### 21.1 HTML 中写 JavaScript

```html
<p id="demo"></p>

<script>
  document.getElementById("demo").innerHTML = "Hello JavaScript";
</script>
```

### 21.2 变量和数据类型

```javascript
var age = 20;
var name = "Wang";
var scores = [80, 90, 100];
var student = {
  firstName: "Liu",
  age: 20
};
var passed = true;
```

### 21.3 条件语句

```javascript
if (age >= 18) {
  console.log("Adult");
} else {
  console.log("Not adult");
}
```

### 21.4 for 循环

```javascript
for (var i = 0; i < 5; i++) {
  console.log(i);
}
```

### 21.5 函数

```javascript
function add(a, b) {
  return a + b;
}

var result = add(4, 3);
```

### 21.6 事件监听器

```javascript
var button = document.getElementById("myButton");

button.addEventListener("click", function () {
  alert("Button clicked");
});
```

### 21.7 定时器

```javascript
setInterval(function () {
  console.log("One second passed");
}, 1000);
```

---

## 22. 如果要复习考试，优先看这些

1. 解释 JavaScript 在 website layers 中负责什么。
2. 写出 `<script>` 的基本用法。
3. 区分 expression 和 statement。
4. 解释 variable declaration 和 assignment。
5. 识别 arithmetic、comparison、logical operators。
6. 区分 number、string、array、object、boolean。
7. 解释数组为什么第一个元素是 `[0]`。
8. 用 `typeof` 判断数据类型。
9. 用 `getElementById()` 找元素，用 `innerHTML` 改内容。
10. 写出 `if...else` 和 `switch` 的基本结构。
11. 写出 `for` 和 `while` 循环。
12. 写出一个简单 function，并说明参数和 return。
13. 解释 event listener 的作用。
14. 解释拖拽图片为什么需要 `mousedown`、`mousemove`、`mouseup`。
15. 解释 Canvas 时钟为什么要用 `setInterval()` 每秒刷新。
16. 解释为什么要学习 Vanilla JavaScript。

---

## 23. 一句话结尾

Lecture 3 的重点是从“静态网页”走向“可交互网页”：JavaScript 让 HTML 元素可以被找到、被修改、被拖动、被定时刷新，也让网页能够根据条件和用户操作运行逻辑。掌握这些原生基础，以后学习任何前端框架都会更容易。

# Unit 1 - Lecture 4: Production and Management 讲解

> [!info] 来源
> 本部分讲解的是 EBU6305 Interactive Media Design and Production 的 **Lecture 4: Production and Management**，原课件见：[[附件/Unit 1 - Coding & Development/Lecture 4. Production and Management.pdf|Lecture 4. Production and Management.pdf]]。

## 1. 这一讲整体在讲什么？

这一讲不再讲“怎么写某个标签或函数”，而是讲“一个真实项目怎么做出来”。重点是如何把设计、实现和管理放在一起看，如何用 Agile 方式迭代开发，如何用 Git/GitHub 做版本控制和协作，以及如何把 GitHub 当成团队协作平台和个人作品集。

这一讲的学习目标可以理解为：

- 管理设计过程，并能评价最终结果。
- 反思自己的开发进度，知道项目做到哪一步了。
- 熟悉行业中常见的生产管理方法，例如 Agile、version control 和 collaborative coding。

---

## 2. Production Process：最终产品由哪三部分组成？

课件把最终产品拆成三块：

| 部分 | 关注点 | 例子 |
| --- | --- | --- |
| Design | 可用性、视觉效果 | 界面是否好用、是否好看 |
| Implementation | 编程、测试 | 代码是否能运行、有没有 bug |
| Project Management | Agile、Version Control | 任务如何分配、版本如何保存 |

意思是：一个项目不是“代码写完就结束”，而是设计、实现、管理缺一不可。

从课件的图示来看，项目开发常常不是一条直线，而是会在主线之外出现分支，再合并回去；这也正好对应后面讲的 branch 和 merge。

---

## 3. 传统瀑布式开发：为什么不够灵活？

瀑布模型是按阶段一路往下走：

- 先做分析和设计。
- 再实现。
- 再测试。
- 最后交付。

它的优点是清楚、直观，常配合 Gantt chart 做时间规划；缺点是如果后面才发现问题，回头修改会很贵。

| Waterfall | Agile |
| --- | --- |
| 一条线往下走 | 一小段一小段推进 |
| 前期计划很重 | 允许不断调整 |
| 后期改动成本高 | 每轮都能修正 |

---

## 4. Unified Process / Agile：核心就是迭代和增量

课件强调：商业项目往往会持续很多个月甚至几年，所以不要一口气做完，而要拆成多个 iteration / sprint。

每一轮迭代通常都做三件事：

1. 找出这一轮要实现的 use cases。
2. 做设计。
3. 实现并检查结果。

所以敏捷的思路不是“慢慢拖”，而是：

> 先做一个能工作的简单版本，再一轮一轮变好。

---

## 5. Kanban、Scrum 和 Trello

课件提到：

- 定期开 scrum meeting，快速同步进度。
- 用 Kanban 把任务可视化。
- 推荐工具是 Trello。
- Kanban 不只适合软件，也能拿来安排生日派对。

最重要的提醒是：不要一开始就把目标定得太大。第一版不用完美，先做出“粗糙但能用”的版本，再在后面的 sprint 里打磨。

---

## 6. Agile 的好处

Agile 的优势主要体现在：

- 很快就能得到一个可运行的产品。
- 任务可以随时重分配、更新。
- 每天或每轮都能检查进度。
- 通常比一开始设想的截止日期更早完成。

课件里的 labs 也被当成 4 个 sprint 来看：

```text
Lab 1 -> Version 1
Lab 2 -> Version 2
Lab 3 -> Version 3
Lab 4 -> Version 4
```

意思就是：每次实验都给项目加一个可见进展。

---

## 7. Version Control：为什么必须用？

版本控制的作用不是“高级”，而是“救命”：

- 记录代码历史。
- 出错时可以回退。
- 避免人手误操作把整个项目弄坏。
- 方便多人协作。

课件推荐 GitHub，因为它是成熟的 Git 托管平台之一。

> [!tip] 先把概念分清
> Git 是版本控制工具；GitHub 是基于 Git 的托管和协作平台。

---

## 8. Git / GitHub 术语

| 术语 | 含义 |
| --- | --- |
| repository | 一个项目仓库，像项目文件夹 |
| clone | 把仓库复制到本地电脑 |
| remote | 放在服务器上的远端仓库 |
| commit | 把一组改动保存成一次历史记录 |
| push | 把本地提交送到远端 |
| pull | 把远端更新拉下来并合并 |
| fetch | 只获取更新，不自动合并 |
| fork | 复制别人的仓库到自己账号 |
| pull request | 提交“请合并我的改动”的请求 |

### 最容易混淆的几个词

> [!tip]
> - commit = 本地保存一次版本。
> - push = 发到远端。
> - pull = 拉取并合并。
> - fetch = 只拉不合。
> - fork = 复制别人的仓库。
> - pull request = 请求对方把你的改动并进来。

---

## 9. Git 命令图在讲什么？

图里有四个区域：

- **workspace**：你正在编辑的文件。
- **index / staging area**：准备提交的暂存区。
- **local repository**：本地历史记录。
- **remote repository**：GitHub 上的远端仓库。

常见流程就是：

```text
add -> commit -> push
```

反过来是：

```text
fetch / pull -> update local copy
```

课件还特别提到，`index` 就是提交前先放文件的地方，像一个“待提交草稿区”。图里也出现了 `checkout` 和 `revert`，可以理解为切换版本或撤回修改。

> [!note] 复习时重点理解
> 不一定要背下所有 Git 命令，但要知道每个命令大概在 workspace、index、local repository 和 remote repository 之间移动什么东西。

---

## 10. Compare Code：为什么有用？

GitHub 可以把两个版本并排比较，直接看到哪几行改了。

这对下面几件事很有帮助：

- code review：别人可以检查你的改动。
- 找 bug：看到问题是从哪个版本开始出现的。
- 看历史：知道某段代码是谁、什么时候改的。
- 检查是否抄袭：课件提到 compare code 对 plagiarism checking 有帮助。

---

## 11. Collaborative Coding：两个经典流程

### 11.1 例 1：你想改别人的项目

如果 Joe 做了一个游戏，你想帮他改进，流程是：

1. **fork** 对方仓库：先把他的仓库复制到你的 GitHub 账号。
2. **clone** 到本地：把你账号里的仓库下载到电脑。
3. 修改文件：用你喜欢的编辑器改代码。
4. **commit**：在本地记录这次改动。
5. **push**：把本地提交发回你的 GitHub 仓库。
6. 发 **pull request**：请求 Joe 把你的改动合并进他的项目。

关键点：你不能直接改别人的原仓库，所以先 fork，再通过 pull request 请求对方接受你的修改。

### 11.2 例 2：别人改了你的项目

如果 Joe 反过来给你的项目做了改动，你想把他的修改拿进来，流程是：

1. **fetch** 对方的新改动。
2. **merge** 到自己的分支或仓库。
3. **push** 回远端，让 GitHub 上的版本也更新。

课件也说明，fetch 和 merge 经常被合并成一个操作，叫 **pull**。

---

## 12. Collaborator、Contributor、Branch 和 Merge

GitHub 上的人可以分成两类：

| 身份 | 含义 |
| --- | --- |
| collaborator | 被项目所有者邀请进来的核心团队成员，有读写权限 |
| contributor | 通过 pull request 贡献过代码的人，但不一定有直接写权限 |

branch 是并行版本，适合做新功能或实验；merge 是把一个分支的改动合并到另一个分支。

课件特别强调：**merge conflict 不是失败，而是多人同时改了同一部分代码的信号。**

---

## 13. 分支和合并策略

常见分支包括：

- **main branch**：稳定、可发布的版本。
- **feature branch**：开发某一个功能。
- **hotfix branch**：修紧急 bug。
- **develop branch**：有些团队会把它作为测试整合分支。

合并方式包括：

| 合并方式 | 特点 |
| --- | --- |
| Direct merge | 直接合并，速度快，但容易把未审核代码放进去 |
| Pull request merge | 先提交请求、讨论、审核，再合并，更适合质量控制 |

课件还提到较高级的方式，比如 squash merge、rebase and merge，但这门课不要求展开。

---

## 14. Pull Request、Issues 和 GitHub Kanban

Pull request 本身就是一个质量关卡，里面通常包含：

- 代码说明。
- 代码差异。
- 讨论区。
- 审核意见。
- 是否合并的决定。

它的质量控制作用包括：

- peer review。
- 记录为什么改代码。
- 明确谁负责这次改动。
- 避免不稳定代码直接进入主分支。
- 让项目历史可追踪。

Issues 则像任务单或讨论单，可以提改进、问问题、记 bug。GitHub 的 Project 标签页还能做 Kanban board，用来管理任务状态。

---

## 15. 学生账号和课程管理

课件要求学生注册 GitHub 账号，并申请 Student Developer Pack。对课程作业来说，推荐流程是：

```text
开发 -> 上传当前版本 -> 在 Kanban 上安排任务 -> 更新进度 -> 进入下一轮 sprint
```

也就是说，作业不是最后一天才交，而是边做边记录。这样老师或队友可以看到你每个阶段做了什么，也方便你自己回顾进度。

---

## 16. GitHub 不只是代码托管

课件最后强调，GitHub 还是一个全球开放平台：

- 能分享项目和知识。
- 可以像数字图书馆一样搜索源码。
- 能学习真实项目中的写法。
- 也能作为个人作品集。

看一个 GitHub 主页时，别人常会关注：

- 仓库数量。
- 项目复杂度。
- stars / forks。
- contribution history。
- 文档质量。
- 合作痕迹。

所以 GitHub 不只是“放代码的网站”，也是展示能力和学习行业实践的地方。

---

## 17. 如果要复习考试，优先看这些

1. 解释 Waterfall 和 Agile 的区别。
2. 解释 iteration / sprint 的作用。
3. 解释 Kanban 如何帮助项目管理。
4. 区分 Git 和 GitHub。
5. 解释 repository、clone、remote、commit、push、pull、fetch、fork、pull request。
6. 画出或解释 workspace、index、local repository、remote repository 的关系。
7. 解释 commit、push、pull request 的区别。
8. 解释 fetch、pull、fork 的区别。
9. 解释 collaborator 和 contributor 的区别。
10. 解释 branch、merge 和 merge conflict。
11. 说明为什么 pull request 是 quality gate。
12. 说明 issues 和 GitHub Project/Kanban 的作用。
13. 说明为什么 GitHub 可以作为开源平台、数字图书馆和个人作品集。

---

## 18. 一句话结尾

Lecture 4 的重点，是把“会写代码”推进到“会做项目”：你不只要让程序跑起来，还要让它能被管理、被协作、被迭代、被交付。

# Unit 1 - Lecture 5: AI-Led Development 讲解

> [!info] 来源
> 本部分讲解的是 EBU6305 Interactive Media Design and Production 的 **Lecture 5: AI-Led Development**，原课件见：[[附件/Unit 1 - Coding & Development/Lecture 5. AI-Led Development.pdf|Lecture 5. AI-Led Development.pdf]]。

## 1. 这一讲整体在讲什么？

Lecture 5 讲的是 **AI-Led Development**，也就是“由 AI 参与主导的开发流程”。它不是简单地说“让 AI 帮你写代码”，而是强调：在交互式媒体设计和网页开发中，学生要学会把 AI 放进完整的设计、实现、测试和反思流程里。

这一讲的学习目标包括：

- 熟悉用 AI 写代码时的要求和期望。
- 理解行业里 AI 赋能软件开发的趋势。
- 形成一种程序化习惯：会用 AI 帮助网页媒体设计，但同时能检查、判断和改进 AI 的输出。

一句话概括：

> AI 可以帮你生成内容、设计和代码，但最终负责判断质量、伦理、可用性和设计方向的人仍然是你。

---

## 2. 本讲的三个主题

课件把 Lecture 5 分成三个大主题：

1. **AI-Led Development Lifecycle**：AI 主导开发生命周期。
2. **AI Skillsets**：使用 AI 做开发需要的能力。
3. **Reflective Learning**：反思式学习，尤其是 coursework 里的 AI log。

这三个主题的关系是：

```text
AI 参与开发流程 -> 学生需要新的 AI 技能 -> 用 AI log 证明自己真的在思考
```

---

## 3. AI Driving License：什么是 AI 能力？

课件提出了类似 **AI Driving License** 的概念，可以理解为“AI 驾照”：

> 不是只会打开 AI 工具，而是能在学习或工作中负责任、有效地使用 AI。

它包含三层能力：

| 层级 | 含义 |
| --- | --- |
| AI Literacy | AI 基础素养，知道 AI 是什么，能让 AI 解释概念、给例子 |
| AI Competency | AI 应用能力，能用 AI 生成具体产物，例如代码、UI、布局 |
| AI for Problem-Solving | AI 问题解决能力，能用 AI 分析问题、比较方案、迭代改进 |

课件强调，高级 AI 能力还包括：分析复杂挑战、设计 AI 支持的解决方案，并能在不同领域创新。

---

## 4. 未来的软件开发技能正在变化

课件提到 Stanford 有软件开发课程要求学生不要手写代码，而是使用 AI 完成开发。这说明软件开发的能力重点正在变化。

传统观念里，开发者的核心能力是：

- 会不会写代码。
- 会不会记语法。
- 能不能手动实现功能。

AI 时代更强调：

- 能不能清楚描述问题。
- 能不能判断 AI 输出是否正确。
- 能不能进行设计思考。
- 能不能把 AI 产物整合进真实项目。

所以课程鼓励你尝试减少手动编码，但不是让你“偷懒”，而是让你练习如何把 AI 当成开发伙伴。

---

## 5. AI-Led Design & Development：和传统开发有什么区别？

课件对比了两种模式。

### 5.1 传统模式

```text
Human -> Design -> Code -> Test -> Iterate
```

意思是：人先设计，再写代码，再测试，再迭代。AI 如果出现，只是 helper。

### 5.2 AI-Led 模式

```text
AI -> Proposal -> Human critique -> AI revision -> Human decision
```

意思是：AI 先提出方案，人类批判性评价，然后让 AI 修改，最后由人类做决定。

重点不是“AI 替代人”，而是：

> AI 负责快速生成可能方案，人负责判断方向和质量。

---

## 6. 行业里的 AI 软件开发流程

课件展示了 AI 在软件开发生命周期中的常见用途：

1. AI 分析问题需求。
2. AI 帮助预测用户遇到问题之前可能发生的风险。
3. AI 生成代码，再由人类编辑。
4. AI 判断哪些内容值得测试，而不是盲目测试所有东西。
5. AI 持续扫描漏洞，辅助处理安全威胁。
6. AI 用于 IT 运维，也就是 AIOps。
7. AI 在真实运行系统中检测 bug、自动扩展和优化。

也就是说，AI 不只出现在“写代码”阶段，而是可以贯穿需求、设计、测试、安全、运维等多个环节。

---

## 7. Coursework 里的简化版 AI 开发流程

课程把复杂行业流程简化成 5 个阶段：

| 阶段 | 英文名称 | 中文理解 |
| --- | --- | --- |
| Step 1 | AI-Initiated Problem Framing | AI 帮助定义问题 |
| Step 2 | AI-Generated Design Artefacts | AI 生成设计产物 |
| Step 3 | AI-Written Implementation | AI 写 HTML/CSS/JS |
| Step 4 | AI-Led Testing and Evaluation | AI 帮助测试和评价 |
| Step 5 | Iterative Refinement for Agile | AI 帮助敏捷迭代改进 |

这五步可以理解为一个循环：

```text
定义问题 -> 生成设计 -> 写代码 -> 测试评价 -> 继续改进
```

---

## 8. Stage 1：AI-Initiated Problem Framing

第一阶段是让 AI 帮你进行问题框定。

AI 可以产出：

- 用户需求。
- 目标用户画像。
- 使用场景假设。

但学生的责任是检查这些内容：

- 这些假设是否符合 usability theory？
- 有没有遗漏重要用户？
- 用户画像是否带有偏见？
- 使用场景是否不现实？

课件的核心提醒是：

> AI 很擅长生成“看起来合理”的需求，但看起来合理不等于正确。

比如 AI 可能会默认用户都熟悉电脑、都能看清屏幕、都使用高速网络，这些假设就需要你检查。

---

## 9. Stage 2：AI-Generated Design Artefacts

第二阶段是让 AI 生成设计产物。

AI 可以产出：

- wireframes：线框图。
- UI component lists：界面组件列表。
- navigation structure：导航结构。
- user flows / use cases：用户流程和用例。

学生需要用设计原则评价这些产物，例如：

- **Simplicity**：是否简单？
- **Structure**：结构是否清楚？
- **Consistency**：是否一致？
- **Tolerance**：是否允许用户犯错并恢复？

课件强调：

> Visual plausibility 不等于 good user experience。

也就是说，一个界面看起来像真的，不代表它真的好用。

---

## 10. Stage 3：AI-Written Implementation

第三阶段是让 AI 写具体实现，也就是 HTML、CSS 和 JavaScript。

AI 可以产出：

- 完整前端代码。
- 样式。
- 交互逻辑。

学生要评价：

- HTML 结构是否语义化？
- 是否有 accessibility 问题？
- 页面是否 responsive？
- 代码是否容易维护？

课件的核心提醒是：

> Correct code is not necessarily good code.

意思是：代码能运行，不代表代码质量好。比如：

- 全部用 `<div>`，没有语义化标签。
- 没有 label，屏幕阅读器不好读。
- 手机端布局崩掉。
- JavaScript 写得很乱，后期难维护。

这些都需要人来判断。

---

## 11. Stage 4：AI-Led Testing and Evaluation

第四阶段是让 AI 帮你提出测试和评价方法。

AI 可以提出：

- test cases：测试用例。
- heuristic evaluation：启发式评价。
- usability metrics：可用性指标。

学生要检查：

- 指标是否符合 ISO usability goals？
- 测试是否反映真实用户行为？
- 是否忽略了 edge cases？

课件提醒：

> AI often tests what is easy, not what is important.

AI 可能会测试最显眼、最简单的情况，但忽略真正重要的边界情况。例如：

- 用户输入空内容。
- 用户使用键盘而不是鼠标。
- 用户在小屏幕手机上操作。
- 用户输入特殊字符。
- 网络慢或资源加载失败。

---

## 12. Stage 5：Iterative Refinement for Agile

第五阶段是迭代改进。

AI 可以建议：

- 改进方向。
- 新功能。
- 设计优化。

但学生必须决定：

- 哪些接受？
- 哪些拒绝？
- 哪些需要重新定义？

课件说：

> Iteration without judgment is just noise.

意思是：如果你只是不断让 AI 改，但没有判断标准，项目只会越来越乱。敏捷迭代不是“随便多改几次”，而是每一次修改都有明确理由。

---

## 13. AI Skillsets：为什么专家和初学者用 AI 的方式不同？

课件用图片说明：

- Beginners use AI for routine tasks。
- Experts use AI to achieve precise, high-value outcomes。

初学者常用 AI 做简单任务，例如解释概念、生成一段代码、翻译文字。专家则会让 AI 达成更精确、更高价值的结果，例如设计一套符合用户需求、可访问性和技术限制的完整方案。

这里的关键问题是：

> Can you control AI to do exactly what you want?

如果你不能控制 AI，它可能会生成“看起来不错但不符合你目标”的东西。

---

## 14. 两个核心技能

课件把 AI-led development 的核心技能分成两类：

1. **AI Prompt Engineering**
2. **Design-Centred Critical Evaluation**

它们之间是循环关系：

```text
更好的 prompt -> 更好的 AI 输出 -> 更好的评价 -> 继续改进 prompt
```

只会 prompt 不会评价，会变成盲目接受 AI。只会评价不会 prompt，又很难让 AI 产出你想要的东西。

---

## 15. Skillset 1：AI Prompt Engineering

课件问了一个重要问题：为什么叫 **Prompt Engineering**，而不是 **Prompt Writing**？

因为 engineering 暗示：

- design：设计。
- structure：结构。
- optimisation：优化。
- iteration：迭代。

简单 prompt writing 可能只是：

```text
Summarise this article.
```

而 prompt engineering 会写成：

```text
Summarise this article for a policymaker who has only 30 seconds to read it.
```

后者更好，因为它说明了：

- 目标读者是谁。
- 输出要多简短。
- 输出要服务什么决策场景。

课件还说，很多研究者把 prompt 看作 AI 的高层编程接口：你不是写给电脑执行的代码，而是写给 AI 模型理解的指令。

---

## 16. Prompt Engineering 包含什么？

Prompt engineering 不只是“把话说清楚”，还包括：

- 知道什么任务可以交给 AI。
- 知道什么时候应该停止 AI。
- 知道什么时候要重新限定任务范围。
- 给 AI 设计约束，而不是只给任务。

例如：

```text
Generate a wireframe.
```

这是弱提示，因为太模糊。

更好的提示是：

```text
Generate a wireframe for first-time users aged 18–25, prioritising efficiency over discoverability, following minimalism principles.
```

这个提示更强，因为它给出了：

- 目标用户。
- 设计优先级。
- 设计原则。

课件把这看作一种 R&D skill，也就是设计和研究能力。

---

## 17. 什么是复杂问题？

课件引用 IET 的定义，大意是：复杂问题没有显而易见的解决方案，而且会涉及广泛或冲突的技术问题和用户需求，需要创造性地应用工程知识，而不是套用简单公式。

在交互式媒体设计中，复杂问题常常表现为：

- 用户需求互相冲突。
- 视觉效果和可用性冲突。
- 功能复杂度和开发时间冲突。
- 桌面端和移动端需求不同。
- 可访问性、安全性、商业目标同时存在。

Prompt engineering 的作用，就是把这些模糊需求翻译成 AI 能处理的结构化上下文和约束。

---

## 18. 高质量 Prompt 模板

课件给出一个 high-quality prompt engineering template。可以理解为写 prompt 时要尽量说明这些部分：

| 部分 | 要回答的问题 |
| --- | --- |
| Task Goal and Purpose | 这个页面或系统要做什么？解决什么问题？ |
| User and Context | 目标用户是谁？在哪些设备或环境使用？ |
| Functional Requirements | 必须支持哪些功能或操作？ |
| Interaction and Behaviour | 用户操作后系统如何响应？有什么交互规则？ |
| UI and Layout Constraints | 布局、视觉结构、响应式有什么要求？ |
| Accessibility and Usability | 可访问性、可用性、容错性有什么要求？ |
| Technical Constraints | 必须用或不能用哪些技术？ |
| Quality and Design Principles | 一致性、清晰度等质量要求是什么？ |
| Deliverables and Output Format | 最终要输出哪些文件或内容？ |
| Evaluation or Verification | 如何检查结果是否正确？ |

这个表非常适合直接用于 coursework。你让 AI 写代码前，可以先照着表补全需求。

---

## 19. 示例 1：活动预约界面 Prompt

课件给的复杂问题是：设计一个单页活动预约界面，能在手机和桌面端使用，能防止常见输入错误，并支持键盘操作。

高质量 prompt 里包含了很多具体约束，例如：

- 只能使用 HTML、CSS、vanilla JavaScript。
- 900px 以上双栏布局，900px 以下单栏布局。
- 所有输入框都有 label。
- 有逻辑 tab 顺序和可见 focus 状态。
- 错误信息要能被屏幕阅读器读到。
- 表单字段包括姓名、邮箱、日期、时间段、票数、无障碍需求。
- blur 和 submit 时都要验证。
- 不使用 `alert()` 显示错误。
- 提供 Reset form 和 Undo last change。
- 提交成功后显示确认面板，并隐藏表单。
- 输出 `index.html`、`styles.css`、`app.js` 三个文件。

这个例子说明：prompt 越具体，AI 越容易生成符合设计目标的代码。

---

## 20. 示例 2：动画状态反馈系统 Prompt

第二个例子是设计一个动画 UI feedback system，用动画表达：

- idle
- loading
- success
- error

这个 prompt 的重点是：动画不是装饰，而是系统反馈。它要求：

- 只用 HTML 和 CSS，不用 JavaScript。
- 四种状态用 CSS classes 表示。
- loading 可以持续循环。
- success 和 error 应该短暂播放一次，不能无限循环。
- 动画要 subtle，不要过度晃动。
- 支持 `prefers-reduced-motion`，让不适合看动画的用户可以减少动画。
- 不能只靠颜色表达状态，还要有文字标签。
- 使用语义化 HTML 和清晰命名的 CSS class。

这个例子和 Lecture 2 的 CSS animation 相关：你不仅要会写动画，还要知道动画为什么存在、是否帮助用户理解状态。

---

## 21. Skillset 2：Design-Centred Critical Evaluation

第二个技能是以设计为中心的批判性评价。

课件强调，学生必须用这些内容来证明自己的决定：

- usability models。
- UI design principles。
- inclusive design considerations。

如果没有批判性评价，AI-led 会变成 AI-dependent。也就是你只是依赖 AI，而没有自己的判断。

如果有批判性评价，AI-led 才会变成 professional practice。

---

## 22. 批判性评价 checklist

课件给出一个评价清单，和后续 Lecture 6、8、9 有关。

| 类别 | 评价点 |
| --- | --- |
| Usability Models | effectiveness、efficiency、user satisfaction、heuristic |
| UI Design Principles | simplicity、structure、consistency、tolerance、screen-fit design |
| Inclusive Design Considerations | security concerns、cultural/social sensitivity、commercial/business concerns、ethics、environment/wellbeing |

这说明你评价 AI 作品时，不应该只说：

> It looks good.

而应该说：

> It improves efficiency because the key action is visible above the fold, but it may reduce accessibility because the error state relies too much on colour.

也就是要用课程理论来解释判断。

---

## 23. Large Software Projects：不要让 AI 一次写完整项目

课件特别提醒：大型项目不要一上来就让 AI 写全部代码。

更安全的方法是：

1. 先让 AI 设计软件结构。
2. 再让 AI 一次写一个文件，或一个小功能切片。
3. 每写完一部分就测试和检查。

如果你直接要求 AI 一次生成所有详细代码，常见失败包括：

- 不同文件之间 API 不一致。
- 忘记前面说过的限制。
- 路由、context、endpoint 路径前后不统一。
- 代码看起来完整，但不能编译或运行。
- 很多文件都有小错误，debug 很困难。

所以 one-at-a-time 的好处是：一致、可测试、容易修。

---

## 24. Three Tier AI-Learning Framework

课件最后提出 AI 学习的三层框架：

| Level | 实际表现 |
| --- | --- |
| AI Literacy | 让 AI 解释、定义、举例 |
| AI Competency | 用 AI 生成 UI、代码、布局等 artefacts |
| AI Problem Solving | 用 AI 诊断问题、比较方案、改进解决方案 |

很多人停留在 AI literacy，也就是只会让 AI 解释知识点。课程目标是让你进步到 AI problem-solving：能用 AI 解决真实设计问题。

---

## 25. AI Log：作业里到底要记录什么？

课件强调：AI log 不是为了证明你用了多少 AI，而是证明你有思考。

不重点考察：

- 你用了多少 AI。
- prompt 写得多“聪明”。
- 你迭代了多少轮。

重点考察：

- 你是否能为 AI 清楚框定任务。
- 你是否能评价 AI 输出。
- 你是否能用 AI 解决设计问题。
- 你是否记录了关键 decision points。

AI log 应该记录：

```text
为什么使用 AI -> AI 给了什么 -> 我接受了什么 -> 我拒绝了什么 -> 它如何改变了我的设计
```

课件特别说：AI log 要记录 decision points，而不是完整聊天记录 transcript。

---

## 26. 这一讲和前面几讲的关系

Lecture 1-4 的基础仍然重要：

- Lecture 1 HTML：你要判断 AI 生成的结构是否语义化。
- Lecture 2 CSS：你要判断 AI 生成的样式、布局、动画是否合理。
- Lecture 3 JavaScript：你要判断 AI 生成的交互逻辑是否能维护。
- Lecture 4 Production and Management：你要把 AI 放进 Agile、GitHub、版本控制和协作流程里。

所以 Lecture 5 不是让你跳过基础，而是告诉你：

> AI 越强，你越需要懂基础，才能判断 AI 有没有做对。

---

## 27. 如果要复习考试，优先看这些

1. 解释 AI-led development 和传统 development 的区别。
2. 解释 AI literacy、AI competency、AI problem-solving 的层级关系。
3. 说明 AI driving license 代表什么能力。
4. 解释 coursework 简化版 5 阶段流程。
5. 解释为什么 AI 生成的 requirements 需要检查。
6. 解释为什么 visual plausibility 不等于 good UX。
7. 解释为什么 correct code 不一定是 good code。
8. 解释为什么 AI 测试可能只测试 easy things，而不是 important things。
9. 解释 iteration without judgment is just noise。
10. 区分 prompt writing 和 prompt engineering。
11. 用高质量 prompt 模板说明一个 prompt 应包含哪些信息。
12. 说明为什么大型项目不能让 AI 一次写完所有代码。
13. 说明 design-centred critical evaluation 为什么重要。
14. 解释 AI log 记录的是 decision points，不是完整 transcript。
15. 说明 AI log 如何体现 critical thinking 和 skill gain。

---

## 28. 一句话结尾

Lecture 5 的重点不是“AI 会不会写代码”，而是“你会不会带着设计目标、用户需求、技术约束和批判性判断来使用 AI”。真正的 AI-led development 不是依赖 AI，而是用 AI 加速探索，再由人类负责判断、取舍和迭代。
