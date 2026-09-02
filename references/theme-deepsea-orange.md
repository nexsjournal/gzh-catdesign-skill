# 公众号排版组件库 —— 深海橙光（Bright Orange × Cool Blue）

> **使用说明**：本组件库为「深海橙光」主题。所有组件使用**内联样式**，可直接复制粘贴到微信公众号编辑器。
>
> **设计理念**：以**亮橙**为主色（温暖、有能量、聚焦），以**深黑**为文字主色（沉稳清晰），提亮蓝（#245688）做标签/英文小字点缀，与橙形成冷暖对比。整体是"暖橙主导 + 蓝灰理性文字"的编辑风：橙色负责线条 / 编号 / 标签 / 分割线圆点 / 首尾大色块的活力，深黑负责标题与金句的分量，浅橙底承载卡片与引用。适合科技、深度分析、观点、评测、专业品牌类文章。
>
> **公众号平台限制须知**：
> - ❌ 不支持 `<style>`/`<script>`、CSS class/id/`<div>`、`position:fixed/absolute/sticky`、`float`、`@media`/`@keyframes`、`display:grid`、CSS 变量 `var(--x)`
> - ✅ 支持内联 `style`、`display:flex`（有限）、`linear-gradient`、`border-radius`、`box-shadow`、`position:relative`、`<section>/<p>/<span>/<strong>/<img>/<h3>` 等基础标签
> - font-size ≤ 24px；正文强调用橙色下划线 / 左竖条 / 小标签，**不用四周虚线框**（dashed）
>
> **WeChat 兼容铁律**（本主题组件全部已按此写好，改动时必须遵守）：
> - 所有"装饰性空元素"（细线分割线、END 短线、编号旁装饰、数据卡分隔、时间线竖线）**必须在内部放 `<span leaf=""><br></span>` 占位**，否则微信会剥掉样式
> - **不要把 `font-size`/`border-bottom` 打在 `<strong>` 上**，也不要在同一个 `<p>` 里混多个不同 `font-size`——微信会自动"纠正"。正确做法：拆成多个 `<p>`，每个 `<p>` 只有一个字号；高亮样式统一挂在外层 `<span>` 上
> - 不用 `position:absolute` 做划线/高亮，删除线用 `text-decoration:line-through`
> - 结构化区域（引言卡署名、图片说明、编号旁标签）没有内容时**整块删掉**，不留空 section
> - **大色块卡片（引言卡 / 签名区）不要加 `box-shadow`**——公众号里投影易发灰发脏，用纯色块 + 圆角即可

---

## 设计变量速查表

```
亮橙（主色）：      #F0691C（下划线 / 编号 / 竖条 / 标签实底 / 分割线圆点）
深橙（数字）：      #E8600C（数据大数字 / 看点编号，饱和干净、不偏棕）
浅橙底：            #FFF3E8（卡片 / 引用 / 提示浅底）
更浅橙底：          #FFF8F0（更浅的卡片底，正文底保持纯白）
深黑（标题/重字）：  #1C1F24（标题 / 金句 / 下划线内字 / 锚点实底 / 签名区底色）
主蓝（辅助强调）：   #245688
正文色：            #33506B（深蓝灰，正文主字，比浅灰更沉稳）
辅助文字色：        #8FA6B8（署名 / 说明 / 编号小字）
次级文字色：        #55708A（说明 / 次级，深蓝灰）
暖细线：            #F2E2D0（分割线 / 边框）
荧光高亮：          #FFE1C7
纯白底：            #FFFFFF
正文字号：          15px（不可改）
行高：              1.8
字间距：            0.3px
最大宽度：          677px
内容区边距：        0 10px（左右各 10px）
章节间距：          56px（后续章节 margin-top）
```

字体栈：`-apple-system,BlinkMacSystemFont,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif`

---

## 组件 1 全局容器

```html
<section style="max-width:677px;margin:0 auto;background:#FFFFFF;font-family:-apple-system,BlinkMacSystemFont,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif;color:#33506B;line-height:1.8;letter-spacing:0.3px;overflow-x:hidden;">

  <!-- 所有组件放在这里 -->

</section>
```

---

## 组件 2 开头引言卡片（白卡 + 橙左竖条 + 大号橙引号，无投影）

> **文案策略（先读，比代码重要）**：
> - 引言卡金句和公众号外标题是**两层**，视角要错开——外标题卖"为什么点开"，引言卡卖"核心观点是什么"
> - 已知外标题时，金句**禁止原样复述**其核心关键词；从文章第一段或核心论点提炼一句有张力的判断句
> - 右下署名按文章实际作者填，未知则整行删掉，**不要固定写"甲木"**
> - 白底卡片 + 左侧 5px 橙竖条 + 大号橙色 `「」` 引号，金句用**深黑**大字，点睛词用**橙下划线**；**不加投影**

