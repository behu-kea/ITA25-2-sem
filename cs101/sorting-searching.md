

# Sorting and searching

This video is fine: [https://www.youtube.com/watch?v=rbbTd-gkajw](https://www.youtube.com/watch?v=rbbTd-gkajw)



## Sorting

- Nævn nogle almindelige sorteringsalgoritmer, og beskriv deres tidskompleksitet.

- Forklar, hvordan en **QuickSort** fungerer, og analyser dens tidskompleksitet i bedste og værste tilfælde.
- Hvordan fungerer MergeSort, og hvorfor er den mere effektiv end BubbleSort?
- Hvorfor bruges ofte **Heapsort** eller **Quicksort** i praksis frem for BubbleSort eller InsertionSort?
- Hvordan kan man forbedre en simpel sorteringsalgoritme som BubbleSort?
- Hvorfor bruger man ikke altid **Counting Sort** selvom den har O(n) kompleksitet?
- Hvilke sorteringsalgoritmer er rekursive, og hvilke er iterative?



- What does it mean for a sorting algorithm to be “stable”?
- In Big-O notation, how would you compare the average and worst-case time complexities of MergeSort, QuickSort, and BubbleSort?
- Can you describe the merge process in MergeSort? How does merging sorted sublists work?
- How do Insertion Sort and Selection Sort differ in terms of their approach and performance characteristics?
- How do the space requirements compare for MergeSort, QuickSort (using in-place partitioning), and Counting Sort?



Merge sort, quickSSort and bubblesort



### BubbleSort

Most popular. Switches place if two elements are in the wrong order. 

Has  O(n<sup>2</sup>)  time complexity worst. O(n) best 



### Selection Sort

For each position in the list: Finds the smallest value and swaps it to the current position of the array. 

Selection sort works by finding the minimum element in an unsorted portion of the array and placing it at the beginning, then repeating this for the remaining elements.



#### Time complexity

We have to first find the smallest element for the first position O(n). But we have to do it for all positions in the array O(n<sup>2</sup>) 



### Insertion sort

[Good explanation](https://www.youtube.com/watch?v=O0VbBkUvriI&t=41s)

Like sorting cards on your hand

Insertion sort is a simple sorting algorithm that works by iteratively inserting each element of an unsorted list into its correct position in a sorted portion of the list. It is like sorting playing cards in your hands.

![Insertion-sorting](assets/Insertion-sorting.png)

We only have to move forward in the array. 

We move specific portions of the array over in order to put the newest unsorted array into the correct position in the array. 



#### Time complexity

O(n<sup>2</sup>) worst. We have to go through each element in the list. But we also have to shift all the elements in the sorted position.



Best O(n). If all elements are sorted. We only have to run through the array. 



### MergeSort

Divide and conquer. Break problem into smaller problems.

We will split the list in half until we have the individual items. 

Now we will compare the individual items and merge them into new temporary lists that are sorted

Now we need to merge the newly created lists with each other. 



Divide the array into its smallest elements. 

Done recursively. 



#### Time complexity

O(n log n)

O(log n) comes from the dividing the lists in half. 

- If we had 8 elements we would split 3 times
- If we had 16 elements we would split 4 times

O(n) comes from merging the sub arrays. We have to visit each element in the list. 



### QuickSort

Uses a pivot point. It is important to choose the right pivot.



Like merge sort.



