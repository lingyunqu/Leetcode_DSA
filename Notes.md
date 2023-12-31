---
title: "leetcode"
output: html_document
date: "2023-06-25"
---

# 算法复杂度
## 时间复杂度

0. 题目： 输入长度为 N 的整数数组 nums ，判断此数组中是否有数字 7 ，若有则返回 true ，否则返回  false 。

```cpp
bool find_seven(vector<int>& nums){
  for (int num: nums){
    if (num==7)
      return true;
}
  return false;
}
```

1. 常数复杂度O(1)：运行次数与 N 大小呈常数关系，即不随输入数据大小 N 的变化而变化。
```cpp
int algorithm(int N){
  int a=1;
  int b=2;
  int x=a*b+N;
  return 1;
}
```
2. 线性复杂度O(N):循环运行次数与 N 大小呈线性关系，时间复杂度为 O(N) 。
```cpp
int algorithm(int N){
  int count=0;
  for(int i=0; i<N; i++)
    count++;
  return count;
}
```
3. 平方复杂度 $O(N^2)$ :两层循环相互独立，都与 N 呈线性关系，因此总体与 N 呈平方关系，时间复杂度为 $O(N^2)$。
```cpp
int algorithm(int N){
  int count=0;
  for (int i=0; i<N; i++){
    for (int j=0; j<N; j++){
      count ++;
}
}
  return count;
}
```
4. 指数 $O(2^N)$:每轮分裂出两倍的情况 
```cpp
int algorithm(int N){
  if(N<=0) return 1;
  int count_1=algorithm(N-1);
  int count_2=algorithm(N-2);
  return count_1+count+2;
}
```

5. 阶乘O(N!):即给定 N 个互不重复的元素，求其所有可能的排列方案
```cpp
int algorithm(int N){
  if(N<=0) return 1;
  int count=0;
  for(int i=0; i<N; i++){
    count += algorithm(N-1);
}
return count;
}
```

6. 对数O(logN):每轮排除一半的情况设循环次数为 m ，则输入数据大小 N 与2^m  呈线性关系，两边同时取 log 2 对数，则得到循环次数m与log2 N呈线性关系，即时间复杂度为 O(logN) 。
```cpp
int algorith(int N){
  int count=0;
  float i=N;
  while(i>1){
    i=i/2;
    count++;
}
return count;
}
```

7. 线性对数O(NlogN):
```cpp
int algorithm (int N){
int count=0;
float i=N;
while(i>1){
	i=i/2;
	for (int j=0; j<N; j++){
		count++;
		}
	return count;
	}	
}
```

# 数据结构
## 1. 请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

示例 1：
```
输入：s = "We are happy."
输出："We%20are%20happy."
```
法1：双指针法
```cpp
class Solution {
public:
    string replaceSpace(string s) {
        int count=0,len=s.size();// 初始化：空格数量 count ，字符串 s 的长度 len
	// 统计空格数量
        for(char c:s){
            if (c==' ') count++;//遍历 s ，遇空格(==)则 count++
        }
	// 修改 s 长度:由于需要将空格替换为 "%20" ，字符串的总字符数增加，因此需要扩展原字符串 s 的长度，添加完 "%20" 后的字符串长度应为 len + 2 * count
        s.resize(len+2*count);//将s的长度改为len+2*count
	// 倒序遍历修改
        for(int i=len-1,j=s.size()-1;i<j;i--,j--){//倒序遍历修改：i 指向原字符串尾部元素， j 指向新字符串尾部元素；当 i = j 时跳出（代表左方已没有空格，无需继续遍历）
            if (s[i]!=' ')//当 s[i] 不为空格时：执行 s[j] = s[i] 
                s[j]=s[i];
            else{//当 s[i] 为空格时：将字符串闭区间 [j-2, j] 的元素修改为 "%20" 
                s[j-2]='%';
                s[j-1]='2';
                s[j]='0';
                j-=2;//由于修改了 3 个元素，因此需要 j -= 2
            }
        }
    return s;
    }
};
```