```html
<section style="margin:10px 10px 40px;background:#FFFFFF;border:1px solid #F2E2D0;border-left:5px solid #F0691C;border-radius:12px;padding:30px 26px 26px;position:relative;">
  <p style="margin:0 0 16px;font-size:11px;color:#F0691C;font-weight:700;letter-spacing:3px;">
    <span leaf="">QUOTE</span>
  </p>
  <p style="margin:0;font-size:19px;font-weight:700;color:#1C1F24;line-height:1.75;letter-spacing:0.5px;">
    <span style="color:#F0691C;font-size:30px;font-weight:900;line-height:1;vertical-align:-6px;">「</span>
    <span leaf="">{{金句前段}}</span>
    <span style="border-bottom:2px solid #F0691C;"><span leaf="">{{点睛关键词}}</span></span>
    <span leaf="">{{金句收尾}}</span>
    <span style="color:#F0691C;font-size:30px;font-weight:900;line-height:1;vertical-align:-4px;">」</span>
  </p>
  <p style="text-align:right;font-size:12px;color:#9AA6B2;margin:18px 0 0;letter-spacing:1px;">
    <span style="display:inline-block;width:22px;height:2px;background:#F0691C;vertical-align:middle;margin-right:8px;"><span leaf=""><br></span></span><span leaf="">{{作者名，未知则删整行}}</span>
  </p>
</section>
```

> **注意**：深黑金句 + 橙色 `「」` 引号 + 橙色点睛下划线，白底干净有设计感、**不加投影**。若金句里没有特别想点睛的词，去掉中间的下划线 span、整句深黑即可。</section>
```

> **注意**：点睛词用白下划线（`border-bottom:2px solid #FFFFFF`）；若无特别想点睛的词，全部白字不加下划线即可。橙底上不要用橙色线条/字（会看不见）。

---

## 组件 3 前言导读区域（本文看点，三列浅橙目录卡）

> 3 个及以上章节时生成。暖浅橙底 + 橙顶线 + 大号橙编号 + 暖细线分隔 + 深黑标题。展示**精选 3 个核心看点**，不是全量章节列表。

```html
<section style="padding:0 10px 40px;">
  <section style="display:flex;align-items:center;margin:0 0 16px;">
    <span style="display:inline-block;width:4px;height:14px;background:#F0691C;border-radius:2px;margin-right:8px;vertical-align:middle;"><span leaf=""><br></span></span>
    <span style="font-size:12px;font-weight:800;color:#1C1F24;letter-spacing:2px;vertical-align:middle;"><span leaf="">本文看点</span></span>
    <span style="font-size:10px;font-weight:600;color:#245688;letter-spacing:3px;margin-left:10px;vertical-align:middle;text-transform:uppercase;"><span leaf="">HIGHLIGHTS</span></span>
  </section>
  <section style="display:flex;justify-content:space-between;">
    <section style="flex:1;background:#FFF8F0;border-top:3px solid #F0691C;border-radius:0 0 10px 10px;padding:16px 14px 18px;margin-right:8px;">
      <p style="font-size:15px;font-weight:900;color:#F0691C;margin:0 0 10px;letter-spacing:1px;"><span leaf="">01</span></p>
      <section style="height:1px;background:#F2E2D0;margin:0 0 10px;"><span leaf=""><br></span></section>
      <p style="font-size:13px;font-weight:800;color:#1C1F24;margin:0;line-height:1.5;"><span leaf=">{{看点一}}</span></p>
    </section>
    <section style="flex:1;background:#FFF8F0;border-top:3px solid #F0691C;border-radius:0 0 10px 10px;padding:16px 14px 18px;margin-right:8px;">
      <p style="font-size:15px;font-weight:900;color:#F0691C;margin:0 0 10px;letter-spacing:1px;"><span leaf="">02</span></p>
      <section style="height:1px;background:#F2E2D0;margin:0 0 10px;"><span leaf=""><br></span></section>
      <p style="font-size:13px;font-weight:800;color:#1C1F24;margin:0;line-height:1.5;"><span leaf=">{{看点二}}</span></p>
    </section>
    <section style="flex:1;background:#FFF8F0;border-top:3px solid #F0691C;border-radius:0 0 10px 10px;padding:16px 14px 18px;">
      <p style="font-size:15px;font-weight:900;color:#F0691C;margin:0 0 10px;letter-spacing:1px;"><span leaf="">03</span></p>
      <section style="height:1px;background:#F2E2D0;margin:0 0 10px;"><span leaf=""><br></span></section>
      <p style="font-size:13px;font-weight:800;color:#1C1F24;margin:0;line-height:1.5;"><span leaf=">{{看点三}}</span></p>
    </section>
  </section>
</section>
```

---

## 组件 4 章节分割线（暖细线 + 居中橙圆点）

> 1px 暖细线，中间一个橙色小圆点做视觉节奏点。两侧留白建立呼吸感。

```html
<section style="padding:0 10px;">
  <section style="display:flex;align-items:center;justify-content:center;margin:0;">
    <span style="height:1px;width:56px;background:#F2E2D0;margin-right:12px;"><span leaf=""><br></span></span>
    <span style="width:8px;height:8px;background:#F0691C;border-radius:50%;margin-right:12px;"><span leaf=""><br></span></span>
    <span style="height:1px;width:56px;background:#F2E2D0;"><span leaf=""><br></span></span>
  </section>
</section>
```

> 若希望更干净（不想要橙色圆点），把中间圆点背景改 `#F2E2D0` 即可（装饰性圆点，不算锚点配额）。

---

## 组件 5 章节标题（橙色大编号 + 标题 + 细线）

> 核心特征：大号亮橙编号（视觉锚）+ 蓝色英文小标签 + 深黑标题 + 底部暖细线。第一章 `margin-top:16px`，后续章节 `margin-top:56px`。

