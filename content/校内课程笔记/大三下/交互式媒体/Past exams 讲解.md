---
title: EBU6305 Past Exams 讲解
date: 2026-06-14
tags:
  - course/interactive-media-design
  - exam-review
  - past-paper
  - ebu6305
source:
  - "[[附件/Past exams/2324_EBU6305.pdf|2324_EBU6305.pdf]]"
  - "[[附件/Past exams/2425_EBU6305.pdf|2425_EBU6305.pdf]]"
---

# EBU6305 Past Exams 讲解：题目与主要考点

> [!info] 来源
> 本笔记整理的是交互式媒体设计 **EBU6305 Interactive Media Design and Production** 的 past exams：[[附件/Past exams/2324_EBU6305.pdf|2324_EBU6305.pdf]] 和 [[附件/Past exams/2425_EBU6305.pdf|2425_EBU6305.pdf]]。

## 1. 总体结构

两份卷子结构非常相似：

- Paper A
- 2 小时
- Answer ALL questions
- 大体是 **4 道大题，每题 25 分**
- 考查范围覆盖：
  - HTML / CSS / JavaScript
  - SVG / CSS animation
  - UI components
  - Usability / UXD
  - Inclusive design
  - Gestalt / cognition
  - Heuristic evaluation
  - User testing / information architecture

> [!important] 复习策略
> 这门考试不是只背定义，而是经常给你代码、界面截图、设计场景，让你判断问题、解释原因、提出改进方案。

---

# 2. 高频考点总结

## 2.1 第一优先级：HTML / CSS / JavaScript coding

必须会：

- 找 HTML / JS 错误
- `id` vs `class`
- `getElementById()`
- `innerHTML`
- `var` / `let`
- comments
- CSS internal / inline / external
- CSS selectors
- CSS box model
- CSS transition / hover
- SVG elements
- CSS animation / keyframes

---

## 2.2 第二优先级：UI components 和 form design

重点是：

- 根据字段选组件
- 输入框、radio、checkbox、dropdown、slider
- mobile keyboard type
- inclusivity
- commercial gain
- user experience

---

## 2.3 第三优先级：Inclusive design

必须准备：

- colour blindness
- impaired vision
- dyslexia
- impaired hearing
- captions
- alt text
- high contrast
- font size adjustment
- reduced motion
- dark mode / energy saving

---

## 2.4 第四优先级：UXD 理论

常考：

- visceral / behavioural / reflective emotion
- curiosity / reward
- hyperbolic discounting
- ethical issues
- Gestalt proximity
- cognitive load

---

## 2.5 第五优先级：Heuristic evaluation

一定要背 Nielsen 10 条：

1. Visibility of system status
2. Match between system and real world
3. User control and freedom
4. Consistency and standards
5. Error prevention
6. Recognition rather than recall
7. Flexibility and efficiency of use
8. Aesthetic and minimalist design
9. Help users recognise and recover from errors
10. Help and documentation

考试通常不是让你背定义，而是给场景让你判断是哪条。

---

## 2.6 第六优先级：User testing / IA

需要会：

- onsite vs remote testing
- pros and cons
- card sorting
- tree testing
- information architecture
- navigation design

---

# 3. 最值得重点复习的题型

如果时间有限，优先练这几类：

1. **代码改错题**
   - HTML / CSS / JS 混合代码
   - 找 `id`、selector、变量、DOM 错误

2. **CSS 解释题**
   - box model
   - transition
   - hover
   - combinator selectors

3. **SVG / animation 题**
   - 看到图说用哪些 SVG elements
   - 写 AI prompt 生成 SVG / CSS 动画

4. **设计评价题**
   - 看到糟糕 UI，用原则批评并改进

5. **heuristic scenario matching**
   - 看到场景，判断违反哪条 heuristic

6. **inclusive design 方案题**
   - 针对某类用户提出具体设计解决方案

---

# 4. 复习路线建议

## 4.1 先复习代码部分

建议顺序：