法2：辅助字符串法
```cpp
class Solution {
public:
    string replaceSpace(string s) {
        string temp;//创建一个辅助字符串
        for(int i=0;i<s.length();i++){//对原字符串依次判断。
            if (s[i]!=' ') temp+=s[i];//不是空格，保留
            if (s[i]==' ') temp+="%20";//是空格就替换（注意==）
        }
        return temp;
    }
};
```
## 2. 输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。
示例 1：
```
输入：head = [1,3,2]
输出：[2,3,1]
```
法1. 回溯
```cpp
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        recur(head);
        return res;
    }
private:
    vector<int> res;
    void recur(ListNode* head) {
        if(head == nullptr) return;\\终止条件： 当 head == None 时，代表越过了链表尾节点，则返回空列表
        recur(head->next);\\递推工作： 访问下一节点 head.next
        res.push_back(head->val);\\将当前节点值 head.val 加入列表 tmp
    }
}
```
法2. reverse函数
reverse函数用于反转[first, last) 范围内的元素，没有返回值
```cpp
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> s;
        while(head != NULL)
        {
            s.push_back(head->val);
            head = head->next;
        }
        reverse(s.begin() , s.end()); //最后进行反转
        return s;
    }
};
```
法3. 辅助栈
链表只能 从前至后 访问每个节点，而题目要求 倒序输出 各节点值，这种 先入后出 的需求可以借助 栈 来实现。
```cpp
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        stack<int> stk;
        while(head != nullptr) {
            stk.push(head->val);//入栈： 遍历链表，将各节点值 push 入栈。
            head = head->next;
        }
        vector<int> res;
        while(!stk.empty()) {
            res.push_back(stk.top());//出栈：将各结点值存储于数组
            stk.pop();//出栈： 将各节点值 pop 出栈，并返回
        }
        return res;
    }
};
```

## 3. 用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )
示例 1：
```
输入：
["CQueue","appendTail","deleteHead","deleteHead","deleteHead"]
[[],[3],[],[],[]]
输出：[null,null,3,-1,-1]
```
示例 2：
```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```
列表倒序操作可使用双栈实现：设有含三个元素的栈 A = [1,2,3] 和空栈 B = [] 。若循环执行 A 元素出栈并添加入栈 B ，直到栈 A 为空，则 A = [] , B = [3,2,1] ，即栈 B 元素为栈 A 元素倒序。
利用栈 B 删除队首元素：倒序后，B 执行出栈则相当于删除了 A 的栈底元素，即对应队首元素。
题目要求实现 加入队尾appendTail() 和 删除队首deleteHead() 两个函数的正常工作。因此，可以设计栈 A 用于加入队尾操作，栈 B 用于将元素倒序，从而实现删除队首元素。

push_back()：将一个新的元素加到vector的最后（当前最后一个元素的下一个元素）
stack::push():在栈顶增加一个元素
queue::push():在队列末端增加一个元素


```cpp
class CQueue {
public:
	stack<int> A, B;
    CQueue() {}
    
    void appendTail(int value) {
	A.push(value);
    }
    
    int deleteHead() {
	if(!B.empty()){//删除的时候先检查B是不是空(栈 B 元素为栈 A 元素倒序，B执行出栈则相当于删除了A的栈底元素)，不是空的直接删除。 
		int tmp = B.top();
		B.pop();
		return tmp;
    }
	if (A.empty()) return -1;//.如果 st2 是空的，检查 st1，如果 st1 也是空的，说明没有可以删除的元素， 返回 -1。
	while (!A.empty()){//如果 st1 不是空的
		int tmp=A.top();//把 st1 里面元素全部倒过去
		A.pop();
		B.push(tmp);
	}
	int tmp=B.top();
	B.pop();//再删除 st2 栈顶元素
	return tmp;
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```



## 3. 请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。

数值（按顺序）可以分成以下几个部分：
若干空格
一个 小数 或者 整数
（可选）一个 'e' 或 'E' ，后面跟着一个 整数
若干空格

