# LEETCODE-Strings-2264

---

## **Code Recap - A(1)**

```java
class Solution {
    public String largestGoodInteger(String num) {
        String ans = "";
        for (int i = 2; i < num.length(); i++) {
            if (num.charAt(i-2) == num.charAt(i-1) 
                && num.charAt(i-1) == num.charAt(i) 
                && num.substring(i-2, i+1).compareTo(ans) > 0) 
            {
                ans = num.substring(i-2, i+1);
            }
        }
        return ans;
    }
}
```

---

## **Logic**

* We check **every consecutive triplet** in `num` (`i` points to the last digit of the triplet).
* Condition 1: All three characters are the same.
* Condition 2: The substring is **lexicographically larger** than `ans`.
* If both pass → update `ans`.
* At the end, return the **largest triplet** found.

---

## **Dry Run Example**

Let’s take:

```java
num = "6777332999888"
```

**Step 0 — Initialize:**

```
ans = ""
```

---

**Step 1 — Loop starts at i = 2**

* i = 2 → check substring `"677"` (indices 0..2)
  `num.charAt(0) = '6'`, `num.charAt(1) = '7'` → not equal → skip.

---

**Step 2 — i = 3**

* substring `"777"` (indices 1..3)
  `'7' == '7' == '7'` ✅
  Compare `"777"` with `""` → `"777"` > `""` ✅
  Update: `ans = "777"`

---

**Step 3 — i = 4**

* substring `"773"` → not all equal → skip.

---

**Step 4 — i = 5**

* substring `"733"` → skip.

---

**Step 5 — i = 6**

* substring `"332"` → skip.

---

**Step 6 — i = 7**

* substring `"329"` → skip.

---

**Step 7 — i = 8**

* substring `"299"` → skip.

---

**Step 8 — i = 9**

* substring `"999"`
  All equal ✅
  Compare `"999"` with `"777"` → `"999"` > `"777"` ✅
  Update: `ans = "999"`

---

**Step 9 — i = 10**

* substring `"998"` → skip.

---

**Step 10 — i = 11**

* substring `"988"` → skip.

---

**Step 11 — i = 12**

* substring `"888"`
  All equal ✅
  Compare `"888"` with `"999"` → `"888"` < `"999"` ❌
  No update.

---

**Loop ends.**

---

**Final Output:**

```
"999"
```

---

## **Key Observations**

* This approach doesn’t need a predefined array — it dynamically finds the largest triplet.
* The lexicographical comparison works here because all good integers have the same length (3 characters).
* Time complexity: O(n), Space: O(1).

---


---


### **Code Recap - A(2)**

```java
class Solution {
    public String largestGoodInteger(String num) {
        String[] nums = {"999","888","777","666","555","444","333","222","111","000"};
        for (String x : nums) {
            if (num.contains(x)) {
                return x;
            }
        }
        return "";
    }
}
```

---

### **Understanding the Problem**

* This method is trying to find the **largest "good" integer** in `num`.
* A *good integer* = three identical consecutive digits (e.g., `"777"`, `"000"`).
* The array `nums` is ordered **from largest to smallest**.
* We return the first match we find because the order guarantees it’s the largest possible.

---

### **Dry Run Example**

Let’s test with:

```java
num = "6777332999888"
```

---

**Step 1 — Initialize array:**

```
nums = ["999", "888", "777", "666", "555", "444", "333", "222", "111", "000"]
```

---

**Step 2 — Loop over each element of nums:**

1. `x = "999"`

   * `num.contains("999")` → ✅ Yes, `"999"` is in `"6777332999888"`.
   * **Return `"999"` immediately**.
   * The loop stops here — we don’t even check `"888"`, `"777"`, etc.

---

**Output:**

```
"999"
```

---

### **Another Example**

```java
num = "1222333444"
```

* `"999"` → ❌ Not found
* `"888"` → ❌ Not found
* `"777"` → ❌ Not found
* `"666"` → ❌ Not found
* `"555"` → ❌ Not found
* `"444"` → ✅ Found → return `"444"`

---

### **Key Points from the Dry Run**

* The method **only needs to scan until it finds the first match** (because array is sorted from largest to smallest).
* Time complexity: O(10 \* n) where `n` is `num` length (practically O(n) because 10 is constant).
* Space complexity: O(1) extra space.

---
