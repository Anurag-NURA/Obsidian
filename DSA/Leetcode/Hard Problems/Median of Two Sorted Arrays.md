# LeetCode 4 - Median of Two Sorted Arrays

> Difficulty: Hard
>
> Pattern: Binary Search on Partition

---

# Problem Statement

Given two **sorted arrays**, find the median of the combined sorted array.

The brute-force solution is to merge both arrays.

```
Time Complexity

O(n + m)
```

However, the problem asks for

```
O(log(m+n))
```

which immediately suggests **Binary Search**.

---

# Step 1 - What are we actually searching for?

Many people think Binary Search is finding the median.

It is **not**.

Binary Search is trying to find the **correct partition**.

Once the partition is correct, the median becomes obvious.

---

# Step 2 - Why Partition?

Suppose

```
nums1 = [1,3,4,7,10,12]

nums2 = [2,3,6,15]
```

Imagine drawing a line between elements.

```
nums1

1 3 4 | 7 10 12

nums2

2 3 | 6 15
```

Everything before the line belongs to the **left half**.

Everything after the line belongs to the **right half**.

Our goal is to place this line correctly.

---

# Step 3 - How many elements should be on the left?

Let

```
n = n1 + n2
```

The left side should always contain

```cpp
leftSize = (n1 + n2 + 1) / 2;
```

This formula is used **before** we find the median. 
Its purpose is **not** to calculate the median.
Its purpose is to determine:

> **How many elements should be on the left side of the partition?**

This formula is used **for both odd and even total elements**.

Example

```
5 elements

1 2 3 | 4 5

Left = 3

Right = 2
```

```
(5+1)/2 = 3
```

For an even number of elements

```
6 elements

1 2 3 | 4 5 6

Left = 3

Right = 3
```

```
(6+1)/2 = 3
```

So the same formula works for both cases.

---

# Step 4 - Why Binary Search on the Smaller Array?

Suppose

```
nums1 = size 1000

nums2 = size 5
```

Searching on

```
nums1

O(log1000)
```

is unnecessary.

Searching on

```
nums2

O(log5)
```

is much smaller.

Therefore

```cpp
if(nums1.size() > nums2.size())
    swap(nums1, nums2);
```

---

# Step 5 - Partition Variables

Suppose Binary Search chooses

```cpp
mid1
```

Then

```cpp
mid2 = leftSize - mid1;
```

Now define

```cpp
l1 = nums1[mid1-1];
r1 = nums1[mid1];

l2 = nums2[mid2-1];
r2 = nums2[mid2];
```

Visualize them.

```
nums1

... l1 | r1 ...

nums2

... l2 | r2 ...
```

These are the only four elements that matter.

---

# Step 6 - Why only these four?

Both arrays are already sorted.

Everything before

```
l1
```

is automatically

```
<= l1
```

Everything after

```
r1
```

is automatically

```
>= r1
```

The same is true for the second array.

Therefore the only place where the ordering can be wrong is **around the partition**.

That is why we only compare

```
l1
r1
l2
r2
```

---

# Step 7 - Correct Partition

The partition is correct if

```cpp
l1 <= r2
&&
l2 <= r1
```

Meaning

The largest value on the left is not greater than the smallest value on the right.

Once this is true,

every element on the left is guaranteed to be less than every element on the right.

---

# Step 8 - How does Binary Search move?

### Case 1

```
l1 > r2
```

Example

```
8 | 9

4 | 5
```

```
8 > 5
```

We took **too many elements from nums1**.

Move left.

```cpp
high = mid1 - 1;
```

---

### Case 2

```
l2 > r1
```

Example

```
3 | 4

5 | 6
```

```
5 > 4
```

We took **too few elements from nums1**.

Move right.

```cpp
low = mid1 + 1;
```

---

# Step 9 - Finding the Median

### Odd Total Elements

The left side contains one extra element.

Therefore

```cpp
median = max(l1,l2);
```

---

### Even Total Elements

The median lies exactly between

- Largest element of the left half
- Smallest element of the right half

Hence

```cpp
median =
(max(l1,l2)+min(r1,r2))/2.0;
```

---

# Step 10 - Edge Cases

Partition can reach the beginning or end of an array.

Use imaginary values.

```cpp
l1 = (mid1==0)?INT_MIN:nums1[mid1-1];

r1 = (mid1==n1)?INT_MAX:nums1[mid1];

l2 = (mid2==0)?INT_MIN:nums2[mid2-1];

r2 = (mid2==n2)?INT_MAX:nums2[mid2];
```

This avoids writing separate boundary conditions.

---

# Algorithm

```
Binary Search on smaller array

↓

Choose partition

↓

Compute second partition

↓

Find

l1 r1 l2 r2

↓

Check

l1<=r2

&&

l2<=r1

↓

Found

↓

Compute Median
```

---

# Complexity

```
Time

O(log(min(n,m)))
```

```
Space

O(1)
```

---

# Key Takeaways

- Never merge the arrays.
- Binary Search finds the partition, not the median.
- Always search on the smaller array.
- Left partition size = `(n1+n2+1)/2`.
- `mid2 = leftSize - mid1`.
- Correct partition:
  - `l1 <= r2`
  - `l2 <= r1`
- `l1 > r2` → move left.
- `l2 > r1` → move right.
- Odd → `max(l1,l2)`.
- Even → `(max(l1,l2)+min(r1,r2))/2.0`.