```html
<section style="margin-top:56px;margin-bottom:32px;padding:0 10px;">
  <section style="position:relative;padding-bottom:20px;border-bottom:1px solid #F2E2D0;">
    <p style="font-size:46px;font-weight:900;color:#F0691C;margin:0;line-height:1;letter-spacing:-2px;">
      <span leaf="">01</span>
    </p>
    <section style="margin-top:-8px;">
      <p style="font-size:10px;color:#245688;font-weight:600;letter-spacing:3px;margin:0 0 6px;text-transform:uppercase;">
        <span leaf="">{{ENGLISH TAG}}</span>
      </p>
      <h3 style="font-size:20px;font-weight:800;color:#1C1F24;margin:0;letter-spacing:0.5px;line-height:1.4;">
        <span leaf="">{{中文章节标题}}</span>
      </h3>
    </section>
  </section>

  <!-- 本章节正文内容放在这里 -->

</section>
```

**结语章节变体**（编号用 `∞` 替代数字，英文标签用 `THE END` / `EPILOGUE`）：

```html
<p style="font-size:46px;font-weight:900;color:#F0691C;margin:0;line-height:1;letter-spacing:-2px;">
  <span leaf="">∞</span>
</p>
```

> **说明**：此处 `position:relative` 在微信公众号被允许（仅 fixed/absolute/sticky 被禁）。

---

## 组件 6 正文段落

> **关键规则**：每段主动识别 1~3 个关键短语，用**橙色下划线（7d）**标记——这是本风格的核心视觉特征，让读者快速扫到每段重点。

**基础段落**：

```html
<p style="margin-bottom:22px;font-size:15px;line-height:1.8;text-align:justify;color:#33506B;letter-spacing:0.3px;">
  <span leaf="">{{正文内容}}</span>
</p>
```

**带关键词下划线标记的段落**（推荐默认）：

```html
<p style="margin-bottom:22px;font-size:15px;line-height:1.8;text-align:justify;color:#33506B;letter-spacing:0.3px;">
  <span leaf="">{{前半句}}</span>
  <span style="border-bottom:2px solid #F0691C;font-weight:600;color:#1C1F24;"><span leaf="">{{需要强调的关键短语}}</span></span>
  <span leaf="">{{后半句}}</span>
</p>
```

**标记原则**：每段选 1~3 个关键短语（4~15 字）加下划线，不要整段都标；优先标核心观点、结论判断、关键数据、专有名词；无重点的段落可不标。

---

## 组件 6b 子标题（`###` 小节标题）

> `###` 子标题用橙色左竖条 + 深黑标题，**不套用组件 5 的大编号章节样式**（大编号只给 `##`）。竖条 3px 橙。

```html
<p style="font-size:15px;font-weight:800;color:#1C1F24;margin:28px 0 14px;padding-left:12px;border-left:3px solid #F0691C;line-height:1.4;">
  <span leaf="">{{子标题}}</span>
</p>
```

---

## 组件 7 正文高亮样式（6 种变体 + 使用策略）

> **核心理念**：橙色是主旋律（下划线 / 标签 / 竖条高频用），深黑负责重字与最强反差锚点。
>
> **优先级**：① 7d 橙色下划线（正文默认标记，每段都应考虑）→ ② 7a 深黑加粗为主 → ③ 7b 浅橙底深黑字标签（每篇 2~4 个）→ ④ 7c 浅橙背景（次要）→ ⑤ 7e 荧光笔（偶尔长句强调）→ ⑥ 7f 深黑实底白字（全篇最强内联锚点，总计 ≤3 处）

### 7a. 加粗强调

深黑加粗（默认，绝大部分加粗用这个）：

```html
<strong style="color:#1C1F24;"><span leaf="">深黑加粗强调</span></strong>
```

橙色加粗（次要强调，与橙色主旋律一致）：

```html
<strong style="color:#F0691C;"><span leaf="">橙色加粗</span></strong>
```

### 7b. 浅橙底深黑字标签（核心概念，每篇 2~4 个）

```html
<span style="background:#FFF3E8;color:#1C1F24;padding:2px 7px;border-radius:4px;font-weight:700;font-size:14px;"><span leaf="">关键词标签</span></span>
```

### 7c. 浅橙背景高亮（次要关键词）

```html
<span style="background:#FFF3E8;padding:1px 6px;border-radius:3px;font-weight:600;color:#E8600C;"><span leaf="">浅橙背景关键词</span></span>
```

### 7d. 橙色下划线（最常用，本风格标志性标记）

```html
<span style="border-bottom:2px solid #F0691C;font-weight:600;color:#1C1F24;"><span leaf="">橙色下划线关键词</span></span>
```

### 7e. 荧光笔效果（偶尔用于长句强调，底部 40% 浅橙高亮）

```html
<span style="background:linear-gradient(180deg,transparent 60%,#FFE1C7 60%);font-weight:700;color:#1C1F24;"><span leaf="">荧光笔效果的重要长句</span></span>
```

### 7f. 深黑实底白字（最强内联锚点，全篇 ≤3 处）

```html
<span style="background:#1C1F24;color:#FFFFFF;padding:2px 8px;border-radius:4px;font-weight:700;"><span leaf="">最强锚点词</span></span>
```

### 7g. 行内代码

```html
<span style="background:#FFF3E8;color:#E8600C;padding:2px 6px;border-radius:4px;font-family:'SF Mono',Consolas,Monaco,monospace;font-size:14px;"><span leaf="">code</span></span>
```

---

## 组件 8 引用高亮块（4 种变体）

### 8a. 橙竖条金句引用（视觉焦点最强，核心金句）

> 左侧 4px 橙竖条 + 浅橙底 + 深黑大字，核心金句。

