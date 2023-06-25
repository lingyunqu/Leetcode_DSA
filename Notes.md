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
3. 平方复杂度$O(N^2)$:两层循环相互独立，都与 N 呈线性关系，因此总体与 N 呈平方关系，时间复杂度为 $O(N^2)$。
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
            stk.push(head->val);
            head = head->next;
        }
        vector<int> res;
        while(!stk.empty()) {
            res.push_back(stk.top());
            stk.pop();
        }
        return res;
    }
};
```
