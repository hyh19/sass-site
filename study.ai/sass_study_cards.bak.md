# Sass 学习卡片

## Sass 变量定义与使用

Tags: #Sass #Sass/Beginner #Sass/Variables

```scss
// Sass 代码
$primary-color: #3498db;
$secondary-color: #2ecc71;
$base-padding: 15px;
$base-border-radius: 4px;

.button {
  background-color: $primary-color;
  padding: $base-padding;
  border-radius: $base-border-radius;
  border: none;
  color: white;
  
  &.success {
    background-color: $secondary-color;
  }
}
```

```css
/* 编译后的 CSS */
.button {
  background-color: #3498db;
  padding: 15px;
  border-radius: 4px;
  border: none;
  color: white;
}
.button.success {
  background-color: #2ecc71;
}
```

```html
<button class="button">普通按钮</button>
<button class="button success">成功按钮</button>
```

---

这个 Sass 代码示例展示了变量定义和使用的基本语法。

### 变量定义
- {{`$primary-color: #3498db`}} 定义了主色调变量
- {{`$secondary-color: #2ecc71`}} 定义了次要色调变量
- {{`$base-padding: 15px`}} 定义了基础内边距变量
- {{`$base-border-radius: 4px`}} 定义了基础圆角变量

### 变量使用
- 变量通过 {{`$变量名`}} 语法在样式中引用
- 使用变量可以确保样式的一致性
- 修改变量值会影响所有使用该变量的地方

### 优势分析
1. **可维护性**：颜色和尺寸值在一处定义，可以轻松更改
2. **一致性**：确保整个样式表中使用相同的值
3. **语义化**：变量名可以表达其用途，提高代码可读性
4. **减少重复**：避免在多个地方重复书写相同的值

> 💡 实践建议：始终将主题相关的值（如颜色、间距、字体大小等）定义为变量，便于后期维护和主题切换。

***

## Sass 选择器嵌套与父选择器引用

Tags: #Sass #Sass/Beginner #Sass/Nesting

```scss
// Sass 代码
.nav {
  background-color: #f8f9fa;
  padding: 15px;
  
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
    display: flex;
  }
  
  li {
    margin-right: 20px;
    
    &:last-child {
      margin-right: 0;
    }
  }
  
  a {
    color: #333;
    text-decoration: none;
    
    &:hover {
      color: #007bff;
      text-decoration: underline;
    }
    
    &.active {
      font-weight: bold;
      color: #007bff;
    }
  }
}
```

```css
/* 编译后的 CSS */
.nav {
  background-color: #f8f9fa;
  padding: 15px;
}
.nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
}
.nav li {
  margin-right: 20px;
}
.nav li:last-child {
  margin-right: 0;
}
.nav a {
  color: #333;
  text-decoration: none;
}
.nav a:hover {
  color: #007bff;
  text-decoration: underline;
}
.nav a.active {
  font-weight: bold;
  color: #007bff;
}
```

```html
<nav class="nav">
  <ul>
    <li><a href="#" class="active">首页</a></li>
    <li><a href="#">关于</a></li>
    <li><a href="#">服务</a></li>
    <li><a href="#">联系我们</a></li>
  </ul>
</nav>
```

---

这个示例展示了 Sass 中的选择器嵌套和父选择器引用功能。

### 选择器嵌套
- 允许按照 HTML 的层级结构组织 CSS 代码
- `.nav` 内部嵌套了 `ul`、`li` 和 `a` 选择器
- 编译后生成对应的后代选择器（如 `.nav ul`、`.nav li` 等）

### 父选择器引用 (&)
- {{`&`}} 符号用于引用父选择器
- {{`&:last-child`}} 编译为 `.nav li:last-child`
- {{`&:hover`}} 编译为 `.nav a:hover`
- {{`&.active`}} 编译为 `.nav a.active`

### 嵌套的优势
1. **结构清晰**：CSS 结构与 HTML 结构保持一致
2. **减少重复**：避免重复书写父选择器
3. **提高可读性**：代码组织更加直观
4. **作用域明确**：样式规则限定在特定上下文内

### 注意事项
- {{嵌套不宜过深}}（通常不超过 3 层），以避免生成过于特定的 CSS 选择器
- 过度嵌套会增加 CSS 选择器的特异性（specificity），可能导致样式覆盖问题
- 保持合理的嵌套层级有助于生成更高效、更易维护的 CSS

***

## Sass Mixins 定义与使用

Tags: #Sass #Sass/Intermediate #Sass/Mixins

