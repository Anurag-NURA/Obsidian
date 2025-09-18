### Pointers Size
All pointes are of same size because all pointers are 32-bit memory address.
But when we operating on an array, not on list of elements, C can track what the size of that array is: 

```C
	int intArray[10];
	char charArray[10];
	double doubleArray[10];
	//%zu if for Unsigned size type
	printf("Size of int array:  %zu bytes\n", sizeof(intArray));
	printf("Size of char array:  %zu bytes\n", sizeof(charArray));
	printf("Size of double array:  %zu bytes\n", sizeof(doubleArray));
	// Size of int array: 40 bytes
	// Size of char array: 10 bytes
	// Size of double array: 80 bytes
```

$\therefore$ __Pointers have the same size on the same system, while Array may have different sizes.__

