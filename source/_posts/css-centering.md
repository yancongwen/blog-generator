title: Centering in CSS
tags:
  - CSS
  - 译文
categories:
  - 技术
date: 2018-04-19 01:29:00
---

> 本文翻译自 CSS-Tricks 中的一篇文章—— [Centering in CSS: A Complete Guide](https://css-tricks.com/centering-css-complete-guide/)，CSS居中完全指南，其中有部分删改。

&emsp;&emsp;Centering things in CSS is the poster child of CSS complaining. Why does it have to be so hard? They jeer. I think the issue isn't that it's difficult to do, but in that there so many different ways of doing it, depending on the situation, it's hard to know which to reach for. 
&emsp;&emsp;居中是一种很常见的布局方式。有人抱怨CSS居中布局很难，其实不然，在我看来，说居中布局难，不是因为居中真的有多么难实现，而是因为实现居中的方法有太多太多，以至于新手总是纠结去用哪个。我们需要根据不同的场景，去选择合适的方法。
&emsp;&emsp;本文将CSS居中布局方法进行归类，以便于理解和简化居中问题。

## 1.水平居中
### 1.1 行内元素
行内元素直接为其父元素设置文本居中即可。
``` CSS
.center-children {
  text-align: center;
}
```
[http://codepen.io/chriscoyier/pen/HulzB](http://codepen.io/chriscoyier/pen/HulzB)

### 1.2 块级元素
块级元素直接设置左右边距为 auto 即可，前提是该块级元素必需有 width ，而且必需处于标准文档流中，浮动、绝对定位、固定定位了的元素就不能。

``` CSS
.center-me {
  margin: 0 auto;
}
```
[http://codepen.io/chriscoyier/pen/eszon](http://codepen.io/chriscoyier/pen/eszon)

### 1.3 多个块级元素
- 多个块元素在一行内居中
  - 方法一：父元素设置 text-align: center ，子元素设置 display: inline-block； 	
  - 方法二：使用 flex 布局，父元素设置 display: flex; justify-content: center;
<iframe src="http://codepen.io/chriscoyier/embed/ebing" width="100%" height="305" frameborder="0"></ifream>
- 多个块元素在一列内居中
如果只是需要让多个块级元素整体水平居中，并且按默认的方式纵向排列，那直接设置左右边距为 auto 即可。
<iframe src="http://codepen.io/chriscoyier/embed/haCGt" width="100%" height="305" frameborder="0"></ifream>

## 2. 垂直居中
### 2.1 行内元素
- 单行居中
    - 设置行高与元素的高度相同
    [http://codepen.io/chriscoyier/pen/LxHmK](http://codepen.io/chriscoyier/pen/LxHmK)
    - 为行内元素/文本元素设置相等的上下内边距
    [http://codepen.io/chriscoyier/pen/ldcwq](http://codepen.io/chriscoyier/pen/ldcwq)
- 多行居中
  - 设置相等的上下内边距
  - vertical-align 属性来实现垂直居中
  	[http://codepen.io/chriscoyier/pen/ekoFx](http://codepen.io/chriscoyier/pen/ekoFx)
  - flexbox
    [http://codepen.io/chriscoyier/pen/uHygv](http://codepen.io/chriscoyier/pen/uHygv)
  ``` CSS
  .flex-center-vertically {
    display: flex;
    justify-content: center;
    flex-direction: column;
    height: 400px;
  }
  ```

### 2.2 块级元素
- 元素高度已知
``` CSS
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  height: 100px;
  margin-top: -50px; /* account for padding and border if not using box-sizing: border-box; */
}
```
[http://codepen.io/chriscoyier/pen/HiydJ](http://codepen.io/chriscoyier/pen/HiydJ)
- **元素高度未知**（最常见的一种场景）
  - 方法一：先将元素相对于其原始位置向下移动父元素高度的一半距离，再将该元素相对其本身的高度向上移动一半，这样就能实现垂直居中的效果了。
  ``` CSS
  .parent {
    position: relative;
  }
  .child {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
  }
  ```
  [http://codepen.io/chriscoyier/pen/lpema](http://codepen.io/chriscoyier/pen/lpema)
   - 方法二：flexbox
  ``` CSS
  .parent {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  ```
  [http://codepen.io/chriscoyier/pen/FqDyi](http://codepen.io/chriscoyier/pen/FqDyi)

## 3. 垂直和水平都居中
当然，我们可以结合以上给出的方法来实现垂直和水平方向都居中的布局。这里我们再进行一下分类总结。
### 3.1 宽高固定
将元素相对于其父元素的宽度/高度值向右并向下移动一半的距离，然后再通过设置负边距值的方法，将元素相对于其自身的宽度/高度值向左并向上移动一半的距离，就可实现水平垂直均居中的效果了。并且这种方法的浏览器兼容性是很好的。
``` CSS
.parent {
  position: relative;
}

.child {
  width: 300px;
  height: 100px;
  padding: 20px;

  position: absolute;
  top: 50%;
  left: 50%;

  margin: -70px 0 0 -170px;
}
```
[http://codepen.io/chriscoyier/pen/JGofm](http://codepen.io/chriscoyier/pen/JGofm)

### 3.2 宽高不固定
如果元素的宽度或者高度未知，则在将元素相对于父元素的宽高往向右并向下移动一半距离后，再用 `transform` 属性来将其向左并向上移动自身宽度及高度值一半的距离即可。
``` CSS
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```
[http://codepen.io/chriscoyier/pen/lgFiq](http://codepen.io/chriscoyier/pen/lgFiq)

### 3.3 使用 flexbox
``` CSS
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
}
```
[http://codepen.io/chriscoyier/pen/msItD](http://codepen.io/chriscoyier/pen/msItD)

### 3.4 使用 grid
这只是一个小技巧，只适用于一个元素的情况。
<iframe src="http://codepen.io/chriscoyier/embed/NvwpyK" width="100%" height="305" frameborder="0"></ifream>

## 4. 结束语
CSS 还是很伟大的，能够实现的布局多种多样，实现的方法也多种多样，重要的是找到合适的方法！这就需要多写多练多总结！