小数（按顺序）可以分成以下几个部分：
（可选）一个符号字符（'+' 或 '-'）
下述格式之一：
至少一位数字，后面跟着一个点 '.'
至少一位数字，后面跟着一个点 '.' ，后面再跟着至少一位数字
一个点 '.' ，后面跟着至少一位数字

整数（按顺序）可以分成以下几个部分：
（可选）一个符号字符（'+' 或 '-'）
至少一位数字

部分数值列举如下：
["+100", "5e2", "-123", "3.1416", "-1E-16", "0123"]
部分非数值列举如下：
["12e", "1a3.14", "1.2.3", "+-5", "12e+5.4"]

‘.’出现正确情况：只出现一次，且在e的前面
‘e’出现正确情况：只出现一次，且出现前有数字
‘+’‘-’出现正确情况：只能在开头和e后一位
```cpp
class Solution {
public:
    bool isNumber(string s) {
    	//去掉首位空格
	int i=0;
 	while(i<s.size() && s[i]==' ')//从头开始，如果有空格
 		i++;//计数+1
   	s=s.substr(i);//substr:返回一个新建的初始化为string对象的子串的拷贝string对象，字串是在字符位置pos开始，跨越len个字符对象的部分
    	while (s.back()==' ')//从末端开始，如果是空格
     		s.pop_back();//则删除空格

       bool numFlag=false;
       bool dotFlag=false;
       bool eFlag=false;
       for (int i=0; i<s.size(); i++){//从头开始数
		if (isdigit(s[i])){
			numFlag=true;
   		}
     		else if (s[i]=='.' && !dotFlag && !eFlag){//没出现过.且没出现过e
			dotFlag=true;
   		}
     		else if ((s[i]=='e'||s[i]=='E')&&!eFlag&&numFlag){//字符为e或E，之前没出现过E或e，之前出现过数字
       			eFlag=true;
	  		numFlag=false;//e后面必须跟着一个整数，所以出现e之后标为false，判断是否为整数
     		}
       		else if ((s[i]=='+'||s[i]=='-')&&(i==0||s[i-1]=='e'||s[i-1]=='E')){// 判定为'+''-'符号，只能出现在第一位或者紧接'e'后面
	 	}
   		else {
     			return false;
			}
   	}
    return numFlag;
    }
};
```

## 反转链表
定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

 
```
示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```
法1. 迭代（双指针）:考虑遍历链表，并在访问各节点时修改 next 引用指向
```cpp
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
    ListNode* reverseList(ListNode* head) {
	ListNode *cur=head, *pre=nullptr;//cur指针指向链表的头节点，pre指针指向null
	while (cur!=nullptr){//终止条件：cur指针指到链表尾的null
		ListNode *tmp = cur->next; //暂存后继节点cur
		cur->next=pre; //修改next引用指向pre
		pre=cur;//pre暂存cur
		cur=tmp;//cur访问下一节点tmp
    	}
	    return pre;
    }
};
```

法2. 递归
考虑使用递归法遍历链表，当越过尾节点后终止递归，在回溯时修改各节点的 next 引用指向。
recur(cur, pre) 递归函数：
终止条件：当 cur 为空，则返回尾节点 pre （即反转链表的头节点）；
递归后继节点，记录返回值（即反转链表的头节点）为 res ；
修改当前节点 cur 引用指向前驱节点 pre ；
返回反转链表的头节点 res ；
reverseList(head) 函数：
调用并返回 recur(head, null) 。传入 null 是因为反转链表后， head 节点指向 null ；
```cpp
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
    ListNode* reverseList(ListNode* head) {
	return recur(head, nullptr);
    }
private:
ListNode* reverseList(ListNode* head, ListNode* pre) {
	if (cur==nullptr) return pre;//终止条件：cur为空，这时候意味着已经指到链表尾了，返回pre
	ListNode* res=recur(cur->next, cur);//递归后续结点
	cur->next=pre;//修改结点引用指向
	return res;//返回反转列表的头结点
};
```

## 定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

```
示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```
建立一个辅助栈，储存栈 A 中所有 非严格降序 元素的子序列，则栈 A 中的最小元素始终对应栈 B 的栈顶元素。此时， min() 函数只需返回栈 B 的栈顶元素即可。

