---
title: JavaScript 对象属性顺序的探索与处理方法
date: '2023-08-18 17:47:53'
updated: '2025-01-07 10:52:23'
excerpt: >-
  本文探讨了 JavaScript 中对象（Object）的顺序问题。虽然 ES3 标准强调对象是无序的，但自 ES6
  以来，逐渐引入了属性顺序的概念。在不同浏览器中，对于 `for...in` 的处理和属性顺序的解析存在差异。一些浏览器遵循 ECMAScript
  第五版规范，而另一些则遵循第三版规范，因此对于对象的排序并不统一。为了避免因不同浏览器导致的排序不一致，建议将对象转换为数组形式（如 `[{ key,
  value }]`）进行处理，尽管在某些情况下，对象的键值可能会按照特定规则排列。文章最后提供了一些参考文献，以便进一步了解 JavaScript
  对象属性的顺序行为。
tags:
  - JavaScript
  - 对象排序
  - 无序性
  - ES6
  - 前端开发
permalink: /post/some-explorations-about-the-order-of-object-in-javascript-z1s1tng.html
comments: true
toc: true
---

![image](https://raw.githubusercontent.com/eeymoo/Eeymoo.github.io/main/images/unsplash-67wjyl7KzRM-20241231145826-n02gwny.jpg)

# 关于 JavaScript 中 Object 顺序的一些探索

面试中出现了一个题目：

> 将 对象 `{6: 46, 8: 23, 14: 5, 10: 3}` 按照值的顺序排列。

由于做开始他说的一个数组，说这个题的时候我以为是类数组对象，结果是是如上的对象，排序嘛，（不考虑时间复杂度和空间复杂度的话）基本上没什么难度， 但是一直有一个疑惑在脑中，Object 不是无序的吗？

> 本文主要探讨不同的 *Object* 定义方式（或者说声明方式）是否影响”*Object* 顺序“，”*Object* 顺序“是什么样的，以及常见处理”Object顺序“的方式。

首先再次之前我的认为是”对象是无序的，数组是有序的，如果处理对象的顺序的话，还是使用数组对象`[{key, value}]`的方式“ 。

在 [ECMA-262_3rd_edition_december_1999](https://www.ecma-international.org/wp-content/uploads/ECMA-262_3rd_edition_december_1999.pdf) 中有提到：

> 4.3.3 Object
> An **object** is a member of the type **Object**. It is an unordered collection of properties each of which contains a primitive value, object, or function. A function stored in a property of an object is called a method.

也就是在 ES3 中是 Objiect 是乱序的，但是在 ES6 中逐渐开始在 Object 的中开始添加 Object 部分放的顺序之说。

不同浏览器在处理 `for...in` 时的解析顺序时不同的，在 Chrome 和 Opera 中遵循的是 **ECMA-262** 第五版本规范，而在 Firefox 和 Safari遵循的是 **ECMA-262**  第三版本规范。

在通常情况下，如果要处理对象的排序，我建议使用数组处理，也就是将对象处理为 `[{ key, value }]` 这样的的数组形式，按照数组排序，因为我还是觉得对象是无序的，尽管他是按照一定的顺序排序的，但为了避免在不同的浏览器中的排序不同还是将他作为数组处理比较好。

### 参考文献

1. [js能够保证object属性的输出顺序吗？ - Jartto's blog](http://jartto.wang/2016/10/25/does-js-guarantee-object-property-order/)
2. [Does JavaScript guarantee object property order? - Stack Overflow](https://stackoverflow.com/questions/5525795/does-javascript-guarantee-object-property-order)
3. [ECMA-262_3rd_edition_december_1999](https://www.ecma-international.org/wp-content/uploads/ECMA-262_3rd_edition_december_1999.pdf)
