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
左闭右开：不包含right
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
```
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int fast = 0; //用来寻找数组里删除目标值之后的元素
        int slow = 0; //新数组里需要更新的位置
        for(fast = 0; fast < nums.size(); fast++){//快指针的移动
            if(nums[fast]!=val){
                nums[slow] = nums[fast];
                slow++;
            }
        }
        return slow;
    }
};
```

## 3
977
```
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> result(nums.size());   //创建 result 向量时，使用 resize() 函数来分配足够的空间，以便能够存储所有的元素。
        int k=nums.size()-1;
        for(int i=0,j=nums.size()-1;i<=j;){//定义两个指针 i 和 j，分别指向 nums 的开头和结尾，循环条件是 i <= j
            if(nums[i]*nums[i]>nums[j]*nums[j]){//如果 nums[i]*nums[i] 大于 nums[j]*nums[j]，说明 nums[i] 的平方更大
                result[k]=nums[i]*nums[i];//将nums[i]的平方存储在 result 的末尾位置 k
                k--;//指针 k 向前移动一位。
                i++;//指针 i 向后移动一位
            }
            else{//如果 nums[i]*nums[i] 不大于 nums[j]*nums[j]，说明 nums[j] 的平方更大
                result[k] = nums[j]*nums[j];//将nums[j]的平方存储在 result 的末尾位置 k
                k--;//指针 k 向前移动一位。
                j--;//指针 j 向前移动一位
            }
        }
        return result;
    }
};
```
