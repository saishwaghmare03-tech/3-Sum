# LeetCode 16. 3Sum Closest

This repository contains an optimal Java solution for the [LeetCode 16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/) problem.

## 💡 Problem Description

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. 

Return the sum of the three integers. You may assume that each input would have exactly one solution.

### Examples

* **Example 1:**
  * **Input:** `nums = [-1, 2, 1, -4]`, `target = 1`
  * **Output:** `2`
  * **Explanation:** The sum that is closest to the target is 2. `(-1 + 2 + 1 = 2)`.

* **Example 2:**
  * **Input:** `nums = [0, 0, 0]`, `target = 1`
  * **Output:** `0`
  * **Explanation:** The sum that is closest to the target is 0. `(0 + 0 + 0 = 0)`.

---

## 🚀 Approach: Sorting & Two Pointers

1. **Sorting:** We first sort the input array `nums`. This allows us to navigate through potential triplet combinations efficiently using two pointers.
2. **Iteration:** We iterate through the array, fixing one element at index `i`, and use two pointers (`left` starting at `i + 1` and `right` starting at the end of the array).
3. **Comparison:** 
   * Calculate the `currentSum`.
   * If `currentSum` matches the `target` perfectly, we return immediately.
   * Compare its distance to the `target` against our tracked `closestSum` and update if it's closer.
   * Adjust the pointers depending on whether the `currentSum` is less than or greater than the `target`.

---

## 📊 Complexity Analysis

* **Time Complexity:** $O(N^2)$ — Sorting takes $O(N \log N)$ and the nested traversal takes $O(N^2)$.
* **Space Complexity:** $O(1)$ or $O(\log N)$ — Auxiliary space required for sorting depending on the implementation.

---

## ☕ Java Code

```java
import java.util.Arrays;

public class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int closestSum = nums[0] + nums[1] + nums[2];
        
        for (int i = 0; i < nums.length - 2; i++) {
            int left = i + 1;
            int right = nums.length - 1;
            
            while (left < right) {
                int currentSum = nums[i] + nums[left] + nums[right];
                
                if (currentSum == target) {
                    return target;
                }
                
                if (Math.abs(currentSum - target) < Math.abs(closestSum - target)) {
                    closestSum = currentSum;
                }
                
                if (currentSum < target) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        
        return closestSum;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();

        int[] nums1 = {-1, 2, 1, -4};
        int target1 = 1;
        System.out.println("Example 1 Output: " + solution.threeSumClosest(nums1, target1)); // Expected: 2

        int[] nums2 = {0, 0, 0};
        int target2 = 1;
        System.out.println("Example 2 Output: " + solution.threeSumClosest(nums2, target2)); // Expected: 0
    }
}
