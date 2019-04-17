title: CSS总结
author: Yan Congwen
tags:
  - CSS
categories: []
date: 2018-07-28 15:41:00
---
> 本文记录一些CSS中的一些常识和技巧	
> CSS 的学习不需要死记硬背，就是经验和熟练度，要会用工具。比如，要会搜索 “css generator”

## 一、知识点

### 1、文档流
- 行内元素
- 块级元素

### 2、盒模型
盒模型的组成大家肯定都懂，由里向外content,padding,border,margin。盒模型是有两种标准的，一个是标准模型，一个是IE模型。
- 标准盒模型
元素宽高 = content 宽高

- IE 盒模型
元素宽高 = content宽高 + padding + border

```css
/* 标准模型，默认值 */
box-sizing:content-box;

 /*IE模型，推荐*/
box-sizing:border-box;
```

### 3、定位 position
- static	
默认，没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。 	
- relative	
相对定位，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素原始位置留下空白）
- absolute	
绝对定位，相对于 static 定位以外的第一个父元素进行定位。    
- fixed	
固定定位，相对于浏览器窗口进行定位。
- sticky	 
粘性定位，基于用户滚动的位置，它的行为就像 position:relative; 而当页面滚动超出目标区域时，它的表现就像 position:fixed;，它会固定在目标位置。
    
## 二、技巧
- 调试技巧：给元素加border;
- 浮动，给父元素清除浮动;	
	 .clearfix{	
     content:'';	
     display:block;	
     clear:both;	
    }
- 不要上来就给div加高度和宽度，要让内容撑开它;
	 - div 的高度是由其文档流的高度决定的
     - height 和 width 是 bug 的来源
- 脱离文档流

## 三、常用工具网站
- [CSS技巧大全 CSS Tricks](https://css-tricks.com/)
- [CSS 代码生成器 CSS3 Generator](http://css3generator.com/)
- [CSS 动画生成器 Animate.css](https://daneden.github.io/animate.css/)
- [特殊符号大全](https://www.copypastecharacter.com/)
- [浏览器测试 BROWSERHACKS](http://browserhacks.com/)
- [获取渐变色 Ultimate CSS Gradient Generator](http://www.colorzilla.com/gradient-editor/)
- [设计社区 dribbble](https://dribbble.com/)