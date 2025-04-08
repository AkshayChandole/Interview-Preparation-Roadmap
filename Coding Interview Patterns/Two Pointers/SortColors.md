# [Sort Colors](#sort-colors)

## Statement:
Given an array `colors` containing only values `0`, `1`, and `2` (representing red, white, and blue respectively), sort the array in place such that the colors appear in the order **red (0)**, **white (1)**, and **blue (2)**.

You must solve this problem **without using any built-in sort functions**.

---

## Constraints:
- `1 <= colors.length <= 300`
- `colors[i] ∈ {0, 1, 2}`

---

## ✅ Problem Understanding

We're given an array of integers where:
- 0 → red
- 1 → white
- 2 → blue

We need to sort this array such that all 0s come first, followed by 1s, and then 2s — **in-place**.

---

## ✅ Constraints and Edge Cases

- The array is small (max 300), so O(n) or O(n log n) is acceptable.
- We must **not** use built-in sorting.
- Edge cases:
  - All elements same: e.g., `[0,0,0]`
  - Only two types present: `[0,2,2,0]`
  - Already sorted array: `[0,0,1,1,2,2]`
  - Reverse sorted: `[2,2,1,1,0,0]`

---

## 🧠 Brute Force Approach: Count Sort

### 👉 Idea:
Use a simple counting approach:
1. Count the number of 0s, 1s, and 2s.
2. Overwrite the original array with that many 0s, then 1s, then 2s.

### 🔧 Java Code:
```java
public static void sortColors(int[] colors) {
    int red = 0, white = 0, blue = 0;

    // Count each color
    for (int color : colors) {
        if (color == 0) red++;
        else if (color == 1) white++;
        else blue++;
    }

    // Overwrite the array
    int index = 0;
    while (red-- > 0) colors[index++] = 0;
    while (white-- > 0) colors[index++] = 1;
    while (blue-- > 0) colors[index++] = 2;
}
```

### ⏱️ Time Complexity:
- **O(N)** — single pass to count, single pass to overwrite

### 🧠 Space Complexity:
- **O(1)** — only counters used

---

## ⚙️ Optimal Solution: Dutch National Flag Algorithm

### 👉 Idea:
Use **three pointers**:
- `low` → where next 0 should go
- `mid` → current element to inspect
- `high` → where next 2 should go

Loop until `mid > high`:
- If `colors[mid] == 0`: swap with `low`, move both `low` and `mid`
- If `colors[mid] == 1`: move `mid`
- If `colors[mid] == 2`: swap with `high`, move `high` only

### 🔧 Java Code:
```java
public static void sortColors(int[] colors) {
    int low = 0, mid = 0, high = colors.length - 1;

    while (mid <= high) {
        if (colors[mid] == 0) {
            // Swap with low
            int temp = colors[low];
            colors[low] = colors[mid];
            colors[mid] = temp;
            low++;
            mid++;
        } else if (colors[mid] == 1) {
            mid++;
        } else {
            // Swap with high
            int temp = colors[mid];
            colors[mid] = colors[high];
            colors[high] = temp;
            high--;
        }
    }
}
```

### 🧪 Dry Run:
Input: `[2, 0, 2, 1, 1, 0]`

After sorting: `[0, 0, 1, 1, 2, 2]`

### ⏱️ Time Complexity:
- **O(N)** — single pass

### 🧠 Space Complexity:
- **O(1)** — no extra space used

---

## ✅ Summary:

| Approach                   | Time Complexity | Space Complexity | Notes                              |
|---------------------------|-----------------|------------------|------------------------------------|
| Brute Force (Count sort)  | O(N)            | O(1)             | 2-pass approach                    |
| Optimal (Dutch Flag Algo) | O(N)            | O(1)             | In-place, 1-pass, very efficient   |

---
