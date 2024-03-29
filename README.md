# Sorting-Algorithms
## Overview

| Sorting Algorithm | Best-case Time Complexity | Worst-case Time Complexity | Space Complexity | Stable? | Inplace? |
|-------------------|---------------------------|----------------------------|------------------|---------|----------|
| Bubble Sort       | &Theta;(N)                | &Theta;(N<sup>2</sup>)     | &Theta;(1)       | Yes     | Yes      |
| Heap Sort         | &Theta;(N)                | &Theta;(NlogN)             | &Theta;(1)       | No      | Yes      |
| Insertion Sort    | &Theta;(N)                | &Theta;(N<sup>2</sup>)     | &Theta;(1)       | Yes     | Yes      |
| Merge Sort        | &Theta;(NlogN)            | &Theta;(NlogN)             | &Theta;(N)       | Yes     | No       |
| Quicksort         | &Theta;(NlogN)            | &Theta;(N<sup>2</sup>)     | &Theta;(N)       | No      | Yes      |
| Selection Sort    | &Theta;(N<sup>2</sup>)    | &Theta;(N<sup>2</sup>)     | &Theta;(1)       | No      | Yes      |
| Shell Sort        | &Theta;(NlogN)            | &Theta;(N<sup>2</sup>)     | &Theta;(1)       | No      | Yes      |

where N is the length of the array to be sorted

## Bubble Sort
### How It Works
Bubble Sort works by taking every element (starting from the leftmost element) and comparing it with every other element (from left to right), swapping them if the element on the left is greater than the element on the right. At the end of each pass, the next largest element will be in its correct position. 

In other words, at the end of the first pass, the largest element will be at the end of the array (rightmost element), at the end of the second pass the second largest element will be at the position to the left of the largest element and so on. If a full pass completes without any swaps being made, we know the array is sorted and do not have to continue any further. 

### Space and Time Complexity
Bubble Sort has a worst-case time complexity of &Theta;(N<sup>2</sup>) due to the two nested for-loops the algorithm requires. Both of these for-loops iterate over (almost) the entire length of the array (N), leading to this order of growth.

Bubble Sort has a best-case time complexity of &Theta;(N) as we can exit the loops if we go through a full pass and find no swaps occurred. This only occurs when the array to be sorted is in fact already sorted.

Bubble Sort is both a stable and in-place sorting algorithm. It does not require any additional memory meaning it has a worst-case space complexity of &Theta;(1).

### Potential Improvements
- **Already Sorted Arrays** - exiting the loops if the array is already sorted is worthwhile as it results in a performance of &Theta;(N) in the case that the array is already sorted. (I have implemented this improvement in my algorithm)
- **Reducing Length of Inner Loop** - with the knowledge that after every pass the next largest element will be in its correct position towards the end of the array, we can reduce the length of the array we have to traverse in every pass of the inner loop. Instead of going through the entire length of the array, we can offset it with the current position of the outer for loop. In other words, instead of `for(int j = 0; j < array.length - 1; j++)`, we can have `for(int j = 0; j < array.length - i - 1)`(I have implemented this improvement in my algorithm)

### Uses and Final Thoughts
Bubble Sort is a simple sorting algorithm and has as advantage over many sorting algorithms (but not Insertion Sort) in that it can detect when the array is already sorted. However, in reality, there are far better algorithms for efficiency and Bubble Sort's order of growth makes it unusable for larger input sizes. For these reasons, it is rarely used other than for educational purposes. 

## Heap Sort
### How It Works
Heap Sort works by treasting the unsorted input array as a complete binary tree. From there, we can construct a maximum binary heap. Once this is done, the maximum element can be removed repeatedly and placed at its correct final position in the array, leading to a fully sorted array.

### Space and Time Complexity
Heap Sort has a worst-case time complexity of &Theta;(NlogN) as the array is treated like a maximum binary heap leading to this order of growth. This is the best possible worst-case time complexity possible (without relying on other special cases).

Heap Sort has a best-case time complexity of &Theta;(N) in the case that the array is already in a maximum binary heap meaning that no initial construction of the maximum binary heap is needed, leading to this order of growth.

Heap Sort is not stable but is an in-place sorting algorithm. It does not require any additional memory meaning it has a worst-case space complexity of &Theta;(1).

