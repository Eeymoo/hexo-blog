---
title: 数组交集判断的性能优化：从双循环到双指针的多种方法
date: '2024-12-31 16:47:50'
updated: '2025-01-07 10:48:14'
excerpt: >-
  本文讨论了在权限判断逻辑中，如何优化判断两个数组是否存在交集的方法。首先介绍了双 For 循环的硬计算方法，时间复杂度为 O(n *
  m)，在性能上较低效。接着，通过使用 `some` 和 `includes` 方法优化了代码，尽管时间复杂度未变，但可读性更好。进一步采用
  `Set.has()` 替代 `includes` 提高了效率，因其时间复杂度更低。


  此外，介绍了使用双指针算法进行极端优化的思路，但需要对数组进行排序，虽然可能在性能上更优，但开发时间较长。在实际开发时，应根据项目需求平衡开发时间与性能优化，选择合适的方法进行实现。最后，文章提及了参考文献，解释了
  `Set.has()` 比 `Array.includes()` 更快的原因。
tags:
  - 性能优化
  - 开发技巧
categories:
  - JavaScript
permalink: /post/shu-zu-shi-fou-cun-zai-jiao-ji-de-xing-neng-you-hua-wen-ti-z1kwfix.html
comments: true
toc: true
---

![image](https://raw.githubusercontent.com/eeymoo/Eeymoo.github.io/main/images/unsplash-IIc73xHTRTg-20241231164817-xj40z5a.jpg)

# 数组是否存在交集的性能优化问题

> 本文使用 `gpt-3.5-turbo`​ 协助完成。

在项目中出现一个这样的权限判断逻辑，存在两个数组，一个是后端返回的所有权限数组，另一个是前端代码中存在的按钮权限数组，我们要判断这两个数组是否存在交集合，如果存在交集就说明具备这个按钮的权限，这个按钮就可以展示。

遇到数组交集的判断存在几种复杂或者简单的思路，一种是硬计算，使用双 for 循环判断，但是这种方式无疑是时间复杂度最大的，也可以使用数组的高阶函数进行判断，这两种时间复杂度相对较高，也可以使用 `Set.has()`​ 进行判断，但是不知道时间复杂度是否会将度，不过这无可厚非，这也是一种简单的写法，最起码代码便简单了，看起来更舒服，当然也存在一些高阶算法写法，比如双指针算法，会极大程度降低时间复杂度，不过暂时不考虑。

## 双 For 循环硬计算

我们已知双 For 循环的时间复杂度是 O(n * m)，这里的 n 和 m 分别是两个数组的长度。

```js
const hasIntersection (arr1, arr2) => {
    for (let i = 0; i < arr1.length; i++) { // 遍历第一个数组
        for (let j = 0; j < arr2.length; j++) { // 遍历第二个数组
            if (arr1[i] === arr2[j]) {
                return true;
            }
        }
    }
    return false;
}
```

## 使用 `some`​ 和 `includes`​

我们可以使用 `some`​ 和 `includes`​ 优化代码，时间复杂度同上，但是代码更加简洁。

```js
const hasIntersection (arr1, arr2) => {
	return arr.some(
		item => arr2.includes(item)
	);
}
```

## 使用 `Set.has`​ 和 `some`​

当然我们也可使用 `Set.has`​ 来代替 `includes`​，而且 `Set.has`​ 的时间复杂度更低。

```js
‍const hasIntersection (arr1, arr2) => {
	const set = new Set(arr1);
	return arr.some(
		item => set.has(item)
	);
}
```

当然在考虑 `includes`​ 和 `Set.has`​ 复杂度的时候也要考虑其他内容，比如说数据集的大小，内容重复度之类，这里不做考虑，不过可以研究，详见参考内容。

## 双指针算法

在极端优化情况下可以使用双指针算法解决这类问题，当然在日常开发中，通常使用上述方法就可以解决问题，简单相对高效，没必要求极端性能，不过这里也给出极端思路解决。

```js
// 首先如果使用双指针算法解决这个问题首先要对内容进行排序，排序也要使用算法排序
// 我们这里不考虑排序算法，并且假定内容为数字
const hasIntersection = (arr1, arr2) => {
	let sortArr1 = sort(arr1);
	let sortArr2 = sort(arr2);
	let current1 = 0;
	let current2 = 0;
	while (current1 < sortArr1.length && current2 < sortArr2.length) {
		if (sortArr1[current1] < sortArr2[current2]) {
			current1 ++;
		} 
		else if (sortArr1[current1] > sortArr2[current2]) {
			current2 ++;
		} 
		else {
			return true;
		}
	}
	return false;
}

const sort = (arr) => arr.sort((a, b) => a - b);

const nums1 = [1, 2, 4, 7, 8, 10, 12];
const nums2 = [3, 4, 8, 9];

console.log(hasIntersection(nums1, nums2));
```

在实际解决问题中要是用开发时间短，性能较好的内容，没必要使用性能特别好，但是开发时间较长的内容（特殊行业除外），我们要结合项目的实际需要实现这样的功能，开发也是妥协的艺术，做开发时间和性能的妥协。

‍

参考文献：

1. [性能对比：为什么 Set.has() 比 Array.includes() 更快？](https://blog.csdn.net/qq_41865545/article/details/143502905)
