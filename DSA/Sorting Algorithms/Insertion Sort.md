In insertion sort we create a hole which is an index whose value  will be compared with its previous index value and then a swap is performed if the previous value is bigger than the hole value.

Then the hole is moved backwards to repeat the process till the very first element is compared then the iteration will move the hole location to it its original location + 1.

```C
void insertionSort(int arr[], int size){
	for(int i=1; i<size; i++){
		int value = arr[i];
		int hole = i;
		while(hole>0 && arr[hole-1]>value){
			//bigger value will be moved right (higher) side
			arr[hole] = arr[hole-1];
			//while smaller value will be moved left (lower) side
			//value will be checked and swaped again if bigger value is founded
			hole = hole - 1;
		}
		arr[hole] = value;
	}
}
```

`for` loop will iterate in forward direction. Meanwhile, `while` loop will iterate elements in backward direction. 
This ensures whichever element the pointer will be on, it will be matched with its previous element and if founded is smaller than will be replaced, i.e., `arr[i]` will be replaced with `arr[i-1]`

But this will done with the help of new variable called `hole` which will be holding __index number__  of every `for` loop iteration and will be changing inside the `while` loop.

`value` will be holding the `arr[i]` value in every iteration of `for` loop. 