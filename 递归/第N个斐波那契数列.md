# 第 N 个泰波那契数 #
## 题目： ##
泰波那契序列 Tn 定义如下： 

T0 = 0, T1 = 1, T2 = 1, 且在 n >= 0 的条件下 Tn+3 = Tn + Tn+1 + Tn+2

给你整数 n，请返回第 n 个泰波那契数 Tn 的值。



## 示例 1： ##



> 输入：n = 4


> 输出：4


> 解释：T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4。

## 示例 2： ##



> 输入：n = 25


> 输出：1389537




## 解题思路： ##


1. 递归，但是时间超时
2. 指针


## 解决代码（递归）： ##
    class Solution:
    	def tribonacci(self, n: int) -> int:
    		if n <= 1:
    			return n
    		elif n == 2:
    			return 1
    		else:
    			return self.tribonacci(n-1) + self.tribonacci(n-2) + self.tribonacci(n-3)

## 解决代码2（指针）： ##
    class Solution:
    	def tribonacci(self, n: int) -> int:
        	t0 = 0
        	t1 = 1
        	t2 = 1
        	for i in range(n):
        	    t0, t1, t2 = t1, t2, t0 + t1 + t2
        	return t0