```cpp
class MinStack {
public:
    stack <int> A,B;
    MinStack() {}
    
    void push(int x) {//重点为保持栈 B 的元素是 非严格降序 的；
	A.push(x);//执行「元素 x 压入栈 A」 ；
	if(B.empty()|| B.top()>=x)//若「栈 B 为空」或「x ≤栈 B 的栈顶元素」
		B.push(x);//则执行「元素 x 压入栈 B」 ；
    }
    
    void pop() {//重点为保持栈 A , B 的 元素一致性 ；
	if(A.top()==B.top())//执行「栈 A 元素出栈」，将出栈元素记为 y ；若 「y 等于栈 B 的栈顶元素」，则执行「栈 B 元素出栈」；
		B.pop();
	A.pop();
    }
    
    int top() {// 直接返回栈 A 的栈顶元素，即返回 A.peek() ；
	return A.top();
    }
    
    int min() {//直接返回栈 B 的栈顶元素，即返回 B.peek() ；
        return B.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->min();
 */
 ```

 ## 请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

法一：哈希表
利用哈希表的查询特点，考虑构建 原链表节点 和 新链表对应节点 的键值对映射关系，再遍历构建新链表各节点的 next 和 random 引用指向即可。
算法流程：
1.若头节点 head 为空节点，直接返回 null ；
2.初始化： 哈希表 dic ， 节点 cur 指向头节点；
3.复制链表：
	1)建立新节点，并向 dic 添加键值对 (原 cur 节点, 新 cur 节点） ；
	2)cur 遍历至原链表下一节点；
4.构建新链表的引用指向：
	1)构建新节点的 next 和 random 引用指向；
	2)cur 遍历至原链表下一节点；
5.返回值： 新链表的头节点 dic[cur] ；
```cpp

/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if(head == nullptr) return nullptr;
        Node* cur = head;
        unordered_map<Node*, Node*> map;
        // 3. 复制各节点，并建立 “原节点 -> 新节点” 的 Map 映射
        while(cur != nullptr) {
            map[cur] = new Node(cur->val);
            cur = cur->next;
        }
        cur = head;
        // 4. 构建新链表的 next 和 random 指向
        while(cur != nullptr) {
            map[cur]->next = map[cur->next];
            map[cur]->random = map[cur->random];
            cur = cur->next;
        }
        // 5. 返回新链表的头节点
        return map[head];
    }
};
```

法二：拼接 + 拆分
算法流程：
1. 复制各节点，构建拼接链表:
	设原链表为 node1→node2→⋯ 
2. 构建新链表各节点的 random 指向： node1→node1_new→node2→node2_new→⋯
	当访问原节点 cur 的随机指向节点 cur.random 时，对应新节点 cur.next 的随机指向节点为 cur.random.next 。
3. 拆分原 / 新链表：
	设置 pre / cur 分别指向原 / 新链表头节点，遍历执行 pre.next = pre.next.next 和 cur.next = cur.next.next 将两链表拆分开。
4. 返回新链表的头节点 res 即可。
```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if(head==nullptr) return nullptr;
	Node* cur=head;
	//1. 复制各结点，构建拼接链表
	while (cur!=nullptr){
 		Node* tmp = new Node(cur->val);
		tmp->next=cur->next;
		cur->next=tmp;
		cur=tmp->next;
    }
	//2.构建各新节点的random指向
	cur=head;
	    while(cur!=nullptr){
		    if(cur->random!=nullptr)
			    cur->next->random=cur->random->next;
		    cur=cur->next->next;
	    }
	//拆分链表
 	cur=head->next;
	Node* pre=head, *res=head->next;
	while (cur->next != nullptr){
		pre->next=pre->next->next;
		cur->next=cur->next->next;
		pre=pre->next;
		cur=cur->next;
	}
	    pre->next=nullptr;
	    return res;
    }
};
```

## 字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。
获取字符串 s[n:] 切片和 s[:n] 切片，使用 "+" 运算符拼接并返回即可。
```cpp
class Solution {
public:
    string reverseLeftWords(string s, int n) {
	return s.substr(n, s.size())+s.substr(0,n)
    }
};
```