```html
<section style="border-left:4px solid #F0691C;background:#FFF8F0;padding:16px 20px;margin:0 10px 28px;border-radius:0 10px 10px 0;">
  <p style="font-size:16px;font-weight:700;color:#1C1F24;margin:0;line-height:1.7;letter-spacing:0.5px;">
    <span leaf="">「{{核心观点或关键金句}}」</span>
  </p>
</section>
```

### 8b. 浅橙底内容引用块（Prompt / 引用内容）

> 浅橙底 + 顶部橙细线，用于展示 Prompt、引用内容、示例等较长内容。

```html
<section style="background:#FFF3E8;border-top:3px solid #F0691C;padding:20px 22px;margin:0 10px 28px;border-radius:0 0 10px 10px;">
  <p style="font-size:11px;color:#E8600C;margin:0 0 8px;letter-spacing:2px;font-weight:700;">
    <span leaf="">REFERENCE</span>
  </p>
  <p style="font-size:15px;color:#33506B;margin:0;line-height:1.8;text-align:justify;">
    {{引用内容，可含 7d 橙下划线等内联样式}}
  </p>
</section>
```

### 8c. 暖细线竖条轻量旁注（个人吐槽 / 补充说明）

> 极细暖竖条 + 小号文字，用于轻量旁注、作者旁白，不抢主文视觉。

```html
<section style="border-left:2px solid #F2E2D0;padding:12px 0 12px 20px;margin:0 10px 24px;">
  <p style="font-size:13px;color:#8FA6B8;margin:0;line-height:1.8;text-align:justify;">
    <span leaf="">{{轻量旁注内容}}</span>
  </p>
</section>
```

### 8d. 居中金句分隔（章节间的过渡金句）

> 上下 1px 暖细线 + 居中深黑字，用于章节之间的过渡金句。

```html
<p style="font-size:15px;margin:0 10px 24px;text-align:center;color:#1C1F24;font-weight:700;letter-spacing:1px;border-top:1px solid #F2E2D0;border-bottom:1px solid #F2E2D0;padding:14px 10px;">
  <span leaf="">{{居中金句}}</span>
</p>
```

---

## 组件 9 提示 / 警示条（3 种变体）

### 9a. 橙竖条提示条（默认，重要提醒 / 核心结论）

```html
<section style="border-left:4px solid #F0691C;background:#FFF8F0;padding:14px 18px;margin:0 10px 24px;border-radius:0 8px 8px 0;">
  <p style="font-size:14px;font-weight:700;color:#1C1F24;margin:0;line-height:1.8;">
    <span leaf="">{{重要提示或核心结论}}</span>
  </p>
</section>
```

### 9b. 深黑竖条提示条（强调反差，用于最关键提醒）

> 深黑竖条 + 浅橙底，用深黑 vs 浅橙的强对比把注意力拉满。

```html
<section style="border-left:4px solid #1C1F24;background:#FFF3E8;padding:14px 18px;margin:0 10px 24px;border-radius:0 8px 8px 0;">
  <p style="font-size:14px;font-weight:700;color:#1C1F24;margin:0;line-height:1.8;">
    <span leaf="">{{最需要引起注意的内容}}</span>
  </p>
</section>
```

### 9c. 踩坑提示（浅橙底，风险 / 注意事项，内容量大时）

```html
<section style="background:#FFF3E8;border-top:3px solid #1C1F24;padding:18px 22px;margin:0 10px 24px;border-radius:0 0 10px 10px;">
  <p style="font-size:11px;color:#E8600C;margin:0 0 10px;letter-spacing:2px;font-weight:700;">
    <span leaf="">NOTE</span>
  </p>
  <p style="font-size:14px;color:#33506B;margin:0;line-height:1.8;">
    <span leaf="">{{较多的提示内容}}</span>
  </p>
</section>
```

---

## 组件 10 内容标签组（STEP / SKILL / TOOL / CASE）

> 教程用 STEP、盘点用 SKILL/TOOL、案例用 CASE。橙实底编号标签 + 深黑标题。

### 10a. step-label（教程步骤）

```html
<section style="margin-bottom:22px;">
  <section style="display:flex;align-items:center;gap:8px;margin-bottom:10px;">
    <span style="display:inline-block;background:#F0691C;color:#fff;font-size:11px;font-weight:700;padding:2px 9px;border-radius:4px;letter-spacing:0.5px;"><span leaf="">STEP 01</span></span>
    <span style="font-size:15px;font-weight:800;color:#1C1F24;"><span leaf="">{{步骤标题}}</span></span>
  </section>
  <p style="font-size:15px;margin:0 0 16px;color:#33506B;line-height:1.8;text-align:justify;">
    {{步骤内容}}
  </p>
</section>
```

`STEP 01` 可替换为 `SKILL 1`、`TOOL 摄像机`、`CASE 01`（盘点/案例场景）；盘点次级层次可把编号标签底色改浅橙 `#FFF3E8` + 字 `#E8600C`。

### 10b. skill/tool-label（盘点编号标签）

```html
<section style="margin-bottom:22px;">
  <section style="display:flex;align-items:center;gap:8px;margin-bottom:10px;">
    <span style="display:inline-block;background:#F0691C;color:#fff;font-size:11px;font-weight:700;padding:2px 9px;border-radius:4px;letter-spacing:0.5px;"><span leaf="">SKILL 1</span></span>
    <span style="font-size:15px;font-weight:800;color:#1C1F24;"><span leaf="">{{名称}}</span></span>
  </section>
</section>
```

