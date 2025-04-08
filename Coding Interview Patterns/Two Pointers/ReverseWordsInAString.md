# [Reverse Words in a String](#reverse-words-in-a-string)

## Statement  
Given a sentence, reverse the order of its words **without affecting the order of letters within the given word**.

---

#### Constraints:
- The sentence contains English uppercase and lowercase letters, digits, and spaces.
- `1 ≤ sentence.length ≤ 10^4`
- Words are separated by spaces.  
- Leading/trailing spaces or multiple spaces may exist.
- The result should only have **single spaces between words** and **no leading/trailing spaces**.

---

## Solution:

### ✅ Problem Understanding

We are asked to **reverse the order of words**, not the characters within the words.  
Also, we must **remove extra spaces** (leading/trailing/multiple spaces between words).

---

### ✅ Constraints and Edge Cases

- Sentence might have:
  - Leading and trailing spaces.
  - Multiple spaces between words.
- Sentence can be a single word.
- Sentence can contain only spaces.

---

### 🧠 Two Pointer Approach using Word Array

#### 👉 Idea:

1. Trim the sentence to remove leading/trailing spaces.
2. Split the sentence using regular expression `"\\s+"` to handle multiple spaces.
3. Use two pointers to reverse the `words[]` array **in-place**.
4. Join the words with a single space to return the final sentence.

---

#### 🔧 Java Code:

```java
import java.util.*;

public class Solution {
    public static String reverseWords(String sentence) {
        sentence = sentence.trim();
        String[] words = sentence.split("\\s+");
        int left = 0, right = words.length - 1;

        while (left < right) {
            String temp = words[left];
            words[left] = words[right];
            words[right] = temp;
            left++;
            right--;
        }

        return String.join(" ", words);
    }
}
```

---

### 🧪 Dry Run:

Input: `"  Hello   world! This   is Java  "`  
- After trimming: `"Hello   world! This   is Java"`  
- After splitting: `["Hello", "world!", "This", "is", "Java"]`  
- After reversing: `["Java", "is", "This", "world!", "Hello"]`  
- Final Output: `"Java is This world! Hello"`

---

### ⏱️ Time Complexity:
- **O(N)** – where N is the length of the string

### 🧠 Space Complexity:
- **O(N)** – due to the array used in split and String.join

---

### ✅ Summary:

| Approach                  | Time Complexity | Space Complexity | Notes                          |
|---------------------------|-----------------|------------------|---------------------------------|
| Two Pointer (split array) | O(N)            | O(N)             | Clean and simple to implement  |

---
