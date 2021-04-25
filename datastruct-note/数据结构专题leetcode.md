# 栈
1. [有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)
2. [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)
  - 解法1： 第一次做，考虑对于某一个高度，其能存水量由左侧最高地基和右侧最高地基中两者的最小值以及该当前高度地基决定。【实际上就是**动态规划**】
```
class Solution:
    def trap(self, height: List[int]) -> int:
        if 0 == len(height):
            return 0
        else:
            lmax = [0]
            rmax = [0]
            lmax_i = 0
            rmax_i = 0
            for i in range(len(height) - 1):
                lmax_i = lmax_i if height[i] <= lmax_i else height[i]
                lmax.append(lmax_i)
                rmax_i = rmax_i if height[len(height) - 1 - i] <= rmax_i else height[len(height) - 1 - i]
                rmax.insert(0, rmax_i)
            for i in range(len(height)):
                rmax[i] = rmax[i] if lmax[i] > rmax[i] else lmax[i]

            sumWater = 0
            for i in range(len(lmax)):
                tempwater = rmax[i] - height[i]
                sumWater += 0 if tempwater < 0 else tempwater
            return sumWater
```
  - 解法2： 双指针，省去lmax和rmax占用的空间
```
class Solution:
    def trap(self, height: List[int]) -> int:
        l_idx = collections.deque()

        sumW = 0
        ptrL = 1
        ptrR = len(height) - 2
        maxL = 0
        maxR = 0
        i = 1
        while i < len(height) - 1:
            if height[ptrL - 1] < height[ptrR + 1]:
                maxL = max(maxL, height[ptrL - 1])
                if maxL > height[ptrL]:
                    sumW = sumW + maxL - height[ptrL]
                ptrL = ptrL + 1
            else:
                maxR = max(maxR, height[ptrR + 1])
                if maxR > height[ptrR]:
                    sumW = sumW + maxR - height[ptrR]
                ptrR = ptrR - 1
            i = i + 1
        return sumW
```
  - 解法3： 参考解法1<https://leetcode-cn.com/problems/trapping-rain-water/solution/wei-en-tu-jie-fa-zui-jian-dan-yi-dong-10xing-jie-j/>
```
class Solution:
    def trap(self, height: List[int]) -> int:
        if 0 == len(height):
            return 0
        else:
            s1 = 0
            s2 = 0
            lmax = 0
            rmax = 0
            for i in range(len(height)):
                if height[i] > lmax:
                    lmax = height[i]
                s1 = s1 + lmax
            for i in range(len(height)):
                if height[len(height) - 1 - i] > rmax:
                    rmax = height[len(height) - 1 - i]
                s2 = s2 + rmax

            sumWater = s1 + s2 - rmax * len(height) - sum(height)

            return sumWater
```