### 10c. tool-card（工具 / 条目说明卡，浅橙卡版）

```html
<section style="border:1px solid #F2E2D0;background:#FFF8F0;padding:16px 20px;margin:0 10px 24px;border-radius:10px;">
  <p style="font-size:14px;color:#33506B;margin:0;line-height:1.8;">
    {{条目说明内容}}
  </p>
</section>
```

---

## 组件 11 列表组件

### 11a. ordered-list（橙圆标数字编号列表）

```html
<section style="margin-bottom:24px;">
  <section style="display:flex;align-items:flex-start;gap:10px;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;width:22px;height:22px;background:#F0691C;color:#fff;font-size:12px;font-weight:700;border-radius:50%;flex-shrink:0;margin-top:2px;"><span leaf="">1</span></span>
    <p style="font-size:15px;color:#33506B;margin:0;line-height:1.8;flex:1;"><span leaf="">{{列表项内容}}</span></p>
  </section>
  <section style="display:flex;align-items:flex-start;gap:10px;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;width:22px;height:22px;background:#F0691C;color:#fff;font-size:12px;font-weight:700;border-radius:50%;flex-shrink:0;margin-top:2px;"><span leaf="">2</span></span>
    <p style="font-size:15px;color:#33506B;margin:0;line-height:1.8;flex:1;"><span leaf="">{{列表项内容}}</span></p>
  </section>
  <section style="display:flex;align-items:flex-start;gap:10px;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;width:22px;height:22px;background:#F0691C;color:#fff;font-size:12px;font-weight:700;border-radius:50%;flex-shrink:0;margin-top:2px;"><span leaf="">3</span></span>
    <p style="font-size:15px;color:#33506B;margin:0;line-height:1.8;flex:1;"><span leaf="">{{列表项内容}}</span></p>
  </section>
</section>
```

### 11b. pill-list（无序要点，药丸标题 + 说明）

```html
<section style="margin-bottom:14px;">
  <p style="margin:0 0 6px;">
    <span style="display:inline-block;font-size:14px;font-weight:700;color:#1C1F24;background:#FFF3E8;padding:3px 10px;border-radius:999px;"><span style="display:inline-block;width:6px;height:6px;background:#F0691C;border-radius:50%;margin-right:5px;vertical-align:middle;"><span leaf=""><br></span></span><span leaf="">{{要点标题}}</span></span>
  </p>
  <p style="font-size:14px;color:#55708A;margin:0;line-height:1.7;text-align:justify;">
    <span leaf="">{{要点说明}}</span>
  </p>
</section>
```

### 11c. timeline（时间线 / 递进脉络，访谈经历、案例演进）

```html
<section style="display:flex;margin-bottom:24px;">
  <section style="display:flex;flex-direction:column;align-items:center;margin-right:16px;flex-shrink:0;">
    <section style="width:14px;height:14px;border-radius:50%;border:3px solid #F0691C;background:#fff;margin-top:4px;"><span leaf=""><br></span></section>
    <section style="width:2px;background:#F2E2D0;flex:1;margin-top:4px;min-height:44px;"><span leaf=""><br></span></section>
  </section>
  <section style="flex:1;padding-bottom:12px;">
    <p style="margin:0 0 6px;font-size:15px;font-weight:800;color:#1C1F24;"><span leaf="">{{节点标题}}</span></p>
    <p style="font-size:15px;margin:0;color:#33506B;line-height:1.8;text-align:justify;">{{节点内容}}</p>
  </section>
</section>
```

最后一个节点去掉竖线段（删掉内层 `width:2px` 的 section）。

---

## 组件 12 数据 / 要点卡片组

### 两列数据卡（浅橙底 + 深橙大数字）

```html
<section style="display:flex;margin:0 10px 28px;">
  <section style="flex:1;background:#FFF3E8;border-radius:12px;padding:22px 16px;margin-right:8px;text-align:center;">
    <p style="font-size:32px;font-weight:900;color:#E8600C;margin:0 0 6px;line-height:1;letter-spacing:-1px;"><span leaf="">{{数字}}</span></p>
    <p style="font-size:11px;color:#55708A;margin:0;letter-spacing:1px;"><span leaf="">{{说明}}</span></p>
  </section>
  <section style="flex:1;background:#FFF3E8;border-radius:12px;padding:22px 16px;text-align:center;">
    <p style="font-size:32px;font-weight:900;color:#E8600C;margin:0 0 6px;line-height:1;letter-spacing:-1px;"><span leaf="">{{数字}}</span></p>
    <p style="font-size:11px;color:#55708A;margin:0;letter-spacing:1px;"><span leaf="">{{说明}}</span></p>
  </section>
</section>
```

### 三列要点卡（橙顶线版）

