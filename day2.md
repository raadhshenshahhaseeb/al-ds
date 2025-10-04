## 918. Maximum Sum Circular Subarray
```
func maxSubarraySumCircular(nums []int) int {
	if len(nums) == 0 {
		return 0
	}
	minValue, maxValue := nums[0], nums[0]   // the most value
	minWeight, maxWeight := nums[0], nums[0] // how much to carry
	sack := nums[0]
	for i := 1; i < len(nums); i++ {
		sack += nums[i]
		if maxValue+nums[i] > nums[i] {
			maxValue += nums[i]
		} else {
			maxValue = nums[i]
		}
		if maxValue > maxWeight {
			maxWeight = maxValue
		}
		if minValue+nums[i] < nums[i] {
			minValue += nums[i]
		} else {
			minValue = nums[i]
		}
		if minValue < minWeight {
			minWeight = minValue
		}
	}
	if maxWeight < 0 {
		return maxWeight
	}
	if sack-minWeight > maxWeight {
		return sack - minWeight
	}
	return maxWeight
}
```

## 53. Maximum Subarray
```
func maxSubArray(nums []int) int {
	if len(nums) == 0 {
		return 0
	}
  
	value := nums[0] // the most value
	weight := nums[0]// how much to carry
  
	for i := 1; i < len(nums); i++ {
		if weight+nums[i] > nums[i] {
			weight += nums[i]
		} else {
			weight = nums[i]
		}
    
		if weight > value {
			value = weight
		}
	}
	return value
}

```
