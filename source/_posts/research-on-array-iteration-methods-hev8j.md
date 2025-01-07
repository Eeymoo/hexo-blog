---
title: 研究数组迭代方法：稀疏数组处理、多种遍历方式
date: '2024-12-31 14:21:53'
updated: '2025-01-07 10:44:16'
excerpt: >-
  本文探讨了数组的不同迭代方法及其在处理稀疏数组时的表现。稀疏数组中存在空槽，而不同的迭代方法对待这些空槽的方式各异。根据 MDN 的说明，旧的迭代方法如
  `forEach` 不会访问空槽，而其他方法（如 `concat`、`copyWithin`
  等）在复制时会保留这些空槽，因此最终数组仍为稀疏状态。相对地，新的迭代方法则将空槽视为包含
  `undefined`。文章列举了处理空槽和不对空槽进行特殊处理的常用数组方法，并总结了各自的特性，强调了在使用迭代方法时需要了解其对稀疏数组的行为，以便做出合适的选择。
tags:
  - 数组
  - 迭代
  - 稀疏
  - 方法
  - 异常处理
categories:
  - JavaScript
permalink: /post/research-on-array-iteration-methods-hev8j.html
comments: true
toc: true
---

![image](https://raw.githubusercontent.com/eeymoo/Eeymoo.github.io/main/images/unsplash-LuiP3ojMg5w-20241231143423-5i448yi.jpg)

# 数组迭代方法的研究

我们知道数组存在一些迭代方法将会遍历数组，在这篇文章中主要研究一些这些方法的相关问题，比如说[稀疏数组](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#%E7%A8%80%E7%96%8F%E6%95%B0%E7%BB%84)处理方法、如何打断、方法内异常处理等等。

## 稀疏数组处理方法

不同的迭代方法在处理稀疏数组的时候存在不同的方式，在 MDN 中指出，在旧的迭代方法中**处理空槽的方式与处理包含** **​`undefined`​**​ **索引的方式不同**，而在新的迭代方法中**不会对空槽进行特殊处理，而是将它们视为包含** **​`undefined`​**​。

在旧的方法中对空槽的方式是  **“诸如** **​`forEach`​**​ **之类的迭代方法根本不会访问空槽。其他方法，如** **​`concat`​**​ **、**​**​`copyWithin`​**​ **等，在进行复制时会保留空槽，因此最终数组依然是稀疏的。”**

以下数组对数组进行了特殊处理 [`concat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)​、[`copyWithin()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin)​、[`every()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/every)​、[`filter()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)​、[`flat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)​、[`flatMap()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap)​、[`forEach()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)​、[`indexOf()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)​、[`lastIndexOf()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)​、[`map()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)​、[`reduce()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)​、[`reduceRight()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight)​、[`reverse()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)​、[`slice()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)​、[`some()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/some)​、[`sort()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)​ 和 [`splice()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)​。

不对空槽进行特殊处理的方法，将其视为 `undifined` ​的方法有：[`entries()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)​、[`fill()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)​、[`find()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/find)​、[`findIndex()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)​、[`findLast()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast)​、[`findLastIndex()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findLastIndex)​、[`includes()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)​、[`join()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join)​、[`keys()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/keys)​、[`toLocaleString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/toLocaleString)​、[`values()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/values)​ 和 [`with()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/with)​。

**引用**

0. [MDN - 数组方法和空槽](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array#%E6%95%B0%E7%BB%84%E6%96%B9%E6%B3%95%E5%92%8C%E7%A9%BA%E6%A7%BD)

## 数组迭代方法的打断方式

> **如果需要在数组迭代时需要灵活的中断迭代，通常建议使用传统的** **​`for`​**​**循环或** **​`for...of`​**​**循环，这样可以更直接地使用** **​`break`​**​**来中断循环。**

当然我们也可以研究一些常见方法的打断方式，比如说，我们在方法外设置一个变量 `isBreak` ​作为判断是否是否需要打断的依据，在需要打断的地方将 isBreak 设置为 true，当然我们需要在方法的前面放一段特殊的代码。整体代码如下：

```js
let isBreak;

let arr = [1, 2, 3, 4, 5];
arr.forEach((item, idnex) => {
    if(idnex === 0){
        isBreak = false;
    }
    if(isBreak){
        return;
    }
    console.log(item);
    if(item === 3) {
        isBreak = true;
    }
})
```

在这个例子中，`isBreak`​ 用于控制循环是否继续。当遇到 `item === 3`​ 时，我们将 `isBreak`​ 设置为 `true`​，从而在下次迭代时跳过后续的逻辑。

当然也有一些方法自带打断，例如：

1. some 会在存在一个元素符合测试函数时，停止遍历，并且返回 true；
2. every 会在存在一个元素不符合测试函数是，停止遍历，并且返回 false；
3. find 和 findIndex 会在找到第一个符合的元素时，停止遍历，并且返回值或者索引；

## 数组迭代方法的异常处理

在数组迭代方法的异常处理中通常需要思考的问题主要是，出现异常是否继续执行接下来的迭代，如果需要执行接下来的迭代通常是将 try-catch 防止方法内，如果出现了异常将不需要迭代剩下的元素，就需要将 try-catch 放在方法外。

```js
let arr = [1, 2, 3, 4, 5];
arr.forEach(item => {
    try {
        if (item === 3) {
            throw new Error('Something went wrong!');
        }
        console.log(item);
    } catch (error) {
        console.error(`Error processing item ${item}: ${error.message}`);
    }
});

// 输出:
// 1
// 2
// Error processing item 3: Something went wrong!
// 4
// 5
```

在上面的代码中，假设在 item===3 的时候出现了一个不是很严重的问题，后续代码可以继续执行。

```js
let arr = [1, 2, 3, 4, 5];
try {
    arr.forEach(item => {
        if (item === 3) {
            throw new Error('Something went wrong!');
        }
        console.log(item);
    });
} catch (error) {
    console.error(`Iteration stopped due to error: ${error.message}`);
}

// 输出:
// 1
// 2
// Iteration stopped due to error: Something went wrong
```

‍
