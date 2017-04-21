
1. [插入排序](#1)
2. [归并排序](#2)
3. [冒泡排序](#3)
4. [选择排序](#4)

<h3 id="1">1. 插入排序</h3>

  ```javascript 
    for (var j = 1; j < arr.length; j++){
        var key = arr[j]; // 从第二个开始，与前面一个比较大小
        var i = j - 1;
        while (i >= 0 && arr[i] > key){
            arr[i+1] = arr[i];
            i = i - 1;
        }
        arr[i+1] = key; // 如果前者比后者小，则不变
    }
  ```


<h3 id="2">2. 归并排序</h3>

  ```javascript 
   /**
     * 原数组：arr = [start,end] 
     * middle：数组一分为二的位置
     */
    function merge(arr, start, middle, end) {
    // 将数组分为两组，假设每组以从小至大排序，开始比较两组中的第一项
    // 将相对较小的付给空数组的第一项，然后将较小的数组的第二项继续与另一数组比较
    // 重复上述步骤
        // 将数组一份为二
        var n1 = middle - start + 1, // 左边数组的长度
            n2 = end - middle; // 右边数组的长度

        var left = [], // 左边的数组
            right = []; // 右边的数组

        // 从arr中赋值给left
        for (let i = 0; i < n1; i++) {
          left[i] = arr[start + i];
        }
        // 从arr中赋值给right
        for (let j = 0; j < n2; j++) {
          right[j] = arr[middle + j + 1];
        }

        // !!!! 数组从零开始的，初始已经+1，因此这里的哨兵直接赋值给最后一个元素即可
        left[n1] = Number.POSITIVE_INFINITY;
        right[n2] = Number.POSITIVE_INFINITY;

        let l = 0, r = 0;
        for (let k = start; k <= end; k++) {
          
          // 从两个数组的第一项开始比较
          if (left[l] <= right[r]) {
            arr[k] = left[l];
            l = l + 1;

          }else{
            arr[k] = right[r];
            r = r + 1;
          }
          
        }
    }
    
    function merge_sort(arr,start,end) {
        // 保证数组长度 > 1
        if (start + 1 < end) {
          var middle = Math.floor((start + end)/2);
          merge_sort(arr,start,middle);
          merge_sort(arr,middle+1,end);
          merge(arr,start,middle,end);
        }
    }
    
    // example
    merge_sort([1,2,4,2,5],0,4);
  ```
<h3 id="3>3. 冒泡排序</h3>
```javascript
function bubbleSort(arr) {
    console.time('冒泡排序耗时');
    for (var i = 0; i < arr.length; i++) {
        // 从第一个数开始依次向右比较大小，比较arr.length次
        for (var j = 0; j < arr.length - 1 - i; j++) {
          // 依次比较，比较arr.length - 1 -i()
          // 减 1 是因为两两比较，比较次数会因为没有自我比较少一次
          // 减 i 是因为每一轮比较完之后，最后一个值就是当前最大的，因此不用参与比较
          // 前者比后者大则交换数值
            if (arr[j] > arr[j + 1]) {
                var small = arr[j + 1];
                arr[j + 1] = arr[j];
                arr[j] = small;
                arrState.push(deepCopy(arr));
            }
        }
    }
    console.timeEnd('冒泡排序耗时');
    return arr;
}
// 改进版，增加pos参数记录每次轮询排序之后最后交换的位置索引
function bubbleSort(arr){
  var i = arr.length - 1; 
  while (i > 0){
    var pos = 0; // 每次轮询排序均从起始位置开始
    for(var j = 0; j < i; j++){
      if(arr[j]>arr[j+1]){
        pos = j; // 前者比后者大，进行位置交换，并记录该值
        var key = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = key;  
      }
    }
    i = pos;
  }
  return arr;
}
```
<h3 id="4>4. 选择排序</h3>
```javascript
function selectionSort(arr) {
  // 原数组称为无序区，排序之后的称为有序区 temp
  // 从原数组轮询，查出每次最小（大）值，与有序区首位进行交换，轮询加1
  // 无序区记录减一，有序区记录加一
  var len = arr.length;
  var minIndex, temp;
  console.time('选择排序耗时');
  for (var i = 0; i < len - 1; i++) {
    minIndex = i;
    for (var j = i + 1; j < len; j++) {
      if (arr[j] < arr[minIndex]) {     //寻找最小的数
        minIndex = j;                 //将最小数的索引保存
      }
    }
    temp = arr[i];
    arr[i] = arr[minIndex];
    arr[minIndex] = temp;
    arrState.push(deepCopy(arr));
  }
  console.timeEnd('选择排序耗时');
  return arr;
}
```