```html
<section style="display:flex;margin:0 10px 28px;">
  <section style="flex:1;background:#FFF8F0;border-top:3px solid #F0691C;padding:18px 12px 16px;margin-right:8px;border-radius:0 0 10px 10px;">
    <p style="font-size:11px;color:#E8600C;margin:0 0 8px;letter-spacing:1px;font-weight:700;"><span leaf="">01</span></p>
    <p style="font-size:13px;font-weight:700;color:#1C1F24;margin:0 0 6px;line-height:1.4;"><span leaf="">{{要点标题}}</span></p>
    <p style="font-size:12px;color:#55708A;margin:0;line-height:1.6;"><span leaf="">{{要点说明}}</span></p>
  </section>
  <section style="flex:1;background:#FFF8F0;border-top:3px solid #F0691C;padding:18px 12px 16px;margin-right:8px;border-radius:0 0 10px 10px;">
    <p style="font-size:11px;color:#E8600C;margin:0 0 8px;letter-spacing:1px;font-weight:700;"><span leaf="">02</span></p>
    <p style="font-size:13px;font-weight:700;color:#1C1F24;margin:0 0 6px;line-height:1.4;"><span leaf="">{{要点标题}}</span></p>
    <p style="font-size:12px;color:#55708A;margin:0;line-height:1.6;"><span leaf="">{{要点说明}}</span></p>
  </section>
  <section style="flex:1;background:#FFF8F0;border-top:3px solid #F0691C;padding:18px 12px 16px;border-radius:0 0 10px 10px;">
    <p style="font-size:11px;color:#E8600C;margin:0 0 8px;letter-spacing:1px;font-weight:700;"><span leaf="">03</span></p>
    <p style="font-size:13px;font-weight:700;color:#1C1F24;margin:0 0 6px;line-height:1.4;"><span leaf="">{{要点标题}}</span></p>
    <p style="font-size:12px;color:#55708A;margin:0;line-height:1.6;"><span leaf="">{{要点说明}}</span></p>
  </section>
</section>
```

### 表格（真实数据表用）

```html
<section style="margin:0 10px 24px;overflow-x:auto;">
  <table style="width:100%;border-collapse:collapse;font-size:14px;">
    <thead>
      <tr>
        <th style="background:#F0691C;color:#fff;font-weight:700;padding:8px 12px;text-align:left;"><span leaf="">{{列标题}}</span></th>
        <th style="background:#F0691C;color:#fff;font-weight:700;padding:8px 12px;text-align:left;"><span leaf="">{{列标题}}</span></th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="padding:8px 12px;border-bottom:1px solid #F2E2D0;color:#33506B;"><span leaf="">{{内容}}</span></td>
        <td style="padding:8px 12px;border-bottom:1px solid #F2E2D0;color:#33506B;"><span leaf="">{{内容}}</span></td>
      </tr>
      <tr>
        <td style="padding:8px 12px;border-bottom:1px solid #F2E2D0;color:#33506B;background:#FFF8F0;"><span leaf="">{{内容}}</span></td>
        <td style="padding:8px 12px;border-bottom:1px solid #F2E2D0;color:#33506B;background:#FFF8F0;"><span leaf="">{{内容}}</span></td>
      </tr>
    </tbody>
  </table>
</section>
```

---

## 组件 13 标签胶囊

蓝色描边（默认）：

```html
<span style="display:inline-block;border:1px solid #245688;color:#1C1F24;font-size:11px;font-weight:500;padding:2px 10px;border-radius:20px;margin-right:6px;letter-spacing:0.5px;"><span leaf="">标签名</span></span>
```

橙色实底（强调标签）：

```html
<span style="display:inline-block;background:#F0691C;color:#FFFFFF;font-size:11px;font-weight:600;padding:2px 10px;border-radius:20px;margin-right:6px;letter-spacing:0.5px;"><span leaf="">标签名</span></span>
```

深黑描边（点睛标签，用于需要沉稳强调时）：

```html
<span style="display:inline-block;border:1px solid #1C1F24;color:#1C1F24;font-size:11px;font-weight:600;padding:2px 10px;border-radius:20px;margin-right:6px;letter-spacing:0.5px;"><span leaf="">核心标签</span></span>
```

---

## 组件 14 图片容器

> 暖细线 + 圆角图片容器。

```html
<section style="border:1px solid #F2E2D0;border-radius:12px;padding:6px;margin:0 10px 12px;background:#fff;">
  <section style="margin:0;overflow:hidden;border-radius:8px;">
    <span leaf=""><img src="{{图片URL}}" style="max-width:100%;height:auto;display:block;margin:0 auto;"></span>
  </section>
</section>
```

带说明文字时，图片容器 `margin-bottom` 改 `8px`，其后加：

```html
<p style="font-size:12px;color:#8FA6B8;text-align:center;margin:0 10px 28px;letter-spacing:0.5px;">
  <span leaf="">— {{图片说明}}</span>
</p>
```

GIF 动图角标：底色用浅橙 `#FFF3E8`、字色用深橙 `#E8600C`。多行代码块用通用增量库 `common-components.md` 的 1a 深色 / 1b 浅色（1b 左竖条换 `#F0691C`），禁 `white-space:pre`。

---

## 组件 15 END 结尾分割线

> 1px 暖细线 + 居中 "END"。

```html
<section style="padding:0 10px;">
  <section style="text-align:center;margin:0 0 36px;">
    <section style="display:flex;align-items:center;justify-content:center;">
      <span style="height:1px;width:48px;background:#F2E2D0;margin-right:16px;"><span leaf=""><br></span></span>
      <span style="font-size:10px;color:#245688;letter-spacing:4px;font-weight:600;"><span leaf="">END</span></span>
      <span style="height:1px;width:48px;background:#F2E2D0;margin-left:16px;"><span leaf=""><br></span></span>
    </section>
  </section>
</section>
```

---

## 组件 16 尾部作者签名区（深黑卡 + 橙边条收尾，呼应顶部，无投影）

> 深黑大色块收尾，与顶部白卡引言形成"白—黑"首尾对比；左上角橙色短边条 + 橙色 `∎` 收束符做点睛。有个人名片 / 引导图素材才放图，无素材整块删。**不加投影**。

