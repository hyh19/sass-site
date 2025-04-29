# Sass 学习卡片

## Sass 变量

Tags: #Sass #Sass/Beginner #Sass/Variables

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```

---

Sass 变量是一种存储信息并在样式表中重复使用的方式。

### 变量定义与使用

- {{`$`}} 符号用于声明一个变量
- {{`$font-stack: Helvetica, sans-serif`}} 定义了一个字体栈变量
- {{`$primary-color: #333`}} 定义了一个颜色变量
- 在样式属性中使用 {{`$变量名`}} 来引用变量值

### 编译过程

当 Sass 文件被处理时，定义的变量会被其实际值替换，生成标准的 CSS。

### 应用价值

- 提高代码的可维护性
- 确保品牌颜色、字体等样式一致性
- 修改一处变量定义即可全局更新样式

> 💡 变量可用于存储颜色、字体栈，或任何你想在样式表中重复使用的 CSS 值。

***

## Sass 嵌套规则

Tags: #Sass #Sass/Beginner #Sass/Nesting

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

---

Sass 嵌套允许你按照 HTML 的视觉层次结构来组织 CSS 选择器。

### 嵌套结构

- 外层选择器 {{`nav`}} 包含了多个内层选择器
- 内层选择器 {{`ul`}}、{{`li`}} 和 {{`a`}} 被嵌套在 {{`nav`}} 选择器内部
- 编译时，Sass 将这种嵌套结构转换为标准的 CSS 选择器组合

### 编译结果

- `nav ul` 选择器用于导航列表样式
- `nav li` 选择器用于列表项样式
- `nav a` 选择器用于导航链接样式

### 优势

- 更符合 HTML 的视觉层次结构
- 减少重复书写父级选择器的名称
- 使 CSS 代码更易读、更易组织

> 💡 注意：过度嵌套的规则会导致过度限定的 CSS，这可能难以维护，通常被认为是不良实践。

***

## Sass 模块化

Tags: #Sass #Sass/Beginner #Sass/Import #Sass/Variables

```scss
// _base.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```scss
// styles.scss
@use 'base';

.inverse {
  background-color: base.$primary-color;
  color: white;
}
```

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}

.inverse {
  background-color: #333;
  color: white;
}
```

---

Sass 允许你将样式表拆分为多个文件，通过 `@use` 规则进行模块化管理。

### 模块化机制

- 文件命名以下划线开头（如 {{`_base.scss`}}）表示这是一个部分文件
- 通过 {{`@use`}} 规则导入另一个 Sass 文件作为模块
- 被导入文件中的变量、混合器和函数可通过命名空间访问

### 命名空间

- {{`@use 'base'`}} 创建了一个基于文件名的命名空间
- 使用 {{`base.$primary-color`}} 引用导入模块中的变量
- 命名空间确保不同模块间的变量、混合器和函数不会冲突

### 编译结果

- 两个文件的内容被合并处理
- 模块中的所有样式都会包含在最终编译的 CSS 中
- 变量引用被其实际值替代

> 💡 Sass 很智能，导入文件时不需要包含文件扩展名，它会自动找到正确的文件。

***

## Sass Mixins

Tags: #Sass #Sass/Intermediate #Sass/Mixins

```scss
@mixin theme($theme: DarkGray) {
  background: $theme;
  box-shadow: 0 0 1px rgba($theme, .25);
  color: #fff;
}

.info {
  @include theme;
}
.alert {
  @include theme($theme: DarkRed);
}
.success {
  @include theme($theme: DarkGreen);
}
```

```css
.info {
  background: DarkGray;
  box-shadow: 0 0 1px rgba(169, 169, 169, 0.25);
  color: #fff;
}

.alert {
  background: DarkRed;
  box-shadow: 0 0 1px rgba(139, 0, 0, 0.25);
  color: #fff;
}

.success {
  background: DarkGreen;
  box-shadow: 0 0 1px rgba(0, 100, 0, 0.25);
  color: #fff;
}
```

---

Sass 混合器（Mixins）允许你定义可重用的样式组，并在整个样式表中引用它们。

### 混合器定义与使用

- 使用 {{`@mixin`}} 指令创建混合器，后跟混合器名称
- 混合器可以接收参数，如示例中的 {{`$theme`}} 参数
- 可以为参数提供默认值：{{`$theme: DarkGray`}}
- 使用 {{`@include`}} 指令应用混合器到选择器中

