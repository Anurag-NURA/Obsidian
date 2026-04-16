In insertion sort we create a hole which is an index whose value  will be compared with its previous index value and then a swap is performed if the previous value is bigger than the hole value.

![[Pasted image 20250921080216.png]]

We can consider that, we are dividing the array in two subsets. 

Initially the subset with index 0 will be part of the sorted subset because we have only one element in set and it is sorted

All other elements are part of unsorted sub set

![[Pasted image 20250921080522.png]]

Now lets say we have taken out index 1 element and temporarily stored in a variable and now that index 1 is empty (i.e., a hole)

Now to place 2 in the sorted subset we will shift all numbers greater than number 2 by one position to right.

![[Pasted image 20250921080746.png]]

Now we will fill up 2 in the hole
![[Pasted image 20250921080804.png]]

Then the hole is moved backwards to repeat the process till the very first element is compared then the iteration will move the hole location to it its original location+1.

Again for index 2, value = 4
![[Pasted image 20250921081228.png]]

We will again compare the very right element of the sorted array with the `value`
and if element from the sorted array is bigger than the `value` we will fill the hole with that element and the very index of that element now becomes that updated `hole`.
![[Pasted image 20250921081505.png]]

![[Pasted image 20250921081515.png]]

As we can see element `2` is not greater than `value`, so we will the hole with value 4.

![[Pasted image 20250921081610.png]]
and the cycle continues...

## Implementation using C
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