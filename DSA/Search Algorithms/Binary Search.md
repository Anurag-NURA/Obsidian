Binary search is a highly efficient algorithm used to find the `position` of a target value within a __Sorted Array__. 
It works by repeatedly dividing the search interval in **half**, making it much faster than [[Linear Search]], which checks every element one by one.

## Binary Search Types:

### __1. Iterative Binary Search__ 

```C
int iterativeBinarySearch(int arr[], int size, int target) {
  int left = 0, right = size - 1;

  //iterate till the elements on the left are smaller 
  //or equal than the elements on the right
  while (left <= right) {
    int mid = left + (right - left) / 2;
    //calculating using low+high/2 is not prefered
    //as this can overflow for value of long interger

    // Check if target is present at mid
    if (arr[mid] == target) {
        return mid;
      //we will exit as soon as we find any (first or last) occurrence of the target
    }

    // If target is greater, ignore the left half
    if (arr[mid] < target) {
        left = mid + 1;
    }
    
    // If target is smaller, ignore the right half
    if (arr[mid] > target) {
        right = mid - 1;
    }
  }
  // Target not found
  return -1;
}
```

### __2. Recursive Binary Search___
```C
int recursiveBinarySearch(int arr[], int low, int high, int target){
  //it is very much similar to iterativeBinarySearch method
  //the only difference is that rather iterating we are calling the same function
  //with updated low or high values depending on the condition
  int mid = 0;
  
  if (low>high) {
    return -1;
  }
  mid = low + (high-low)/2;

  if(target == arr[mid]){
    return mid;
  }else if(target<arr[mid]){
    recursiveBinarySearch(arr, low, mid-1, target);
  }else if(target>arr[mid]){
    recursiveBinarySearch(arr, mid+1, high, target);
  }
}
```


## First Or Last Occurrence of Target element

To find the first or last occurrence of a target element using binary search, we will need to slightly modify the standard binary search algorithm. Here's how we can achieve that:

1. __First Occurrence of Target Element__
	We will introduce a variable naming `result` which will hold any occurrence of the target element that was first founded in the iteration. 
	
	Than we will reduce our search space even removing the element index in which target was founded and move the `high` variable towards left side of `mid` variable.
	
	This will let us search for any other instance other than the one we founded earlier and if exist will update the `result`  variable with this new occurrence index of the same target value.  

```C
int findFirstOccurence(int arr[], int size, int target){
	int low = 0, high = size-1, result = -1;
	while (low <= high) {
		int mid = low + (high-low)/2;
		if(target == arr[mid]){
		  result = mid;
		  high = mid-1;
		}else if (target < arr[mid]) {
		  high = mid - 1;
		} else if (target > arr[mid]) {
		  low = mid + 1;
		} 
	}
	return result;
}
```
1. __Last Occurrence of Target Element__

