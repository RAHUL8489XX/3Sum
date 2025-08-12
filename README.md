# 🧠 3Sum — LeetCode Problem 15

[Link to Problem](https://leetcode.com/problems/3sum)

## 🧩 Problem Statement

Given an integer array `nums`, return all **unique triplets** `[nums[i], nums[j], nums[k]]` such that:

- `i ≠ j`, `i ≠ k`, `j ≠ k`
- `nums[i] + nums[j] + nums[k] == 0`

The solution set must not contain duplicate triplets.

---

## ✅ Approach: Sorting + Two Pointers

1. **Sort the array** to simplify duplicate handling and pointer movement.
2. **Iterate** through each element `i`:
   - Skip duplicates.
   - Use **two pointers** (`left`, `right`) to find pairs that sum with `nums[i]` to zero.
   - Skip duplicate pairs after finding a valid triplet.

---

## 📦 Code

```python
class Solution(object):
    def threeSum(self, nums):
        nums.sort()
        res = []

        for i in range(len(nums)):
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            left, right = i + 1, len(nums) - 1
            while left < right:
                total = nums[i] + nums[left] + nums[right]
                if total < 0:
                    left += 1
                elif total > 0:
                    right -= 1
                else:
                    res.append([nums[i], nums[left], nums[right]])
                    left += 1
                    right -= 1
                    while left < right and nums[left] == nums[left - 1]:
                        left += 1
                    while left < right and nums[right] == nums[right + 1]:
                        right -= 1
        return res
```

## Example Test Cases
| Input              | Output                  | Explanation                              |
|-------------------|-------------------------|------------------------------------------|
| `[-1,0,1,2,-1,-4]` | `[[-1,-1,2],[-1,0,1]]`  | Two valid triplets that sum to zero      |
| `[0,1,1]`          | `[]`                    | No combination adds up to zero           |
| `[0,0,0]`          | `[[0,0,0]]`             | Only one valid triplet with all zeros    |



## Complexity Analysis
| Metric     | Value     | Notes                                      |
|------------|-----------|--------------------------------------------|
| Time       | O(n²)     | Due to nested iteration with two pointers |
| Space      | O(n)      | For sorting and storing results           |
