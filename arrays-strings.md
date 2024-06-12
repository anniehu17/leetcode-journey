Dutch National Flag Algorithm (3-way Partitioning) [Leetcode Problem](https://leetcode.com/problems/sort-colors/description/)

```
class Solution {
    public void sortColors(int[] nums) {
        int low = 0, mid = 0, high = nums.length - 1;
        while (mid <= high) {
            if (nums[mid] == 0) {
                swap(nums, low, mid);
                low++;
                mid++;
            } else if (nums[mid] == 1) {
                mid++;
            } else {
                swap(nums, mid, high);
                high--;
            }
        }
    }
    
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```
Prefix Sum [Leetcode Problem](https://leetcode.com/problems/range-sum-query-immutable/)
```
class NumArray {

    private int[] prefixSum;
    public NumArray(int[] nums) {
        prefixSum = new int[nums.length + 1];
        for(int i = 0; i < nums.length; i++){
            prefixSum[i + 1] = prefixSum[i] + nums[i];
        }
        System.out.println(prefixSum)
    }
    
    public int sumRange(int left, int right) {
        return prefixSum[right + 1] - prefixSum[left];
    }
}
```