1. [[Unit 1#Unit 1 - HTML Basics 讲解|HTML Basics]]
2. [[Unit 1#Unit 1 - Lecture 2: CSS Basics & Animations 讲解|CSS Basics & Animations]]
3. [[Unit 1#Unit 1 - Lecture 3: JavaScript Basics 讲解|JavaScript Basics]]

重点练习：

- 改错
- 解释代码效果
- 盒模型计算
- SVG 元素识别

## 4.2 再复习设计理论

优先准备：

- UI components
- usability attributes
- inclusive design
- UXD emotions and motivations
- Gestalt law of proximity

## 4.3 最后刷 heuristic 和 user testing

这部分很适合背模板：

- 场景 → heuristic → 问题 → severity → solution
- onsite / remote → pros / cons
- card sorting / tree testing → 用途和区别

---

# 5. 逐题题目与参考答案（非官方）

> [!note]
> 以下答案是根据 past exam 题面和课程内容整理的 **复习用参考答案**，不是官方 mark scheme。较长题面用“原题要点”保留题目核心要求，方便复习和避免整份卷子逐字重复。

---

# 5.1 2023/24 Paper A 逐题答案

## 2023/24 Question 1：HTML, CSS, and JavaScript

### Q1(a) 原题要点

代码想输出：

> There are 242 students in EBU6305

但结果不能正常显示。题目要求找出并修正 **3 个错误**。

题目代码核心问题包括：

```html
<script>
  var group = 242;
  var group = "EBU6305";
  var group = new Object();
  group.module = "EBU6305";
  group.number = "242";
  document.getElementByID("Telecom").innerHTML =
    "There are " + group.number + " students in " + group.module;
<p class="Telecom"></p>
```

### Q1(a) 参考答案

主要错误：

1. `getElementByID` 大小写错误，应为 `getElementById`。
2. HTML 元素用的是 `class="Telecom"`，但 JavaScript 用的是 `getElementById("Telecom")`，所以应该改成 `id="Telecom"`。
3. `<p>` 标签不应该写在 `<script>` 里面；并且为了确保 JS 能找到元素，最好先放 `<p id="Telecom"></p>`，再执行 script。

一种正确写法：

```html
<html>
<body>
  <p id="Telecom"></p>

  <script>
    var group = new Object();
    group.module = "EBU6305";
    group.number = "242";

    document.getElementById("Telecom").innerHTML =
      "There are " + group.number + " students in " + group.module;
  </script>
</body>
</html>
```

解释：

- `id="Telecom"` 和 `getElementById("Telecom")` 对应。
- `innerHTML` 会把 `<p>` 里面的内容改成目标句子。
- `group.module` 是 `"EBU6305"`。
- `group.number` 是 `"242"`。
- 最终显示：`There are 242 students in EBU6305`。

### Q1(a) 主要考点

这题重点是 **debug**，不是从零写代码。

必须会看：

```javascript
document.getElementById("Telecom").innerHTML = ...
```

它要求 HTML 中必须有：

```html
id="Telecom"
```

如果 HTML 写的是：

```html
<p class="Telecom"></p>
```

那 `getElementById("Telecom")` 找不到，因为它找的是 `id`，不是 `class`。

常考点：

- `getElementById()` 大小写必须正确。
- `id` 和 `class` 区别。
- JavaScript object 属性调用。
- `<script>` 是否正确闭合。
- DOM 元素是否在脚本执行前存在。

---

### Q1(b) 原题要点

给出 CSS：

```css
div {
  width: 300px;
  height: 200px;
  padding: 5px;
  border: 3px;
  margin: 1;
}
```

要求计算 div 在屏幕上的总宽度和总高度。

### Q1(b) 参考答案

CSS box model 总宽度计算：

```text
总宽度 = content width + left padding + right padding + left border + right border + left margin + right margin
```

如果把 `margin: 1` 按题目意图理解成 `1px`：

```text
总宽度 = 300 + 5 + 5 + 3 + 3 + 1 + 1 = 318px
总高度 = 200 + 5 + 5 + 3 + 3 + 1 + 1 = 218px
```

所以答案：

```text
Total width = 318px
Total height = 218px
```

> [!warning]
> 严格 CSS 中 `margin: 1;` 缺少单位，浏览器可能忽略这条声明。考试通常是考盒模型计算，所以一般按 `1px` 理解。

### Q1(b) 主要考点

这是 **CSS box model**。

总宽度通常是：

```text
content width
+ left padding + right padding
+ left border + right border
+ left margin + right margin
```

总高度同理。

要注意：

- `width` 和 `height` 默认只表示 content 区域。
- padding、border、margin 会增加实际占用空间。
- `margin: 1;` 严格来说缺少单位，实际 CSS 中应写成 `1px` 等。

---

### Q1(c) 原题要点

题目给出一段 HTML/CSS，要求解释显示效果。代码大意是：

```css
div {
  width: 100px;
  height: 100px;
  background: blue;
  transition: width 1s, height 4s;
}

div:hover {
  width: 500px;
  height: 500px;
}
```

### Q1(c) 参考答案

页面初始显示一个蓝色 `div` 方块：

```text
width = 100px
height = 100px
background = blue
```

当鼠标悬停在这个 `div` 上时，触发：

```css
div:hover
```

于是：

```text
width 变成 500px
height 变成 500px
```

因为设置了：

```css
transition: width 1s, height 4s;
```

所以变化不是瞬间完成，而是动画过渡：

- 宽度从 `100px` 到 `500px`，用 1 秒。
- 高度从 `100px` 到 `500px`，用 4 秒。

最终效果：

> 鼠标悬停时，蓝色方块会平滑变大；宽度变化快，高度变化慢。


### Q1(c) 主要考点

这是 **CSS transition** 和 pseudo-class `:hover`。

答题时应说明：

- 页面初始显示一个蓝色方块。
- 默认大小是 `100px × 100px`。
- 当鼠标悬停在 div 上时，触发 `div:hover`。
- 宽度变成 `500px`。
- 高度变成 `500px`。
- 宽度变化用 1 秒完成。
- 高度变化用 4 秒完成。
- 因为有 `transition`，变化是平滑动画，不是瞬间改变。

---

### Q1(d) 原题要点

题目给出一个房子图，问可以用哪些 SVG elements 绘制。

图中包括：

- 背景
- 地面
- 房子主体
- 屋顶
- 门
- 烟囱
- 烟雾

### Q1(d) 参考答案

可以使用：

| 图形部分 | SVG 元素 |
|---|---|
| 背景 | `<rect>` |
| 地面 | `<rect>` |
| 房子主体 | `<rect>` |
| 门 | `<rect>` |
| 屋顶 | `<polygon>` |
| 烟囱 | `<rect>` |
| 烟雾 | `<circle>` |
| 分组 | `<g>` |

解释：

- `<rect>` 适合画矩形，例如背景、地面、墙、门、烟囱。
- `<polygon>` 适合画屋顶这种三角形或多边形。
- `<circle>` 适合画烟雾圆圈。
- `<g>` 可以把房子相关元素组合成一组，方便统一移动或设置样式。

### Q1(d) 主要考点

SVG 基础元素：

| 图形部分 | 可用 SVG 元素 |
|---|---|
| 房子主体 | `<rect>` |
| 屋顶 | `<polygon>` |
| 门 | `<rect>` |
| 烟囱 | `<rect>` |
| 烟雾 | `<circle>` |
| 地面 | `<rect>` |
| 背景 | `<rect>` |
| 分组 | `<g>` |

重点是能根据图像判断用什么 SVG 标签。

---

## 2023/24 Question 2：Design Theory and Tools

### Q2(a) 原题要点

一个免费手机棋盘游戏要求用户必须观看 5 秒广告才能正常使用。题目要求：

1. 说明它影响 ISO usability model 的哪个属性。
2. 解释该属性含义。
3. 评价这个属性如何影响产品利润。

### Q2(a) 参考答案

最直接影响的是：

> **Efficiency 效率**

也会间接影响：

> **Satisfaction 满意度**

#### i) 哪个 usability attribute？

主要是 **Efficiency**。

因为用户本来想直接玩游戏，但必须先等 5 秒广告，完成目标所需时间增加了。

#### ii) Efficiency 是什么意思？

Efficiency 指用户完成目标时所消耗的资源，例如：

- 时间
- 操作步骤
- 注意力
- 精力

如果用户能更快、更少步骤地完成目标，效率就高。

#### iii) 如何影响利润？

正面影响：

- 广告可以带来直接收入。
- 免费游戏通过广告变现。
- 如果广告较短，用户可能愿意接受。

负面影响：

- 用户等待会降低满意度。
- 频繁广告可能导致用户卸载。
- 用户留存率下降会影响长期利润。

更好的设计：

- 控制广告频率。
- 使用奖励广告。
- 允许付费去广告。
- 广告结束后给明确反馈。

### Q2(a) 主要考点

ISO usability 常见属性：

- Effectiveness
- Efficiency
- Satisfaction

这个题重点通常落在：

> **Efficiency 效率** 和 **Satisfaction 满意度**

因为广告让用户多等 5 秒，会降低完成任务效率，也可能影响满意度。

商业影响可以这样答：

- 好处：广告带来收入。
- 坏处：用户体验变差，可能降低留存率。
- 平衡点：广告时间短、可跳过、奖励广告等方式更好。

---

### Q2(b) 原题要点

解释四种移动端常见 layout，包括 smartphone 和 tablet，可用图示辅助。

### Q2(b) 参考答案

可以写以下四种。

#### 1. List layout

```text
Item 1
Item 2
Item 3
Item 4
```

适合：

- 新闻列表
- 消息列表
- 联系人列表

优点：清晰、适合手机窄屏。

#### 2. Grid layout

```text
[ A ] [ B ]
[ C ] [ D ]
```

适合：

- 图片库
- 商品分类
- 图标菜单

优点：视觉均衡，适合展示多个同级项目。

#### 3. Tab layout

```text
Home | Search | Cart | Profile
```

适合：

- 多个主要功能区之间切换
- 手机底部导航栏

优点：用户容易理解当前位置和可切换页面。

#### 4. Master-detail layout

```text
Tablet:
左侧列表 | 右侧详情
```

适合：

- 邮件应用
- 文件管理
- 平板界面

优点：大屏上可以同时看列表和详情，提高效率。

### Q2(b) 主要考点

可准备这些布局：

1. **List layout**
   - 新闻列表、联系人列表。
2. **Grid layout**
   - 图片库、商品分类。
3. **Tab layout**
   - 底部导航栏：首页、搜索、我的。
4. **Master-detail layout**
   - 平板常见，左侧列表，右侧详情。
5. **Dashboard layout**
   - 多个功能模块集中展示。

考试重点：

- 说清楚适用场景。
- 简单画结构。
- 说明手机和平板布局差异。

---

### Q2(c) 原题要点

一个网站结构很深，题目要求提出帮助用户知道自己当前位置的方案。

### Q2(c) 参考答案

推荐使用：

> **Breadcrumb navigation 面包屑导航**

例子：

```text
Home > Products > Electronics > Phones > Android
```

优点：

- 显示用户当前位置。
- 帮助用户返回上一级或更高层级。
- 减少迷路感。
- 适合层级很深的网站。

还可以补充：

- 高亮当前菜单项。
- 提供 sitemap。
- 提供搜索功能。
- 使用清晰的页面标题。

### Q2(c) 主要考点

核心答案：

> Breadcrumb navigation 面包屑导航

例如：

```text
Home > Products > Phones > Android > Samsung
```

主要说明：

- 显示当前位置。
- 帮助用户返回上级。
- 降低迷路感。
- 适合层级很深的网站。

---

### Q2(d) 原题要点

设计一个 UI，让用户可以调整显示文字大小。

### Q2(d) 参考答案

可以设计：

```text
Text size:  A-   [ slider ]   A+
```

或：

```text
Text size:  Small | Medium | Large
```

推荐组件：

- `A-` 减小字体。
- `A+` 增大字体。
- slider 精细调整。
- 下拉菜单选择 small / medium / large。

设计理由：

- 图标 `A- / A+` 易理解。
- slider 能提供连续调节。
- 调整后应立即预览效果。
- 有助于 elderly users、low vision users 和 dyslexia users。

### Q2(d) 主要考点

可用组件：

- `A- / A+` 按钮
- slider 滑块
- dropdown 下拉菜单
- segmented buttons：Small / Medium / Large

重点：

- accessibility
- readable text
- clear affordance
- immediate feedback
- inclusive design

---

## 2023/24 Question 3：UXD, Media, Inclusive Design

### Q3(a)(i) 原题要点

解释用户情绪的三个方面：

- visceral
- behavioural
- reflective

并说明 meditation mobile app 如何激发这些情绪。

### Q3(a)(i) 参考答案

| 情绪层面 | 含义 | Meditation app 例子 |
|---|---|---|
| Visceral | 用户第一眼的本能反应 | 柔和颜色、自然风景、平静声音，让用户一打开就感觉放松 |
| Behavioural | 使用过程中的感受 | 操作简单、引导清楚、冥想计时顺畅，让用户觉得好用 |
| Reflective | 使用后的价值感和自我认同 | 用户觉得自己更健康、更自律、更会管理压力 |

总结：

- visceral 关注第一印象。
- behavioural 关注使用过程。
- reflective 关注长期意义和自我评价。

### Q3(a)(i) 主要考点

| 类型 | 含义 | Meditation app 例子 |
|---|---|---|
| Visceral | 第一眼感受 | 柔和颜色、自然声音、平静插画 |
| Behavioural | 使用过程体验 | 操作简单、计时清楚、引导顺畅 |
| Reflective | 使用后的价值感 | 觉得自己更健康、更自律 |

---

### Q3(a)(ii) 原题要点

说明 hyperbolic discounting 如何用于电商网站促进即时购买，并给两个例子，同时评论伦理问题。

### Q3(a)(ii) 参考答案

Hyperbolic discounting 指：

> 人们倾向于更重视立即获得的奖励，而低估未来收益或未来成本。

电商例子 1：限时折扣

```text
Only 10 minutes left: 30% off
```

解释：用户看到马上结束的优惠，会更想立即购买。

电商例子 2：稀缺提示

```text
Only 2 left in stock
```

解释：用户担心错过机会，所以更容易马上付款。

其他例子：

- Buy now, get free delivery today.
- Checkout now to receive a coupon.
- Flash sale countdown.

伦理问题：

- 可能诱导冲动消费。
- 如果稀缺信息是假的，就是误导。
- 倒计时压力可能操纵用户。
- 对自控力较弱或经济压力大的用户不公平。

好的设计应保证：

- 信息真实。
- 价格透明。
- 不制造虚假紧迫感。
- 允许用户冷静比较。

### Q3(a)(ii) 主要考点

Hyperbolic discounting 指人们倾向于重视即时奖励，而低估长期收益。

电商例子：

- 限时折扣
- 倒计时优惠
- “Only 2 left”
- “Buy now, get today”
- 立即下单送优惠券

伦理问题：

- 是否制造焦虑？
- 是否误导用户？
- 是否诱导冲动消费？
- 是否对弱势用户不公平？

---

### Q3(b)(i) 原题要点

解释三种 colour association：

- built-in
- cultural
- work association

并举例。

### Q3(b)(i) 参考答案

| 类型 | 含义 | 例子 |
|---|---|---|
| Built-in association | 人类基于自然或生理经验形成的颜色联想 | 红色常让人联想到血、危险、警告 |
| Cultural association | 由文化背景形成的颜色意义 | 中国文化中红色常代表喜庆和好运 |
| Work association | 在职业或工作环境中形成的颜色含义 | 医疗或安全系统中绿色常表示正常或安全 |

设计时要注意：

- 颜色意义并不总是全球通用。
- 同一种颜色在不同文化中可能含义不同。
- 不应只依靠颜色传达重要信息。

### Q3(b)(i) 主要考点

解释三种颜色关联。

| 类型 | 含义 | 例子 |
|---|---|---|
| Built-in | 生理或自然联想 | 红色表示危险，蓝色冷静 |
| Cultural | 文化差异造成 | 红色在中国常表示喜庆 |
| Work association | 工作环境中形成 | 医疗系统中绿色表示安全 |

---

### Q3(b)(ii) 原题要点

说明 dyslexia 对阅读能力的影响，以及如何设计文字属性避免排除 dyslexia 用户。

### Q3(b)(ii) 参考答案

Dyslexia 可能导致：

- 阅读速度较慢。
- 字母或单词识别困难。
- 容易混淆相似字母。
- 长段文字难以跟踪。
- 密集排版会增加认知负担。

设计建议：

1. 使用清晰易读字体，例如 sans-serif。
2. 增大字号和行距。
3. 避免整段大写。
4. 避免过长段落。
5. 使用左对齐，避免两端对齐。
6. 保持足够但不过度刺眼的对比度。
7. 使用浅色背景，避免复杂背景图。
8. 用标题、列表和分段帮助扫描。

例子：

```text
不推荐：密集长段、全大写、行距很小。
推荐：短段落、清晰标题、足够行距、左对齐。
```

### Q3(b)(ii) 主要考点

影响：

- 阅读速度慢。
- 容易混淆字母。
- 长段文字难理解。
- 高对比或密集文字会造成压力。

设计建议：

- 使用清晰字体。
- 增大行距。
- 避免整段大写。
- 避免过长段落。
- 左对齐。
- 使用足够字号。
- 避免复杂背景。
- 使用浅色背景而不是强烈白底黑字。

---

## 2023/24 Question 4：Design Process + Heuristic Evaluation

### Q4(a)(i) 原题要点

问：What is a mind map?

### Q4(a)(i) 参考答案

Mind map 是一种视觉化的发散思维工具。

特点：

- 中心放主题。
- 从中心向外扩展关键词。
- 用分支表示相关想法。
- 可以加入图像、符号、颜色。

作用：

- 帮助 brainstorming。
- 帮助整理想法。
- 帮助发现内容结构和关系。

### Q4(a)(i) 主要考点

Mind map 是一种发散思维工具。

常用于：

- early design stage
- brainstorming
- idea generation
- understanding content structure
- identifying target audience and purpose

---

---

### Q4(a)(ii) 原题要点

问：Mind mapping 在 interactive media design process 的哪个 task 和 phase 中有用？

### Q4(a)(ii) 参考答案

Mind mapping 通常用于设计早期阶段。

适合：

- idea generation
- brainstorming
- defining purpose
- exploring content
- understanding target audience

可以说它属于：

> 设计流程早期的 research / concept / idea generation 阶段。

用途：

- 扩展设计想法。
- 明确应用主题。
- 整理信息结构。
- 找到潜在功能和用户需求。

### Q4(a)(ii) 主要考点

同 Q4(a)(i) 主要考点。

### Q4(a)(iii) 原题要点

给一个关于 global warming 的 mind map，要求判断该 interactive media application 的 purpose 和 target audience，并说明理由。

### Q4(a)(iii) 参考答案

可能的 purpose：

> 教育和鼓励用户采取行动减少 global warming / carbon footprint。

理由：mind map 中包含：

- travel choices
- use public transport
- walk / bike
- home energy saving
- buy local food
- plant trees
- reduce meat
- talk to MPs
- vote

说明它不是单纯介绍气候变化，而是鼓励用户采取实际行动。

可能的 target audience：

- 普通公众
- 家庭用户
- 学生 / 年轻人
- 对环保感兴趣的人

如果强调教学场景，也可以说：

> target audience 可能是 school students，因为图中有鼓励朋友、学校和公众行动的内容，形式也比较图像化，适合教育用途。

### Q4(a)(iii) 主要考点

Mind map 是一种发散思维工具。

常用于：

- early design stage
- brainstorming
- idea generation
- understanding content structure
- identifying target audience and purpose

---

### Q4(b)(i) 原题要点

场景：表单中 submit 按钮紧挨着 reset 按钮。问违反哪条 heuristic，给 severity rating 并解释。

### Q4(b)(i) 参考答案

违反：

> UH5 Error prevention

原因：

- Submit 和 Reset 太近，用户容易误点 Reset。
- Reset 可能清空已填写内容。
- 这会导致用户挫败和数据丢失。

Severity rating：

```text
3 = major usability problem
```

理由：

- 影响较严重。
- 用户可能需要重新填写整个表单。
- 但如果有确认弹窗或撤销功能，严重程度可降低。

改进：

- 将 Reset 放远。
- 降低 Reset 的视觉优先级。
- 增加确认对话框。
- 提供 undo。

### Q4(b)(i) 主要考点

| 场景 | 对应 heuristic |
|---|---|
| Submit 和 Reset 太近 | Error prevention |
| VR 操作不符合现实 | Match between system and real world |
| 高级功能只能靠复杂快捷键 | Flexibility and efficiency of use / Recognition rather than recall |
| 错误修正提示 | Help users recognise and recover from errors |

还要会：

- assign severity rating
- justify rating
- propose solution
- 说明好的 error message 特点

---

---

### Q4(b)(ii) 原题要点

场景：VR 游戏中的操作控制与现实手势或动作完全无关。问违反哪条 heuristic，给 severity rating 并解释。

### Q4(b)(ii) 参考答案

违反：

> UH2 Match between system and real world

原因：

- VR 游戏强调沉浸感。
- 控制方式如果和现实动作完全无关，用户难以理解。
- 用户需要额外学习，交互不自然。

Severity rating：

```text
3 或 4
```

如果这是核心控制方式，可以给：

```text
4 = usability catastrophe
```

理由：

- 控制是 VR 游戏核心体验。
- 如果控制不符合现实习惯，可能导致用户无法顺利玩游戏。

改进：

- 使用类似现实的手势映射。
- 提供训练模式。
- 使用清晰提示。
- 允许用户自定义控制方式。

### Q4(b)(ii) 主要考点

同 Q4(b)(i) 主要考点。

### Q4(b)(iii) 原题要点

场景：productivity app 的高级功能只能通过复杂快捷键使用。要求判断 heuristic，给 severity rating，并提出方案。

### Q4(b)(iii) 参考答案

主要违反：

> UH6 Recognition rather than recall

也可能影响：

> UH7 Flexibility and efficiency of use

原因：

- 用户必须记住复杂快捷键。
- 新手用户难以发现高级功能。
- 功能隐藏太深，增加记忆负担。

Severity rating：

```text
3 = major usability problem
```

解决方案：

- 在菜单中显示高级功能。
- 提供工具栏按钮。
- 在菜单旁显示快捷键提示。
- 允许用户自定义快捷键。
- 提供模板和搜索命令功能。
- 提供 onboarding 或 help documentation。

### Q4(b)(iii) 主要考点

同 Q4(b)(i) 主要考点。

### Q4(b)(iv) 原题要点

场景：电商网站提供清晰说明或提示，帮助用户修正错误并完成交易。问它满足哪条 heuristic，并说明好的 error message 特点。

### Q4(b)(iv) 参考答案

满足：

> UH9 Help users recognise and recover from errors

好的 error message 应该：

1. 清楚说明发生了什么错误。
2. 使用用户能理解的语言，避免技术术语。
3. 指出错误位置。
4. 给出具体修复建议。
5. 语气礼貌，不责怪用户。
6. 尽量保留用户已输入内容。
7. 如果可能，提供自动修复或示例。

例子：

```text
不推荐：Error 403.
推荐：Your card number seems too short. Please enter the 16-digit number on your card.
```

### Q4(b)(iv) 主要考点

| 场景 | 对应 heuristic |
|---|---|
| Submit 和 Reset 太近 | Error prevention |
| VR 操作不符合现实 | Match between system and real world |
| 高级功能只能靠复杂快捷键 | Flexibility and efficiency of use / Recognition rather than recall |
| 错误修正提示 | Help users recognise and recover from errors |

还要会：

- assign severity rating
- justify rating
- propose solution
- 说明好的 error message 特点

---

# 5.2 2024/25 Paper A 逐题答案

## 2024/25 Question 1：HTML, CSS, and JavaScript

### Q1(a)(i) 原题要点

题目给一个 Telecom Sales Dashboard 页面代码，要求找出 **6 个错误** 并提出修正。

代码核心包括：

- CSS 中的 `background-colour`、`colour`、`centre`
- JavaScript 中的 `let isActive == !!"False";`
- `count+;`
- `document.getElementById("Telecom").innerHTML = count;`

### Q1(a)(i) 参考答案

6 个错误和修正：

| 位置 | 错误 | 修正 |
|---|---|---|
| CSS body | `background-colour` | `background-color` |
| CSS body | `colour` | `color` |
| CSS `#Telecom` | `colour` | `color` |
| CSS `#Telecom` | `text-align: centre;` | `text-align: center;` |
| JS line 24 | `let isActive == ...` | `let isActive = true;` 或 `let isActive = false;` |
| JS line 25 | `count+;` | `count++;` 或 `count += 1;` |

一个修正版片段：

```html
<style>
body {
  background-color: lightgray;
  color: black;
}
#Telecom {
  color: blue;
  text-align: center;
}
</style>

<script>
var count = 0;

function updateSales() {
  let isActive = true;
  count++;
  if (isActive) {
    document.getElementById("Telecom").innerHTML = count;
  } else {
    document.getElementById("Telecom").innerHTML = count;
  }
}
</script>
```

补充说明：

- JavaScript 中赋值用 `=`。
- `==` 是比较，不适合放在 `let isActive == ...` 这种声明语句中。
- `count++` 表示 count 增加 1。

### Q1(a)(i) 主要考点

这是 2425 的核心 coding 题。

考点包括：

- HTML structure
- `<title>`
- internal CSS
- inline CSS
- external CSS
- CSS selector
- `id` selector
- JavaScript `var` 和 `let`
- Boolean
- `getElementById()`
- `innerHTML`
- comments

尤其注意：

```javascript
document.getElementById("Telecom")
```

必须对应：

```html
<span id="Telecom"></span>
```

还要注意大小写：

```javascript
getElementById
```

不能写错。

---

---

### Q1(a)(ii) 原题要点

解释 line 2 的作用，也就是：

```html
<title>Telecom Sales</title>
```

### Q1(a)(ii) 参考答案

`<title>` 定义网页标题。

作用：

- 显示在浏览器标签页上。
- 作为收藏夹标题。
- 可能显示在搜索引擎结果中。
- 帮助用户识别当前页面内容。

所以：

```html
<title>Telecom Sales</title>
```

会让浏览器标签页显示类似：

```text
Telecom Sales
```

### Q1(a)(ii) 主要考点

同 Q1(a)(i) 主要考点。

### Q1(a)(iii) 原题要点

区分 line 21 和 line 24 的变量声明方式。

题目中 line 21 使用：

```javascript
var count = 0;
```

line 24 使用：

```javascript
let isActive = ...;
```

### Q1(a)(iii) 参考答案

| 对比 | `var` | `let` |
|---|---|---|
| 出现时间 | 旧写法 | ES6 之后的新写法 |
| 作用域 | function scope | block scope |
| 是否可重复声明 | 可以重复声明 | 同一作用域中不允许重复声明 |
| 推荐程度 | 仍可用，但容易出错 | 现代 JS 更推荐 |

解释：

- `var count = 0;` 声明一个函数作用域或全局作用域变量。
- `let isActive = true;` 声明一个块级作用域变量，只在当前 `{}` 中有效。

在本题中：

- `count` 需要在多次点击之间保留数值，所以放在函数外。
- `isActive` 只用于 `updateSales()` 函数内部判断，所以适合用 `let`。

### Q1(a)(iii) 主要考点

同 Q1(a)(i) 主要考点。

### Q1(a)(iv) 原题要点

把 internal CSS 转成 inline CSS，并评价 internal CSS 和 inline CSS 的限制，同时说明 external CSS 适合什么场景。

### Q1(a)(iv) 参考答案

原 internal CSS：

```css
body {
  background-color: lightgray;
  color: black;
}
#Telecom {
  color: blue;
  text-align: center;
}
```

转成 inline CSS：

```html
<body style="background-color: lightgray; color: black;">
  <p>Total Active Sales Checked-in:
    <span id="Telecom" style="color: blue; text-align: center;">0</span>
  </p>
</body>
```

限制：

#### Inline CSS 的限制

- 样式和 HTML 内容混在一起。
- 重复代码多。
- 不方便维护。
- 只影响单个元素。

#### Internal CSS 的限制

- 只适合当前页面。
- 多页面网站会重复写样式。
- 不利于统一维护全站风格。

#### External CSS 适合场景

External CSS 最适合：

- 多页面网站。
- 需要统一品牌视觉。
- 团队合作项目。
- 需要长期维护的项目。

写法：

```html
<link rel="stylesheet" href="style.css">
```

### Q1(a)(iv) 主要考点

同 Q1(a)(i) 主要考点。

### Q1(a)(v) 原题要点

在指定位置插入三条 comments：

- line 4：说明颜色主题符合公司 logo 设计。
- line 18：说明点击按钮进行 check in。
- line 22：说明更新显示信息。

### Q1(a)(v) 参考答案

CSS comment：

```css
/* The colour theme complies with the company logo design. */
```

HTML comment：

```html
<!-- Click the button to check in. -->
```

JavaScript comment：

```javascript
// Update the displayed message.
```

放置示例：

```html
<style>
/* The colour theme complies with the company logo design. */
body {
  background-color: lightgray;
  color: black;
}
</style>

<!-- Click the button to check in. -->
<button onclick="updateSales()">Add Sale</button>

<script>
var count = 0;
// Update the displayed message.
function updateSales() {
  count++;
}
</script>
```

### Q1(a)(v) 主要考点

这是 2425 的核心 coding 题。

考点包括：

- HTML structure
- `<title>`
- internal CSS
- inline CSS
- external CSS
- CSS selector
- `id` selector
- JavaScript `var` 和 `let`
- Boolean
- `getElementById()`
- `innerHTML`
- comments

尤其注意：

```javascript
document.getElementById("Telecom")
```

必须对应：

```html
<span id="Telecom"></span>
```

还要注意大小写：

```javascript
getElementById
```

不能写错。

---

### Q1(b) 原题要点

题目给出 sunset animation：太阳从左上角逐渐落到右下角。要求写出可能给生成式 AI 的 prompt，只允许使用 SVG 和 CSS。

### Q1(b) 参考答案

可以写 prompt：

```text
Create an SVG animation of a sunset scene using only SVG and CSS. The scene should have a grey rectangular sky background, several dark mountain shapes drawn with polygon elements, and a circular sun. The sun should start near the top-left corner and gradually move to the bottom-right corner. Use CSS @keyframes to animate the sun position smoothly over time. Do not use JavaScript. Keep the style simple and monochrome.
```

需要包含的关键要求：

- 用 `<svg>` 创建画布。
- 用 `<rect>` 画背景。
- 用 `<polygon>` 画山。
- 用 `<circle>` 画太阳。
- 用 CSS `@keyframes` 制作太阳移动。
- 太阳从 top-left 移动到 bottom-right。
- 只用 SVG 和 CSS，不用 JS。

可以进一步指定：

```text
Animate the circle with transform: translate(x, y), duration 5 seconds, repeat infinitely or play once.
```

### Q1(b) 主要考点

这题考：

- prompt engineering
- SVG elements
- CSS animation
- keyframes
- visual description

应该提到：

- background rectangle
- mountain polygons
- sun circle
- sun moving path
- CSS `@keyframes`
- `transform` 或 `cx/cy` 变化
- animation duration
- smooth transition

---

### Q1(c)(i) 原题要点

给嵌套 navigation menu，判断 selector 会选中哪些菜单项：

```css
ul ol ol {
  color: red;
}
```

### Q1(c)(i) 参考答案

这个 selector 中间是空格，表示 **descendant selector 后代选择器**。

```css
ul ol ol
```

意思是：

> 选择在 `ul` 里面的 `ol` 里面的 `ol`。

也就是说，它会选中嵌套在有序列表中的更深层有序列表。

根据题图，可能被选中的项目包括：

- CEO / CTO / COO 所在的 nested ordered list。
- Physics / Chemistry / Biology 所在的 nested ordered list。
- English / Spanish / Mandarin 所在的 nested ordered list，如果它仍然处在 `ul` 后代中的 `ol ol` 结构内。

核心解释：

- 空格不要求直接父子关系。
- 只要是后代层级，符合 `ul` → `ol` → `ol` 就会被选中。

### Q1(c)(i) 主要考点

CSS combinators：

| Selector | 含义 |
|---|---|
| 空格 | descendant 后代选择器 |
| `>` | direct child 直接子元素选择器 |

重点是看懂 HTML list 层级：

- `ul`
- `ol`
- nested `ol`
- 哪些列表是后代
- 哪些是直接子元素

---

---

### Q1(c)(ii) 原题要点

判断 selector 会选中哪些菜单项：

```css
ul > li > ol > li > ol {
  color: red;
}
```

### Q1(c)(ii) 参考答案

这个 selector 使用 `>`，表示 **direct child selector 直接子元素选择器**。

它要求结构必须严格是：

```text
ul
└── li
    └── ol
        └── li
            └── ol
```

所以它只会选择符合这个直接父子层级的 `ol`。

根据题图，通常会选中：

- Leadership Team 下面的 CEO / CTO / COO 列表。
- Science 下面的 Physics / Chemistry / Biology 列表。

它不会选中层级中间夹了额外 `ul` 的列表，例如 Languages 下的 English / Spanish / Mandarin，如果结构不是直接 `ol > li > ol`。

核心考点：

- 空格 = 后代。
- `>` = 直接子元素。

### Q1(c)(ii) 主要考点

CSS combinators：

| Selector | 含义 |
|---|---|
| 空格 | descendant 后代选择器 |
| `>` | direct child 直接子元素选择器 |

重点是看懂 HTML list 层级：

- `ul`
- `ol`
- nested `ol`
- 哪些列表是后代
- 哪些是直接子元素

---

## 2024/25 Question 2：Design Theory and Tools

### Q2(a)(i) 原题要点

药店网站要做 online form，字段包括：

- Name
- Gender
- Age
- Telephone Number
- Subscribe to newsletter

要求为 A-E 选择合适 UI components，并考虑 user experience、social inclusivity、commercial gain。

### Q2(a)(i) 参考答案

| 区域 | 字段 | 推荐 UI component | 理由 |
|---|---|---|---|
| A | Name | text input | 姓名是自由文本 |
| B | Gender | radio buttons / dropdown / self-describe option | 性别选项应包容，不应只限二元 |
| C | Age | number input / dropdown | 年龄应输入数字，可限制范围 |
| D | Telephone Number | telephone input | 方便输入电话 |
| E | Newsletter | checkbox / toggle | 用户可选择是否订阅 |

推荐设计：

```html
<input type="text" name="name">
<select name="gender">
  <option>Female</option>
  <option>Male</option>
  <option>Non-binary</option>
  <option>Prefer not to say</option>
  <option>Self-describe</option>
</select>
<input type="number" name="age">
<input type="tel" name="telephone">
<input type="checkbox" name="newsletter">
```

UX 角度：

- 输入类型应匹配数据类型。
- 表单应短、清楚、易填写。
- 错误提示要明确。

Inclusivity 角度：

- Gender 不应只给 male / female。
- 电话、年龄输入应支持不同用户能力。
- 标签和控件应清楚关联。

Commercial gain 角度：

- Newsletter checkbox 可以帮助药店后续营销。
- 表单越容易填写，潜在客户转化越高。

### Q2(a)(i) 主要考点

UI components：

| 字段 | 合适组件 |
|---|---|
| Name | text input |
| Gender | radio buttons / dropdown / inclusive self-describe option |
| Age | number input / dropdown |
| Telephone Number | tel input |
| Newsletter | checkbox / toggle |

手机键盘：

```html
<input type="tel">
```

会弹出数字电话键盘，提高效率，减少输入错误。

---

---

### Q2(a)(ii) 原题要点

说明 area D 在 smartphone 上应该使用什么 keyboard type，并评价其 UX 影响。

### Q2(a)(ii) 参考答案

Area D 是 telephone number，应使用 telephone keyboard。

HTML 可写：

```html
<input type="tel" name="telephone">
```

UX 影响：

- 手机上会弹出数字电话键盘。
- 用户输入更快。
- 减少输入错误。
- 更符合用户预期。
- 对手部操作不便的用户也更友好。

### Q2(a)(ii) 主要考点

UI components：

| 字段 | 合适组件 |
|---|---|
| Name | text input |
| Gender | radio buttons / dropdown / inclusive self-describe option |
| Age | number input / dropdown |
| Telephone Number | tel input |
| Newsletter | checkbox / toggle |

手机键盘：

```html
<input type="tel">
```

会弹出数字电话键盘，提高效率，减少输入错误。

---

### Q2(b)(i) 原题要点

为 Paralympic Winter Games 网站选择最能体现 diversity 的 emoji set，并说明理由。

### Q2(b)(i) 参考答案

应选择能体现最多样化用户群体的一组，例如图中同时包含：

- 不同性别
- 不同肤色
- 不同身份或角色
- 对残障和多元群体更包容的视觉表达

如果按题图选项判断，可以选择最能同时呈现 gender diversity 和 skin-tone diversity 的那一组，并说明：

> 该组更能代表社会中不同用户，不会只呈现单一性别或单一肤色，因此更符合 Paralympic event 的 inclusive value。

答题重点不是猜图，而是说明选择标准：

- diversity
- representation
- inclusiveness
- avoiding stereotypes

### Q2(b)(i) 主要考点

Inclusive design：

- 不只用颜色传达信息。
- 高对比度。
- 可调字体大小。
- alt text。
- captions / transcripts。
- keyboard navigation。
- dark mode / low brightness mode。
- 减少 autoplay 视频。
- 减少高耗能动画。
- 提供 reduced motion 选项。

---

---

### Q2(b)(ii) 原题要点

为以下用户提供 equal access：

- colour-blindness
- impaired vision
- impaired hearing

### Q2(b)(ii) 参考答案

#### Colour-blindness

设计方案：

- 不只用颜色传达信息。
- 加文字、图标、纹理。
- 使用色盲友好配色。
- 保证足够对比度。

例子：

```text
错误状态不要只用红色，也要加 “Error” 文本和图标。
```

#### Impaired vision

设计方案：

- 支持字体放大。
- 高对比模式。
- 屏幕阅读器支持。
- 图片提供 alt text。
- 支持键盘导航。

#### Impaired hearing

设计方案：

- 视频提供 captions。
- 音频提供 transcript。
- 重要提示不要只用声音。
- 使用视觉提示或震动提示。

### Q2(b)(ii) 主要考点

同 Q2(b)(i) 主要考点。

### Q2(b)(iii) 原题要点

提出设计方案，强调 energy efficiency 和 environmental sustainability，同时降低眼疲劳，并说明 configuration options。

### Q2(b)(iii) 参考答案

可以提供：

- dark mode
- low brightness mode
- reduced motion
- disable autoplay video
- compress images
- lazy loading
- reduce heavy animations
- eco mode

配置选项示例：

```text
Display mode: Light / Dark / Eco
Animation: Full / Reduced / Off
Media autoplay: On / Off
Text contrast: Normal / High
```

解释：

- Dark mode 可降低部分屏幕耗电，也减少夜间眼疲劳。
- Reduced motion 减少动画负担，对前庭敏感用户也更友好。
- 图片压缩和 lazy loading 降低数据传输和能耗。
- 禁止 autoplay 可减少无意义播放。

### Q2(b)(iii) 主要考点

Inclusive design：

- 不只用颜色传达信息。
- 高对比度。
- 可调字体大小。
- alt text。
- captions / transcripts。
- keyboard navigation。
- dark mode / low brightness mode。
- 减少 autoplay 视频。
- 减少高耗能动画。
- 提供 reduced motion 选项。

---

### Q2(c) 原题要点

给一个混乱的 online store 页面截图，要求用 4 个 common UI design principles 分析并提出改进。

### Q2(c) 参考答案

可以使用以下四个原则。

#### 1. Aesthetic and minimalist design

问题：页面信息过多，文字和图片太密集。

改进：减少不必要内容，只保留核心商品信息和主要 CTA。

#### 2. Visual hierarchy

问题：用户不知道先看哪里。

改进：突出分类、商品标题、价格和购买按钮。

#### 3. Consistency

问题：图片大小、字体、布局不统一。

改进：使用统一商品卡片 layout。

#### 4. Proximity / grouping

问题：相关信息没有清楚分组。

改进：按商品类别分组，增加留白和边界。

其他可写：

- clear navigation
- search and filter
- alignment
- readability
- responsive layout

### Q2(c) 主要考点

可用原则：

- Consistency
- Simplicity
- Visual hierarchy
- Alignment
- Proximity
- Aesthetic and minimalist design
- Clear navigation
- Readability
- Reduce cognitive load

图里问题：

- 信息过载。
- 产品太密集。
- 缺乏视觉层级。
- 导航混乱。
- 字体和图片大小不统一。
- 不知道用户该先看哪里。

解决方案：

- 分类导航。
- 搜索和筛选。
- 统一 card layout。
- 留白。
- 突出主要 CTA。
- 减少无关信息。
- 响应式布局。

---

## 2024/25 Question 3：Design and Cognition / UXD / Design Process

### Q3(a) 原题要点

说明 Gestalt law of proximity 如何改善表单 usability，并画 before-and-after。

### Q3(a) 参考答案

Gestalt law of proximity 指：

> 距离近的元素会被用户认为属于同一组。

在表单中，label 应该靠近对应 input。

不好的设计：

```text
Name:        [        ]

Email:
             [        ]

Age:               [  ]
```

问题：label 和 input 距离不一致，用户可能不知道哪个标签对应哪个输入框。

改进后：

```text
Name:   [        ]
Email:  [        ]
Age:    [        ]
```

或分组：

```text
Personal information
Name:   [        ]
Age:    [        ]

Contact information
Email:  [        ]
Phone:  [        ]
```

为什么改善 usability：

- 降低认知负担。
- 用户更快理解表单结构。
- 减少输入错误。
- 扫描更容易。

### Q3(a) 主要考点

Proximity 是接近原则：

> 距离近的元素会被用户认为属于同一组。

表单设计中：

- label 应该靠近对应 input。
- 不同字段组之间要有足够间距。
- submit/reset 要合理分组或分隔。
- 相关选项放在一起。

---

### Q3(b)(i) 原题要点

解释两种 motivation：curiosity 和 reward，并举例。

### Q3(b)(i) 参考答案

#### Curiosity

Curiosity 是用户想探索未知内容的动机。

例子：

- “Discover your recommended products.”
- “Open today’s mystery deal.”
- “Find out what style suits you.”

#### Reward

Reward 是用户因为能获得奖励而产生行动动机。

例子：

- 积分。
- 优惠券。
- 免费配送。
- 徽章。
- 抽奖机会。

区别：

- Curiosity 让用户想知道“里面有什么”。
- Reward 让用户想获得“实际好处”。

### Q3(b)(i) 主要考点

| Motivation | 含义 | 电商例子 |
|---|---|---|
| Curiosity | 激发探索欲 | Mystery deal, “see what’s inside”, personalized recommendations |
| Reward | 给用户回报 | points, coupons, free shipping, badges |

也可以补充伦理角度：

- 不应诱导过度消费。
- 不应制造虚假稀缺。
- 不应隐藏真实价格。

---

---

### Q3(b)(ii) 原题要点

说明电商网站如何触发 curiosity 和 reward。

### Q3(b)(ii) 参考答案

触发 curiosity：

- 个性化推荐：`You may also like...`
- mystery box / mystery discount
- 限时探索活动
- 商品故事或隐藏详情

触发 reward：

- 下单返积分。
- 满减优惠。
- 免费配送。
- 签到奖励。
- 会员等级权益。

伦理注意：

- 不要制造虚假稀缺。
- 不要诱导过度消费。
- 不要隐藏真实价格。
- 奖励规则要清楚透明。

### Q3(b)(ii) 主要考点

| Motivation | 含义 | 电商例子 |
|---|---|---|
| Curiosity | 激发探索欲 | Mystery deal, “see what’s inside”, personalized recommendations |
| Reward | 给用户回报 | points, coupons, free shipping, badges |

也可以补充伦理角度：

- 不应诱导过度消费。
- 不应制造虚假稀缺。
- 不应隐藏真实价格。

---

### Q3(c)(i) 原题要点

你要为高中数学学生设计 interactive media learning tool。根据课堂设计流程，第一项任务是什么？并讨论该任务在此情境下包含什么。

### Q3(c)(i) 参考答案

第一项任务通常是：

> 明确 purpose / problem / design brief。

在这个项目中，要明确：

- 工具要帮助学生学习什么数学内容。
- 是代数、几何、函数还是考试复习。
- 学生遇到的主要困难是什么。
- 工具目标是教学、练习、测验还是可视化理解。
- 成功标准是什么，例如提高理解、提高练习完成率。

例子：

```text
Purpose: help high school students understand quadratic functions through interactive graphs and step-by-step exercises.
```

### Q3(c)(i) 主要考点

Design process：

- 明确 purpose
- 确定 target audience
- 收集用户需求
- 分析学习目标
- interaction design
- user flow
- wireframe
- storyboard
- prototype

针对高中数学学习工具，应考虑：

- 学生年龄和数学水平。
- 学习困难点。
- 使用设备。
- 课堂 / 自学场景。
- 交互方式：练习题、反馈、提示、可视化。
- 教师或学生需求。

---

---

### Q3(c)(ii) 原题要点

第二项任务是收集目标用户数据。问需要了解什么。

### Q3(c)(ii) 参考答案

需要了解：

- 学生年龄。
- 数学水平。
- 课程大纲。
- 常见学习困难。
- 使用设备：手机、平板、电脑。
- 使用场景：课堂、自学、作业。
- 学习动机。
- 注意力特点。
- 是否需要 accessibility 支持。
- 教师和家长的需求。

收集方法：

- questionnaire
- interview
- observation
- teacher consultation
- analysis of existing learning tools

### Q3(c)(ii) 主要考点

同 Q3(c)(i) 主要考点。

### Q3(c)(iii) 原题要点

第二阶段是 interaction phase。解释它包含什么，以及什么设计技术能支持这个阶段。

### Q3(c)(iii) 参考答案

Interaction phase 关注用户如何与系统互动。

包含：

- 用户流程 user flow。
- 页面之间如何跳转。
- 用户如何选择题目。
- 如何输入答案。
- 如何获得反馈。
- 如何查看提示和解析。
- 如何追踪进度。

支持技术：

- wireframe
- storyboard
- flowchart
- low-fidelity prototype
- interactive prototype

在数学学习工具中，可设计：

```text
Choose topic → Watch example → Try exercise → Get feedback → Retry or continue
```

### Q3(c)(iii) 主要考点

Design process：

- 明确 purpose
- 确定 target audience
- 收集用户需求
- 分析学习目标
- interaction design
- user flow
- wireframe
- storyboard
- prototype

针对高中数学学习工具，应考虑：

- 学生年龄和数学水平。
- 学习困难点。
- 使用设备。
- 课堂 / 自学场景。
- 交互方式：练习题、反馈、提示、可视化。
- 教师或学生需求。

---

## 2024/25 Question 4：Heuristic Evaluation + User Testing

### Q4(a)(i) 原题要点

场景：网站充满太多文字、图片和 pop-ups。问为什么是问题，违反哪个 heuristic，给 severity rating。

### Q4(a)(i) 参考答案

违反：

> UH8 Aesthetic and minimalist design

原因：

- 信息过载。
- 用户难以找到重点。
- pop-ups 干扰任务。
- 页面视觉噪声大。

Severity rating：

```text
3 = major usability problem
```

如果 pop-ups 阻挡核心任务，可给 4。

解决方案：

- 减少不必要信息。
- 分层组织内容。
- 限制 pop-ups。
- 使用清晰视觉层级。
- 增加留白。

### Q4(a)(i) 主要考点

| 场景 | 对应 heuristic |
|---|---|
| 页面混乱 | UH8 Aesthetic and minimalist design |
| 要记住订单号 | UH6 Recognition rather than recall |
| 不能自定义快捷键 / 模板 | UH7 Flexibility and efficiency of use |
| 上传无反馈 | UH1 Visibility of system status |

还要会：

- 解释为什么是问题。
- 给 severity rating 0-4。
- 给解决方案。

---

---

### Q4(a)(ii) 原题要点

场景：电商网站要求用户记住 order number 才能追踪物流。问问题、heuristic、severity 和 solution。

### Q4(a)(ii) 参考答案

违反：

> UH6 Recognition rather than recall

原因：

- 用户被迫记住订单号。
- 增加记忆负担。
- 用户可能丢失订单号。

Severity rating：

```text
3 = major usability problem
```

解决方案：

- 用户登录后显示订单列表。
- 允许通过 email / phone 查询。
- 提供 tracking link。
- 自动保存最近订单。
- 邮件和短信中提供直接追踪入口。

### Q4(a)(ii) 主要考点

同 Q4(a)(i) 主要考点。

### Q4(a)(iii) 原题要点

场景：productivity app 不允许自定义快捷键或创建模板。问问题、heuristic、severity 和 solution。

### Q4(a)(iii) 参考答案

违反：

> UH7 Flexibility and efficiency of use

原因：

- 高级用户无法优化工作流。
- 重复任务效率低。
- 无法适应不同用户习惯。

Severity rating：

```text
2 或 3
```

如果该 app 面向专业用户，可给 3。

解决方案：

- 允许自定义快捷键。
- 提供模板功能。
- 提供最近操作和自动化功能。
- 提供可配置工作区。

### Q4(a)(iii) 主要考点

同 Q4(a)(i) 主要考点。

### Q4(a)(iv) 原题要点

场景：文件上传后没有进度条或确认信息。问问题、heuristic、severity 和 solution。

### Q4(a)(iv) 参考答案

违反：

> UH1 Visibility of system status

原因：

- 用户不知道上传是否开始。
- 用户不知道是否成功。
- 用户可能重复点击 upload。
- 大文件上传时尤其令人焦虑。

Severity rating：

```text
3 = major usability problem
```

解决方案：

- 显示上传进度条。
- 显示百分比。
- 上传成功后显示 confirmation message。
- 上传失败时显示错误原因和 retry 按钮。

### Q4(a)(iv) 主要考点

| 场景 | 对应 heuristic |
|---|---|
| 页面混乱 | UH8 Aesthetic and minimalist design |
| 要记住订单号 | UH6 Recognition rather than recall |
| 不能自定义快捷键 / 模板 | UH7 Flexibility and efficiency of use |
| 上传无反馈 | UH1 Visibility of system status |

还要会：

- 解释为什么是问题。
- 给 severity rating 0-4。
- 给解决方案。

---

### Q4(b)(i) 原题要点

讨论 onsite usability testing 和 remote usability testing 的优缺点。

### Q4(b)(i) 参考答案

#### Onsite testing 优点

- 可以直接观察用户表情、姿势和困惑。
- 测试环境可控。
- 研究者可以即时追问。
- 适合复杂任务或早期原型。

#### Onsite testing 缺点

- 成本高。
- 招募困难。
- 样本量可能较小。
- 用户在实验室中可能表现不自然。

#### Remote testing 优点

- 成本低。
- 可招募更多地区用户。
- 更接近真实使用环境。
- 时间安排灵活。

#### Remote testing 缺点

- 难以观察细微行为。
- 网络和设备问题会干扰测试。
- 研究者控制力较低。
- 用户可能分心。

### Q4(b)(i) 主要考点

#### Onsite testing

优点：

- 观察细节更清楚。
- 能看到表情、姿态、困惑。
- 控制测试环境。

缺点：

- 成本高。
- 样本少。
- 用户可能不自然。

#### Remote testing

优点：

- 成本低。
- 可招募更多用户。
- 更接近真实使用环境。

缺点：

- 控制力低。
- 观察细节少。
- 技术问题可能干扰测试。

#### Card sorting

用于发现用户如何分类信息。

适合：

- 商品分类。
- 菜单结构。
- 用户心智模型。

#### Tree testing

用于验证网站结构是否容易找到目标内容。

适合：

- 测试导航。
- 测试分类是否清晰。
- 发现找不到信息的路径问题。

---

---

### Q4(b)(ii) 原题要点

设计电商网站 information architecture，说明如何用 tree testing 和 card sorting。

### Q4(b)(ii) 参考答案

#### Card sorting

作用：发现用户如何分类信息。

在电商网站中：

- 让用户把商品卡片分组。
- 观察用户如何命名类别。
- 了解用户心智模型。

例子：

```text
用户可能把 “phone case” 放到 Accessories，而不是 Phones。
```

#### Tree testing

作用：验证网站分类结构是否容易导航。

在电商网站中：

- 给用户一个文字版菜单树。
- 要求用户找到指定商品。
- 记录成功率、路径和耗时。

例子：

```text
Task: Find a waterproof hiking jacket.
观察用户是否能通过 Clothing > Outdoor > Jackets 找到。
```

两者区别：

| 方法 | 目的 |
|---|---|
| Card sorting | 建立分类结构 |
| Tree testing | 验证分类结构是否好用 |

### Q4(b)(ii) 主要考点

#### Onsite testing

优点：

- 观察细节更清楚。
- 能看到表情、姿态、困惑。
- 控制测试环境。

缺点：

- 成本高。
- 样本少。
- 用户可能不自然。

#### Remote testing

优点：

- 成本低。
- 可招募更多用户。
- 更接近真实使用环境。

缺点：

- 控制力低。
- 观察细节少。
- 技术问题可能干扰测试。

#### Card sorting

用于发现用户如何分类信息。

适合：

- 商品分类。
- 菜单结构。
- 用户心智模型。

#### Tree testing

用于验证网站结构是否容易找到目标内容。

适合：

- 测试导航。
- 测试分类是否清晰。
- 发现找不到信息的路径问题。

---

# 6. 考前可直接套用的答题模板

> [!important]
> 这一部分不是新的题目，而是把两套 past exams 中反复出现的题型整理成“考试可以直接套”的答案框架。考试时不要只背关键词，要把 **概念 + 题目场景 + 影响 + 改进方案** 写出来。

---

## 6.1 代码纠错题模板：HTML / CSS / JavaScript

代码纠错题通常不是考你写一个完整网站，而是考你能不能发现基础语法错误、连接错误和逻辑错误。

答题顺序可以这样写：

```text
Error 1: ...
Correction: ...
Reason: ...
```

### 常见错误 1：HTML `id` 和 JavaScript 选择器不匹配

如果 JavaScript 写：

```js
document.getElementById("message")
```

那么 HTML 里必须有：

```html
<p id="message"></p>
```

不能写成：

```html
<p class="message"></p>
```

原因：

- `id` 是唯一标识。
- `getElementById()` 只能找 `id`，不能找 `class`。
- 如果找不到元素，后面的 `.innerHTML`、`.style` 等操作可能失败。

考试可写答案：

```text
The JavaScript uses getElementById(), so the HTML element must have a matching id attribute. If the element uses class instead of id, the script cannot find the element.
```

---

### 常见错误 2：CSS 属性拼写错误

英国英语拼法在普通文字中可以用 `colour`，但 CSS 属性名必须用美式拼法：

```css
color: red;
background-color: yellow;
```

错误写法：

```css
colour: red;
background-colour: yellow;
```

考试可写答案：

```text
CSS property names must use the correct spelling. The correct property is color or background-color, not colour or background-colour.
```

---

### 常见错误 3：文本居中写错

正确：

```css
text-align: center;
```

错误：

```css
text-align: centre;
```

原因：

- CSS 关键字也必须用固定英文拼写。
- `center` 是合法值。
- `centre` 不是 CSS 合法值。

---

### 常见错误 4：JavaScript 赋值和比较混淆

赋值：

```js
let isActive = true;
```

比较：

```js
if (isActive == true) {
  ...
}
```

或更推荐：

```js
if (isActive) {
  ...
}
```

错误：

```js
let isActive == true;
```

原因：

- `=` 用于赋值。
- `==` / `===` 用于比较。
- 变量声明时应该使用 `=`.

考试可写答案：

```text
The variable declaration should use the assignment operator =. The operator == is used for comparison, not for assigning a value.
```

---

### 常见错误 5：自增写错

正确：

```js
count++;
```

或：

```js
count = count + 1;
```

错误：

```js
count+;
```

原因：

- `++` 表示增加 1。
- `count+` 是不完整表达式。

---

### 常见错误 6：`<script>` 放置位置

如果脚本需要访问页面元素，常见安全写法是把 `<script>` 放在 `</body>` 前：

```html
<body>
  <button id="btn">Click</button>

  <script>
    const btn = document.getElementById("btn");
  </script>
</body>
```

原因：

- 浏览器从上到下读取 HTML。
- 如果 JS 在元素出现之前运行，可能找不到该元素。
- 放在 body 底部可以确保 HTML 元素已经被加载。

也可以用：

```js
window.onload = function () {
  ...
};
```

或：

```js
document.addEventListener("DOMContentLoaded", function () {
  ...
});
```

---

## 6.2 `var`、`let`、`const` 答题模板

如果题目问 `var` 和 `let` 的区别，可以这样答：

| 关键词 | `var` | `let` |
|---|---|---|
| Scope | function scope | block scope |
| Redeclare | 可以重复声明 | 同一作用域不建议/不能重复声明 |
| Hoisting | 会提升，容易造成混乱 | 也会提升但有 temporal dead zone |
| Modern JS | 较旧写法 | 更推荐 |

考试可写答案：

```text
var has function scope, while let has block scope. This means a variable declared with let only exists inside the block where it is defined, such as inside an if statement or a loop. let is preferred in modern JavaScript because it reduces accidental reuse of variables.
```

如果题目问什么时候用 `const`：

```text
const is used for values that should not be reassigned. It makes the code safer and easier to understand because readers know the variable reference will not change.
```

---

## 6.3 CSS Box Model 计算模板

CSS box model 的总宽度：

```text
total width = content width + left padding + right padding + left border + right border + left margin + right margin
```

总高度：

```text
total height = content height + top padding + bottom padding + top border + bottom border + top margin + bottom margin
```

如果题目给：

```css
width: 300px;
height: 200px;
padding: 5px;
border: 3px solid black;
margin: 1px;
```

则：

```text
Total width = 300 + 5 + 5 + 3 + 3 + 1 + 1 = 318px
Total height = 200 + 5 + 5 + 3 + 3 + 1 + 1 = 218px
```

考试注意：

- `width` 和 `height` 默认只指 content area。
- padding、border、margin 都要加上。
- 如果题目使用 `box-sizing: border-box;`，计算方式会改变。

---

## 6.4 CSS transition / hover 效果模板

如果题目给类似：

```css
.box {
  background-color: blue;
  transition: background-color 1s ease;
}

.box:hover {
  background-color: red;
}
```

答题可以这样写：

```text
When the user moves the mouse over the element, the :hover rule is applied. The background colour changes from blue to red. Because a transition is defined, the change does not happen instantly. Instead, it is animated smoothly over 1 second using the specified timing function.
```

中文理解：

- `:hover`：鼠标悬停时应用的样式。
- `transition-property`：哪一个属性要动画。
- `transition-duration`：动画持续多久。
- `transition-timing-function`：动画速度变化方式。
- `ease`：开始和结束较慢，中间较快。

如果题目问为什么 transition 有用：

```text
It improves user experience by making visual changes smoother and more understandable. It also provides feedback that the element is interactive.
```

---

## 6.5 CSS animation 答题模板

CSS animation 通常由两部分组成：

1. `@keyframes` 定义动画过程。
2. `animation` 属性把动画应用到元素上。

例子：

```css
@keyframes moveCloud {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(200px);
  }
}

.cloud {
  animation: moveCloud 5s linear infinite;
}
```

考试可写答案：

```text
The @keyframes rule defines the stages of the animation. The animation property then applies this keyframe sequence to an element, controlling the duration, timing function, delay, repetition and direction.
```

常见属性：

| 属性 | 意思 |
|---|---|
| `animation-name` | 使用哪个 keyframes |
| `animation-duration` | 动画持续时间 |
| `animation-timing-function` | 速度曲线 |
| `animation-delay` | 延迟多久开始 |
| `animation-iteration-count` | 播放次数 |
| `animation-direction` | 是否反向播放 |

---

## 6.6 SVG 画图题模板

SVG 是用 XML-like 标签画矢量图。考试中常见标签：

| 标签 | 用途 | 常见属性 |
|---|---|---|
| `<rect>` | 矩形 | `x`, `y`, `width`, `height`, `fill` |
| `<circle>` | 圆形 | `cx`, `cy`, `r`, `fill` |
| `<ellipse>` | 椭圆 | `cx`, `cy`, `rx`, `ry` |
| `<line>` | 直线 | `x1`, `y1`, `x2`, `y2`, `stroke` |
| `<polyline>` | 多段折线 | `points`, `fill`, `stroke` |
| `<polygon>` | 闭合多边形 | `points`, `fill`, `stroke` |
| `<path>` | 复杂路径 | `d`, `fill`, `stroke` |
| `<text>` | 文字 | `x`, `y`, `font-size` |

### `<line>` 和 `<path>` 区别

`<line>` 只能画一条直线：

```html
<line x1="10" y1="10" x2="100" y2="10" stroke="black" />
```

`<path>` 可以画直线、曲线、复杂形状：

```html
<path d="M10 10 L100 10 L100 80 Z" fill="red" />
```

考试可写：

```text
The line element is used for a single straight line between two points. The path element is more flexible because it can describe complex shapes using commands such as M, L, C and Z.
```

### `polygon` 和 `polyline` 区别

`polygon` 会自动闭合：

```html
<polygon points="50,10 90,80 10,80" fill="orange" />
```

`polyline` 不会自动闭合：

```html
<polyline points="10,10 50,50 90,10" fill="none" stroke="black" />
```

考试可写：

```text
polygon creates a closed shape, while polyline creates a connected series of line segments that does not automatically close.
```

---

## 6.7 AI prompt for SVG / CSS animation 模板

如果题目要求写一个 prompt，让 AI 生成一个 sunset animation，可以按这个结构写：

```text
Create an SVG and CSS animation of a sunset scene.
The scene should include the sun, sky, clouds, sea and horizon.
Use SVG shapes such as circle, rect, polygon and path.
Animate the sun moving down slowly behind the horizon.
Animate the sky colour changing from light blue to orange and then dark purple.
Use CSS keyframes and make the animation smooth and looping.
Keep the code simple, readable and suitable for an HTML page.
```

好的 prompt 要包括：

1. 要生成什么。
2. 需要哪些视觉元素。
3. 用什么技术。
4. 动画怎么变化。
5. 风格和限制。
6. 输出格式。

考试可写：

```text
A good AI prompt should specify the visual goal, the required elements, the technologies to use, the desired animation behaviour, and any constraints such as readability or responsiveness.
```

---

## 6.8 CSS combinator selectors 模板

常见 combinators：

| Selector | 名称 | 含义 |
|---|---|---|
| `A B` | descendant | A 里面所有 B 后代 |
| `A > B` | child | A 的直接子元素 B |
| `A + B` | adjacent sibling | A 后面紧挨着的第一个 B |
| `A ~ B` | general sibling | A 后面所有同级 B |

例子：

```css
nav ul li {
  color: blue;
}
```

意思：

```text
Select all li elements that are inside a ul that is inside a nav.
```

如果题目给嵌套列表，要先看层级：

```html
<ul class="menu">
  <li>Home</li>
  <li>Products
    <ul>
      <li>Phones</li>
      <li>Laptops</li>
    </ul>
  </li>
</ul>
```

选择所有后代 li：

```css
.menu li { ... }
```

只选择第一层 li：

```css
.menu > li { ... }
```

---

## 6.9 UI component / form design 模板

表单设计题通常考：

- 选择合适 input type。
- label 是否清楚。
- placeholder 是否合理。
- validation 是否及时。
- error message 是否具体。
- 是否考虑 accessibility。

### 答题框架

```text
The form should use suitable UI components for each type of data.
Each input should have a clear label.
Required fields should be marked clearly.
The interface should provide validation and helpful error messages.
The form should be accessible, for example by supporting keyboard navigation and screen readers.
```

### 常见字段对应组件

| 信息类型 | 推荐组件 |
|---|---|
| 姓名 | text input |
| Email | `<input type="email">` |
| 电话 | `<input type="tel">` |
| 日期 | date picker |
| 地址 | textarea 或多行地址字段 |
| 性别 / 单选 | radio buttons |
| 多选偏好 | checkboxes |
| 国家 / 地区 | dropdown |
| 密码 | password input |
| 文件上传 | file input |

### 为什么电话用 `type="tel"`

考试可写：

```text
The telephone field should use input type="tel" because mobile devices can display a telephone keypad. This makes input faster and reduces typing errors.
```

中文理解：

- 手机会弹出数字键盘。
- 用户输入更快。
- 减少输错。
- 更符合移动端使用场景。

---

## 6.10 Inclusive design 模板

Inclusive design 的核心不是只为“平均用户”设计，而是让不同能力、不同设备、不同环境的用户都能使用。

考试答题结构：

```text
Inclusive design means designing products that can be used by as many people as possible, including users with disabilities or different needs. In this scenario, the design should consider users with visual, hearing, motor or cognitive impairments.
```

### Colour-blindness

问题：

- 用户可能无法区分红色和绿色。
- 如果只用颜色表达状态，会造成误解。

改进：

- 不只依赖颜色。
- 加图标、文字、形状。
- 使用高对比度。

可写答案：

```text
For colour-blind users, the interface should not rely on colour alone. Important information should also be shown using text labels, icons or patterns.
```

### Impaired vision

问题：

- 字太小看不清。
- 对比度低。
- 图片没有替代文本。

改进：

- 大字号。
- 高对比度。
- 支持放大。
- 图片加 `alt`。
- 支持 screen reader。

可写答案：

```text
For users with impaired vision, the interface should provide large readable text, strong contrast, scalable layout and alternative text for images.
```

### Impaired hearing

问题：

- 如果信息只靠声音，听障用户无法获得。

改进：

- 视频加字幕。
- 声音提示搭配视觉提示。
- 提供文字 transcript。

可写答案：

```text
For users with impaired hearing, audio content should be supported by captions, transcripts and visual feedback.
```

### Dyslexia

问题：

- 阅读速度慢。
- 容易混淆字母。
- 长段落负担大。

改进：

- 清晰字体。
- 短段落。
- 增大行距。
- 左对齐。
- 避免全大写。

可写答案：

```text
For users with dyslexia, the text should be clear, left-aligned, well-spaced and broken into short sections. The design should avoid dense paragraphs and all-capital text.
```

---

## 6.11 UXD 情绪题模板：visceral / behavioural / reflective

这类题通常要求解释三层用户情绪，并结合具体 app 举例。

| 层次 | 关注点 | 例子 |
|---|---|---|
| Visceral | 第一眼、本能感受 | 颜色、声音、图片、动效 |
| Behavioural | 使用过程是否顺畅 | 操作简单、反馈清楚、任务效率 |
| Reflective | 使用后的意义和价值 | 自我认同、成就感、长期价值 |

考试可写：

```text
Visceral emotion is the user's immediate first impression of the product, such as whether it looks calm, exciting or attractive. Behavioural emotion comes from using the product, for example whether the interaction is smooth and easy. Reflective emotion is the user's longer-term evaluation, such as whether the product supports their identity, goals or values.
```

如果题目是 meditation app：

```text
A meditation app can create visceral emotion through calm colours, natural images and soft sounds. It can create behavioural emotion through simple navigation, clear timers and smooth guidance. It can create reflective emotion by helping users feel healthier, calmer and more disciplined over time.
```

---

## 6.12 Hyperbolic discounting 模板

定义：

```text
Hyperbolic discounting means people tend to prefer smaller immediate rewards over larger future rewards. They give too much weight to the present and discount future consequences.
```

电商例子：

- 限时折扣。
- 倒计时。
- “Only 2 left”。
- 立即下单免运费。
- 今天买，今天送达。

考试可写：

```text
An e-commerce site can use hyperbolic discounting by offering immediate benefits, such as a limited-time discount or free delivery if the user buys now. This makes the immediate reward more attractive and encourages quick purchase decisions.
```

伦理问题：

```text
However, this can be unethical if it manipulates users, creates false urgency or encourages impulsive spending. The design should be transparent and should not use fake scarcity or misleading countdowns.
```

---

## 6.13 Gestalt law of proximity 模板

定义：

```text
The law of proximity means that elements placed close together are perceived as belonging to the same group.
```

表单例子：

```text
Labels should be placed close to their corresponding input fields. Related fields, such as address line, city and postcode, should be grouped together. This helps users understand the structure of the form and reduces errors.
```

可画 before / after：

```text
Before:
Name:                 [        ]

Email:
                      [        ]

After:
Name:  [        ]
Email: [        ]
```

重点：

- label 靠近 input。
- 相关字段分组。
- 不相关字段留出距离。
- 用 spacing 创造结构。

---

## 6.14 Curiosity and reward 模板

如果题目问 curiosity 和 reward 如何提高学习/应用体验：

### Curiosity

```text
Curiosity motivates users by making them want to explore, discover or find out what happens next.
```

设计方法：

- 解锁新内容。
- 提供小挑战。
- 提出问题。
- 展示未知内容预览。
- 允许探索。

### Reward

```text
Reward motivates users by giving positive feedback after they complete an action or achieve a goal.
```

设计方法：

- badges。
- points。
- progress bar。
- levels。
- encouraging feedback。

考试可写：

```text
Curiosity can keep users engaged by encouraging exploration and discovery. Reward can reinforce desired behaviour by giving users feedback, points, badges or a sense of progress after completing tasks.
```

注意：

- reward 不一定是钱。
- 学习工具中 reward 可以是进度、鼓励、徽章、解锁下一关。

---

## 6.15 UI critique 题模板

题目给一个很乱的页面截图，让你用 UI principles 分析时，可以按这个模板：

```text
The interface has a problem with [principle].
This affects users because [impact].
It can be improved by [solution].
```

常用原则：

| 原则 | 常见问题 | 改进 |
|---|---|---|
| Visual hierarchy | 不知道先看哪里 | 突出标题、价格、CTA |
| Consistency | 字体/按钮/卡片不统一 | 使用统一组件 |
| Proximity | 相关内容没分组 | 把相关信息放近 |
| Alignment | 元素不对齐 | 使用网格布局 |
| Aesthetic/minimalist | 信息太多 | 删除不必要元素 |
| Readability | 字太小/对比低 | 增大字号和对比度 |
| Feedback | 点击后没反应 | 显示 loading/confirmation |
| Affordance | 不知道哪里能点 | 按钮样式更明显 |

考试可以写四点，每点都用：

```text
Principle:
Problem:
Impact:
Improvement:
```

---

## 6.16 Nielsen Heuristics 十条速记

| 编号 | 英文名 | 中文理解 | 关键词 |
|---|---|---|---|
| UH1 | Visibility of system status | 系统状态可见 | loading、progress、confirmation |
| UH2 | Match between system and real world | 符合现实世界 | 用户熟悉语言、现实映射 |
| UH3 | User control and freedom | 用户控制与自由 | undo、back、cancel |
| UH4 | Consistency and standards | 一致性和标准 | 相同按钮相同功能 |
| UH5 | Error prevention | 防止错误 | confirm、constraints、disable invalid actions |
| UH6 | Recognition rather than recall | 识别优于回忆 | 菜单、提示、可见选项 |
| UH7 | Flexibility and efficiency of use | 灵活高效 | shortcuts、customisation |
| UH8 | Aesthetic and minimalist design | 美观简洁 | 减少无关信息 |
| UH9 | Help users recognise, diagnose, and recover from errors | 帮助识别和恢复错误 | clear error message |
| UH10 | Help and documentation | 帮助文档 | FAQ、tutorial、help |

### Heuristic evaluation 标准作答格式

```text
This violates UH[number]: [name].
It is a problem because ...
The severity rating is ... because ...
To improve it, the system should ...
```

### Severity rating 常用写法

| 分数 | 含义 | 什么时候用 |
|---|---|---|
| 0 | not a problem | 不是问题 |
| 1 | cosmetic problem | 小问题，不影响完成任务 |
| 2 | minor usability problem | 有影响，但不严重 |
| 3 | major usability problem | 明显影响任务，需要修 |
| 4 | usability catastrophe | 用户无法完成核心任务 |

考试建议：

- 一般严重问题写 3。
- 如果导致核心功能完全不能用，写 4。
- 如果只是视觉不舒服但不影响任务，写 1 或 2。

---

## 6.17 常见 heuristic 场景对照表

| 场景 | 最可能 heuristic | 理由 |
|---|---|---|
| submit 和 reset 按钮太近 | UH5 Error prevention | 容易误点造成数据丢失 |
| VR 控制和现实动作无关 | UH2 Match real world | 不符合用户现实经验 |
| 高级功能只能靠记快捷键 | UH6 Recognition rather than recall | 用户必须记忆 |
| 同时提供快捷键和菜单 | UH7 Flexibility and efficiency | 新手和专家都能用 |
| 上传文件没有进度 | UH1 Visibility of system status | 用户不知道发生了什么 |
| 页面塞满广告和无关内容 | UH8 Aesthetic and minimalist design | 干扰核心任务 |
| 错误只显示 Error 403 | UH9 Help recover from errors | 用户不知道怎么修 |
| 按钮在不同页面含义不同 | UH4 Consistency and standards | 不一致导致误解 |
| 没有撤销删除 | UH3 User control and freedom | 用户不能恢复 |
| 功能复杂但没有说明 | UH10 Help and documentation | 用户缺少帮助 |

---

## 6.18 Onsite testing vs Remote testing 模板

### Onsite testing

优点：

- 可以观察表情、肢体语言、犹豫。
- 环境可控。
- 研究者可以追问。
- 适合早期原型和复杂任务。

缺点：

- 成本高。
- 招募困难。
- 用户可能因为被观察而不自然。
- 样本量可能小。

考试可写：

```text
Onsite testing allows researchers to observe users directly, including facial expressions, hesitation and body language. However, it is more expensive and less natural because users are in a controlled environment.
```

### Remote testing

优点：

- 成本低。
- 可以招募更多地区用户。
- 更接近真实使用环境。
- 时间安排灵活。

缺点：

- 难观察细节。
- 网络和设备问题会干扰。
- 研究者控制力较低。
- 用户可能分心。

考试可写：

```text
Remote testing is cheaper and can reach a wider range of users in their natural environment. However, it gives researchers less control and makes it harder to observe subtle behaviour.
```

---

## 6.19 Card sorting vs Tree testing 模板

### Card sorting

用途：

```text
Card sorting is used to understand how users group and label information.
```

适合阶段：

- 设计信息架构之前。
- 想知道用户如何分类。
- 想设计菜单结构。

电商例子：

```text
Users are given product cards such as phones, laptop cases and chargers. They group them into categories and name the groups. This helps designers understand users' mental models.
```

### Tree testing

用途：

```text
Tree testing is used to evaluate whether an existing information structure is easy to navigate.
```

适合阶段：

- 已经有菜单结构之后。
- 想测试用户能否找到内容。

电商例子：

```text
Users are asked to find a waterproof hiking jacket in a text-only category tree. The designer records whether they choose the correct path, how long they take and where they get lost.
```

### 一句话区分

```text
Card sorting helps create the structure; tree testing checks whether the structure works.
```

---

# 7. 两套 Past Exams 逐题速背版

这一部分用于考前最后快速扫一遍。详细答案看上面的第 7 部分。

---

## 7.1 2023/24 速背

| 题号 | 题型 | 必背答案核心 |
|---|---|---|
| Q1(a) | HTML/JS 纠错 | `id` 与 `getElementById()` 匹配；script 放置；函数名/属性名拼写 |
| Q1(b) | Box model | 总尺寸 = content + padding + border + margin |
| Q1(c) | Transition | hover 触发样式变化，transition 让变化平滑 |
| Q1(d) | SVG | 用 `rect`、`polygon`、`line`、`circle`、`path` 组合画图 |
| Q2(a) | Usability attribute | 广告影响 efficiency 和 satisfaction，可能影响利润 |
| Q2(b) | Mobile layout | list、grid、tab、master-detail，各自适合不同内容 |
| Q2(c) | Navigation | breadcrumb 帮助用户知道当前位置和返回路径 |
| Q2(d) | Font-size UI | slider/buttons + preview + accessibility |
| Q3(a) | Emotion | visceral 第一印象，behavioural 使用体验，reflective 长期价值 |
| Q3(b) | Hyperbolic discounting | 即时奖励促进购买，但要避免操纵 |
| Q3(c) | Colour association | built-in、cultural、work association |
| Q3(d) | Dyslexia | 清晰字体、短段落、行距、左对齐、避免全大写 |
| Q4(a) | Mind map | 早期 brainstorming / idea generation，用于发散和整理 |
| Q4(b) | Heuristic | 根据场景判断 UH，并写 severity + reason + solution |

---

## 7.2 2024/25 速背

| 题号 | 题型 | 必背答案核心 |
|---|---|---|
| Q1(a)(i) | 代码纠错 | `background-color`、`color`、`center`、`=`、`++` 等 |
| Q1(a)(ii) | `<title>` | 浏览器标签页标题，也有助于识别页面 |
| Q1(a)(iii) | `var` vs `let` | `var` function scope，`let` block scope |
| Q1(a)(iv) | CSS 类型 | inline、internal、external 的位置、优缺点和适用场景 |
| Q1(a)(v) | comments | HTML `<!-- -->`，CSS/JS `/* */`，JS `//` |
| Q1(b) | AI prompt | 目标、元素、技术、动画行为、输出格式 |
| Q1(c) | CSS combinators | descendant、child、adjacent sibling、general sibling |
| Q2(a) | Pharmacy form | 选择合适 input type，label，validation，accessibility |
| Q2(b) | Inclusive design | colour-blindness、vision、hearing，对应设计改进 |
| Q2(c) | UI critique | hierarchy、consistency、proximity、minimalism |
| Q3(a) | Gestalt proximity | 靠近的元素被看成一组，表单 label 靠近 input |
| Q3(b) | Curiosity/reward | 探索动机 + 反馈奖励，提高参与度 |
| Q3(c) | Design process | 需求、用户、原型、测试、迭代 |
| Q4(a) | Heuristics | UH8、UH6、UH7、UH1 等场景判断 |
| Q4(b) | User testing / IA | onsite vs remote；card sorting vs tree testing |

---

# 8. 考试答题拿分技巧

## 8.1 每道理论题尽量写四层

不要只写定义。按这个结构写更容易拿分：

```text
1. Definition: 这个概念是什么意思。
2. Scenario: 它在题目场景中怎么体现。
3. Impact: 它对用户有什么影响。
4. Improvement/example: 应该如何改进，或举一个具体例子。
```

例子：

```text
Visibility of system status means the system should keep users informed about what is happening. In a file upload interface, if there is no progress bar, users do not know whether the upload has started or finished. This can cause confusion and repeated clicking. The interface should show a progress bar, percentage and success message.
```

---

## 8.2 如果不确定 heuristic 编号，先写英文名和理由

如果忘记 UH 编号，不要空着。可以写：

```text
This is related to visibility of system status because the user is not informed about the current progress of the system.
```

编号错可能扣分，但如果概念和理由写对，仍然可能得部分分。

---

## 8.3 设计题不要只说“make it better”

低分答案：

```text
Make the page better and easier to use.
```

高分答案：

```text
Increase the font size, group related product information into cards, use a consistent button style, and highlight the main call-to-action so that users can find and purchase products more efficiently.
```

区别：

- 高分答案具体。
- 高分答案说明改什么。
- 高分答案说明为什么有用。

---

## 8.4 代码题写原因，不只是写改正

低分：

```text
Change colour to color.
```

更好：

```text
Change colour to color because CSS property names use the standard spelling color. The incorrect property will be ignored by the browser.
```

---

## 8.5 画图题和 UI 题可以用文字补解释

如果 SVG / UI sketch 画得不完美，要在旁边写清楚：

```text
The rectangle represents the house body.
The polygon represents the roof.
The circle represents the sun.
The line elements represent the ground and window frames.
```

这样阅卷老师更容易看出你的设计意图。

---

## 8.6 最后 10 分钟检查清单

- 代码题：有没有拼写错误？
- CSS：是不是 `color`、`background-color`、`center`？
- JS：是不是把 `=` 和 `==` 混了？
- HTML：`id` 是否匹配？
- Heuristic：有没有写 reason、severity、solution？
- 设计题：有没有结合题目场景？
- Inclusive design：有没有说具体 impairment 和具体改进？
- User testing：有没有写优点和缺点？
- IA：有没有区分 card sorting 和 tree testing？