### Potential Improvements
- **Bottom-Up HeapSort** - the number of comparisons required can be reduced by implementing a bottom-up approach. In the standard top-down approach, when a largest element is removed from the heap, it is replaced by an element from the lowest level of the heap and then is sunk down to its correct position to restore the maximum binary heap. However, this element taken from the bottom level is usually one of the smallest elements in the heap meaning it takes more steps and therefore more comparisons to sink the element back down the heap to its correct position. In the bottom-up approach, it finds a leaf which has the property that it and all of its ancestors are greater than or equal to their siblings (similar to insertion in a binary heap), and then searches upward from this leaf for the correct position to insert the element taken from the bottom level to replace the largest element that was removed. Both approaches result in the same binary heap state, however, the bottom-up approach requires only one comparison per level which is far less than that of the top-down approach. [See here for more information.](https://en.wikipedia.org/wiki/Heapsort#Variations) (I have not implemented this improvement in my algorithm)
- **Ternary HeapSort** - using a ternary heap instead of a binary heap can have some performance improvements but is far more complicated to program. A ternary heap would have three children for each node in the ternary heap as opposed to the two children in a binary heap. (I have not implemented this improvement in my algorithm)

### Uses and Final Thoughts

## Insertion Sort
### How It Works
Insertion Sort works by splitting the array conceptually into two parts: a sorted part and an unsorted part. At the beginning of the algorithm, the sorted part consists of just the leftmost element (i.e. the element at index 0), while the remaining elements exist in the unsorted part. 

With every pass, the algorithm takes the first element in the unsorted part and places it in the correct position in the sorted part. For example, in the first pass, the first element in the unsorted part is at index 1. This element is compared with all elements in the sorted part (just the element at index 0 at this point) and inserted accordingly. With every pass, the sorted part grows by one and the unsorted part shrinks by one until the unsorted part is empty.

### Space and Time Complexity
Insertion Sort has a worst-case time complexity of &Theta;(N<sup>2</sup>) due to the nested while-loop within a for-loop the algorithm requires. Both of these loops iterate over (almost) the entire length of the array (N), leading to this order of growth.

Insertion Sort has a best-case time complexity of &Theta;(N) as the while-loop will not be entered if every element that is being inserted is greater than the largest element currently in the sorted part. This only occurs when the array to be sorted is in fact already sorted.

Insertion Sort is both a stable and in-place sorting algorithm. It does not require any additional memory meaning it has a worst-case space complexity of &Theta;(1).

### Potential Improvements
- **Swap Elements Before Sorting** - by comparing array[0] with array[array.length - 1] and swapping accordingly, comparing array[1] with array[array.length - 2] and swapping accordingly and so on, we can drastically improve the number of comparisons needed within the Insertion Sort algorithm. [See here for more information.](http://ijcset.com/docs/IJCSET13-04-05-068.pdf) (I have not implemented this improvement in my algorithm)

### Uses and Final Thoughts
Insertion Sort is widely used, particularly in improving other algorithms for small input sizes. Insertion Sort works very well in cases where the array is sorted or almost sorted, resulting in many algorithms switching to Insertion Sort once the array is almost sorted (Heap Sort, Merge Sort and Quicksort are some algorithms that can take advantage of switching to Insertion Sort for small input sizes). However, it is not useful on its own for sorting large input sizes due to its order of growth. 

## Merge Sort
### How It Works
Merge Sort works by dividing the array into two halves (repeatedly) and then merging the two sorted halves afterwards. Merge Sort can be implemented in two different ways: using a top-down approach (which is recursive) or using a bottom-up approach (which is iterative).

In the top-down approach, the array is divided in two and the Merge Sort is recursively called on the two halves. Once the subarrays created by this consist of just a single element, the process of merging the subarrays can begin. As the recursion unravels, the subarrays are merged with each other such that the merged array is in sorted order.

In the bottom-up approach, the array is also divided in two halves but two for-loops are used instead of recursive calls to Merge Sort. The loops start by merging subarrays of size 1, then merging the subarrays of size 2, then merging the subarrays of size 4, then 8, and so on until all sorted subarrays have been merged into an array in sorted order.

In both approaches, merging the subarrays together plays an important role. This is done by making use of an auxiliary array. Firstly, the elements from the two subarrays are copied to this auxiliary array before they are merged back into the original such that they are in sorted order. 

### Space and Time Complexity
Merge Sort has a worst-case time complexity of &Theta;(NlogN) as the array is continuously divided in halves and the merging of these subarrays takes linear time, leading to this order of growth. This is the best possible worst-case time complexity possible (without relying on other special cases).

Merge Sort has a best-case time complexity of &Theta;(NlogN) as the array is continuously divided in halves and the merging of these subarrays takes linear time, leading to this order of growth.

Merge Sort is stable but is not an in-place sorting algorithm. It requires additional memory for the auxiliary array meaning it has a worst-case space complexity of &Theta;(N).

### Potential Improvements
- **Use Insertion Sort For Small Subarrays** - by making use of Insertion Sort instead of performing additional merges when the array is nearly sorted (<10 items left to be sorted), the performance can be improved. (I have not implemented this improvement in my algorithm)
- **Stop Merging If Already Sorted** - by checking if the largest element in the first half is smaller than the smallest element in the second half, we can determine whether the array is already sorted. If this is the case, we can prevent the algorithm from doing pointless merges and hence improve performance. (I have implemented this improvement in my algorithm)
- **Eliminate Time Taken To Copy To The Auxiliary Array** - we can use the two recursive invocations of Merge Sort (in the top-down approach) to eliminate the time taken to copy the subarrays to the auxiliary array. This is done by alternating which array is considered the input and which gets the sorted output, i.e. in one the input is the array itself and it puts the sorted output in the auxiliary array while in the other the auxiliary array is the input and it puts the sorted output in the array itself. (I have not implemented this improvement in my algorithm)

### Uses and Final Thoughts
Merge Sort is stable and has the best possible worst-case performance (&Theta;(N)), which makes it very useful. While it is worse than Quicksort in the average case, it is still widely used and provides guarantees that Quicksort cannot provide. In particular, it is excellent for sorting linked lists.

## Quicksort
### How It Works
Quicksort works by recursively partitioning the array around a pivot. In other words, Quicksort takes an arbitrary element, called the pivot, and places all elements smaller than that element to the left and all elements larger than that element to the right. This process is repeated recursively to sort the array.

The partitioning is where the sorting happens. In this partitioning, we take the the first element in the array to be our pivot (this is an implementation decision - the pivot could be any other element). We then continuously find both the leftmost element larger than the pivot and the rightmost element smaller than the pivot. These elements are then swapped. This process stops once all elements greater than the pivot lie to its right and all elements smaller lie to its left.

With each recursive call, the array is broken down into two smaller subarrays, which eventually leads to the subarrays of one or two elements, which will be in sorted order following partitioning. The recursive unravelling from this point leaves the array in a sorted state.

### Space and Time Complexity
Quicksort has a worst-case time complexity of &Theta;(N<sup>2</sup>) due to the fact that if the pivot chosen is the largest or smallest element in that subarray, we are essentially only going to have elements to the left or right of the pivot. This leads to many more recursively calls and this order of growth. This performance happens when the array is almost sorted or completely sorted, hence it is recommended to shuffle the array prior to sorting.

Quicksort has a best-case time complexity of &Theta;(NlogN) as in an ideal scenario, the pivot chosen results in half the elements lying to its left and the other half to its left. This would divide the array in half with each recursive call and lead to this performance.

Quicksort is not stable but is an in-place sorting algorithm. However, it does require additional memory due to the recursive calls meaning it has a worst-case space complexity of &Theta;(N). This worst-case space complexity can be improved to &Theta;(N) with some minor modifications to the algorithm.

### Potential Improvements
- **Shuffle Array Before Sorting** - as mentioned previously, Quicksort has quadratic performance in cases where the array is sorted or almost sorted. Hence, by shuffling the array prior to sorting, we can minimise the chance of this performance occurring. (I have implemented this improvement in my algorithm)
- **Use Insertion Sort For Small Subarrays** - by making use of Insertion Sort instead of performing additional partitions when the subarray size becomes relatively small (<10), the performance can be improved. (I have not implemented this improvement in my algorithm)
- **Use Median Value For Pivot** - ideally, the pivot would be the middle element but the time it would take to calculate this precisely would far outweigh the performance benefit. However, we could take the median of a small number of values (say the first three elements) which may lead to better performance. (I have not implemented this improvement in my algorithm)
- **3-Way Quicksort** - instead of partitioning elements into smaller than and larger than subarrays, we could partition the array into smaller than, equal to and larger than subarrays. This prevents poor performance when many of the same element exist in the array. (I have not implemented this improvement in my algorithm)
- **2-Pivot and 3-Pivot Quicksort** - we could use two or three pivots to enable us to partition the array into more subarrays. This results in fewer cache misses and improves cache performance. (I have not implemented this improvement in my algorithm)

### Uses and Final Thoughts
Quicksort is widely used and is considered one of the better sorting algorithms for average performance. While its worst-case order of growth is poor, this can be avoided through shuffling the array prior to sorting. In fact, Quicksort's average-case performance is &Theta;(NlogN) and hence it is used in many libraries.

## Selection Sort
### How It Works
Selection Sort works by splitting the array conceptually into two parts: a sorted part and an unsorted part. At the beginning of the algorithm, the sorted part consists of no elements, while the all the elements exist in the unsorted part. 

With every pass, the algorithm searches through the unsorted part to find the minimum element. This minimum element is then swapped into the sorted part starting at index 0. With every pass, the sorted part grows by one and the unsorted part shrinks by one until the unsorted part consists of only a single element (as we know the array is sorted at this point). 

### Space and Time Complexity
Selection Sort has a worst-case time complexity of &Theta;(N<sup>2</sup>) due to the nested for-loops the algorithm requires. Both of these for-loops iterate over (almost) the entire length of the array (N), leading to this order of growth.

Selection Sort has a best-case time complexity of &Theta;(N<sup>2</sup>) as regardless of input the two nested for-loops will be executed. With every pass we need to find the minimum element in the unsorted part, and in order to do this we need to look through every element in the unsorted part. This results in every input being a worst-case input.

Selection Sort is not stable but is an in-place sorting algorithm. It does not require any additional memory meaning it has a worst-case space complexity of &Theta;(1).

### Potential Improvements
- **Find Maximum Element As Well** - in each pass we find the minimum element in the unsorted part of the array and place it in the correct position in the sorted part. We could also find the maximum element on each pass and then place this at its correct position in the sorted part of the array also. (I have not implemented this improvement in my algorithm)

### Uses and Final Thoughts
Selection Sort may be used when auxiliary memory is limited and where a minimal number of swaps is required. However, its quadratic order of growth makes it unusable for large input sizes and Insertion Sort is generally a better option for smaller arrays. The main advantage of Selection Sort is that it makes the minimal number of swaps in the worst case (N - 1 swaps where N is the length of the array).

## Shell Sort
### How It Works
Shell Sort is a variation of Insertion Sort that reduces the number of swaps required in the case where an element being inserted into the sorted part of the array requires many swaps.

In Shell Sort we introduce a gap between which we compare elements and make swaps. In each pass, we reduce this gap until it becomes 1. On the final pass, it acts exactly like insertion sort. When the gap becomes 0, the array is sorted. (In my implementation, the gap starts at half the array size and is reduced by half in each iteration i.e. `gap = array.length/2 -> array.length/4 -> array.length/8 ...`)

### Space and Time Complexity
Shell Sort has a worst-case time complexity of &Theta;(N<sup>2</sup>) due to the nested for-loops the algorithm requires. The outer for-loop contributes &Theta;(logN) while the inner two for-loops contribute &Theta;(N<sup>2</sup>). This results in a &Theta;(logN * N<sup>2</sup>) worst-case time complexity but is in fact better. If we introduce the gap variable we see that it becomes &Theta;(N<sup>2</sup>). In simpler terms, Shell Sort is just Insertion Sort with a gap, which makes it at the very worst &Theta;(N<sup>2</sup>). This occurs when the smallest elements are located in odd positions in the array and the largest elements are located in even positions in the array (or vice-versa).

Shell Sort has a best-case time complexity of &Theta;(NlogN) as the outer for loop will be executed logN times as we reduce the gap by half each time and the inner loop will execute N times. The innermost loop will act as constant time expression if it is never executed, which it won't be in the case that the array is already sorted. Hence, we get a worst-case time complexity of &Theta;(NlogN).

Shell Sort is is not stable but is an in-place sorting algorithm. It does not require any additional memory meaning it has a worst-case space complexity of &Theta;(1).

### Potential Improvements
- **Gap Sequences** - choosing the right gap size can improve the algorithm further but this depends on a variety of factors. I've just gone with a basic approach which leads to a worst-case runtime of &Theta;(N<sup>2</sup>) but this can be improved upon by changing the gap sequence. For example, using Hibbard's Sequence or Sedgewick's Sequence lead to better worse-case time complexities.

### Uses and Final Thoughts
Shell Sort is an adapted version of Insertion Sort but this adaptation results in the loss of stability. Insertion Sort does not perform well when the gaps between elements are large, and this is where Shell Sort comes in. By introducing the gap sequence, less swaps will be required when the gap between two elements is large.
