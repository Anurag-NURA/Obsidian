```C
int arr[5];
int *ptr = arr; // 'arr' decays to 'int*'
int value = *(arr+2); // 'arr' decays to 'int*'
```

So basically what it mean that we can have array in our code and compiler remembers how large that array is. But as soon as we cast that array into a pointer, like above, we have lost that additional information.

### When arrays don't decay
- `sizeof` __Operator:__ returns the size of the entire array not just the size of a pointer.
- `&` __Operator:__ Taking the address of an array with `&arr` gives you a pointer to the whole array, not just the first element. The type of `&arr` is a pointer to the array type, e.g., `int (*)[5]` for an `int` array with 5 elements.
- __Initialization:__ When an array is declared and initialized, it is fully allocated in memory and does not decay to a pointer.

```C
#include<stdio.h>

void core_utils_func(int core_utilization[]){
  printf("sizeof core_utilization in core_utils_func: %zu\n", sizeof(*core_utilization));
}

void main(){
  int core_utilization[] = {43, 67, 89, 92, 71, 43, 56,12};
  int len = sizeof(core_utilization)/sizeof(core_utilization[0]);
  printf("sizeof core_utilization in main: %zu\n", sizeof(core_utilization));
  printf("len of core_utilization: %d\n", len);

  core_utils_func(core_utilization);

  printf("\n");
}
```

__Output:__
![[Pasted image 20250313210905.png]]