```scss
// Sass 代码
@mixin flex-container($direction: row, $justify: center, $align: center) {
  display: flex;
  flex-direction: $direction;
  justify-content: $justify;
  align-items: $align;
}

@mixin button-variant($bg-color, $text-color: white, $hover-darken: 10%) {
  background-color: $bg-color;
  color: $text-color;
  border: none;
  padding: 10px 15px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
  
  &:hover {
    background-color: darken($bg-color, $hover-darken);
  }
}

.container {
  @include flex-container;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

.button {
  &-primary {
    @include button-variant(#3498db);
  }
  
  &-success {
    @include button-variant(#2ecc71);
  }
  
  &-danger {
    @include button-variant(#e74c3c);
  }
  
  &-warning {
    @include button-variant(#f39c12, black, 15%);
  }
}
```

```css
/* 编译后的 CSS */
.container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

.button-primary {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}
.button-primary:hover {
  background-color: #217dbb;
}

.button-success {
  background-color: #2ecc71;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}
.button-success:hover {
  background-color: #25a25a;
}

.button-danger {
  background-color: #e74c3c;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}
.button-danger:hover {
  background-color: #d62c1a;
}

.button-warning {
  background-color: #f39c12;
  color: black;
  border: none;
  padding: 10px 15px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}
.button-warning:hover {
  background-color: #c87f0a;
}
```

```html
<div class="container">
  <button class="button-primary">主要按钮</button>
  <button class="button-success">成功按钮</button>
  <button class="button-danger">危险按钮</button>
  <button class="button-warning">警告按钮</button>
</div>
```

---

这个 Sass 代码示例展示了 Mixins 的定义和使用。

### Mixin 定义
- 使用 {{`@mixin`}} 指令定义可重用的代码块
- {{`@mixin flex-container($direction: row, $justify: center, $align: center)`}} 定义了一个带参数的 mixin
- 参数可以设置默认值，如 `$direction: row`
- Mixin 内部可以包含任何有效的 CSS 规则

### Mixin 使用
- 使用 {{`@include`}} 指令调用 mixin
- {{`@include flex-container`}} 使用默认参数值
- {{`@include button-variant(#3498db)`}} 使用部分自定义参数
- {{`@include button-variant(#f39c12, black, 15%)`}} 使用全部自定义参数

### Mixin 的优势
1. **代码复用**：将重复的样式封装为可重用的模块
2. **参数化**：通过参数自定义 mixin 的行为
3. **维护性**：修改 mixin 定义即可更新所有使用处
4. **可读性**：通过语义化的 mixin 名称提高代码清晰度

### 实际应用
- `flex-container` mixin 用于创建灵活的弹性布局容器
- `button-variant` mixin 用于创建不同样式的按钮
- 与父选择器引用 `&` 结合使用，创建了 BEM 风格的命名

> 💡 技巧：Mixins 特别适合封装供应商前缀、媒体查询和经常重复的 CSS 模式，如卡片、表单元素样式等。

***

## Sass 控制指令与循环

Tags: #Sass #Sass/Intermediate #Sass/Control

```scss
// Sass 代码
$colors: (
  "primary": #3498db,
  "success": #2ecc71,
  "warning": #f39c12,
  "danger": #e74c3c,
  "info": #1abc9c
);

$breakpoints: (
  "xs": 0,
  "sm": 576px,
  "md": 768px,
  "lg": 992px,
  "xl": 1200px
);

// 使用 @each 循环生成颜色类
@each $name, $color in $colors {
  .text-#{$name} {
    color: $color;
  }
  
  .bg-#{$name} {
    background-color: $color;
  }
  
  .border-#{$name} {
    border-color: $color;
  }
}

// 使用 @for 循环生成间距类
@for $i from 1 through 5 {
  .m-#{$i} {
    margin: $i * 0.25rem;
  }
  
  .p-#{$i} {
    padding: $i * 0.25rem;
  }
}

// 使用 @if/@else 生成响应式工具类
@mixin responsive($breakpoint) {
  @if map-has-key($breakpoints, $breakpoint) {
    $value: map-get($breakpoints, $breakpoint);
    
    @media (min-width: $value) {
      @content;
    }
  } @else {
    @warn "未知的断点: #{$breakpoint}";
  }
}

.hide {
  display: none;
}

@each $breakpoint, $width in $breakpoints {
  @include responsive($breakpoint) {
    .d-#{$breakpoint}-none {
      display: none;
    }
    
    .d-#{$breakpoint}-block {
      display: block;
    }
    
    .d-#{$breakpoint}-flex {
      display: flex;
    }
  }
}
```

