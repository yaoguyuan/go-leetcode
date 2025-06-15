# [LC1 - 两数之和](https://leetcode.cn/problems/two-sum/description/?envType=study-plan-v2&envId=top-100-liked)

```go title="TwoSum.go" linenums="1"
package HashTable

import (
	"cmp"
	"slices"
)

func twoSum(nums []int, target int) []int {
	return twoSum1(nums, target)
}

type indexedNum struct {
	Value int
	Index int
}

// 时间复杂度: O(n * log n), 空间复杂度: O(n)
func twoSum1(nums []int, target int) []int {
	indexedNums := make([]indexedNum, len(nums))
	for i, num := range nums {
		indexedNums[i] = indexedNum{num, i}
	}
	slices.SortFunc(indexedNums, func(a, b indexedNum) int {
		return cmp.Compare(a.Value, b.Value)
	})
	left, right := 0, len(nums)-1
	for left < right {
		sum := indexedNums[left].Value + indexedNums[right].Value
		if sum == target {
			return []int{indexedNums[left].Index, indexedNums[right].Index}
		} else if sum > target {
			right--
		} else {
			left++
		}
	}
	return nil
}

// 时间复杂度: O(n), 空间复杂度: O(n)
func twoSum2(nums []int, target int) []int {
	hashTable := make(map[int]int)
	for index2, num2 := range nums {
		num1 := target - num2
		if index1, ok := hashTable[num1]; ok {
			return []int{index1, index2}
		} else {
			hashTable[num2] = index2
		}
	}
	return nil
}
```

第一反应是排序后双指针，但由于需要返回原数组索引而非数值，因此必须借助辅助数组。