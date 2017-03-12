
1. [排序](#1)


<h3 id="1">1. 排序</h3>
* 插入排序

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