```css
/* 编译后的 CSS（部分） */
.text-primary {
  color: #3498db;
}

.bg-primary {
  background-color: #3498db;
}

.border-primary {
  border-color: #3498db;
}

/* ... 其他颜色类 ... */

.m-1 {
  margin: 0.25rem;
}

.p-1 {
  padding: 0.25rem;
}

/* ... 其他间距类 ... */

.hide {
  display: none;
}

.d-xs-none {
  display: none;
}

.d-xs-block {
  display: block;
}

.d-xs-flex {
  display: flex;
}

@media (min-width: 576px) {
  .d-sm-none {
    display: none;
  }
  .d-sm-block {
    display: block;
  }
  .d-sm-flex {
    display: flex;
  }
}

/* ... 其他响应式类 ... */
```

---

这个 Sass 代码示例展示了控制指令和循环的使用。

### 数据结构
- 使用 Sass maps 存储颜色和断点值
- `$colors` 和 `$breakpoints` 是键值对集合

### @each 循环
- {{`@each $name, $color in $colors`}} 遍历颜色 map
- {{`#{$name}`}} 使用插值语法将变量用于选择器名
- 为每种颜色生成文本、背景和边框类

### @for 循环
- {{`@for $i from 1 through 5`}} 创建从 1 到 5 的循环
- 生成递增的间距工具类
- 使用数学运算 `$i * 0.25rem` 计算尺寸

### @if/@else 条件
- {{`@if map-has-key($breakpoints, $breakpoint)`}} 检查键是否存在
- {{`@else`}} 处理备用情况
- {{`@warn`}} 提供编译时警告

### @mixin 与 @content
- `responsive` mixin 接受断点名称参数
- {{`@content`}} 允许在调用 mixin 时传入内容
- `@include responsive($breakpoint) { ... }` 向 mixin 传递内容

### 实际应用
1. **实用工具类**：创建类似 Bootstrap 的工具类系统
2. **响应式设计**：根据断点生成媒体查询
3. **主题系统**：为多个组件批量生成样式变体
4. **减少重复**：避免手动编写重复的样式规则

> 💡 技巧：控制指令特别适合创建灵活的工具类库和组件系统，但要避免生成过多未使用的 CSS。

***

## Sass 函数与数学运算

Tags: #Sass #Sass/Intermediate #Sass/Functions #Sass/Math #Sass/Operators

```scss
// Sass 代码
@use "sass:math";
@use "sass:color";
@use "sass:list";
@use "sass:map";

// 自定义函数：计算栅格列宽
@function col-width($columns, $total-columns: 12) {
  @return math.percentage(math.div($columns, $total-columns));
}

// 自定义函数：计算带单位的值
@function rem($pixels) {
  @return math.div($pixels, 16px) * 1rem;
}

// 自定义函数：创建颜色变化
@function theme-color($base-color, $shade: "base") {
  $shades: (
    "lighter": color.scale($base-color, $lightness: 40%),
    "light": color.scale($base-color, $lightness: 20%),
    "base": $base-color,
    "dark": color.scale($base-color, $lightness: -20%),
    "darker": color.scale($base-color, $lightness: -40%)
  );
  
  @return map.get($shades, $shade);
}

$primary-color: #3498db;
$spacing-unit: 8px;
$border-radius: 4px;

// 使用数学运算和函数
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: rem(20px);
}

.grid {
  display: flex;
  flex-wrap: wrap;
  margin: 0 math.div(-$spacing-unit, 2);
  
  &__col {
    padding: 0 math.div($spacing-unit, 2);
    
    &--1 { width: col-width(1); }
    &--2 { width: col-width(2); }
    &--3 { width: col-width(3); }
    &--4 { width: col-width(4); }
    &--6 { width: col-width(6); }
    &--12 { width: col-width(12); }
  }
}

.card {
  border-radius: $border-radius * 2;
  padding: $spacing-unit * 2;
  
  &--primary {
    background-color: theme-color($primary-color);
    color: white;
  }
  
  &--primary-light {
    background-color: theme-color($primary-color, "light");
    color: white;
  }
  
  &--primary-dark {
    background-color: theme-color($primary-color, "dark");
    color: white;
  }
}
```

```css
/* 编译后的 CSS */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1.25rem;
}

.grid {
  display: flex;
  flex-wrap: wrap;
  margin: 0 -4px;
}
.grid__col {
  padding: 0 4px;
}
.grid__col--1 {
  width: 8.3333333333%;
}
.grid__col--2 {
  width: 16.6666666667%;
}
.grid__col--3 {
  width: 25%;
}
.grid__col--4 {
  width: 33.3333333333%;
}
.grid__col--6 {
  width: 50%;
}
.grid__col--12 {
  width: 100%;
}

.card {
  border-radius: 8px;
  padding: 16px;
}
.card--primary {
  background-color: #3498db;
  color: white;
}
.card--primary-light {
  background-color: #5faee3;
  color: white;
}
.card--primary-dark {
  background-color: #217dbb;
  color: white;
}
```

