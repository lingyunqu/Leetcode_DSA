代码随想录的听课及做题笔记

##1
704. 二分查找
```
class Solution {
public:
    int search(vector<int>& nums, int target) {
            //左闭右闭：
//left 被设置为数组的第一个元素的索引，右边界 right 被设置为数组的最后一个元素的索引。
            int left = 0; //从下标0开始

            int right = nums.size() - 1;
            //已有左右边界，进入while循环
            //循环条件是 left <= right，也就是说只要搜索区间不为空，就继续进行查找。这个条件保证了即使搜索区间只剩下一个元素，也会继续查找。
            //循环条件不能使用 middle != target 的原因是，这个条件无法保证在所有情况下都能正确地找到目标值。
            while(left <= right){ //左闭右闭，left=right的情况是合法的
                int middle = (left + right)/2;
                if (nums[middle] > target){//nums[middle]不是搜索的值，接下来的区间不能包含这个值
                //通过比较中间元素 nums[middle] 与目标值 target 的大小关系，可以确定目标值在左半部分还是右半部分。
                //不是比较middle和target！
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

```
class Solution {
public:
    int search(vector<int>& nums, int target) {
        //左闭右开：包含左，不包含右
        int left = 0; // 从左边开始
        int right = nums.size() - 1; //最右边

        while (left = right){
            int middle  = (left + right)/2;
            if (nums[middle] > target){
                right = middle; //左闭右开区间不包含right，下一个搜索的区间也不包含middle，则直接就是middle - 1
            }
            else if(nums[middle] < target){
                left = middle + 1; //接下来的区间不包含middle，需要是middle + 1
            }
            else return middle;
        }
        return -1;
    }
};
```

## 2 
27. 移除元素

