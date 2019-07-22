# TwoSum
---
layout:     post
title:      TwoSum
subtitle:   leetcode:tow sum�)
date:       2017-02-06
author:     BY
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - leetcode 算法

---
> 正所谓前人栽树，后人乘凉。
> 感谢[Huxpro](https://github.com/huxpro)提供的博客模板
---
# 1、最初模式
2次for循环，其时间复杂度为`O(2n)`,采用`map`存放`target`于`nums[i]`的差及`i`,也就是`iMap[target-nums[i]] = i`，发现这样空间消耗过高，遂有了下文的优化。
```
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int>iMap;
		vector<int>iVec;
		for (unsigned int i = 0; i < nums.size(); i++) {
			iMap[target-nums[i]] = i;
		}
		for (unsigned int i = 0; i < nums.size(); i++) {
		    int iNum = nums[i];
			auto it = iMap.find(iNum);
			if (it != iMap.end() && it->second!=i) {
			    iVec.push_back(i);
				iVec.push_back(it->second);
				break;
			}
		}
		return iVec;
    }
```
# 2、第一次优化
1次for循环，其时间复杂度为`O(n)`。
```
    map<int, int>iMap;
		vector<int>iVec;
		for (unsigned int i = 0; i < nums.size(); i++) {
			iMap[target-nums[i]] =i ;
            auto it = iMap.find(nums[i]);
			if (it != iMap.end() && it->second!=i) {
				iVec.push_back(i);
				iVec.push_back(it->second);
				break;
			}
		}
		return iVec;
```
# 3、参考其他人解法1
1次for循环，其时间复杂度为`O(n)`。采用`map`的`count`方法来判断是否包含`target - nums[i]`，但是发现其效率没有`find`高。
```
	 vector<int> twoSum(vector<int>& nums, int target) {
		map<int, int>iMap;
		vector<int>iVec;
		for (unsigned int i = 0; i < nums.size(); i++) {
			int sub = target - nums[i];
			if (iMap.count(sub) <= 0)
				iMap[nums[i]] = i;
			else {
				iVec.push_back(i);
				iVec.push_back(iMap[sub]);
				break;
			}
		}
		return iVec;
	}
```	
# 4、最终解法
1次for循环，其时间复杂度为`O(n)`。采用`map`的`find`方法来判断是否包含`target - nums[i]`。
```	
    vector<int> twoSum(vector<int>& nums, int target) {
	    map<int, int>iMap;
		vector<int>iVec;
		for (unsigned int i = 0; i < nums.size(); i++) {
            auto it = iMap.find(nums[i]);
            if(it==iMap.end())
                iMap[target-nums[i]] =i ;
			else if (it->second!=i) {
				iVec.push_back(i);
				iVec.push_back(it->second);
				break;
			}
		}
		return iVec;
	}
	 
```		
	