```html
<div class="container">
  <div class="grid">
    <div class="grid__col grid__col--6">
      <div class="card card--primary">主色卡片</div>
    </div>
    <div class="grid__col grid__col--3">
      <div class="card card--primary-light">亮色卡片</div>
    </div>
    <div class="grid__col grid__col--3">
      <div class="card card--primary-dark">暗色卡片</div>
    </div>
  </div>
</div>
```

---

这个 Sass 代码示例展示了函数定义和数学运算的应用。

### 引入 Sass 模块
- {{`@use "sass:math"`}} 引入数学模块
- {{`@use "sass:color"`}} 引入颜色模块
- {{`@use "sass:list"`}} 引入列表模块
- {{`@use "sass:map"`}} 引入映射模块

### 自定义函数
- 使用 {{`@function`}} 关键字定义函数
- {{`@return`}} 语句返回计算结果
- `col-width` 函数计算栅格列宽
- `rem` 函数将像素值转换为 rem 单位
- `theme-color` 函数创建颜色变体

### 数学运算
- {{`math.div($pixels, 16px)`}} 执行除法运算（Sass 不再支持直接使用 `/` 进行除法）
- {{`$spacing-unit * 2`}} 执行乘法运算
- {{`$border-radius * 2`}} 执行乘法运算
- {{`math.percentage()`}} 将小数转换为百分比

### 应用场景
1. **栅格系统**：使用函数动态计算列宽
2. **单位转换**：将设计值（如 px）转换为相对单位（如 rem）
3. **颜色管理**：基于基础颜色创建色调变体
4. **布局计算**：处理间距、边距等布局值

### 函数的优势
- 提供语义化的计算方法
- 确保计算一致性
- 简化复杂的数值计算
- 增强代码可维护性

> 💡 技巧：Sass 函数最适合用于返回值的计算，而 mixins 则适合生成样式规则集。函数可以在属性值或其他表达式中使用。

***

## Sass 继承与占位符选择器

Tags: #Sass #Sass/Intermediate #Sass/Extend

```scss
// Sass 代码
// 定义基础样式占位符
%button-base {
  display: inline-block;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  text-align: center;
  transition: all 0.3s ease;
}

%clearfix {
  &::after {
    content: "";
    display: table;
    clear: both;
  }
}

%box-shadow {
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

// 使用继承应用样式
.btn {
  &-primary {
    @extend %button-base;
    background-color: #3498db;
    color: white;
    
    &:hover {
      background-color: darken(#3498db, 10%);
    }
  }
  
  &-secondary {
    @extend %button-base;
    background-color: #95a5a6;
    color: white;
    
    &:hover {
      background-color: darken(#95a5a6, 10%);
    }
  }
  
  &-outline {
    @extend %button-base;
    background-color: transparent;
    border: 1px solid #3498db;
    color: #3498db;
    
    &:hover {
      background-color: rgba(#3498db, 0.1);
    }
  }
}

.card {
  @extend %box-shadow;
  padding: 15px;
  border-radius: 4px;
  background-color: white;
}

.container {
  @extend %clearfix;
  max-width: 1200px;
  margin: 0 auto;
}
```

```css
/* 编译后的 CSS */
.btn-primary, .btn-secondary, .btn-outline {
  display: inline-block;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  text-align: center;
  transition: all 0.3s ease;
}

.container::after {
  content: "";
  display: table;
  clear: both;
}

.card {
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.btn-primary {
  background-color: #3498db;
  color: white;
}
.btn-primary:hover {
  background-color: #217dbb;
}

.btn-secondary {
  background-color: #95a5a6;
  color: white;
}
.btn-secondary:hover {
  background-color: #798d8f;
}

.btn-outline {
  background-color: transparent;
  border: 1px solid #3498db;
  color: #3498db;
}
.btn-outline:hover {
  background-color: rgba(52, 152, 219, 0.1);
}

.card {
  padding: 15px;
  border-radius: 4px;
  background-color: white;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}
```

```html
<div class="container">
  <div class="card">
    <button class="btn-primary">主要按钮</button>
    <button class="btn-secondary">次要按钮</button>
    <button class="btn-outline">轮廓按钮</button>
  </div>
</div>
```

---

这个 Sass 代码示例展示了继承和占位符选择器的使用。

### 占位符选择器
- 使用 {{`%selector-name`}} 语法定义占位符
- 占位符本身不会编译到 CSS 中（除非被继承）
- `%button-base`、`%clearfix` 和 `%box-shadow` 是占位符选择器
- 占位符用于存储想要共享的样式