## 给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。
窗口对应的数据结构为 双端队列 ，本题使用 单调队列 即可解决以上问题。遍历数组时，每轮保证单调队列 deque ：
deque 内 仅包含窗口内的元素 ⇒ 每轮窗口滑动移除了元素 nums[i−1] ，需将 deque 内的对应元素一起删除。
deque 内的元素 非严格递减 ⇒ 每轮窗口滑动添加了元素 nums[j+1] ，需将deque 内所有 <nums[j+1] 的元素删除。
```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
	vector<int> res:
	if(num.size()==0||k==0) return res;
	deque<int> d;
	for (int j=0, i=1-k; j<nums.size(); i++,j++){
		
	}	
    }
};
```

# 算法
## 
```cpp
class Solution{
public:
	int findRepeatNumber (vector <int> &nums){
		unordered_map<int, bool> map;
		for(int num:nums){
			if(map[num]) return num;
			map[num]=true;
		}
		return -1;
	}
};
```

##  在排序数组中查找数字 I
```cpp
class Solution{
public:
	int search(vector<int> &nums,int target){
		//搜索右边界right
		int i=0, j=nums.size()-1;
		while(i<=j){
			int m=(i+j)/2;
			if (nums[m]<=target) i=m+1;
			else j=m-1;
		}
		int right=i;
		//数组中无target
		if(j>=0 && nums[j]!=target) return 0;
		//搜索左边界left
		i=0, j=nums.size()-1;
		while(i<=j){
			int m=(i+j)/2;
			if (nums[m]<=target) i=m+1;
			else j=m-1;
		}
		int left=j;
		return right-left-1;
	}
}
```

```cpp
class Solution{
public:
	int search(vector<int>&nums, int target){
		return helper(nums, target) - helper(nums, target-1);
	}
private:
	int helper(vector<int>&nums, int tar){
		int i=0,j=num.size()-1;
		while(i<=j){
			int m=(i+j)/2;
			if(nums[m]<=tar) i=m+1;
			else j=m-1;
		}
		return i;
	}
}
```
## 一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。


```cpp
class Solution{
	public int missingNumber (int[] nums){
	for(int i=0;i<nums;i++){
		if (nums[i]!=i){return i;}
	}
		return nums.length;
}
}
```


```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        
        int i = 0, j = nums.size() - 1;
        if(nums.size()==0)  return 0;//如果输入为空返回0，避免出现bug

        while(i <= j) {// 搜索左边界 left
            int m = (i + j) / 2;
            if(nums[m] < target) i = m + 1;/*当m位置数字小于target时，移动i到m+1位置；
            //当m位置数字大于等于target时，将j移动到m-1位置。 
            如此，最后可找到的是位置j，j是所有小于target的数字中最靠右的*/
            else j = m - 1;
        }
        int left = j;
        // 若数组中无 target ，则提前返回
        if(i>=nums.size()) return 0;//做完循环后i==j+1,如果i位于nums.size()或更多，说明i超出范围
        if(i>=nums.size()-1 && nums[i] != target) return 0;//如果i不为target，说明此时没有target   
        // 搜索右边界 right
        i = 0; j = nums.size() - 1;
        while(i <= j) {
            int m = (i + j) / 2;
            if(nums[m] <= target) i = m + 1;/*当m位置数字小于等于target时，移动i到m+1位置；
            //当m位置数字大于target时，将j移动到m-1位置。 
            如此，最后可找到的是位置i，i是所有大于target的数字中最靠左的*/
            else j = m - 1;
        }
        int right = i;
        return right - left - 1;
    }
};
```

从上到下打印二叉树

