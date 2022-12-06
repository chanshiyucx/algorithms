# Palindrome Number

题述：回文数，给你一个整数 x，如果 x 是一个回文整数，返回 true；否则，返回 false。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

思路一：讲整数转为字符串，再转为字符数组，反序合并后比较。

复杂度分析：
时间复杂度：O(n)，n 是整数位数。
空间复杂度：O(n)。

```javascript
const isPalindrome = (x) => {
  return String(x) === String(x).split("").reverse().join("")
}
```

思路二：负数或个位不为 0 的数都不会是回文数，然后我们目标是将整数从中间拆分成前后两部分，我们通过对 10 取余得到最后一位，再取余得到倒数第二位，依次进行，我们将取余后的值乘 10 进行升位，就得到反序的值。

问题是如何知道已经取余到中间位置？由于整个过程我们不断将原始数字除以 10，然后给反转后的数字乘上 10，所以，当原始数字小于或等于反转后的数字时，就意味着我们已经处理了一半位数的数字了。

复杂度分析：  
时间复杂度：O(logn)，n 是整数位数，对于每次迭代，都会将输入除以 10。  
空间复杂度：O(1)。

```javascript
const isPalindrome = (x) => {
  if (x < 0 || (x % 10 === 0 && x !== 0)) {
    return false
  }
  let revertedNumber = 0
  while (x > revertedNumber) {
    revertedNumber = revertedNumber * 10 + (x % 10)
    x = Math.floor(x / 10)
  }
  return x === revertedNumber || x === Math.floor(revertedNumber / 10)
}
```