### 使用 @extend 继承样式
- {{`@extend %selector-name`}} 语法用于继承样式
- {{`@extend %button-base`}} 将占位符中的样式应用到当前选择器
- 继承会在 CSS 中创建以逗号分隔的选择器组
- 编译后 `.btn-primary`, `.btn-secondary`, `.btn-outline` 共享相同的基础样式

### 继承的工作原理
1. **样式合并**：共享的样式在 CSS 中只写一次
2. **选择器组合**：Sass 创建选择器组（`,` 分隔的选择器列表）
3. **优化输出**：减少重复代码，生成更精简的 CSS

### 继承与 Mixins 的区别
- **继承**：合并选择器，生成更精简的 CSS，但可能导致复杂的选择器组
- **Mixins**：复制样式到每个选择器，生成更多 CSS 代码，但选择器保持独立

### 最佳实践
- 使用占位符选择器配合 `@extend` 而非直接继承实际的类
- 将 `@extend` 放在规则块的顶部，保持代码一致性
- 避免过度使用继承，尤其是在嵌套很深的选择器内部
- 对于主题变体和状态变化，继承特别有用

> 💡 技巧：在大型项目中谨慎使用 `@extend`，它可能导致 CSS 输出难以预测。在复杂场景下，考虑使用 mixins 代替。

***

## Sass 模块化与组织结构

Tags: #Sass #Sass/Advanced #Sass/Import #Sass/Architecture

```scss
// _variables.scss
$primary-color: #3498db;
$secondary-color: #2ecc71;
$text-color: #333;
$background-color: #f9f9f9;
$border-color: #ddd;

$font-family-sans: 'Helvetica Neue', Arial, sans-serif;
$font-family-serif: Georgia, Times, serif;
$font-size-base: 16px;

$breakpoints: (
  small: 576px,
  medium: 768px,
  large: 992px,
  xlarge: 1200px
);
```

```scss
// _mixins.scss
@use "sass:math";

@mixin media-breakpoint-up($breakpoint) {
  @if map-has-key($breakpoints, $breakpoint) {
    @media (min-width: map-get($breakpoints, $breakpoint)) {
      @content;
    }
  }
}

@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

@mixin truncate {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

@function rem($pixels) {
  @return math.div($pixels, 16px) * 1rem;
}
```

```scss
// _base.scss
@use "variables" as v;

body {
  font-family: v.$font-family-sans;
  font-size: v.$font-size-base;
  color: v.$text-color;
  background-color: v.$background-color;
  line-height: 1.5;
}

a {
  color: v.$primary-color;
  text-decoration: none;
  
  &:hover {
    text-decoration: underline;
  }
}

h1, h2, h3, h4, h5, h6 {
  margin-top: 0;
  margin-bottom: 0.5rem;
}
```

```scss
// components/_button.scss
@use "../variables" as v;
@use "../mixins" as m;

.button {
  display: inline-block;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  font-size: m.rem(16px);
  cursor: pointer;
  
  &-primary {
    background-color: v.$primary-color;
    color: white;
    
    &:hover {
      background-color: darken(v.$primary-color, 10%);
    }
  }
  
  &-secondary {
    background-color: v.$secondary-color;
    color: white;
    
    &:hover {
      background-color: darken(v.$secondary-color, 10%);
    }
  }
}
```

```scss
// main.scss
@use "variables";
@use "mixins";
@use "base";
@use "components/button";

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
  
  @include mixins.media-breakpoint-up(medium) {
    padding: 0 30px;
  }
}

.card {
  background-color: white;
  border: 1px solid variables.$border-color;
  border-radius: 4px;
  padding: 20px;
  margin-bottom: 20px;
  
  &__title {
    font-size: mixins.rem(20px);
    margin-bottom: 10px;
    @include mixins.truncate;
  }
  
  &__content {
    color: variables.$text-color;
  }
}
```

---

这个 Sass 代码示例展示了模块化和项目组织结构。

### 文件组织
- 使用前缀下划线 `_` 命名部分文件（partials）
- 按功能和类型分离文件：变量、混合器、基础样式、组件
- 使用目录结构组织复杂项目

### 模块系统
- 使用 {{`@use`}} 引入其他 Sass 文件
- {{`@use "variables" as v`}} 设置命名空间别名
- 通过命名空间访问变量和混合器：`v.$primary-color`
- 模块只会被导入一次，不会重复

### 模块化的优势
1. **代码组织**：将相关功能分组到独立文件中
2. **可维护性**：更容易定位和修改特定功能
3. **可重用性**：模块可以在不同项目间共享
4. **命名空间**：避免变量和混合器命名冲突

