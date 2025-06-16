# LC3 - 无重复字符的最长子串

```go title="LongestSubstringWithoutRepeatingCharacters.go" linenums="1"
package SlidingWindow

// 时间复杂度: O(n), 空间复杂度: O(∣Σ∣) [∣Σ∣为字符集大小]
func lengthOfLongestSubstring(s string) int {
	hashSet := make(map[byte]bool)
	lbound, rbound, result := 0, 0, 0
	for ; rbound < len(s); rbound++ {
		if !hashSet[s[rbound]] {
			hashSet[s[rbound]] = true
		} else {
			result = max(result, rbound-lbound)
			for ; s[lbound] != s[rbound]; lbound++ {
				hashSet[s[lbound]] = false
			}
			lbound++
		}
	}
	result = max(result, rbound-lbound)
	return result
}
```

