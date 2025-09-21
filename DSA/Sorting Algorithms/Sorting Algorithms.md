Sorting is arranging the elements in a list or collection in increasing or decreasing order of some property.

If a list is __Unsorted List__ than we perform [[Linear Search]] but if it is a __Sorted List__ we can then perform a [[Binary Search]].

### Classification of Sorting Algorithm:
1. On the basis of `Time Complexity`
2. On the basis of `Space Complexity` or `Memory Usage`
	- In-place, Constant memory 
	- Memory usage grows with input size
3. `Stability`, preserves the relative order of elements
4. `Internal` Sort (records are on main memory) v/s `External` Sort (records are on disk/tapes) 
5. `Recursive` or Non-Recursive 

### Types of Sorting Algorithm:
1.  **Simple Comparison-based Sorting**
- These compare elements and arrange them in order.
- Easy to implement but not always efficient.
- **Examples:**
    - [[Bubble Sort]] – repeatedly swaps adjacent elements.
        - Time: $O(n^2)$
    - [[Selection Sort]] – selects the smallest/largest element and places it in order.
        - Time: $O(n^2)$
    - [[Insertion Sort]] – builds sorted array one element at a time.
        - Time: $O(n^2)$ (but $O(n)$ for nearly sorted data)
    
2. **Efficient Comparison-based Sorting**
- Use **divide-and-conquer** or clever strategies.
- Much faster for large datasets.
- **Examples:**
    - [[Merge Sort]] – splits array into halves, sorts them, and merges.
        - Time: $O(nlog⁡n)$, Space: $O(n)$
    - [[Quick Sort]] – partitions array around a pivot, then recursively sorts.
        - Time: $O(nlog⁡n)$ average, $O(n2)$ worst
    - [[Heap Sort]]– builds a heap and extracts elements.
        - Time: $O(nlog⁡n)$, Space: $O(1)$
		
3. **Non-comparison-based Sorting**
- Do not compare elements directly.
- Work best with integers in a limited range.
- **Examples:**
    - [[Counting Sort]] – counts occurrences of each element.
        - Time: $O(n+k)$, where k = range of values
    - [[Radix Sort]] – sorts numbers digit by digit (using Counting Sort as subroutine).
        - Time: $O(nk)$, where k = number of digits
    - [[Bucket Sort]] – distributes elements into buckets, then sorts each bucket.
        - Time: $O(n+k)$ average, worst $O(n^2)$