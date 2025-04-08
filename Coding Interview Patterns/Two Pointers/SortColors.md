# [Sort Colors](#sort-colors)

## Statement:  
Given an array `colors`, which contains only `0`s (red), `1`s (white), and `2`s (blue), **sort it in-place** such that elements of the same color are adjacent and the colors are in the order: red (0), white (1), blue (2).  

**You must not use built-in sort functions.**

---

### ✅ Constraints:
- `1 <= colors.length <= 300`
- Each value in `colors[i]` is either `0`, `1`, or `2`

---

## ✅ Problem Understanding

You are given an array representing colors using values `0`, `1`, and `2`. The task is to sort the array such that all 0s come first, then 1s, and finally 2s.  

---

## ✅ Constraints and Edge Cases

- **All values are valid (0, 1, 2)**
- The array must be sorted **in-place**
- Minimum array length is 1
- Edge cases:
  - Already sorted array
  - All elements are the same
  - Random permutations of 0, 1, and 2

---

## 🧠 Brute Force Approach

### 👉 Idea:
1. Count the number of `0`s, `1`s, and `2`s.
2. Override the original array using the counts.

### 🔧 Java Code:
```java
public static int[] sortColors(int[] colors) {
    int count0 = 0, count1 = 0, count2 = 0;

    // Count occurrences
    for (int color : colors) {
        if (color == 0) count0++;
        else if (color == 1) count1++;
        else count2++;
    }

    // Overwrite original array
    int i = 0;
    while (count0-- > 0) colors[i++] = 0;
    while (count1-- > 0) colors[i++] = 1;
    while (count2-- > 0) colors[i++] = 2;

    return colors;
}
```

### ⏱️ Time Complexity:
- **O(N)**

### 🧠 Space Complexity:
- **O(1)** (counting only, no extra array)

---

## ⚙️ Optimal Solution: Dutch National Flag Algorithm

### 👉 Idea:
Use 3 pointers:
- `low` for the next 0 position
- `mid` for current processing index
- `high` for the next 2 position

Swap values accordingly:
- If `colors[mid] == 0`: swap with `low`, move both `low` and `mid`
- If `colors[mid] == 1`: just move `mid`
- If `colors[mid] == 2`: swap with `high`, move `high`

---

### 🔧 Java Code (As per your format):

```java
import java.util.*;

public class Solution {
    public static int[] sortColors(int[] colors) {
        int low = 0, mid = 0, high = colors.length - 1;

        while (mid <= high) {
            if (colors[mid] == 0) {
                int temp = colors[low];
                colors[low] = colors[mid];
                colors[mid] = temp;
                low++;
                mid++;
            } else if (colors[mid] == 1) {
                mid++;
            } else { // colors[mid] == 2
                int temp = colors[mid];
                colors[mid] = colors[high];
                colors[high] = temp;
                high--;
            }
        }

        return colors;
    }
}
```

---

### ⏱️ Time Complexity:
- **O(N)** → one pass through the array

### 🧠 Space Complexity:
- **O(1)** → constant space

---

### ✅ Summary:

| Approach                   | Time Complexity | Space Complexity | Notes                          |
|---------------------------|-----------------|------------------|--------------------------------|
| Brute Force (Counting)    | O(N)            | O(1)             | Easy to implement              |
| Dutch National Flag Algo  | O(N)            | O(1)             | Optimal, single-pass, in-place |

---
