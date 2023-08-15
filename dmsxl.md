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
                else return middle;//如果目标值存在返回下标
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
                nums[slow] = nums[fast];//将nums[fast]的值赋给nums[slow]。换句话说，它将nums[fast]的值复制到nums[slow]的位置上。这意味着nums[slow]的值将被更新为nums[fast]的值。
//nums[fast] = nums[slow]将nums[slow]的值赋给nums[fast]。
//将nums[slow]的值复制到nums[fast]的位置上。这意味着nums[fast]的值将被更新为nums[slow]的值。
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
                for (int column = right - 1; column >= left; column--) {//使用一个for循环从右到左填充矩阵的下边界。
                    matrix[bottom][column] = num;
                    num++;
                }
                for (int row = bottom-1; row > top; row--) {//使用一个for循环从下到上填充矩阵的左边界。
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

## 6
203
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        while(head!=NULL && head->val == val){//持续移除，所以用while
           ListNode* tmp = head; //创建一个临时指针 tmp 指向 head
           //在修改链表结构之前，我们需要保存当前节点的指针，以便在删除节点后能够释放该节点的内存。
            head = head->next; //head更新为下一个节点
            delete tmp;
        }
        ListNode* cur=head;
        while(cur != NULL && cur->next!=NULL){//如果 cur 为 NULL，说明已经遍历到链表的末尾，没有更多的节点需要处理，循环结束。如果 cur->next 为 NULL，说明当前节点是链表中的最后一个节点，不需要再继续判断和删除操作，循环结束。
            if(cur->next->val == val){
                ListNode* tmp = cur->next;//如果是，创建一个临时指针 tmp 指向 cur->next，将当前节点的下一个节点的指针保存到临时指针 tmp 中
                cur->next=cur->next->next;//将 cur->next 更新为下一个节点的下一个节点
                delete tmp;//删除tmp
            }
            else{
                cur = cur->next;//cur更新为下一个节点
            }
        }
    return head;
    }
};
```
```
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummyhead = new ListNode(0);
        dummyhead->next = head;
        ListNode* cur = dummyhead; 
        while(cur->next != NULL){//使用一个 while 循环来遍历链表，直到当前节点的下一个节点 cur->next 为 NULL。遍历链表并处理每个节点，直到当前节点的下一个节点为 NULL，即遍历到链表的末尾。
            if(cur->next->val==val){//检查当前节点的下一个节点的值是否等于 val
            //如果当前节点的下一个节点的值为val，则需要删除
                ListNode* tmp = cur->next;//建一个临时指针 tmp 指向当前节点的下一个节点
                cur->next=cur->next->next;//当前节点的 next 指针更新为下一个节点的下一个节点，即跳过了要删除的节点
                delete tmp;//删除临时指针 tmp 指向的节点
            }
            else{
            ////如果当前节点的下一个节点的值不为val
                cur = cur->next;//将当前节点更新为下一个节点，继续遍历。
            }
        }
        head = dummyhead->next;
        delete dummyhead;
        return head;

    }
};
```

## 7 
707. 设计链表
```
class MyLinkedList {
public:
int size;
ListNode *head;
    MyLinkedList() {
        this->size=0;//size初始化为0
        this->head=new ListNode(0);//表示创建一个值为 0 的新节点，并将其地址赋给当前对象的 head 成员变量。
    }
    
    int get(int index) {
        if(index<0||index >=size){//通过条件判断 if (index < 0 || index >= size) 检查索引是否越界。如果索引小于 0 或者大于等于链表的大小 size，则表示索引无效，返回 -1 表示获取失败。
            return -1;
        }
        ListNode* cur = head;//创建一个指针 cur 并将其初始化为链表的头节点 head
        for(int i=0; i<=index;i++){//循环的终止条件是 i <= index，即循环执行 index + 1 次，使 cur 指向目标节点
            cur = cur->next;//从头节点开始，依次移动到指定索引位置的节点。
        }
        return cur->val;//返回目标节点的值 cur->val。
    }
    
    void addAtHead(int val) {
        addAtIndex(0, val);
    }
    
    void addAtTail(int val) {
        addAtIndex(size, val);
    }
    
    void addAtIndex(int index, int val) {
        if(index > size){
            return;
        }
        index = max(0, index);//使用 max(0, index) 将索引 index 限制在合法范围内，即最小为 0。这是为了确保索引不会小于 0，以防止插入位置为负数。
        size++;//要插入一个新节点。
        ListNode *pred = head;//创建一个指针 pred 并将其初始化为链表的头节点 head
        for(int i=0; i<index; i++){//循环执行 index 次,将 pred 指针移动到要插入位置的前一个节点
            pred = pred->next;//使 pred 指向插入位置的前一个节点
        }
        ListNode *toAdd = new ListNode(val);//创建一个新节点 toAdd，值为 val
        toAdd->next = pred->next;//将新节点的 next 指针指向 pred 的下一个节点，即插入位置原本的节点。
        pred->next = toAdd;//将 pred 的 next 指针指向新节点 toAdd，完成节点的插入操作。
    }
    
    void deleteAtIndex(int index) {
        if(index<0||index >=size){//通过条件判断 if (index < 0 || index >= size) 检查索引是否越界。如果索引小于 0 或者大于等于链表的大小 size，则表示索引无效，返回 -1 表示获取失败。
            return ;
        }
        size--;//表示要删除一个节点。
        ListNode *pred = head;//创建一个指针 pred 并将其初始化为链表的头节点 head。
        for(int i=0; i<index; i++){//循环执行 index 次,将 pred 指针移动到要删除位置的前一个节点
            pred = pred->next;//使 pred 指向删除位置的前一个节点
        }
        ListNode *p = pred->next;
        pred->next = pred->next->next;
        delete p;
    }

};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */
 ```

## 8
206
双指针
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *cur = head;//
        ListNode *pre = NULL;//让head翻转后指向null
        ListNode *tmp = NULL;
        while(cur!=NULL){
            tmp=cur->next;//在cur还没和后面分开的时候保存后面的节点
            cur->next=pre;
            pre=cur;
            cur=tmp;
        }
        return pre;
    }
};
```


