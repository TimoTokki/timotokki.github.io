---
layout: post

title: JSDOM`s Notes
---

## 性能优化

+ 尽量少访问DOM

+ 尽量减少文档（比如HTML文档）中不必要的元素，以避免增加生成DOM即文档树（document tree）的负担。

+ 合并脚本，即把多个JS文件合并在一个JS文档中，以减少加载页面时发送的请求数量。

+ 将JS脚本放置在文档末尾。

+ 利用压缩脚本工具，去掉不必要的空格、换行符，甚者简化变量名。

## 不推荐的方法

+ javascript:伪协议（href = 'javascript:functionname(agruements)'）以及内嵌的事件处理函数（href = '#' onclick = 'functionname(agruements); ...'）；

+ 浏览器探测技术

+ document.write方法，违反了结构、行为分离的原则
+ ...

## 重点

+ W3C推出的标准化DOM可以让任意一种程序设计语言对使用任意一种标记语言编写的任意文档进行任意操控。

+ nodetype：

	+ 元素节点： 1

	+ 属性节点： 2

	+ 文本节点： 3

+ 平稳退化

+ 渐进增强

+ 质疑一切，不要假定，也就是说充分地进行对象探测，也不要假定任何函数都能够成功返回true。

+ nodeName属性总是返回一个大写字母的值，即使元素在HTML文档中是小写字母。

+ 三位一体的网页：结构层、表现层、行为层

+ innerHTML属性可直接给元素节点直接添加内容。

## 疑点

+ 一个元素节点的.childNodes包括属性节点吗？这些子节点如何排序？

+ DOM模型中只包括元素节点吗？
