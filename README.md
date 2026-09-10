# Insertion Sort Algorithm

Insertion Sort builds the sorted array gradually.

At every iteration, one element is selected as the `key`. The elements already processed are treated as a sorted section, and any values larger than the key are shifted one position to the right. The key is then inserted into the newly available position.

## Example

Starting array:

```text
13 46 24 52 20 9
```

After sorting:

```text
9 13 20 24 46 52
```

## Implementation

```python
class Solution:
    def insertionSort(self, nums):
        n = len(nums)

        for i in range(1, n):
            key = nums[i]
            j = i - 1

            while j >= 0 and nums[j] > key:
                nums[j + 1] = nums[j]
                j -= 1

            nums[j + 1] = key

        return nums


if __name__ == "__main__":
    solution = Solution()

    nums = [13, 46, 24, 52, 20, 9]

    print("Before Using Insertion Sort:")
    for num in nums:
        print(num, end=" ")

    print()

    nums = solution.insertionSort(nums)

    print("After Using Insertion Sort:")
    for num in nums:
        print(num, end=" ")

    print()
```

## The Main Idea

Insertion Sort can be understood as repeatedly asking:

```text
Where should the current element be inserted
inside the sorted portion?
```

The array is gradually divided into:

```text
[ Sorted | Unsorted ]
```

Initially, the first element is considered sorted:

```text
[13 | 46 24 52 20 9]
```

The next element is then inserted into its correct position.

## Role of `key`

The current element is stored in:

```python
key = nums[i]
```

This value is temporarily removed from consideration while the sorted portion is adjusted.

For example:

```text
[13 | 46 24 52 20 9]
       ↑
      key
```

Since `46` is already greater than `13`, no shifting is required.

The sorted section becomes:

```text
[13 46 | 24 52 20 9]
```

## Shifting Elements

Consider the next key:

```text
24
```

The sorted portion is:

```text
13 46
```

Since:

```text
46 > 24
```

`46` is shifted one position to the right:

```text
13 46 46
```

Then `24` is placed in the empty position:

```text
13 24 46
```

This is performed by:

```python
while j >= 0 and nums[j] > key:
    nums[j + 1] = nums[j]
    j -= 1

nums[j + 1] = key
```

## Step-by-Step Example

Starting array:

```text
13 46 24 52 20 9
```

### First Insertion

Key:

```text
46
```

Already in the correct position:

```text
13 46 | 24 52 20 9
```

### Second Insertion

Key:

```text
24
```

Shift `46`:

```text
13 46 46 52 20 9
```

Insert `24`:

```text
13 24 46 | 52 20 9
```

### Third Insertion

Key:

```text
52
```

No shifting is required:

```text
13 24 46 52 | 20 9
```

### Fourth Insertion

Key:

```text
20
```

Shift the larger values:

```text
13 24 46 46 52 9
13 24 24 46 52 9
```

Insert `20`:

```text
13 20 24 46 52 | 9
```

### Final Insertion

Key:

```text
9
```

Every value in the sorted section is larger than `9`, so they are shifted right.

Final result:

```text
9 13 20 24 46 52
```

## Why Shift Instead of Repeatedly Swap?

Insertion Sort normally shifts larger elements rather than performing a series of adjacent swaps.

The implementation preserves the current value in:

```python
key
```

and moves larger elements:

```python
nums[j + 1] = nums[j]
```

Once the correct position is found:

```python
nums[j + 1] = key
```

This creates the space needed for insertion.

## Sorted Portion

After every iteration, the portion from index `0` through `i` is sorted.

For example:

```text
13 20 24 | 52 46 9
```

The left side is already ordered.

The algorithm only needs to determine where the next unsorted element belongs.

This invariant continues until the entire array becomes sorted.

## Complexity Analysis

| Case | Time Complexity |
|---|---|
| Best Case | `O(N)` |
| Average Case | `O(N²)` |
| Worst Case | `O(N²)` |

| Metric | Complexity |
|---|---|
| Auxiliary Space | `O(1)` |

The best case occurs when the array is already sorted because the inner `while` condition fails immediately for each element.

In the worst case, elements may need to be shifted across most of the sorted section.

The algorithm works directly on the original array, so it requires constant auxiliary space.

## Characteristics

- In-place sorting algorithm
- Builds the sorted section incrementally
- Uses shifting rather than an additional array
- Performs well on small or nearly sorted arrays
- Can be implemented with constant auxiliary space
- Has quadratic worst-case time complexity

## Selection Sort vs Insertion Sort

Both algorithms use an in-place approach, but their strategies differ.

| Selection Sort | Insertion Sort |
|---|---|
| Searches for the minimum | Takes the current element as a key |
| Swaps the minimum into position | Shifts larger elements |
| Builds the sorted section through selection | Builds the sorted section through insertion |
| `O(N²)` in best case | `O(N)` in best case |

## Key Observation

Insertion Sort does not need to rebuild the entire array after every iteration.

It preserves what has already been sorted and concentrates only on placing the next element correctly:

```text
Take key
   ↓
Compare with sorted section
   ↓
Shift larger values
   ↓
Insert key
   ↓
Expand sorted section
```

That process continues until the unsorted section disappears.