```html
<section style="padding:0 10px 24px;">
  <section style="background:#1C1F24;border-top:4px solid #F0691C;border-radius:12px;padding:28px 26px;position:relative;">
    <p style="margin:0 0 14px;font-size:11px;color:#F0691C;font-weight:700;letter-spacing:3px;">
      <span leaf="">ABOUT</span>
    </p>
    <p style="margin-bottom:16px;font-size:15px;line-height:1.85;color:#E7EAEF;text-align:justify;">
      <span leaf="">我是 {{作者名}}，{{一句话简介，如：热衷于分享 AI 观察与干货}}。</span>
    </p>
    <p style="margin-bottom:0;font-size:15px;line-height:1.85;color:#E7EAEF;text-align:justify;">
      <span leaf="">如果你觉得今天这篇有收获，欢迎</span>
      <strong style="color:#FFFFFF;"><span leaf="">点赞、在看、转发</span></strong>
      <span leaf="">三连，我们下篇见</span>
      <span style="color:#F0691C;font-weight:900;">∎</span>
    </p>
  </section>
</section>
```

> 深黑底上的文字用白 / 亮灰，橙只做边条、标签与收束符，克制而呼应顶部。

---

### 组件 16b 签名区 · 猫 IP 作者卡版（有猫图外链时才用）

> 经典"作者卡"布局：猫头像在左，右侧**名字（大）+ 简介（小）竖向堆叠**，下方一条浅色分隔线，再是互动引导。猫图必须是**外链 URL**。

```html
<section style="padding:0 10px 24px;">
  <section style="background:#1C1F24;border-top:4px solid #F0691C;border-radius:12px;padding:26px 24px;">
    <p style="margin:0 0 18px;font-size:11px;color:#F0691C;font-weight:700;letter-spacing:3px;"><span leaf="">ABOUT</span></p>
    <section style="display:flex;align-items:center;margin-bottom:18px;">
      <span style="flex-shrink:0;margin-right:14px;"><span leaf=""><img src="{{猫图URL}}" style="width:62px;height:62px;border-radius:50%;object-fit:cover;border:2px solid #fff;box-shadow:0 0 0 2px #F0691C;display:block;"></span></span>
      <section style="flex:1;">
        <p style="margin:0 0 4px;font-size:16px;font-weight:800;color:#FFFFFF;letter-spacing:0.5px;"><span leaf="">我是 {{作者名}}</span></p>
        <p style="margin:0;font-size:13px;line-height:1.6;color:#9AA6B2;"><span leaf=">{{一句话简介}}</span></p>
      </section>
    </section>
    <section style="height:1px;background:rgba(255,255,255,0.14);margin:0 0 16px;"><span leaf=""><br></span></section>
    <p style="margin:0;font-size:14px;line-height:1.8;color:#E7EAEF;text-align:justify;">
      <span leaf=">{{互动引导文案}}</span>
      <span style="color:#F0691C;font-weight:900;">∎</span>
    </p>
  </section>
</section>
```

> 头像白描边 + 橙外圈；名字用白字大号、简介用浅灰小字，竖向堆叠避免原来"头像横着一长条文字"的失衡；分隔线把作者信息与 CTA 分组，版面干净。

## 完整文章模板骨架

```html
<section style="max-width:677px;margin:0 auto;background:#FFFFFF;font-family:-apple-system,BlinkMacSystemFont,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif;color:#33506B;line-height:1.8;letter-spacing:0.3px;overflow-x:hidden;">

  <!-- 1. 开头引言卡片（组件2，白卡 + 橙左竖条 + 大号橙引号，无投影） -->

  <!-- 2. 前言正文（组件6 段落 × N，放 0 10px 边距 section，第一章之前的开场白） -->

  <!-- 3. 前言导读（组件3，3+ 章节时生成，精选 3 看点） -->

  <!-- 4. 第一章（组件5 章节标题，margin-top:16px） -->
  <!--    章内：组件6 正文 + 6b 子标题 + 7 行内高亮 + 8 引用 + 9 提示 + 10 标签组 + 11 列表 + 12 数据 + 14 图片 -->

  <!-- 5. 章节分割线（组件4）+ 第二章…第N章（组件5，margin-top:56px） -->

  <!-- 6. 结语章（组件5 变体：编号 ∞，英文 THE END） -->

  <!-- 7. END 分割线（组件15） -->

  <!-- 8. 尾部签名（组件16，深黑卡 + 橙边条收尾） -->

</section>
```

**骨架铁律**：引言卡在最前；导读区在前言正文之后、第一章之前；章节之间用组件 4 分割线分隔；一篇只有一个 END + 一个签名区。顶部白卡（橙竖条+橙引号）与底部深黑卡（橙边条+橙收束符）形成"白—黑"首尾对比闭环。

---

## 视觉层级（3 层递进）

| 层级 | 样式 | 用途 | 频率 |
|------|------|------|------|
| **锚点层** | 深黑实底白字标签 7f / 引言卡·签名区大色块 / 深黑加粗金句 8a | 全文最关键锚点 | 内联锚点 ≤3 处（大色块为版面级） |
| **标记层** | 橙色下划线 7d（默认）/ 深黑加粗 7a / 浅橙底标签 7b | 正文关键词强调 | 每段 1~3 处 |
| **容器层** | 橙竖条引用 8x / 提示 9x / 标签组 10 / 卡片 11-12 | 引用、旁注、提示、结构化信息 | 按需 |

