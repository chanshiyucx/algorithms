# [Valid Parentheses](https://leetcode.cn/problems/valid-parentheses/)

题述：有效的括号，给定一个只包括 '(){}[]' 的字符串 s，判断字符串是否有效。有效字符串需满足：

- 左括号必须用相同类型的右括号闭合。
- 左括号必须以正确的顺序闭合。
- 每个右括号都有一个对应的相同类型的左括号。

思路：如果字符串长度不是偶数，则一定不是有效字符串。使用 map 保存右括号/左括号匹配的键值，遍历字符串，如果是左括号，则推入栈中，如果是右括号，则判断栈顶的字符是不是相匹配的左括号，如果是，则将左括号推出栈顶，进行下个字符遍历；如果不匹配，则不是有效字符串。

复杂度分析：  
时间复杂度：O(n)，n 为字符串的长度。  
空间复杂度：O(n+|Σ|)，其中 Σ 表示字符集，本题中字符串只包含 6 种括号，|Σ|= 6。栈中的字符数量为 O(n)，而哈希表使用的空间为 O(|Σ|)，相加即可得到总空间复杂度。

```javascript
const isValid = (s) => {
  if (s.length % 2 !== 0) {
    return false
  }
  const map = new Map([
    [")", "("],
    ["}", "{"],
    ["]", "["],
  ])
  const ret = []
  for (const ch of s) {
    if (map.has(ch)) {
      if (map.get(ch) === ret.at(-1)) {
        ret.pop()
      } else {
        return false
      }
    } else {
      ret.push(ch)
    }
  }
  return ret.length === 0
}
```
