# LC5 - 最长回文子串

```go title="LongestPalindromicSubstring.go" linenums="1"
func longestPalindrome(s string) string {
	size := len(s)
	dp := make([][]bool, size)
	for i := 0; i < size; i++ {
		dp[i] = make([]bool, size)
	}
	// (1) 计算dp表
	// dp[i][j]: s[i...j]是不是回文子串
	for i := 0; i < size; i++ {
		dp[i][i] = true
	}
	for i := 0; i < size-1; i++ {
		dp[i][i+1] = s[i] == s[i+1]
	}
	for i := size - 3; i >= 0; i-- {
		for j := i + 2; j < size; j++ {
			dp[i][j] = (s[i] == s[j]) && dp[i+1][j-1]
		}
	}
	// (2) 寻找最大回文子串
	for k := size; k > 0; k-- {
		for start, end := 0, k-1; end < size; start, end = start+1, end+1 {
			if dp[start][end] {
				return s[start : end+1]
			}
		}
	}
	return ""
}
```