**设计原则**：
- **橙色是主旋律**：下划线、章节编号、竖条、标签实底、分割线圆点、STEP 标签高频用橙
- **深黑（`#1C1F24`）负责重字**：标题、金句、下划线里的字、最强锚点实底——与橙形成冷暖反差，避免满屏橙发闷
- **最强内联锚点**（深黑实底白字 7f）全篇 ≤3 处；引言卡（白卡橙竖条）/ 签名区（深黑卡）是版面级锚点
- 浅橙底（`#FFF3E8` / `#FFF8F0`）用于目录卡、引用块、提示块、数据卡，正文底色保持纯白
- 引用/提示统一用左竖条 + 浅橙底，**不用四周虚线框**（dashed）
- 大色块卡片（引言 / 签名）**不加投影**

---

## 文章类型 → 组件组合配方

按 SKILL.md 第 3 步判定的文章类型选配方；核心组件构成本篇排版主旋律，点缀组件按内容出现处使用，一篇文章点缀组件种类 ≤3，避免花哨。

| 文章类型 | 核心组件组合 | 点缀组件 |
|---|---|---|
| 观点/深度分析 | 正文6 + 橙竖条金句8a + 居中金句8d | 浅橙引用8b、暖竖条旁注8c |
| 教程/操作指南 | step-label 10a + 代码块（通用库1a）+ ordered-list 11a | 橙提示9a、tool-card 10c |
| 盘点/工具清单 | skill/tool-label 10b + tool-card 10c + pill-list 11b | 数据卡12、标签胶囊13 |
| 访谈/人物特稿 | 正文6 + 橙竖条金句8a（引语）+ timeline 11c（经历脉络） | 居中金句8d、暖竖条旁注8c |
| 数据复盘/报告 | 数据卡12（两列/三列）+ 表格12 + ordered-list 11a | 橙提示9a、荧光笔7e |
| 生活/情感随笔 | 正文6 + 居中金句8d + 暖竖条旁注8c | 橙竖条金句8a（少量） |
| 案例实战 | case-label 10a / timeline 11c + step-label 10a | 浅橙引用8b、踩坑提示9c |

所有类型共用固定结构：引言卡 2 + 导读 3（3+ 章节）+ 大编号章节 5 + END 15 + 签名 16。

---

## Markdown → 深海橙光排版 映射规则

| Markdown 元素 | 对应组件 | 说明 |
|---|---|---|
| `# 标题` | 不使用 | 公众号文章标题在平台设置 |
| 文章开头 `> 引言金句` | 组件 2 白卡橙竖条引言卡（无投影） | 视角与外标题错开 |
| `## 章节标题` | 组件 5 橙大编号 + 标题 | 自动编号 01/02…，末章 ∞ + THE END |
| `### 子标题` | 组件 6b 橙左竖条小标题 | 不套大编号章节样式 |
| 普通段落 | 组件 6 正文段落 | 每段主动标 1~3 处橙下划线 7d |
| `**加粗文字**` | 组件 7a 深黑加粗（默认）/ 橙加粗 | 深黑加粗为主 |
| `==高亮文字==` | 组件 7b 浅橙底深黑字标签 | 核心概念 |
| `<u>下划线</u>` / `++文字++` | 组件 7d 橙色下划线 | `2px #F0691C` |
| `~~删除线~~` | `text-decoration:line-through` + 次级灰蓝字 | 被淘汰概念 |
| 行内 `` `code` `` | 组件 7g 行内代码 | |
| `> 引用段落`（金句） | 组件 8a 橙竖条金句 | 核心金句，浅橙底 |
| `> 引用段落`（内容块） | 组件 8b 浅橙底引用块 | 有 REFERENCE 标签行 |
| `> 引用段落`（旁注） | 组件 8c 暖竖条轻量旁注 | 极细暖竖条 |
| 核心金句 | 组件 8a / 8d 居中金句 | 视觉焦点 |
| 最强锚点词 | 组件 7f 深黑实底白字 | 全篇 ≤3 处 |
| 操作步骤 | 组件 10a step-label | STEP 01/02… |
| 技能/工具清单 | 组件 10b skill/tool-label + 10c tool-card | |
| 案例/经历脉络 | 组件 10a case-label / 11c timeline | |
| Prompt 提示词 | 组件 8b 浅橙引用块 / 通用库 1a（长多行） | |
| ` ``` 多行代码块 ``` ` | 通用库 1a 深色 / 1b 浅色（左竖条换 #F0691C） | 每行一个 `<p style="margin:0">` |
| 并列要点 | 组件 11b pill-list | |
| `1. 2. 3.` 编号列表 | 组件 11a ordered-list | 橙圆标 |
| 数据展示 | 组件 12 数据/要点卡片组 | 浅橙底，深橙大数字 |
| Markdown 表格 | 组件 12 表格 | 橙表头，偶数行浅橙底 |
| 注意/警告 | 组件 9a 橙提示 / 9b 深黑提示 / 9c 踩坑提示 | |
| 行内标签 | 组件 13 标签胶囊 | 蓝描边默认 / 橙实底强调 |
| `---` | 组件 4 章节分割线 | 暖细线 + 橙圆点 |
| `![](图片)` | 组件 14 图片容器 | 暖细线圆角 |
| 文末 | 组件 15 END + 16 签名 | END线 + 深黑卡签名（无投影） |
