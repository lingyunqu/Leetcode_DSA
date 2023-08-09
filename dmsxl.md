代码随想录的听课及做题笔记

## 1
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
                int middle = (left + right)/2;//注意middle是一个索引值
                if (nums[middle] > target){//nums[middle]不是搜索的值，接下来的区间不能包含这个值
                //通过比较中间元素 nums[middle] 与目标值 target 的大小关系，可以确定目标值在左半部分还是右半部分。
                //不是比较middle和target！
                //当nums[middle] 大于 target，说明目标在左半部分，应该更新右边界
                    right = middle - 1;
                }
                else if(nums[middle] < target){//更新右区间的左边界
                //如果 nums[middle] 小于 target，则说明目标值在右半部分，应该更新 left 为 middle + 1
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
## 4
209
```
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        long long sum = 0 ;//声明一个名为sum的长整型变量，并将其初始化为0。这个变量用于计算滑动窗口中元素的总和
        int start=0, end=0; //声明两个整型变量start和end，并将它们都初始化为0。这两个变量用于表示滑动窗口的起始位置和结束位置。
        int n=nums.size();// 声明一个整型变量n，并将其赋值为nums向量的大小。这个变量用于表示输入向量nums的长度。
        int result = INT_MAX;//通过将result初始化为INT_MAX，代码表达了一个意图，即将result设置为一个初始值，该值在后续的计算中可以被替换为更小的值。这种做法常用于需要找到最小值的算法中，例如在搜索最短路径或最小生成树等问题时。在这些情况下，将result初始化为INT_MAX可以确保在找到更小的值之前，任何其他可能的值都会被替换掉。


        while (end<n){//使用一个循环来遍历 nums，循环条件是 end 小于 n。将滑动窗口的右边界 end 向右移动，直到子数组的和大于等于目标值 s 或者 end 达到数组的末尾。在每次移动 end 的过程中，会更新子数组的和 sum。
            sum += nums[end];//在循环内部，将 nums[end] 加到 sum 中。
            while(sum>=target){//持续向后移动更新滑动窗口，如果是if，则只判断一次
                result = min(result, end-start+1);//最终取的最小的长度
                sum -= nums[start];//更新 sum 的值，使其反映出移动 start 指针后的新的子数组的和。
                start++;//将 start 指针向右移动一位，继续寻找更短的子数组
            }
        end++;
        }
        return result == INT_MAX ? 0:result;
    }
};
```
## 5
59
```
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        int num = 1;
        vector<vector<int>> matrix(n, vector<int>(n));//创建一个二维向量matrix，大小为n x n，用于存储生成的螺旋矩阵。初始时，二维向量中的所有元素都被初始化为0。
        int left = 0, right = n - 1 //由于数组的索引是从0开始的，所以右边界的索引应该是n-1，其中n是矩阵的维度。left表示矩阵的左边界，初始值为0，而right表示矩阵的右边界，初始值为n-1。这样，初始时螺旋矩阵的宽度为n。
        int top = 0, bottom = n - 1;//top表示矩阵的上边界，初始值为0，而bottom表示矩阵的下边界，初始值为n-1。这样，初始时螺旋矩阵的高度为n。
        while (left <= right && top <= bottom) {
            for (int column = left; column <= right; column++) {//使用一个for循环从左到右填充矩阵的上边界。循环变量column从left开始，逐渐增加到right。
                matrix[top][column] = num;//将num赋值给matrix[top][column]
                num++;
            }
            for (int row = top + 1; row <= bottom; row++) {//使用一个for循环从上到下填充矩阵的右边界。
                matrix[row][right] = num;
                num++;
            }
            if (left < right && top < bottom) {// 如果left小于right且top小于bottom，说明还有内部的环需要填充。
                for (int column = right - 1; column > left; column--) {//使用一个for循环从右到左填充矩阵的下边界。
                    matrix[bottom][column] = num;
                    num++;
                }
                for (int row = bottom; row > top; row--) {//使用一个for循环从下到上填充矩阵的左边界。
                    matrix[row][left] = num;
                    num++;
                }
            }
            left++;
            right--;
            top++;
            bottom--;
        }
        return matrix;
    }
};
```
