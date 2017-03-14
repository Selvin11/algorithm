
1. [插入排序](#1)
1. [归并排序](#1)


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
    // 归并排序  
    // 将数组分为两组，假设每组以从小至大排序，开始比较两组中的第一项
    // 将相对较小的付给空数组的第一项，然后将较小的数组的第二项继续与另一数组比较
    // 重复上述步骤

    /**
     * 原数组：arr = [start,end] 
     * middle：数组一分为二的位置
     */
    function merge(arr, start, middle, end) {
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
