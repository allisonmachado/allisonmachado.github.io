---
layout: post
title:  Ensaiando Ordenação (JS)
tags:
- JS
- Algorithms
---

<h2 id="1-SelectionSort">0 - Selection Sort</h2>

<pre>
  <code>
    let numbers = [7,5,6,3,1,2,0,4];

    let swap = (arr, i, j) => {
        let tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    };

    let selectionsort = (arr) => {
      let index = 0;
      
      while(index < arr.length) {
        let min = Infinity;
        let minIndex = null;
        for(let i = index; i < arr.length; i++) {
          if (arr[i] < min) {
            min = arr[i];
            minIndex = i;
          }
        }
        if (!!minIndex) {
          swap(arr, minIndex, index);
        }
        index++;
      }
    }

    let sort = (arr) => {
        selectionsort(arr);
    };

    console.log(numbers);
    sort(numbers);
    console.log(numbers);
  </code>
</pre>
<h4 style="text-align-last: right;"> Performance: O(n<sup>2</sup>), Space : O(1) </h4>

<h2 id="1-BubbleSort">1 - Bubble Sort</h2>

<pre>
  <code>
    let numbers = [7,5,6,3,1,2,0,4];

    let swap = (arr, i, j) => {
        let tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    };

    let bubblesort = (arr) => {
      let sorted = false;

      while(!sorted) {
          sorted = true;

          for (let i = 0; i < arr.length - 1; i++) {
              if (arr[i] > arr[i + 1]) {
                  swap(arr, i, i + 1);
                  sorted = false;
              }
          }
      }
    };

    let sort = (arr) => {
        bubblesort(arr);
    };

    console.log(numbers);
    sort(numbers);
    console.log(numbers);
  </code>
</pre>
<h4 style="text-align-last: right;"> Performance: O(n<sup>2</sup>), Space : O(1) </h4>

<h2 id="2-MergeSort">2 - Merge Sort</h2>

<pre>
  <code>
    let numbers = [7,5,6,3,1,2,0,4];

    let merge = (main, helper, low, middle, high) => {
        for (let i = low; i <= high; i++) {
            helper[i] = main[i];
        }

        let helperLeft = low;
        let helperRight = middle + 1;
        let current = low;

        while(helperLeft <= middle && helperRight <= high) {
            if(helper[helperLeft] < helper[helperRight]) {
                main[current] = helper[helperLeft];
                helperLeft++;
            }
            else {
                main[current] = helper[helperRight];
                helperRight++;  
            }
            current++;
        }

        if (helperLeft <= middle) {
            while(helperLeft <= middle) {
                main[current] = helper[helperLeft];
                helperLeft++;
                current++
            }
        }
    }

    let mergesort = (arr, helper, low, high) => {
        if (low < high) {
            let middle = Math.round(((low + high) / 2) - 1);
            mergesort(arr, helper, low, middle);
            mergesort(arr, helper, middle + 1, high);
            merge(arr, helper, low, middle, high);
        }
    }

    let sort = (arr) => {
        let helper = new Array(arr.length);
        return mergesort(arr, helper, 0, arr.length - 1);
    };

    console.log(numbers);
    sort(numbers);
    console.log(numbers);
  </code>
</pre>
<h4 style="text-align-last: right;"> Performance: O(n log n), Space : O(n) </h4>

<h2 id="3-QuickSortMiddlePivot">3 - Quick Sort Middle Pivot</h2>

<pre>
  <code>
    let numbers = [ 9, 8, 7, 6, 5, 4, 3, 2, 1, 0 ];

    let swap = (arr, i, j) => {
        let tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    };

    let partition = (arr, start, end, pivot) => {
        while(start < end) {
            while(arr[start] < pivot) {
                start++;
            }
            while(arr[end] > pivot) {
                end--;
            }
            if (start < end) {
                swap(arr, start, end);
            }
        }

        return start;
    };

    let quicksort = (arr, start, end) => {
        if (start < end) {
            let pivot = arr[Math.round((start + end)/2)];
            let index = partition(arr, start, end, pivot);
            quicksort(arr, start, index - 1);
            quicksort(arr, index + 1, end);
        }
    };

    let sort = (arr) => {
        quicksort(arr, 0, arr.length - 1);
    };

    console.log(numbers);
    sort(numbers);  
    console.log(numbers);
  </code>
</pre>
<h4 style="text-align-last: right;">Performance: O(n log n), Space : O(n) </h4>
