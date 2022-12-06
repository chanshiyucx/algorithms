# [Two Sum](https://leetcode.cn/problems/two-sum/)

题述：两数之和，给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出和为目标值 target 的那两个整数，并返回它们的数组下标。

思路：使用暴力循环数组，利用 Map 缓存当前项的值与索引，并计算数组项与目标值 target 的差值，如果在循环过程中发现缓存中存在差值匹配，则返回。

复杂度分析：
时间复杂度：O(n)，其中 n 是数组的长度，对于每一个元素 x，我们可以 O(1) 地寻找 target - x。
空间复杂度：O(n)，主要为 map 的开销。

```javascript
const twoSum = (nums, target) => {
  const map = new Map()
  for (let i = 0; i < nums.length; i++) {
    const s = target - nums[i]
    if (map.has(s)) {
      return [map.get(s), i]
    }
    map.set(nums[i], i)
  }
}
```
