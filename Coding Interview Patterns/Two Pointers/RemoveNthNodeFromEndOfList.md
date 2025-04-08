# [Remove nth Node from End of List](#remove-nth-node-from-end-of-list)

## Statement: 
Given the head of a singly linked list, remove the nth node from the end of the list and return its head.

#### Constraints:
* The number of nodes in the list is k.
* 1 <= k <= 10^3
* -10^3 <= Node.value <= 10^3
* 1 <= n <= k

## Solution:

### ✅ Problem Understanding

Given a singly linked list, remove the **n-th node from the end** and return the **head of the modified list**.

---

### ✅ Constraints and Edge Cases

- `1 <= k <= 10^3` → Reasonable for O(N) solutions.
- `-10^3 <= Node.val <= 10^3`
- `1 <= n <= k`
- Edge cases:
  - Removing the **head node** (i.e., `n == k`)
  - Single node list (`k == 1`)
  - `n == 1` → Remove the **last node**

---

### 🧠 Brute Force Approach

#### 👉 Idea:

1. Traverse the list to count the total number of nodes `len`.
2. Find the position to delete from the beginning: `len - n`.
3. Traverse again to that position and remove the node.

#### 🔧 Java Code:
```java
public static ListNode removeNthLastNode(ListNode head, int n) {
    int len = 0;
    ListNode curr = head;

    // Step 1: Count the number of nodes
    while (curr != null) {
        len++;
        curr = curr.next;
    }

    // If we need to delete the head
    if (n == len) {
        return head.next;
    }

    // Step 2: Find the (len - n)th node
    curr = head;
    for (int i = 1; i < len - n; i++) {
        curr = curr.next;
    }

    // Step 3: Skip the target node
    curr.next = curr.next.next;

    return head;
}
```

#### ⏱️ Time Complexity:
- O(N) for first traversal + O(N) for second = **O(N)**

#### 🧠 Space Complexity:
- No extra space = **O(1)**

---

### ⚙️ Better / Optimal Solution: Two Pointers (Fast & Slow)

#### 👉 Idea:

1. Use two pointers: `fast` and `slow`.
2. Move `fast` ahead by `n` steps.
3. Move both `fast` and `slow` until `fast` reaches the end.
4. `slow` will be just before the node to delete.

#### 🔧 Java Code:
```java
public static ListNode removeNthLastNode(ListNode head, int n) {
    // Create a dummy node to simplify edge cases
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    
    ListNode fast = dummy;
    ListNode slow = dummy;

    // Move fast ahead by n+1 steps to maintain the gap
    for (int i = 0; i <= n; i++) {
        fast = fast.next;
    }

    // Move both until fast reaches the end
    while (fast != null) {
        fast = fast.next;
        slow = slow.next;
    }

    // Skip the target node
    slow.next = slow.next.next;

    return dummy.next;
}
```

#### 🧪 Dry Run:

```
List: 1 → 2 → 3 → 4 → 5, n = 2

Dummy → 1 → 2 → 3 → 4 → 5
         ↑              ↑
       slow           fast

After loop: remove node 4
Result: 1 → 2 → 3 → 5
```

#### ⏱️ Time Complexity:
- **O(N)**: Single traversal

#### 🧠 Space Complexity:
- **O(1)**

---

### ✅ Summary:

| Approach        | Time Complexity | Space Complexity | Notes                          |
|----------------|-----------------|------------------|--------------------------------|
| Brute Force     | O(N)            | O(1)             | Two passes                     |
| Two Pointer     | O(N)            | O(1)             | One pass, optimal solution     |

---