## 9
24两两交换链表中的节点
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode *dummyhead = new ListNode(0);
        dummyhead->next=head;
        ListNode *cur = dummyhead;
        ListNode *tmp = NULL;
        ListNode *tmp1 = NULL;
        while(cur->next!=NULL && cur->next->next!=NULL){
            tmp = cur->next;//保存节点1
            tmp1 = cur->next->next->next;//保存节点3
            cur->next=cur->next->next;//cur指向2
            cur->next->next=tmp;//2指向1
            tmp->next=tmp1;//1指向3
            cur=cur->next->next;//cur后移两位
        }
    return dummyhead->next;
    }
};
```

## 10
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *dummyhead = new ListNode(0);
        dummyhead->next=head;
        ListNode *fast = dummyhead;
        ListNode *slow = dummyhead;
        n++;
        while(n-- && fast !=NULL){
            fast = fast->next;
        }
        while(fast!=NULL){
            fast = fast->next;
            slow=slow->next;
        }
        slow->next=slow->next->next;
        return dummyhead->next;
    }
};
```
在这个解决方案中，我们将n的值增加1。这是因为我们需要在fast指针和slow指针之间保持n个节点的间隔。
假设链表中有k个节点，我们要删除倒数第n个节点。如果我们不将n增加1，那么fast指针将比slow指针多移动n-1个位置，而不是n个位置。这将导致fast指针和slow指针之间的间隔只有n-1个节点，而不是n个节点。
通过将n增加1，我们确保fast指针和slow指针之间的间隔为n个节点，从而正确地找到倒数第n个节点。这样，当fast指针到达链表末尾时，slow指针将指向倒数第n+1个节点，我们可以轻松删除倒数第n个节点。

## 11
142
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while(fast != NULL && fast->next != NULL) {//条件是fast指针不为空且fast->next指针也不为空。这是为了确保在遍历过程中不会出现空指针异常。
            //在每次循环迭代中，slow指针向前移动一步，而fast指针向前移动两步
            slow = slow->next;
            fast = fast->next->next;
            // 快慢指针相遇，此时从head 和 相遇点，同时查找直至相遇
            if (slow == fast) {
                ListNode* index1 = fast;
                ListNode* index2 = head;
                while (index1 != index2) {
                    index1 = index1->next;
                    index2 = index2->next;
                }
                return index2; // 返回环的入口
            }
        }
        return NULL;
    }
};
```

## 12
242
```
class Solution {
public:
    bool isAnagram(string s, string t) {
        int record[26] = {0};//代码定义了一个长度为26的整型数组record，并将数组中的所有元素初始化为0。这个数组被用作哈希表，用于记录每个字母在字符串s中出现的次数。
        for(int i=0; i<s.size(); i++){
            record[s[i] - 'a']++; //字母到下标为0做了一个映射
        }
        for(int i=0; i<t.size(); i++){
            record[t[i] - 'a']--;
        }
        for(int i=0; i<26; i++){
            if(record[i]!=0){
                return false;
            }
        }
        return true;
    }
};
```


## 13
349
```
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result_set;
        unordered_set<int> nums_set(nums1.begin(), nums1.end());//将nums1中的元素通过迭代器传递给nums_set，以初始化nums_set。
        for (int num : nums2) {//对于nums2里的每一个元素来说，遍历nums2
            //通过nums_set.find(num)查找nums_set中是否存在与当前num相等的元素。
            // 发现nums2的元素 在nums_set里又出现过
            if (nums_set.find(num) != nums_set.end()) {
                result_set.insert(num);
            }
        }
        return vector<int>(result_set.begin(), result_set.end());//将result_set转换为向量，并返回该向量作为函数的结果
    }
};
```

```
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result_set; // 存放结果，之所以用set是为了给结果集去重
        int hash[1005] = {0}; // 默认数值为0
        for (int i=0; i<nums1.size(); i++) { // nums1中出现的字母在hash数组中做记录
            hash[nums1[i]] = 1;
        }
        for (int i=0; i<nums2.size(); i++) { // nums2中出现话，result记录
            if (hash[nums2[i]] == 1) {
                result_set.insert(nums2[i]);
            }
        }
        return vector<int>(result_set.begin(), result_set.end());
    }
};
```

```
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result_set; // 存放结果，之所以用set是为了给结果集去重
        int hash[1005] = {0}; // 默认数值为0
        for (int num : nums1) { // nums1中出现的字母在hash数组中做记录
            hash[num] = 1;
        }
        for (int num : nums2) { // nums2中出现话，result记录
            if (hash[num] == 1) {
                result_set.insert(num);
            }
        }
        return vector<int>(result_set.begin(), result_set.end());
    }
};

```

## 14
1
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map <int,int> map;//定义unordered map，用来存放🏪过的元素
        for(int i = 0; i < nums.size(); i++) {// 遍历当前元素
            //在map中寻找是否有匹配的key
            int s = target - nums[i]
            auto iter = map.find(s); 
            if(iter != map.end()) {
                return {iter->second, i};//一个下标是需要的数字，一个下标是当前的数
            }
            // 如果没找到匹配对，就把访问过的元素和下标加入到map中
            map.insert(pair<int, int>(nums[i], i)); 
        }
        return {};
    }
};
```
