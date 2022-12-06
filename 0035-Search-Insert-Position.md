# [Search Insert Position](https://leetcode.cn/problems/search-insert-position)

题述：搜索插入位置，给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

思路：使用二分查找，设置初始查找范围为左右边界，每次取查找范围的中点 mid，比较 nums[mid] 与 target 的大小，如果相等则 mid 即为要求的下表，否则根据大小关系缩小查找范围。

复杂度分析：  
时间复杂度：O(log⁡n)，其中 n 是数组的长度。  
空间复杂度：O(1)。

```js
const searchInsert = (nums, target) => {
  const length = nums.length
  let left = 0,
    right = length - 1
  while (left <= right) {
    let mid = Math.floor((right - left) / 2) + left
    if (nums[mid] === target) {
      return mid
    } else if (nums[mid] > target) {
      right = mid - 1
    } else {
      left = mid + 1
    }
  }
  return left
}
```
