# 中心对称数II #
## 题目： ##
中心对称数是指一个数字在旋转了 180 度之后看起来依旧相同的数字（或者上下颠倒地看）。

找到所有长度为 n 的中心对称数。


## 示例 1： ##

> 输入：n = 2


> 输出： ["11","69","88","96"]


## 解题思路： ##


1. 当 n=0 的时候，应该输出空字符串：“ ”。


1. 当 n=1 的时候，也就是长度为 1 的中心对称数有：0，1，8。


1. 当 n=2 的时候，长度为 2 的中心对称数有：11， 69，88，96。注意：00 并不是一个合法的结果。


1. 当 n=3 的时候，只需要在长度为 1 的合法中心对称数的基础上，不断地在两边添加 11，69，88，96 就可以了。
[101, 609, 808, 906, 111, 619, 818, 916, 181, 689, 888, 986]
随着 n 不断地增长，我们只需要在长度为 n-2 的中心对称数两边添加 11，69，88，96 即可。



- n=0

![](https://pic.leetcode-cn.com/4b737261da853a11869b5c3c939f6ca16145aef14515138f2ada618ba581f0b4-%E5%9B%BE%E7%89%87.png)

- n=1

![](https://pic.leetcode-cn.com/175cbc8a1da7eaedb9abc132abba3e9f7f941153cbac230db7b8c922408baf14-%E5%9B%BE%E7%89%87.png)

- n=2

![](https://pic.leetcode-cn.com/b67cd3ff48533c393eeb0e361e0705264f93178ffca0221f9b2fdde01aa76473-%E5%9B%BE%E7%89%87.png)

- n=3

![](https://pic.leetcode-cn.com/5deb5246d3566543801a2d406d9ddc868208e27cb30f99dfbced5b08df68c34a-%E5%9B%BE%E7%89%87.png)

- n=4

![](https://pic.leetcode-cn.com/7a2e3ae14d8feeea7487b8d678a436e8ba57f05fea08e311039015eb7d01be4e-%E5%9B%BE%E7%89%87.png)



## 解决代码 ##
    class Solution:
    	def findStrobogrammatic(self, n: int) -> List[str]:
        	dict = {"1":"1", "9":"6", "6":"9", "8":"8"} # 按照前文分析构造字典用于抓取数字字符串
        
        	def find(x): # 定义递归函数
            	if x == 0: # 定义基准条件，长度为0和长度为1，长度大于1时，类似“00”不算数字，故提前定义
                	return [""]
            	elif x == 1:
                	return ["0", "1", "8"]
            
            	anslist = [] # 定义初始列表
            	for num in find(x-2): # 将二阶之前的列表，在每个数字前后添加数字“1”、“1”或“6”、“9”等即可
                	for key, value in dict.items():
                    	anslist.append(key + num + value)

                	if x != n: # 在非最后一项之前的列表中数字还可以添加“0”、“0”变成类似“080”，因为后想变换后“6000008000009”这样的数也符合要求
                    	anslist.append("0" + num + "0")
            	return anslist # 递归函数输出的为此列表
        	
			return find(n)