We will find the minimum element in the array and then swap the element with the very first index's element of the array as the lowest element should always be at the first location of a sorted array.

Then we will iterate in such a manner that the previous iterated integer will be ignored and then we will find the second minimum element in the array which will be like finding smallest element from i+1 till size-1 and then repeat. 

The very last element will already be its place i.e., the highest/largest element will be at the last index of the sorted array. 

```C
void selectionSort(int arr[], int size){
	for(int i=0; i<size-1; i++){
		int indexMin = i;
		for(int j=i+1; j<size; j++){
			if(arr[j]<arr[indexMin]){
				indexMin = j;
			}
		}
		int temp = arr[i];
		arr[i] = arr[indexMin];
		arr[indexMin] = temp;
	}
}
```
