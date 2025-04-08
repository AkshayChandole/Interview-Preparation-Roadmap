
# [Reverse Words in a String](#reverse-words-in-a-string)

## Statement  
Given a sentence, reverse the **order of the words** without reversing the characters inside the words.  

The output string should have:
- No leading/trailing spaces.
- A **single space** between words.

---

### ✅ Constraints:

- `1 <= sentence.length <= 10⁴`
- Input contains English letters (a-z, A-Z), digits (0-9), and spaces.
- Words are defined as sequences of non-space characters.

---

## ✅ Problem Understanding

You're given a string that may contain:
- Extra leading/trailing spaces
- Multiple spaces between words

Your goal:
- Clean it up (one space between words)
- Reverse the **order of words**, **not** the letters in each word.

---

## 🔍 Example

### Input:
```text
"  Hello   world! This   is Java  "
```

### Output:
```text
"Java is This world! Hello"
```

---

## 🧠 Brute Force Approach

### 👉 Idea:
1. Use `trim()` to remove leading/trailing spaces.
2. Use `split("\\s+")` to split by one or more spaces.
3. Reverse the resulting array of words.
4. Join them using `" "`.

### 🔧 Java Code:
```java
import java.util.*;

public class Solution {
    public static String reverseWords(String sentence) {
        // Trim and split by multiple spaces
        String[] words = sentence.trim().split("\\s+");

        // Reverse the array
        Collections.reverse(Arrays.asList(words));

        // Join using single space
        return String.join(" ", words);
    }
}
```

---

### ⏱️ Time Complexity:
- **O(N)** → to split, reverse, and join the string  
### 🧠 Space Complexity:
- **O(N)** → for storing the words array

---

## ⚙️ In-Place (Character Array Manipulation) — Optional

This version:
- Converts the string to a char array
- Reverses the whole array
- Then reverses individual words

More complex, but not needed unless strict in-place is required.

---

### ✅ Summary:

| Approach       | Time Complexity | Space Complexity | Notes                           |
|----------------|----------------|------------------|---------------------------------|
| Brute Force    | O(N)           | O(N)             | Clean, readable, easy to implement |
| In-place (opt) | O(N)           | O(1) (char array) | Complex, useful for low-level optimization |

---
