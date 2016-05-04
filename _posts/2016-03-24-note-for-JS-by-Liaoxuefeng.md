---
layout: post
tag:
    - JS
    - study notes
---

<a name="14946">

# JavaScript廖雪峰笔记

<div>

<table bgcolor="#D4DDE5" border="0">

<tbody>

<tr>

<td>**创建时间：**</td>

<td>_2016/3/7 13:00_</td>

</tr>

<tr>

<td>**更新时间：**</td>

<td>_2016/3/12 22:59_</td>

</tr>

<tr>

<td>**作者：**</td>

<td>_阿迪_</td>

</tr>

</tbody>

</table>

</div>

</a>

<div><a name="14946"><span></span></a>

<a name="14946"></a>
2.  <a name="14946">参考教程：</a>
    <a name="14946"></a>
    2.  <a name="14946">廖雪峰的JavaScript教程</a>[http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000)  

    3.  w3cschool的JavaScript教程[http://www.w3school.com.cn/js/js_intro.asp](http://www.w3school.com.cn/js/js_intro.asp)  

3.  感觉大体上和C的语法有相通之处
4.  strict模式  

    1.  JavaScript一开始为了方便学习，就不强制要求用var定义变量，但未用var定义的变量会被认为是全局变量，进而导致不同函数内的变量相互捣乱。所以，在后续的ECMA规范中，推出了strict模式，即要求所有变量必须用var定义，否则非法。在代码开头加上'use strict'即可开启strict模式。
5.  iterable类型：array,map,set
    1.  除了set外，array, map都有索引
    2.  函数new可创建iterable类型，例如：new map();
    3.  .forEach()方法：`iterable`<span>内置，</span><span>它接收一个函数，每次迭代就自动回调该函数。</span>
        *   .forEach(function (element, index, array) 

        *   .forEach(function (value, key, map) 

        *   <span style="font-family: Monaco, Courier, monospace;">参数位置固定，名字随意起</span>
6.  <span>`<span>for in 和for of</span>`</span>
    1.  <span>`<span>for of 是ES6引入的新的语法</span>`</span>
    2.  <span>`<span>for in遍历的是属性名字，所以会出现这样的问题：[JavaScript循环得到的是索引，还是value](JavaScript循环得到的是索引，还是value.html);而for of遍历的是集合本身的元素</span>`</span>
    3.  <span>`<span>`for`<span>循环的一个变体是</span>`for ... in`<span>循环，它可以把一个对象的所有属性依次循环出来：</span></span>`</span>
    4.  <span>`<span><span>由于</span>`Array`<span>也是对象，而它的每个元素的索引被视为对象的属性，因此，</span>`for ... in`<span>循环可以直接循环出</span>`Array`<span>的索引：</span></span>`</span>
    5.  <span>`<span>_请注意_<span>，</span>`for ... in`<span>对</span>`Array`<span>的循环得到的是</span>`String`<span>而不是</span>`Number`<span>。</span>  </span>`</span>
7.  <span>`<span>[JavaScript中==和===的区别](JavaScript中==和===的区别.html)  
    </span>`</span>
8.  <span>`<span>[JavaScript是动态语言](JavaScript是动态语言.html)  
    </span>`</span>
9.  <span>`<span>[JavaScrpt中null和undefined的区别](JavaScrpt中null和undefined的区别.html)  
    </span>`</span>
10.  <span>`<span>alert()函数——弹出一个框</span>`</span>  

    1.  用'+'连接要显示的元素。比如alert('Adi' + 'das');//显示Adidas;  

11.  chrome console可以调试javascript
12.  NAN这个特殊字符，跟谁都不相等，包括它自己
13.  最新的标准是ES6：2015年6月正式发布
14.  <span>JavaScript用一个</span>`{...}`<span>表示一个对象，键值对以</span>`xxx: xxx`<span>形式申明，用</span>`,`<span>隔开。注意，最后一个键值对不需要在末尾加</span>`,`<span>，如果加了，有的浏览器（如低版本的IE）将报错。</span>  

15.  <span>MAP:ES6新增</span>
    1.  <span>JavaScript的默认对象表示方式`{}`可以视为其他语言中的`Map`或`Dictionary`的数据结构，即一组键值对。</span>但是JavaScript的对象有个小问题，就是键必须是字符串。但实际上Number或者其他数据类型作为键也是非常合理的。为了解决这个问题，最新的ES6规范引入了新的数据类型`Map`。
16.  SET：ES6新增
    1.  只是一些KEY的集合，且不能有重复元素
17.  .forEach()是ES5.1新增语法
18.  函数定义和调用
    1.  [函数定义和调用](函数定义和调用.html)  

19.  变量作用域
    1.  [变量作用域](变量作用域.html)  

    2.  JS只有一个全局作用域。所以，不同JS文件的同名全局变量就会发生冲突
    3.  所以为了避免冲突，在一个文件内，最好只定义一个全局变量，然后<span>把其他剩余的变量和函数全部绑定到这个全局变量上。</span>

</div>