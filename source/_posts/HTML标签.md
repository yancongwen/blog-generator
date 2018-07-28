title: HTML标签
tags:
  - HTML
categories: []
date: 2017-04-13 19:46:00
---
## 1、iframe 标签
iframe 元素会创建包含另外一个文档的内联框架,相当于是一个独立的新窗口；
- src 属性，窗口对应的链接地址，支持相对路径；
- frameborder 属性，一般会设置 `frameborder=0`，表示没有边框；
- name 属性，框架名称，一般配合 a 标签使用；
``` HTML
<iframe name="xxx" src="http://www.baidu.com" frameborder="0"></iframe>
<a href="http://www.qq.com" target="xxx">在iframe中打开QQ页面</a>
```

## 2、a 标签
定义超链接
- href 属性 ，指示链接的目标
    - 常规：`href="http://www.qq.com"`
    - 省略协议，就会使用当前协议：`href="www.qq.com"`
    - 相对路径：`href="/index.html"`
    - 空值：`href="" `(会请求当前页面，极少使用)
    - 查询参数：`href="?name=xxx" `（会触发请求）
    - 锚点：`href="#top"`（只有锚点的话不会触发请求）
        - `href="#" `，空锚点，会指向页面顶部；
        - 关于锚点定位，更多知识可以看张鑫旭文章[《URL锚点HTML定位技术机制、应用与问题》](http://www.zhangxinxu.com/wordpress/2013/08/url-anchor-html-%E9%94%9A%E7%82%B9%E5%AE%9A%E4%BD%8D%E6%9C%BA%E5%88%B6-%E5%BA%94%E7%94%A8-%E9%97%AE%E9%A2%98/)
    - javascript伪协议：`href="javascript: js代码段"`
        - `href="javascript: ;" `，这种方法是很多网站最常用的方法，也是最周全的方法，既不会做请求、不会跳转页面，也不会改变当前页面位置，还能达到想要的效果；
        - `href="javascript: void(0);" `，和上面这种用法类似，类似的还有一些，请看[这里](https://segmentfault.com/q/1010000000339082)；
        - 在浏览器地址栏输入 "javascript: alert('hello')" 同样会执行js代码；
        - W3C标准不推荐在href里面执行javascript语句；
- target 属性，指定窗口
    - _blank：新窗口
    - _self：当前，默认值
    - _parent：父框架
    - _top：最顶层,即在整个窗口中打开被链接文档
    - framename：指定 iframe 内联框架名称
- download 属性，规定被下载的超链接目标
    - href 属性中就是下载内容的地址
    - download 属性值就是下载文件的文件名
    ```
    <a href="http://img.yancongwen.cn/18-4-12/34996969.jpg" download="ycw.jpg">下载图片</a>
    ```
## 3、from 标签
表示了文档中的一个区域，这个区域包含有交互控制元件，用来向服务器提交信息。；表单能够包含 input 元素，比如文本字段、复选框、单选框、提交按钮等；
- action 属性，URL值，绝对路径或相对路径，规定当提交表单时向何处发送表单数据
- method 属性，规定用于发送 form-data 的 HTTP 方法，只能是 GET 或者 POST，其它方法无效（a 标签只能用 GET）
    - POST (最常用)    
    POST 请求会将数据包含在 HTTP 请求体的第四部分中
    - GET (一般不用)    
    GET 请求会将数据以参数的形式附在请求URL后面
- target 属性，和 a 标签中用法相同
- name 属性，
- 其他注意点：
    - form 标签中 input 标签必需要有 name 属性值，否则对应数据不会被提交；
    - form 标签中必须要有一个 submit 按钮才能被提交，正是因为有 submit 按钮，才能按 <kbd>回车</kbd> 提交表单；
    - 如果一个 form 标签中没有 submit 按钮 `<input type='submit'>`， 而有 `<button></button>`，则 button 会默认为 submit 按钮，若写成这样 `<button type='button'>button</button>`” 则不会成为 submit;
    - form 提交会刷新页面；

## 4、input\button 标签
- label 的两种用法，推荐第二种
``` HTML
    <label id="name">名字：</label><input type="text" name="xxx" for="name">
    <label>名字：<input type="text" name="xxx" for="name"></label>
```
- button
    - type 属性
        - submit， 提交表单数据，表单中未指定时，此值为默认值；
        - reset，重置所有组件为初始值；
        - button，没有默认行为；
        - menu，打开一个由指定 `<menu\>` 元素进行定义的弹出菜单；
- input
    - type 属性
        - text，默认
        - button、reset、submit
        - checkbox、radio
        - date、datetime、datetime-local、month、time、week
        - color
        - file
        - number
        - password
        - email
        - range
        - serch
        - url
        - tel
        - hidden
    - name 属性，必须有
    - 详细细节请看 MDN 文档
    - input 标签的 button、reset、submit 按钮和 button 标签区别主要在于 input 标签只支持文本内容，不能再包含其他标签，但是 button 标签可以。button 比 input 更容易使用样式。

## 5、table 标签
- 过去 table 常用语页面布局，现在不推荐，专业的事情交给专业的人来做；
- 应当使用 CSS 定制 table 样式的样式，不推荐使用table标签中的属性设置（诸如：align、border、bgcolor、cellpadding、cellspacing 等不在推荐使用）；
- thead tbody tfoot不写浏览器也不会报错，而会自动补全；
- colgroup 用于定义数据列的样式
``` HTML
<table border="1">
    <colgroup>
        <col width="100">
        <col bgcolor="red" width="200">
        <col width="100">
        <col width="100">
    </colgroup>
    <thead>
        <tr>
            <th>姓名</th><th>数学</th><th>语文</th><th>总分</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>小明</th><td>100</td><td>100</td><td>200</td>
        </tr>
        <tr>
            <th>小白</th><td>100</td><td>99</td><td>199</td>
        </tr>
        <tr>
            <th>小黑</th><td>99</td><td>99</td><td>198</td>
        </tr>
    </tbody>
    <tfoot>
    <tr>
        <th>平均分</th><td>100</td><td>99</td><td>199</td>
    </tr>
    </tfoot>
</table>
```
![](https://img.yancongwen.cn/18-4-14/87365473.jpg)