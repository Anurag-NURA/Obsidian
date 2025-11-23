Counting Sort is a sorting algorithm that works by **counting the occurrences** of each unique value in the input array.
### **How it works**

1. **Count frequencies**
    - Create an auxiliary array (called the _count array_) where each index represents a number from the input.
    - Store how many times each value appears.
2. **Cumulative sum (prefix sum)**
    - Modify the count array so that each index now stores the _position_ of the number in the sorted output.
3. **Build output array**
    - Traverse the input array from right to left (to maintain stability).
    - Place each element in its correct sorted position using the cumulative count.

### **Key Characteristics**

- It does **not** use comparisons (`<`, `>`, etc.) → so it is **NOT a comparison sort**.
- It is very fast when the range of numbers (**k**) is not much larger than the number of elements (**n**).
- Used frequently inside **Radix Sort**.

# ⏱ **Time Complexity:**

### **O(n + k)**
- **n** = number of elements
- **k** = range of input values (0 to max)

# 📦 **Space Complexity:**

### **O(n + k)**
- Needs extra arrays (`count array` + `output array`)

![[3b1ec73b-695c-4cf3-8794-f0307b018519.png]]

![[Pasted image 20251123203947.png]]

```cpp
void countSort(vector<int> &input_array){
	if(input_array.empty()){
		return;
	}
	int range = maxElement(input_array) + 1; // range of input elements
	vector<int> count_array(range);
	vector<int> output_array(input_array.size());
	
	// Initialize count_array to 0
	for(int i=0; i<range; ++i){
		count_array[i] = 0;
	}
	
	// Store the frequency of each element in count_array
	for(int i=0; i<input_array.size(); ++i){
		++count_array[input_array[i]];
	}
	
	//cumulative count of count_array to get the positions
	//of each element to be stored in the output_array
	for(int i=1; i<range; ++i){
		count_array[i] = count_array[i] + count_array[i-1];
	}
	
	//placing input array elements into output array in proper positions
	//such that result is a sorted array in ascending order
	for(int i=0; i<input_array.size(); ++i){
		output_array[--count_array[input_array[i]]] = input_array[i];
	}
	
	for(int i=0; i<input_array.size(); ++i){
		input_array[i] = output_array[i];
	}
}
```