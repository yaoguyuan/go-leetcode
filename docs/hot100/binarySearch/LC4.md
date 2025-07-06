# LC4 - 寻找两个正序数组的中位数

```go title="MedianOfTwoSortedArrays.go" linenums="1"
package BinarySearch

// findKSortedArrays is a helper function to find the k-th smallest element in two sorted arrays.
// k: the k-th element to find
// nums1: the first sorted array
// s1: the starting index for nums1
// nums2: the second sorted array
// s2: the starting index for nums2
func findKSortedArrays(k int, nums1 []int, s1 int, nums2 []int, s2 int) int {
	len1 := len(nums1)
	len2 := len(nums2)

	// If nums1 is exhausted, the k-th element must be in nums2.
	if s1 == len1 {
		return nums2[s2+k-1]
	}
	// If nums2 is exhausted, the k-th element must be in nums1.
	if s2 == len2 {
		return nums1[s1+k-1]
	}
	// If k is 1, return the minimum of the current elements in both arrays.
	if k == 1 {
		return min(nums1[s1], nums2[s2])
	}

	half := k / 2

	// newS1 is the next starting index for nums1.
	// newS2 is the next starting index for nums2.
	// We take 'half' elements from each array if possible.
	newS1 := min(len1, s1+half)
	newS2 := min(len2, s2+half)

	// cnt1 is the number of elements considered from nums1 in this step.
	// cnt2 is the number of elements considered from nums2 in this step.
	cnt1 := newS1 - s1
	cnt2 := newS2 - s2

	// Compare the last elements of the considered parts of nums1 and nums2.
	if nums1[newS1-1] <= nums2[newS2-1] {
		return findKSortedArrays(k-cnt1, nums1, newS1, nums2, s2)
	} else {
		return findKSortedArrays(k-cnt2, nums1, s1, nums2, newS2)
	}
}

// findMedianSortedArrays finds the median of two sorted arrays.
func findMedianSortedArrays(nums1 []int, nums2 []int) float64 {
	len1 := len(nums1)
	len2 := len(nums2)
	lenTotal := len1 + len2

	// For an odd length, the median is the single middle element.
	// For an even length, the median is the average of the two middle elements.
	// We can unify these two situations by calculating 'k1' and 'k2' :
	k1 := (lenTotal + 1) / 2
	k2 := (lenTotal + 2) / 2

	// Find the k1-th and k2-th smallest elements.
	r1 := findKSortedArrays(k1, nums1, 0, nums2, 0)
	r2 := findKSortedArrays(k2, nums1, 0, nums2, 0)

	return float64(r1+r2) / 2
}
```

注释写的比较清楚，详细分析过程参考热门题解。