### 7-1 模式结构
这个示例遵循了类似 7-1 模式的结构（7 个文件夹，1 个主文件）:
- **abstracts/**: 变量、函数、mixins（示例中的 _variables.scss, _mixins.scss）
- **base/**: 基础样式、排版、动画（示例中的 _base.scss）
- **components/**: 组件样式（示例中的 components/_button.scss）
- **layout/**: 布局相关样式
- **pages/**: 页面特定样式
- **themes/**: 主题样式
- **vendors/**: 第三方样式
- **main.scss**: 主入口文件，引入所有部分文件

### 最佳实践
- 按功能而非页面组织样式
- 保持每个文件简短、聚焦于单一职责
- 使用一致的命名和导入约定
- 在主文件中按逻辑顺序导入文件（变量 → mixins → 基础 → 组件 → 页面）

> 💡 技巧：使用 Sass 模块化可以更好地组织大型项目，但要避免创建过多小文件导致项目结构过度复杂。

***

## Sass Maps 数据结构与操作

Tags: #Sass #Sass/Advanced #Sass/Maps

```scss
// Sass 代码
@use "sass:map";
@use "sass:color";

// 定义颜色系统
$colors: (
  "primary": #3498db,
  "secondary": #2ecc71,
  "success": #27ae60,
  "info": #3498db,
  "warning": #f39c12,
  "danger": #e74c3c,
  "light": #f8f9fa,
  "dark": #343a40
);

// 定义间距系统
$spacers: (
  0: 0,
  1: 0.25rem,
  2: 0.5rem,
  3: 1rem,
  4: 1.5rem,
  5: 3rem
);

// 定义断点系统
$breakpoints: (
  "xs": 0,
  "sm": 576px,
  "md": 768px,
  "lg": 992px,
  "xl": 1200px,
  "xxl": 1400px
);

// 合并 Maps
$theme-colors: map.merge(
  $colors,
  (
    "primary-light": color.scale(map.get($colors, "primary"), $lightness: 30%),
    "primary-dark": color.scale(map.get($colors, "primary"), $lightness: -20%)
  )
);

// 遍历 Maps 生成工具类
@each $color-name, $color-value in $theme-colors {
  .text-#{$color-name} {
    color: $color-value;
  }
  
  .bg-#{$color-name} {
    background-color: $color-value;
  }
  
  .border-#{$color-name} {
    border-color: $color-value;
  }
}

@each $space-key, $space-value in $spacers {
  .m-#{$space-key} { margin: $space-value; }
  .mt-#{$space-key} { margin-top: $space-value; }
  .mr-#{$space-key} { margin-right: $space-value; }
  .mb-#{$space-key} { margin-bottom: $space-value; }
  .ml-#{$space-key} { margin-left: $space-value; }
  .mx-#{$space-key} { 
    margin-left: $space-value;
    margin-right: $space-value;
  }
  .my-#{$space-key} { 
    margin-top: $space-value;
    margin-bottom: $space-value;
  }
  
  .p-#{$space-key} { padding: $space-value; }
  .pt-#{$space-key} { padding-top: $space-value; }
  .pr-#{$space-key} { padding-right: $space-value; }
  .pb-#{$space-key} { padding-bottom: $space-value; }
  .pl-#{$space-key} { padding-left: $space-value; }
  .px-#{$space-key} { 
    padding-left: $space-value;
    padding-right: $space-value;
  }
  .py-#{$space-key} { 
    padding-top: $space-value;
    padding-bottom: $space-value;
  }
}

// Map 函数使用
@function get-breakpoint($name) {
  @if map.has-key($breakpoints, $name) {
    @return map.get($breakpoints, $name);
  } @else {
    @error "未知的断点名称: #{$name}";
    @return null;
  }
}

// 使用断点值生成媒体查询 mixin
@mixin media-up($breakpoint) {
  $min-width: get-breakpoint($breakpoint);
  @if $min-width {
    @media (min-width: $min-width) {
      @content;
    }
  }
}
```

```css
/* 编译后的 CSS（部分示例） */
.text-primary {
  color: #3498db;
}

.bg-primary {
  background-color: #3498db;
}

.border-primary {
  border-color: #3498db;
}

/* ... 其他颜色工具类 ... */

.m-0 {
  margin: 0;
}

.mt-0 {
  margin-top: 0;
}

/* ... 其他间距工具类 ... */

.p-3 {
  padding: 1rem;
}

.pt-3 {
  padding-top: 1rem;
}

