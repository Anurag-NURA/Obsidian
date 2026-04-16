https://www.geeksforgeeks.org/dsa/bucket-sort-2/

```cpp
void bucketSort(vector<int>& arr){
    vector<vector<int>> buckets(arr.size());
	
    // Distribute input array values into buckets
    for(int element: arr ) {
        //arr[i] can be float or double
        //but since we are storing it an 'int'
        //C++ automatically truncates the decimal part
        int index = element * arr.size();
        if (index >= arr.size()) {
            index = arr.size() - 1; // Handle edge case for max value
        }
        buckets[index].push_back(element);  
    }
	
    // Clear original array
    arr.clear();
	
    // Sort individual buckets using insertion sort
    for(int i = 0; i < buckets.size(); i++){
        insertionSort(buckets[i]);
    }
	
    //Concatenate all buckets into arr
    for(int i = 0; i < buckets.size(); i++){
        for(int j = 0; j < buckets[i].size(); j++){
            arr.push_back(buckets[i][j]);
        }
    }
}
```