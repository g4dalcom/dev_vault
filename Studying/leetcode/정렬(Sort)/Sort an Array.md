Given an array of integers `nums`, sort the array in ascending order and return it.

You must solve the problem **without using any built-in** functions in `O(nlog(n))` time complexity and with the smallest space complexity possible.

**Example 1:**

**Input:** nums = [5,2,3,1]
**Output:** [1,2,3,5]
**Explanation:** After sorting the array, the positions of some numbers are not changed (for example, 2 and 3), while the positions of other numbers are changed (for example, 1 and 5).

**Example 2:**

**Input:** nums = [5,1,1,2,0,0]
**Output:** [0,0,1,1,2,5]
**Explanation:** Note that the values of nums are not necessairly unique.

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `-5 * 104 <= nums[i] <= 5 * 104`

---

```java
class Solution {
    public int[] sortArray(int[] nums) {
        for (int i = (nums.length-1)/2; i >= 0; i--) {
            heapify(nums, i, nums.length);
        }
        
        for (int i = nums.length-1; i > 0; i--) {
            swap(nums, 0, i);
            heapify(nums, 0, i);
        }
        
        return nums;
    }
    
    public void heapify(int[] nums, int parentIdx, int size) {
        int left;
        int right;
        int largest;
        
        while ((parentIdx * 2) + 1 < size) {
            left = parentIdx * 2 + 1;
            right = parentIdx * 2 + 2;
            largest = parentIdx;
            
            if (nums[left] > nums[largest]) largest = left;
            
            if (right < size && nums[right] > nums[largest]) largest = right;
            
            if (largest != parentIdx) {
                swap(nums, parentIdx, largest);
                parentIdx = largest;
            } 
            else return;
        }
    }
    
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```