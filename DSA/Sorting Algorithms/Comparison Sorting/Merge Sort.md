This sorting algorithm has a time complexity of $O(n logn)$ in worst case scenario, which is much better as compared to [[Selection Sort]], [[Bubble Sort]], [[Insertion Sort]] which has a time complexity of $O(n^2)$ in average case.

### If Sub Arrays are Sorted
In this sorting algorithm we will divide the array into two possibly __equal halves__. 
![[Pasted image 20250315130055.png]]

Now all the elements of array `A` is either present in `left` array or `right` array. So we can overwrite the elements in `A` without any worry of losing the elements.

![[Pasted image 20250315133237.png]]

On comparing, Which ever element is smaller from either of the two array, it will be added to `A` array, starting from `0` index of course. 
let's say that all the elements from `left` array are _picked_ than we need to introduce a different `while` loop whose job specifically is to iterate over the _unpicked_ elements of `right` array. vice versa will be the case if all the elements in `right` array is _picked_. 

```C
//this function will merge only two sorted sub arrays into one array
void merge(int arr[], int left[], int right[], int sizeLeft, int sizeRight){
	int i=0, j=0, k=0;
	//`i` for left array, 'j' for right array and 'k' for main array
	while (i<sizeLeft && j<sizeRight) { 
	    //picking smallest 'unpicked' from left with smallest 'unpicked' in right 
	    //and comparing it with each other
	    if(left[i] <= right[j]){
	      arr[k++] = left[i++];
	    }else{
	      arr[k++] = right[j++];
	    }
	    //remember those are post increment, 
	    //value will be used first & then will be incremented
    }
    
	//copy remaining elements from left, if any
	while (i<sizeLeft) {
		arr[k++] = left[i++]; 
	}
	//copy remaining elements from right, if any
	while (j<sizeRight) {
		arr[k++] = right[j++]; 
	}
}
```

### If Sub Arrays are NOT Sorted
If the sub arrays are not sorted then we can further subdivide these two sub lists. 
![[Pasted image 20250315135953.png]]

and divide further
![[Pasted image 20250315140048.png]]

Once we reach the stage where there is only one element in each list then we cannot reduce that sub list any further. And the list with only one element is already sorted, so we don't need to sort any further. 

```C
//this is the recursion function
void mergeSort(int arr[], int size){
	if(size<2){
		//list having only 1 element is already a sorted list
		return;
	} 
	
	//find the midpoint
	int mid = size/2;
	
	int *left = (int *)malloc(mid * sizeof(int));
	int *right = (int *)malloc((size-mid) * sizeof(int));
	
	//copy data to left and right sub arrays
	for (int i=0; i<mid; i++) {
		left[i] = arr[i];
	}
	for (int i=mid; i<size; i++) {
		right[i-mid] = arr[i];
	}
	
	//recursively sort the subarrays
	mergeSort(left, mid);
	mergeSort(right, size - mid);
	
	//Merge the sorted sub arrays back into the original array
	merge(arr, left, right, mid, size-mid);
	
	//free allocated memeory for the sub arrays
	free(left);
	free(right);
}
```