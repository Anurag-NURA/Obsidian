It is a simple sorting algorithm in which `ith` index value is compared with it's next index value i.e., `i+1` and if founded larger than next value than a swap is performed. With each iteration the size of the for comparison keep getting smaller and values keep getting arranged from right side having the larger value and then never compared again.

Bubble Sort for Array of Integers
```C
int bubbleSort(int arr[], int size){
  for (int i=0; i<size-1; ++i) {
    for (int j=0; j<size-i-1; ++j) {
      if (arr[j]>arr[j+1]) {
      //below is just a swap value logic
        int temp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = temp;
      } 
    }
  }
}
```
 we did size-2 instead of size-1 because it could have caused a bug where the last element would have tried to access index which is out of bound from original size array.
 
After first iteration of `i` loop is complete we will have the largest element in the `arr` at the very last `index` of the `arr`. 

In second iteration of `i` loop the second largest at second last `index` of the `arr` and so on.

Bubble Sort for Array of Strings
```C
void bubbleSortStrings(char arr[0][10], int size){
	int i, j, k;
	char temp[10];
	for (i=0;i<4;i++) {
	    for (j=0;j<4;j++) {
	    if(strcmp(arr[j], arr[j+1])>0){
		        strcpy(temp, arr[j]);
		        strcpy(arr[j], arr[j+1]);
		        strcpy(arr[j+1] ,temp);
		    }
	    }
	}
	for (k=0;k<5;k++) { 
	    printf("\n %d name: %s", k, arr[k]);
	}
}
```