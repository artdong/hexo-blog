---
title: js实现几种常见排序算法
date: 2019-07-02 16:30:11
categories: "js"
tags:
     - js
---

> ***

js实现几种常见排序算法。
 
冒泡排序：

{% img /gif/bubbleSort.gif %}

```javascript
const arr = [3, 44, 38, 5, 47, 15, 36, 26, 27, 2, 46, 4, 19, 50, 48];

function bubbleSort(arr) {
    let len = arr.length;
    if(len >= 1) {
        for(let i = 0;i < len - 1; i++) {
            for(let j = 0;j < len - 1 - i; j++) {
                if(arr[j] > arr[j + 1]) {
                    let temp = arr[j + 1];
                    arr[j + 1] = arr[j];
                    arr[j] = temp;
                }
            }
        }

    }
    return arr;
}

console.log(bubbleSort(arr));
```


 ***


 <!-- more -->

冒泡排序优化版： 

```javascript
const arr = [3, 44, 38, 5, 47, 15, 36, 26, 27, 2, 46, 4, 19, 50, 48];

function bubbleSort(arr) {
    let len = arr.length;
    let lastExchangeIndex = 0;
    //无序数列的边界，每次比较只需要比到这里为止
    let sortBorder = len - 1;
    if(len >= 1) {
        for(let i = 0;i < len; i++) {
            //有序标记，每一轮的初始是true
            let isSorted = true;
            for(let j = 0;j < sortBorder - i; j++) {
                if(arr[j] > arr[j + 1]) {
                    let temp = arr[j + 1];
                    arr[j + 1] = arr[j];
                    arr[j] = temp;
                    //有元素交换，所以不是有序，标记变为false
                    isSorted = false;
                    //把无序数列的边界更新为最后一次交换元素的位置
                    lastExchangeIndex = j;
                }
            }
            sortBorder = lastExchangeIndex;
            if(isSorted) { //有序,跳出循环
                break;
            }
        }

    }
    return arr;
}

console.log(bubbleSort(arr));
```

选择排序：

{% img /gif/selectSort.gif %}

```javacript
const arr=[3,44,38,5,47,15,36,26,27,2,46,4,19,50,48];

function selectionSort(arr) { 
    let len = arr.length;
    let minIndex, temp;
    for (let i = 0; i < len - 1; i++) {
        minIndex = i;
        for (let j = i + 1; j < len; j++) {
            if (arr[j] < arr[minIndex]) { 
                // 寻找最小的数
                minIndex = j; 
                // 将最小数的索引保存
            }
        }
        temp = arr[i]; 
        arr[i] = arr[minIndex];
        arr[minIndex] = temp; 
    } 
    return arr;
}

console.log(selectionSort(arr));
```

选择排序优化版：

```javascript
const arr = [3, 44, 38, 5, 47, 15, 36, 26, 27, 2, 46, 4, 19, 50, 48];

function selectionSort(arr) { 
    let len = arr.length;
    let left = 0;
    let right = len - 1;
    while (left < right) {
        let max = left;//记录无序区最大元素下标
        let min = left;//记录无序区最小元素下标
        let j = 0;
        for (j = left + 1; j <= right; j++) {
            //找最大元素下标
            if (arr[j] < arr[min])
            {
                min = j;
            }
            //找最小元素下标
            if (arr[j] > arr[max])
            {
                max = j;
            }
        }
        //最小值如果是第一个则没有必要交换
        if (min != left) {
            let tmp = arr[left];
            arr[left] = arr[min];
            arr[min] = tmp;
        }
        //这里很重要，如果最大元素下标是left,前面已经和最小元素交换了，此时最大元素下标应该是min
        if (max == left) {
            max = min;
        }
        //最大值如果是最后一个则没必要交换
        if (max != right) {
            let tmp = arr[right];
            arr[right] = arr[max];
            arr[max] = tmp;
        }
        left++;
        right--;
    }
	return arr;
}

console.log(selectionSort(arr));
```

插入排序：

{% img /gif/insertSort.gif %}

```javacript
const arr=[3,44,38,5,47,15,36,26,27,2,46,4,19,50,48];

function insertSort(arr) {
    const len = arr.length;
    let preIndex, current;
    for (let i = 1; i < len; i++) {
        preIndex = i - 1;
        current = arr[i];
        while (preIndex >= 0 && arr[preIndex] > current) {
            arr[preIndex + 1] = arr[preIndex];
            preIndex--;
        }
        arr[preIndex + 1] = current;
    }
    return arr;
}

console.log(insertSort(arr));
```

