# css-flexbox

## 前言

css3引入了一种新的布局模型flex布局。flex是flexible-box的缩写，一般称之为弹性盒模型。和css3其他属性不一样，flexbox并不是一个属性，而是一个模块，包括多个css3属性。flex布局提供一种更加有效的方式来进行容器内的项目布局，以适应各种类型的显示设备和各种尺寸的屏幕

## 版本迭代

flexbox布局的语法规范经过几年发生了很大的变化。从2007年07月，flex第一版本的工作草案发布，到2012年09月，flex最新版本成为候选推荐。flex主要经历了三个版本：旧版本、混合版本、新版本。

[相关兼容性查看](https://caniuse.com/#search=flex)

## 基本概念

伸缩容器默认存在两条轴: 水平的主轴(main-axis) 和垂直的侧轴(cross-axis)，主轴方向不一定是水平的，它主要取决于flex-direction属性，主轴起点叫main-start，主轴终点叫main-end；侧轴起点叫cross-start，侧轴终点叫cross-end。

伸缩项目默认沿主轴排列。单个伸缩项目占据的主轴空间叫main-size，占据的侧轴空间叫cross-size。
伸缩项目的main-size和cross-size主要由宽度或高度决定

### 伸缩容器

要让一个元素变成伸缩容器，需要使用display属性。采用flex布局的元素，称为伸缩容器(flex container)，容器内的子元素称为伸缩项目(flex item)。

弹性盒模型的两种容器块级伸缩容器和内联伸缩容器的区别类似于block和inline-block的区别，一个独占一行，另一个非独占一行。

```
/*弹性盒模型: 块级伸缩容器 | 内联伸缩容器*/
/*新版本*/
display: flex | inline-flex;
/*混合版本*/
display: flexbox | inline-flexbox;
/*旧版本*/
display: box | inline-box;
```

[demo](https://demo.xiaohuochai.site/css/flex/f1.html)

以下6个属性作用在伸缩容器上

* 伸缩流方向 flex-direction
* 伸缩流换行 flex-wrap
* 伸缩流(包括方向与换行) flex-flow
* 主轴对齐 justify-content
* 侧轴对齐 align-items
* 堆栈伸缩行 align-content

#### 伸缩流方向

指定主轴的方向(即伸缩项目在伸缩容器中的排列方向)。

```
/*伸缩流方向: 水平方向 | 反向水平 | 垂直方向 | 反向垂直*/
/*新版本同混合版本，默认row*/
flex-direction: row | row-reverse | column | column-reverse;
/*旧版本*/
box-orient: horizontal(水平) |vertical(垂直) |inline-axis[默认](内联轴方向) |block-axis(块级轴方向)
box-direction: normal(正常) | reverse(反向)
```

[demo](https://demo.xiaohuochai.site/css/flex/f2.html)

伸缩流方向与direction和writing-mode有关系

[demo](https://demo.xiaohuochai.site/css/flex/f3.html)

#### 伸缩流换行

指定伸缩项目溢出伸缩容器时是否换行

```
/*伸缩行换行:不换行 | 换行 | 反转换行*/
/*新版本同混合版本*/
flex-wrap: nowrap[默认] | wrap | wrap-reverse
/*旧版本，没有浏览器支持box-lines属性，所以在旧版本中无法实现伸缩项目换行显示*/
box-lines: single[默认] | multiple | N/A
```

[demo](https://demo.xiaohuochai.site/css/flex/f4.html)

此时，CSS允许使用overflow属性来处理溢出内容的显示方式

伸缩项目的排列顺序同样与direction和wrinting-mode有关系

[demo](https://demo.xiaohuochai.site/css/flex/f5.html)

#### 伸缩流

伸缩流方向与伸缩行换行的缩写

```
/*伸缩流: 伸缩流方向 | 伸缩行换行*/
/*新版本同混合版本*/
flex-flow: <flex-direction> | <flex-wrap> 
[默认值] flex-flow: row nowrap
/*旧版本无对应属性*/
```

[demo](https://demo.xiaohuochai.site/css/flex/f6.html)

[demo](https://demo.xiaohuochai.site/css/flex/f7.html)

#### 主轴对齐

用来设置伸缩容器当前行伸缩项目在主轴方向的对齐方式，指定如何在伸缩项目之间分布伸缩容器额外空间

当一行上的所伸缩项目不能伸缩或可伸缩已达到最大长度时，这一属性才会对伸缩容器额外空间进行分配。当伸缩项目溢出某一行时，这一属性也会在项目的对齐上施加一些控制

```
/*主轴对齐方式: 左对齐 | 居中对齐 | 右对齐 | 两端对齐 | 扩散对齐*/
/*新版本*/
justify-content: flex-start[默认] | center | flex-end | space-between | space-around
/*混合版本*/
flex-pack: start[默认] | center | end | justify | distribute
/*旧版本*/
box-pack: start[默认] | center | end | justify | N/A
```

[demo](https://demo.xiaohuochai.site/css/flex/f8.html)

主轴对齐方式与direction、writing-mode、flex-flow都有关

[demo](https://demo.xiaohuochai.site/css/flex/f9.html)

#### 侧轴对齐

用来设置伸缩容器当前行在侧轴方向的对齐方式

```
/*侧轴对齐方式: 顶边对齐 | 中间对齐 | 底部对齐 | 基线对齐 | 伸缩项目拉伸填充整个伸缩容器*/
/*新版本*/
align-items: flex-start | center | flex-end | baseline | stretch[默认]
/*混合版本*/
flex-align: start | center | end | baseline | stretch[默认]
/*旧版本*/
box-align: start | center | end | baseline | stretch[默认]
```

[demo](https://demo.xiaohuochai.site/css/flex/f10.html)

侧轴对齐方式与direction、writing-mode、flex-flow都有关

[demo](https://demo.xiaohuochai.site/css/flex/f11.html)

#### 堆栈伸缩行

指定多个伸缩项目行在侧轴的对齐方式

```
/*侧轴对齐方式: 顶边对齐 | 中间对齐 | 底部对齐 | 两端对齐 | 扩散对齐 | 伸缩项目拉伸填充整个伸缩容器*/
/*新版本*/
align-content: flex-start | center | flex-end | space-between | space-around | stretch[默认]
/*混合版本*/
flex-line-pack: start | center | end | justify | distribute | stretch[默认]
/*旧版本无对应属性*/
```

[demo](https://demo.xiaohuochai.site/css/flex/f12.html)

堆栈伸缩行与direction、writing-mode、flex-flow都有关

[demo](https://demo.xiaohuochai.site/css/flex/f13.html)


### 伸缩项目

一个伸缩项目就是伸缩容器的一个子元素。伸缩容器中的文本也被视为一个伸缩项目。以下6个属性设置在伸缩项目上。

* 自身侧轴对齐方式 align-self
* 伸缩基准值 flex-basis
* 扩展比率 flex-grow
* 收缩比率 flex-shrink
* 伸缩性 flex
* 显示顺序 order

#### 自身侧轴对齐方式align-self

单个伸缩项目在侧轴的对齐方式，该属性可以覆盖伸缩容器的侧轴对齐方式，对于匿名伸缩项目，align-self的值永远与其关联的伸缩容器的align-items的值相同。

```
/*侧轴对齐方式: 自动 | 顶边对齐 | 中间对齐 | 底部对齐 | 基线对齐 | 伸缩项目拉伸填充整个伸缩容器*/
/*新版本*/
align-self: auto[默认] | flex-start | center | flex-end | baseline | stretch
/*混合版本*/
flex-item-align: auto[默认] | start | center | end | baseline | stretch
/*旧版本无对应属性*/
```

如果align-self的值为auto，则其计算值为伸缩项目的伸缩容器的align-items值

如果伸缩项目的任一个侧轴上的外边距为auto，则该伸缩项目在伸缩容器的剩余空间内居中对齐，且align-self没有效果。

[demo](https://demo.xiaohuochai.site/css/flex/f14.html)

#### 伸缩基准值

伸缩项目在主轴方向上的初始大小

```
/*新版本*/
flex-basis: <length> | auto[默认]
/*混合版本*/
positive-flex: <number>[默认为1]
/*旧版本无对应属性*/
```

如果flex-basis的值为0，表示伸缩项目在主轴方向上的初始大小为0，分配所有空间；如果flex-basis的值为auto，表示伸缩项目在主轴方向上的初始大小为设置宽度(如果没有设置宽度，则为内容宽度)，再分配剩余空间

flex-basis的length值可以是一个数字后面跟着px、em等单位，也可以是一个百分数，相对于其父伸缩容器的主轴长度

[demo](https://demo.xiaohuochai.site/css/flex/f15.html)

#### 扩展比率

当伸缩容器的额外空间为正值时，此伸缩项目相对伸缩容器里其他伸缩项目能扩展的空间比例

```
/*新版本*/
flex-grow: <number>[默认为0]
/*混合版本*/
positive-flex: <number>[默认为0]
/*旧版本无对应属性*/
```

若flex-grow的值为0表示即使存在剩余空间也不放大；若所有项目的flex-grow属性都为1，则它们将等分剩余空间(如果有的话)；若一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍

#### 收缩比率

当伸缩容器的额外空间为负值时，此伸缩项目相对于伸缩容器里其他伸缩项目能收缩的空间比例

```
/*新版本*/
flex-shrink: <number>[默认为1]
/*混合版本*/
negative-flex: <number>[默认为0]
/*旧版本无对应属性*/
```

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。

伸缩基准值、扩展比率和收缩比率都可以为小数，但不能为负数

[demo](https://demo.xiaohuochai.site/css/flex/f17.html)

#### 伸缩性

伸缩性是扩展比率、收缩比率和伸缩基准值的缩写

```
flex: none => flex: 0 0 auto;//表示宽度为原始宽度，不发生扩展或收缩
flex: auto => flex: 1 1 auto;//表示除了占据原先的宽度外，还要分配剩余宽度(包括扩展或收缩)
flex: 0 => flex: 0 1 0%;//表示收缩为最小宽度
flex: 1 => flex: 1 1 0%;//表示分配所有宽度(包括扩展或收缩)
flex: 0 auto => flex: 0 1 auto;(默认值)//表除了占据原先的宽度外，还要分配剩余宽度(只收缩，不扩展)
flex: 0 1 => flex: 0 1 0%;
```

当flex为关键字none或存在auto时，flex-basis为auto；若flex只有数字值，则flex-basis为0%；

```
/*新版本*/
flex: none | [<flex-grow> <flex-shrink>? || <flex-basis>]
/*混合版本*/
flex: none | [<pos-flex> <neg-flex>? || <preferred-size>]
/*旧版本*/
box-flex: <number>
```

[demo](https://demo.xiaohuochai.site/css/flex/f18.html)


#### 显示顺序

定义伸缩项目的排列顺序，数值越小，排列越靠前

```
/*新版本*/
order: <number>[默认为0]
/*混合版本*/
flex-order: <number>[默认为0]
/*旧版本*/
box-ordinal-group: <integer>[默认为1]
```

order的属性值可以是负数，但不能是小数

[demo](https://demo.xiaohuochai.site/css/flex/f19.html)

## 学习完玩个小游戏

[http://flexboxfroggy.com/](http://flexboxfroggy.com/)

## 注意事项

* 浏览器会将任何直接在伸缩容器里的连续文字块包起来成为匿名伸缩项目
* 使用flex布局实现上是使元素FFC化(flex formatting context伸缩格式化上下文)，FFC是普通流的一种。而浮动流和定位流以及CSS其他属性对FFC是有影响的，主要表现在以下几点:
    * float、clear和vertical-align属性在伸缩项目上没有效果
    * 伸缩容器的margin与其内容的margin不会重叠
    * text-align属性在伸缩容器上没有效果，因为其只可应用于块级block容器
    * 另外，columns属性伸缩容器上没有效果
* 旧版本flex要求伸缩项目必须是block元素
* 旧版本flex的伸缩流方向中的reverse值，只改变伸缩项目的排列顺序，并不改变其对齐方式。所以建议使用direction:rtl来实现伸缩流反向效果
* 旧版本flex不支持伸缩流换行，所以在其他版本flex中尽量不要使用换行操作
* 旧版本flex的主轴对齐属性中没有扩散对齐属性space-around，所以在其他版本flex中尽量不要使用该属性值
* 旧版本flex的伸缩性只有一个值，表示基于伸缩项目本身尺寸大小的扩展或收缩比率，旧版本的-webkit-box-flex:1;相当于新版本的flex:auto;所以要想实现不基于伸缩项目本身尺寸大小的伸缩需要显式地将伸缩项目的宽度width设置为0。注意该值支持小数，但不能为负数
* 旧版本flex的显示顺序是以1为默认值的正整数，而新版本flex的显示顺序是以0为默认值的自然数。所以在设置显示顺序时，跳过1，从2开始设置
* 在flex容器上不能正常应用text-overflow:ellipsis属性，转为容器项目完成打点

更多[flexbugs](https://github.com/philipwalton/flexbugs)

## 本页转载推荐博文

[深入理解css弹性盒模型flex](http://www.cnblogs.com/xiaohuochai/p/5323146.html#anchor4-1)

[CSS旧版flex及兼容](http://www.cnblogs.com/xiaohuochai/p/5334936.html)


