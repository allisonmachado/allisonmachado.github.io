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

    let copy = (origin, destination, startIndex, endIndex) => {
        for (let i = startIndex, destinationIndex = 0; 
                 i <= endIndex; 
                 i++, destinationIndex++) { destination[destinationIndex] = origin[i]; }
    };

    let merge = (first, second) => {
        let tmp = new Array(first.length + second.length);
        let i = 0;
        let j = 0;
        let track = 0;

        while(i < first.length && j < second.length) {
            if (first[i] < second[j]) {
                tmp[track] = first[i];
                i++;
                track++;
            }
            else if (second[j] < first[i]) {
                tmp[track] = second[j];
                j++;
                track++;
            }
        }

        if (i < first.length) {
            while (i < first.length) {
                tmp[track] = first[i];
                i++;
                track++;
            }
        }
        else if (j < second.length) {
            while (j < second.length) {
                tmp[track] = second[j];
                j++;
                track++;
            }
        }

        return tmp;
    };

    let mergesort = (arr) => {
        if (arr.length == 1) return arr;

        let midIndex = Math.round(arr.length / 2);
        let firstHalf = new Array(midIndex - 1);
        let secondHalf = new Array(arr.length - midIndex);

        copy(arr, firstHalf, 0, midIndex - 1);
        copy(arr, secondHalf, midIndex, arr.length - 1);

        firstHalf = mergesort(firstHalf);
        secondHalf = mergesort(secondHalf);

        return merge(firstHalf, secondHalf);
    };

    let sort = (arr) => {
        return mergesort(arr);
    };

    console.log(numbers);
    let result = sort(numbers);
    console.log(result);
  </code>
</pre>
<h4 style="text-align-last: right;"> Performance: O(n log n), Space : O(n) </h4>

<h2 id="3-QuickSortFixedPivot">3 - Quick Sort Fixed Pivot</h2>

<pre>
  <code>
    let numbers = [7,5,6,3,1,2,0,4];

    let swap = (arr, i, j) => {
        let tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    };

    let partition = (arr, start, end) => {
        let pivot = arr[end];
        let reference = start;

        for (let i = start; i < end; i++) {
            if (arr[i] < pivot) {
                swap(arr, i, reference);
                reference++;
            }
        }

        swap(arr, end, reference);

        return reference;
    };

    let quicksort = (arr, start, end) => {
        if (start < end) {
            let pivotIndex = partition(arr, start, end);
            quicksort(arr, start, pivotIndex - 1);
            quicksort(arr, pivotIndex + 1, end);
        }
    };

    let sort = (arr) => {
        let start = 0;
        let end   = arr.length - 1;
        quicksort(arr, start, end);
    };

    console.log(numbers);
    sort(numbers);
    console.log(numbers);
  </code>
</pre>
<h4 style="text-align-last: right;"> Performance: O(n<sup>2</sup>), Space : O(n) </h4>

<h2 id="4-QuickSortMiddlePivot">4 - Quick Sort Middle Pivot</h2>

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
<h4 style="text-align-last: right;"> Performance: O(n<sup>2</sup>), Space : O(n) </h4>
