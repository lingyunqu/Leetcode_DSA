代码随想录的听课及做题笔记

##1
```
class Solution {
public:
    int search(vector<int>& nums, int target) {
            //左闭右闭
            int left = 0; //从下标0开始
            int right = nums.size() - 1;
            //已有左右边界，进入while循环
            while(left <= right){ //左闭右闭，left=right的情况是合法的
                int middle = (left + right)/2;
                if (nums[middle] > target){//nums[middle]不是搜索的值，接下来的区间不能包含这个值
                    right = middle - 1;
                }
                else if(nums[middle] < target){//更新右区间的左边界
                    left = middle + 1;
                }
                else return middle;
            }
    return -1;
    }
};
```