/* ... 其他工具类 ... */
```

```html
<!-- 使用生成的工具类 -->
<div class="bg-light p-4 border-primary">
  <h2 class="text-primary mb-3">标题</h2>
  <p class="text-dark mb-2">这是一段示例文本，使用了 Sass Maps 生成的工具类。</p>
  <div class="bg-primary-light p-3 mt-2">
    <span class="text-dark">高亮内容区域</span>
  </div>
</div>
```

---

这个 Sass 代码示例展示了 Maps 数据结构的使用与操作。

### Maps 定义
- Maps 是键值对集合，类似于 JavaScript 中的对象
- 使用 {{`(key1: value1, key2: value2)`}} 语法定义 Map
- 示例中定义了颜色、间距和断点系统的 Maps

### Map 操作函数
- {{`map.get($map, $key)`}} 获取特定键的值
- {{`map.merge($map1, $map2)`}} 合并两个 Maps
- {{`map.has-key($map, $key)`}} 检查键是否存在
- 其他函数：`map.keys()`、`map.values()`、`map.remove()` 等

### Maps 应用场景
1. **设计令牌系统**：存储颜色、字体、间距等主题变量
2. **响应式断点**：管理媒体查询断点值
3. **配置存储**：集中管理配置选项
4. **生成工具类**：批量创建类似 Bootstrap 的工具类

### Maps 与循环结合
- 使用 `@each` 循环遍历 Map 中的键值对
- 使用插值语法 `#{$variable}` 在选择器名中使用变量
- 自动生成大量的工具类和组件变体

### 自定义函数与 Maps
- 创建处理 Maps 数据的函数如 `get-breakpoint()`
- 添加错误处理和默认值
- 与 mixins 结合使用提供灵活的 API

### 最佳实践
- 使用 Maps 存储关联数据而非多个单独变量
- 利用命名空间避免变量名冲突
- 为复杂的 Map 操作创建辅助函数
- 集中管理设计令牌，便于主题切换

> 💡 技巧：Maps 结合循环是创建一致性设计系统的强大工具，特别适合生成工具类库和组件变体。

***

## Sass 响应式设计技巧

Tags: #Sass #Sass/Advanced #Sass/Responsive #Sass/Mixins

```scss
// Sass 代码
@use "sass:map";

// 断点配置
$breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px,
  xxl: 1400px
);

// 容器宽度配置
$container-max-widths: (
  sm: 540px,
  md: 720px,
  lg: 960px,
  xl: 1140px,
  xxl: 1320px
);

// 响应式工具 mixins
@mixin media-breakpoint-up($breakpoint) {
  $min: map.get($breakpoints, $breakpoint);
  @if $min {
    @media (min-width: $min) {
      @content;
    }
  } @else {
    @content;
  }
}

@mixin media-breakpoint-down($breakpoint) {
  $max: map.get($breakpoints, $breakpoint);
  @if $max {
    @media (max-width: $max - 0.02px) {
      @content;
    }
  } @else {
    @content;
  }
}

@mixin media-breakpoint-between($lower, $upper) {
  $min: map.get($breakpoints, $lower);
  $max: map.get($breakpoints, $upper);
  
  @if $min and $max {
    @media (min-width: $min) and (max-width: $max - 0.02px) {
      @content;
    }
  } @else if $min {
    @include media-breakpoint-up($lower) {
      @content;
    }
  } @else if $max {
    @include media-breakpoint-down($upper) {
      @content;
    }
  } @else {
    @content;
  }
}

// 响应式文本
@mixin responsive-font-size($min-size, $max-size, $min-viewport: map.get($breakpoints, sm), $max-viewport: map.get($breakpoints, xl)) {
  font-size: $min-size;
  
  @media (min-width: $min-viewport) {
    font-size: calc(#{$min-size} + #{strip-unit($max-size - $min-size)} * ((100vw - #{$min-viewport}) / #{strip-unit($max-viewport - $min-viewport)}));
  }
  
  @media (min-width: $max-viewport) {
    font-size: $max-size;
  }
}

// 辅助函数：移除单位
@function strip-unit($value) {
  @return $value / ($value * 0 + 1);
}

// 响应式容器
.container {
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
  
  @each $breakpoint, $container-max-width in $container-max-widths {
    @include media-breakpoint-up($breakpoint) {
      max-width: $container-max-width;
    }
  }
}

// 响应式栅格系统
.row {
  display: flex;
  flex-wrap: wrap;
  margin-right: -15px;
  margin-left: -15px;
}

@mixin make-col($size, $columns: 12) {
  flex: 0 0 percentage($size / $columns);
  max-width: percentage($size / $columns);
}

@for $i from 1 through 12 {
  .col-#{$i} {
    @include make-col($i);
  }
}

@each $breakpoint in map.keys($breakpoints) {
  @include media-breakpoint-up($breakpoint) {
    @for $i from 1 through 12 {
      .col-#{$breakpoint}-#{$i} {
        @include make-col($i);
      }
    }
  }
}

// 响应式导航
.navbar {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  padding: 0.5rem 1rem;
  
  &-nav {
    display: flex;
    flex-direction: column;
    width: 100%;
    
    @include media-breakpoint-up(md) {
      flex-direction: row;
      width: auto;
    }
  }
  
  &-toggler {
    display: block;
    
    @include media-breakpoint-up(md) {
      display: none;
    }
  }
}

// 响应式排版
h1 {
  @include responsive-font-size(1.75rem, 2.5rem);
}

p {
  @include responsive-font-size(1rem, 1.2rem);
}
```

