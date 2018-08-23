title: CSS-Sticky-Footer
author: Yan Congwen
tags:
  - CSS
categories: []
date: 2017-07-28 19:21:00
---
## 什么是 Sticky Footer 
&emsp;&emsp;Sticky Footer 即绝对底部。具体效果就是：当页面内容超出屏幕，页脚模块会像正常页面一样，被推到内容下方，需要拖动滚动条才能看到。而当页面内容小于屏幕高度，页脚模块会固定在屏幕底部，就像是底边距为零的固定定位。    
![](http://img.yancongwen.cn/18-7-28/37046212.jpg)

## 常见解决方法
- 经典思路
    HTML：  
    ```
    <div class="wrap">
        <div class="content">
            <p>内容</p>
        </div>
    </div>
    <div class="footer">
        <p>页脚</p>
    </div>
    ```
    CSS：
    ```
    html,body {
        height: 100%;
    }
    body > .wrap {
        min-height: 100%;
    }
    .content {
        /* padding-bottom 等于 footer 的高度 */
        padding-bottom: 60px;
    }
    .footer {
        width: 100%;
        height: 60px;
        /* margin-top 为 footer 高度的负值 */
        margin-top: -60px;
    }
    ```

- Flexbox解决方案	
    HTML：
    ```
    <div class="content">
        <p>内容</p>
    </div>
    <div class="footer">
        <p>页脚</p>
    </div>
    ```
    CSS：
    ```
    html, body {
        display: flex;
        height: 100%;
        flex-direction: column;
    }
    body .content {
        flex: 1;
    }
    ```
- 固定高度的解决方案(不推荐)	
    HTML：
    ```
    <body>
    　　<div class="content"></div>
    　　<div class="footer"></div>
    </body>
    ```
    CSS：
    ```
    .content{
        min-height:calc(100vh-footer的高度);
        box-sizing:border-box;
    }
    ```
