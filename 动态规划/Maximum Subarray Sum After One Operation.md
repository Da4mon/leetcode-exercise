# 删除一次得到子数组最大和 #
## 题目： ##
You are given an integer array nums. You must perform exactly one operation where you can replace one element nums[i] with nums[i] * nums[i]. 

Return the maximum possible subarray sum after exactly one operation. The 


## 示例 1： ##



> 输入： nums = [2,-1,-4,-3]


> 输出：17


> 解释：You can perform the operation on index 2 (0-indexed) to make nums = [2,-1,16,-3]. Now, the maximum subarray sum is 2 + -1 + 16 = 17.


## 示例 2： ##



> 输入：nums = [1,-1,1,1,-1,-1,1]


> 输出：4


> 解释：Explanation: You can perform the operation on index 1 (0-indexed) to make nums = [1,1,1,1,-1,-1,1]. Now, the maximum subarray sum is 1 + 1 + 1 + 1 = 4.



## 解题思路： ##
动态规划，用二维数据dp[i][0]表示以第i个数字为结尾的未替换的连续子数组最大和，dp[i][1]表示以第i个数字为结尾的替换过的连续子数组最大和。

dp[i][0]可以是

1. 之前dp[i-1][0]的结果加上当前num

1. 或者仅仅是当前num

两者取最大


dp[i][1]可以是

1. 替换当前num，则结果为之前dp[i-1][0]的结果加上当前num的平方

1. 替换的不是当前num，则结果是之前替换过的dp[i-1][1]加上当前num

1. 仅仅是当前num的平方这一项

三者取最大

## 解决代码： ##
    class Solution:
    	def maxSumAfterOperation(self, nums: List[int]) -> int:
        	n = len(nums) # 定义初始列表
        	dp = [[0,0] for i in range(n)]
        	dp[0][0] = nums[0]
        	dp[0][1] = nums[0]**2
        	ans = nums[0]**2
        
        	for i in range(1, n):
            	dp[i][0] = max(dp[i-1][0] + nums[i], nums[i])
            	dp[i][1] = max(dp[i-1][0] + nums[i]**2, dp[i-1][1] + nums[i], nums[i]**2)
            	ans = max(ans, dp[i][1]) # 时刻更新最大值，第一次与长度为1的列表替换后结果做对比
			
			return ans