```css
/* 编译后的 CSS（部分示例） */
.container {
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}
@media (min-width: 576px) {
  .container {
    max-width: 540px;
  }
}
@media (min-width: 768px) {
  .container {
    max-width: 720px;
  }
}
@media (min-width: 992px) {
  .container {
    max-width: 960px;
  }
}
@media (min-width: 1200px) {
  .container {
    max-width: 1140px;
  }
}
@media (min-width: 1400px) {
  .container {
    max-width: 1320px;
  }
}

.row {
  display: flex;
  flex-wrap: wrap;
  margin-right: -15px;
  margin-left: -15px;
}

.col-1 {
  flex: 0 0 8.3333333333%;
  max-width: 8.3333333333%;
}

/* ... 其他栅格类 ... */

@media (min-width: 768px) {
  .col-md-6 {
    flex: 0 0 50%;
    max-width: 50%;
  }
}

/* ... 其他响应式类 ... */

.navbar {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  padding: 0.5rem 1rem;
}
.navbar-nav {
  display: flex;
  flex-direction: column;
  width: 100%;
}
@media (min-width: 768px) {
  .navbar-nav {
    flex-direction: row;
    width: auto;
  }
}
.navbar-toggler {
  display: block;
}
@media (min-width: 768px) {
  .navbar-toggler {
    display: none;
  }
}

h1 {
  font-size: 1.75rem;
}
@media (min-width: 576px) {
  h1 {
    font-size: calc(1.75rem + 0.75 * ((100vw - 576px) / 624));
  }
}
@media (min-width: 1200px) {
  h1 {
    font-size: 2.5rem;
  }
}

/* ... 其他样式 ... */
```

```html
<div class="container">
  <div class="row">
    <div class="col-12 col-md-6">
      <h1>响应式标题</h1>
      <p>这是一段响应式文本，字体大小会根据视口宽度自动调整。</p>
    </div>
    <div class="col-12 col-md-6">
      <nav class="navbar">
        <button class="navbar-toggler">菜单</button>
        <div class="navbar-nav">
          <a href="#">首页</a>
          <a href="#">关于</a>
          <a href="#">服务</a>
          <a href="#">联系我们</a>
        </div>
      </nav>
    </div>
  </div>
</div>
```

---

这个 Sass 代码示例展示了响应式设计的实现技巧。

### 响应式基础配置
- 使用 Maps 定义断点系统
- 配置容器最大宽度
- 为媒体查询创建可复用的 mixins

### 媒体查询 Mixins
- {{`@mixin media-breakpoint-up()`}} 处理最小宽度查询
- {{`@mixin media-breakpoint-down()`}} 处理最大宽度查询
- {{`@mixin media-breakpoint-between()`}} 处理宽度范围查询
- 使用 {{`@content`}} 指令传递内容到 mixin

### 响应式容器
- 基本容器样式支持填充父元素宽度
- 根据断点设置不同的最大宽度
- 使用 `@each` 循环自动生成断点样式

### 响应式栅格系统
- 创建 `make-col` mixin 生成列样式
- 使用循环生成基础列类
- 为每个断点生成响应式列类

### 响应式排版
- 使用 `responsive-font-size` mixin 实现流体文本大小
- 基于视口宽度的计算属性（`calc()`）
- 设置最小和最大尺寸以及断点范围

### 响应式组件
- 导航栏在移动设备上显示为列布局，在桌面设备上显示为行布局
- 移动设备上显示菜单触发器，桌面设备上隐藏

### 响应式设计模式
1. **移动优先**：先设计移动端样式，再使用媒体查询添加大屏样式
2. **断点系统**：统一管理响应式断点
3. **流体布局**：结合百分比和弹性布局
4. **组件适应**：组件外观和行为根据屏幕尺寸变化

> 💡 技巧：将响应式逻辑封装到 mixins 中，使其可在整个项目中重用，同时保持一致的断点系统。
``` 