```cpp
class Solution {
public:
    vector<int> levelOrder(TreeNode* root) {
        vector<int> res;//捏了一个res，这个是新做出来的准备打印的结点，创建一个空的向量 res，用于存储最终的层序遍历结果。
        queue<TreeNode*> que;//捏了一个que，这是一个队列，用来存储你还没有遍历过的结点，
        if (!root) return res;//根判空返回，如果根节点 root 为空，表示二叉树为空树，直接返回空的结果向量 res。
        que.push(root);//队列先进根，队列中初始只有根节点 root。
        while (!que.empty()) {//进入一个循环，只要队列 que 不为空，就一直进行遍历操作。
            TreeNode* node = que.front();//循环取队头：在每次循环迭代中，通过 que.front() 获取队列头部的节点，并将其赋值给指针变量 node。，然后把这个头从队里踢走，
            que.pop();//然后从que队列中拿出第一个结点，使用 que.pop() 将已经访问过的队列头部节点移出队列。
            res.push_back(node->val);//看值进左右：把这个头的数值给res，将当前节点 node 的值 node->val 添加到结果向量 res 中，以记录遍历顺序。，左右子节点存在的话塞进que中
            if (node->left) que.push(node->left);//如果结点有左右子叶，将结点的左右子叶放入队列末尾，如果当前节点 node 存在左子节点，将左子节点加入队列 que 中。
            if (node->right) que.push(node->right);//如果当前节点 node 存在右子节点，将右子节点加入队列 que 中。
        }
        return res;
    }
};
/*遍历完成后可以保证你的res队列中是所有结点从上到下从左到右的
（因为每一个结点都会放入que，如果它有左右结点也会进入que，而他们进入que的顺序是符合题目要求的）
找过左右结点的则放入res，这样保证不重不漏 */
```


```cpp

int fibonacci(int n, vector<int> dp) {//将dp传递给fibonacci
    if (n == 0) return 0;           // 返回 f(0)
    if (n == 1) return 1;           // 返回 f(1)
    if (dp[n] != 0) return dp[n];   // 若 f(n) 以前已经计算过，则直接返回记录的解dp[n]=f（n-1）+f（n-2）
    dp[n] = fibonacci(n - 1, dp) + fibonacci(n - 2, dp); // 如果f（n）以前没有计算过，则将f（n）计算然后记录到对应的dp（n）中
    return dp[n];
}

// 求第 n 个斐波那契数
int fibonacciMemorized(int n) {
    vector<int> dp(n + 1, 0); // 意思是一个动态数组，叫做dp，一共有n+1个数据，每个数据都是0，用于保存 f(0) 至 f(n) 问题的解
    return fibonacci(n, dp);
}


```

20230706
剑指 Offer 42. 连续子数组的最大和
输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

 

示例1:

输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
 
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {\\是函数的声明，接收一个整数向量 nums 作为参数，并返回一个整数值。
        int res = nums[0];\\定义并初始化变量 res，用于存储当前的最大子序和，默认为第一个元素
        for(int i = 1; i < nums.size(); i++) {\\开始遍历数组 nums，从第二个元素开始（索引为 1）
            if(nums[i - 1] > 0) nums[i] += nums[i - 1];\\判断前一个元素是否大于 0，如果是，则将当前元素与前一个元素相加，更新当前元素的值。这一步的目的是，如果前一个元素对当前元素的和是正值，则可以将前一个元素的值累加到当前元素上，以得到更大的子序和。
            if(nums[i] > res) res = nums[i];\\判断当前元素是否大于 res，如果是，则更新 res 的值为当前元素。这一步的目的是，如果当前元素本身比之前累加的和更大，则更新 res 为当前元素。
        }
        return res;  
    }
};
```







剑指 Offer 47. 礼物的最大价值
在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

```cpp
class Solution {
public:
    int maxValue(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();\\获取数组的行数m，列数n
        for(int i = 0; i < m; i++) {\\对行迭代，从第一行开始逐行遍历到最后一行（共 m 行）。
            for(int j = 0; j < n; j++) {\\对列迭代，在每一行中从第一列开始逐列遍历到最后一列（共 n 列）。
                if(i == 0 && j == 0) continue;
                if(i == 0) grid[i][j] += grid[i][j - 1] ;
                else if(j == 0) grid[i][j] += grid[i - 1][j];
                else grid[i][j] += max(grid[i][j - 1], grid[i - 1][j]);
            }
        }
        return grid[m - 1][n - 1];
    }
};
```