### 参数传递

- `.info` 类使用默认主题（DarkGray）
- `.alert` 类显式指定 {{`$theme: DarkRed`}} 作为参数
- `.success` 类使用 {{`$theme: DarkGreen`}} 作为参数

### 编译结果

- 每个使用混合器的选择器都会展开包含混合器中定义的所有 CSS 属性
- 函数 {{`rgba()`}} 处理传入的颜色参数，创建半透明效果
- 相同的样式结构应用于多个选择器，但具有不同的颜色值

> 💡 混合器使 Sass 代码更加 DRY（Don't Repeat Yourself），特别适合需要供应商前缀的 CSS3 特性。

***

## Sass 继承/扩展

Tags: #Sass #Sass/Intermediate #Sass/Extend

```scss
/* This CSS will print because %message-shared is extended. */
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

// This CSS won't print because %equal-heights is never extended.
%equal-heights {
  display: flex;
  flex-wrap: wrap;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}
```

```css
/* This CSS will print because %message-shared is extended. */
.message, .success, .error, .warning {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  border-color: green;
}

.error {
  border-color: red;
}

.warning {
  border-color: yellow;
}
```

---

Sass 中的继承机制允许选择器共享一组 CSS 属性，通过 `@extend` 指令实现。

### 占位符选择器

- {{`%message-shared`}} 是一个占位符选择器
- 占位符选择器以 {{`%`}} 开头，只有在被扩展时才会输出到 CSS 中
- {{`%equal-heights`}} 没有被任何选择器扩展，所以不会出现在编译后的 CSS 中

### 继承机制

- {{`@extend`}} 指令让一个选择器继承另一个选择器的样式
- `.message`、`.success`、`.error` 和 `.warning` 都继承了 {{`%message-shared`}} 的样式
- 在编译后的 CSS 中，这些选择器会被组合在一起，共享相同的 CSS 规则

### 选择器覆盖

- 继承后，各选择器可以添加或覆盖特定样式
- `.success` 覆盖了边框颜色为绿色
- `.error` 覆盖了边框颜色为红色
- `.warning` 覆盖了边框颜色为黄色

### 编译优化

Sass 继承机制会生成优化的 CSS 选择器组，减少代码重复：

```css
.message, .success, .error, .warning {
  /* 共享样式 */
}
```

> 💡 占位符选择器是一种特殊类型的类，仅在被扩展时才会输出到 CSS 中，可以帮助保持编译后的 CSS 整洁和高效。

***

## Sass 运算符

Tags: #Sass #Sass/Intermediate #Sass/Operators #Sass/Math

```scss
@use "sass:math";

.container {
  display: flex;
}

article[role="main"] {
  width: math.div(600px, 960px) * 100%;
}

aside[role="complementary"] {
  width: math.div(300px, 960px) * 100%;
  margin-left: auto;
}
```

```css
.container {
  display: flex;
}

article[role="main"] {
  width: 62.5%;
}

aside[role="complementary"] {
  width: 31.25%;
  margin-left: auto;
}
```

---

Sass 提供了丰富的数学运算能力，让你可以在 CSS 中进行计算。

### 数学模块

- {{`@use "sass:math"`}} 导入 Sass 内置的数学模块
- 通过模块导入可以使用更高级的数学函数

### 数学运算与函数

- {{`math.div(600px, 960px)`}} 计算两个数值的除法结果
- 除法运算结果（0.625）再乘以 100% 得到百分比值
- 这种方式将像素值转换为响应式的百分比单位

### 实际应用

- 示例中创建了一个简单的流式栅格系统
- 主内容区宽度为容器的 62.5%（600px ÷ 960px × 100%）
- 侧边栏宽度为容器的 31.25%（300px ÷ 960px × 100%）
- `margin-left: auto` 将侧边栏推到右侧

### Sass 运算符

除了 {{`math.div()`}}，Sass 还支持其他数学运算：

- 加法：{{`+`}}
- 减法：{{`-`}}
- 乘法：{{`*`}}
- 取模：{{`%`}}

> 💡 Sass 的数学运算对于创建灵活的、响应式的布局非常有用，可以轻松实现像素到百分比的转换。
