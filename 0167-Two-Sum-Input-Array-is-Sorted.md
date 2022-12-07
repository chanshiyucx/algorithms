# [Two Sum Input Array is Sorted](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted)

题述：给你一个下标从 1 开始的整数数组 numbers，该数组已按**非递减顺序排列**，请你从数组中找出满足相加之和等于目标数 target 的两个数。如果设这两个数分别是 numbers[index1] 和 numbers[index2] ，则 `1 <= index1 < index2 <= numbers.length`。以长度为 2 的整数数组 [index1, index2] 的形式返回这两个整数的下标 index1 和 index2。

思路一：使用和两数之和一样的解法，暴力循环数组，利用 Map 缓存当前项的值与索引，并计算数组项与目标值 target 的差值，如果在循环过程中发现缓存中存在差值匹配，则返回，这里需要注意下标是从 1 开始，所以返回的索引要加 1。

复杂度分析：  
时间复杂度：O(n)，其中 n 是数组的长度，对于每一个元素 x，我们可以 O(1) 地寻找 target - x。  
空间复杂度：O(n)，主要为 map 的开销。

```javascript
const twoSum = (numbers, target) => {
  const map = new Map()
  for (let i = 0; i < numbers.length; i++) {
    const s = target - numbers[i]
    if (map.has(s)) {
      return [map.get(s) + 1, i + 1]
    }
    map.set(numbers[i], i)
  }
}
```

思路二：注意到数组已按**非递减顺序排列**，即数组是升序数组，可以使用二分查找的方式优化算法。先确定第一个数，再从右侧查找第二个数，用二分法逐步缩小第二个数的查找范围，直到找出第二个数。

复杂度分析：  
时间复杂度：O(nlogn)，其中 n 是数组的长度，需要遍历数组一次确定第一个数，时间复杂度是 O(n)，寻找第二个数使用二分查找，时间复杂度是 O(log⁡n)，因此总时间复杂度是 O(nlog⁡n)。
空间复杂度：O(1)。

```javascript
const twoSum = (numbers, target) => {
  for (let i = 0; i < numbers.length - 1; i++) {
    const s = target - numbers[i]
    let left = i + 1,
      right = numbers.length - 1
    while (left <= right) {
      let mid = Math.floor((right - left) / 2) + left
      if (numbers[mid] < s) {
        left = mid + 1
      } else if (numbers[mid] > s) {
        right = mid - 1
      } else {
        return [i + 1, mid + 1]
      }
    }
  }
}
```
