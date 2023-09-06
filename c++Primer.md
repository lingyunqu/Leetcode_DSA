循环
```cpp
#include<iostream>
int main(){
    int count=0;
    int i=50;
    while (i<100){
        count +=i;
        i++;
    }
    std::cout<< count<<std::endl;
}
```

两数之和
```cpp
#include<iostream>
int main(){
  std::cout <<"enter two words" << std::endl;
  int v1, v2;
  std::cin >> v1 >> v2;
  std::cout << "The sum of" << v1 << " and " << v2 << " is " << v1+v2 << std::endl;
  return 0;
}
```

```cpp
#include <iostream> 
int main()
 {
 std::cout << "Enter two numbers:" << std::endl;
 int v1, v2;
 std::cin >> v1 >> v2; // read input
 // use smaller number as lower bound for summation
 // and larger number as upper bound
 int lower, upper;
 if (v1 <= v2) {
     lower = v1;
     upper = v2;
 } else {
     lower = v2;
     upper = v1;
 }
 int sum = 0;
 // sum values from lower up to and including upper
 for (int val = lower; val <= upper; ++val)
 sum += val; // sum = sum + val
 std::cout << "Sum of " << lower
 << " to " << upper
 << " inclusive is "
 << sum << std::endl;
 return 0;
 }
```

读入与写出Sales_item对象
```cpp
#include <iostream>
#include "Sales_item.h"

int main(){
    Sales_item book;
    std::cin >> book;
    std::cout << book << std::endl;
    return 0;
}
```

两个sales_item相加
```cpp
#include <iostream>
#include "Sales_item.h"

int main(){
    Sales_item item1, item2;
    std::cin >> item1 >> item2;
    std::cout << item1+item2 << std::endl;
    return 0;
}
```


```cpp
#include <iostream>
#include "Sales_item.h"

int main(){
    Sales_item total, trans; \\们定义了所需要的对象 total 用来计算给定的 ISBN 的交易的总数，trans 用来存储读取的交易。
    if (std::cin >> total){\\将交易读入 total 并测试是否读取成功；
        while(std::cin >> trans){\\循环遍历剩余的所有记录
            if (total.same_isbn(trans))\\测试 ISBN 是否相等
                total = total + trans;\\相等, 将这两个对象相加并将结果存储到 total 中。
            else{\\ISBN不相等
                std::cout << total << std::endl; \\输出存储在 total 中的值
                total = trans; \\trans 赋值给 total 来重置 total
            }
            std::cout << total << std::endl; \\在每次循环中，都会输出total的值，以显示与最后一个ISBN相关联的数据。
        }
    }
    else {\\如果读取失败，表示没有记录，程序进入最外层的 else 分支，输出信息警告用户没有输入。 
            std::cout << "No Data " << std::endl;
            return -1;
        }
        return 0;

}
```

计算 2 的 10 次方的替代方法： 
```cpp
#include <iostream>
int main(){
    int value=2;
    int pow=10;
    int result=1;
    for(int cnt=0; cnt!=pow; cnt++){
        result *= value;
    }
    std::cout << value << "raised to the power of " << pow <<":\t" << result << std::endl;
    return 0;
}
```
编写程序，要求用户输入两个数——底数（base）和指数（exponent），输出底数的指数次方的结果。 
```cpp
#include <iostream>
int main(){
    std::cout << "Enter two numbers:" << std::endl;
    int v1, v2;
    std::cin >> v1 >> v2; // read input
    // int value=2;
    // int pow=10;
    int result=1;
    for(int cnt=0; cnt<v2; cnt++){
        result *= v1;
    }
    std::cout << v1 << "raised to the power of " << v2 <<":\t" << result << std::endl;
    return 0;
}
```

枚举
```cpp
// point2d is 2, point2w is 3, point3d is 3, point3w is 4 
enum Points { point2d = 2, point2w,
 point3d = 3, point3w };

 Points pt3d = point3d; // ok: point3d is a Points enumerator
 Points pt2w = 3; // error: pt2w initialized with int
 pt2w = polygon; // error: polygon is not a Points enumerator
 pt2w = pt3d; // ok: both are objects of Points enum type 
```
如果使用 class 关键字来定义类，那么定义在第一个访问标号前的任何成员都隐式指定为 private；如果使用 struct 关键字，那么这些成员都是public。使用 class 还是 struct 关键字来定义类，仅仅影响默认的初始访问级别。 

定义之后要加分号！ 
```cpp
 struct Sales_item {
 // no need for public label, members are public by default
 // operations on Sales_item objects
 private:
 std::string isbn;
 unsigned units_sold;
 double revenue;
 };
```

因为头文件包含在多个源文件中，所以不应该含有变量或函数的定义。 有三个例外。头文件可以定义类、值在编译时就已知道的 const 对象和 inline 函数（第 7.6 节介绍 inline 函数）。这些实体可在多个源文件中定义，只要每个源文件中的定义是相同的。


为了避免名字冲突，预处理器变量经常用全大写字母表示。
预处理器变量有两种状态：已定义或未定义。定义预处理器变量和检测其状态所用的预处理器指示不同。#define 指示接受一个名字并定义该名字为预处理器变量。#ifndef 指示检测指定的预处理器变量是否未定义。如果预处理器变量未定义，那么跟在其后的所有指示都被处理，直到出现 #endif。
可以使用这些设施来预防多次包含同一头文件：
```cpp
 #ifndef SALESITEM_H
 #define SALESITEM_H
 // Definition of Sales_itemclass and related functions goes here
 #endif
```


```
if(st.size()=0)
//ok: empty
```

```cpp
if(st.empty())
//ok: empty
```

```cpp
string s1("hello, ");
string s2("world\n");
string3 = s1 + s2; // s3 is hello, world\n
s1 += s2; // equivalent to s1 = s1 + s2
string s5 = s1 + ", " + "world"; // ok: each + has string operand string
s6 = "hello" + ", " + s2; // error: can't add string literals
```
当进行 string 对象和字符串字面值混合连接操作时，+ 操作符的左右操作数必须至少有一个是 string 类型的

读入多个string
```cpp
#include <iostream>
#include <string>
using namespace std;
int main( )
{
    string str, ss;
    cout<<"请输入字符串：\n";
    while(cin>>str)
        ss = ss + str;
    cout<<"连接后的字符串为："<<ss<<endl;
    system("PAUSE");
    return 0;
}
```
去掉标点
```cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;
int main( )
{
    string str, ss;
    cout<<"请输入字符串：\n";
    getline(cin, str);
    for(string::size_type i=0; i!=str.size(); ++i) {
        if(!ispunct(str[i]))
            ss+=str[i];
    }
    cout<<"连接后的字符串为："<<ss<<endl;
    system("PAUSE");
    return 0;
}
```

ector 是一个类模板(class template)。使用模板可以编写一个类定义 或函数定义，而用于多个不同的数据类型。因此，我们可以定义保存 string 对 象的 vector，或保存 int 值的 vector，又或是保存自定义的类类型对象(如 Sales_items 对象)的 vector。声明从类模板产生的某种类型的对象，需要提供附加信息，信息的种类取决 于模板。以 vector 为例，必须说明 vector 保存何种对象的类型，通过将类型 放在类型放在类模板名称后面的尖括号中来指定类型:
```cpp
vector<int> ivec; // ivec holds objects of type int
vector<Sales_item> Sales_vec; // holds Sales_items
```

可以用元素个数和元素值对 vector 对象进行初始化。构造函数用元素个数 来决定 vector 对象保存元素的个数，元素值指定每个元素的初始值:
```cpp
vector<int> ivec4(10, -1); // 10 elements, each initialized to -1
vector<string>svec(10,"hi!"); //10strings,eachinitializedto "hi!"
```
读一组整数到 vector 对象，计算并输出每对相邻元素的 和。如果读入元素个数为奇数，则提示用户最后一个元素 没有求和，并输出其值。然后修改程序:头尾元素两两配 对(第一个和最后一个，第二个和倒数第二个，以此类推)， 计算每对元素的和，并输出。
```
#include <iostream>
#include <string>
#include <vector>
using namespace std;
int main()
{
	vector<int> ivec;
	int ival;
	cout << "Enter numbers(Ctrl+Z to end):" << endl;
	while(cin >> ival)
	{
		ivec.push_back(ival);
	}//用cin读入一组整数并把它们存入一个vector对象中
 
	// 计算相邻元素的和并输出
	if (ivec.size() == 0) 
	{
		cout << "No element?!" << endl;
		return -1;
	}
 
	cout << "Sum of each pair of adjacent elements in the vector:"<< endl;
 
	for (vector<int>::size_type ix = 0; ix < ivec.size()-1;ix = ix + 2) 
	{
			cout << ivec[ix] + ivec[ix+1] << "\t";
			if ( (ix+1) % 6 == 0) // 每行输出6 个和
				cout << endl;
	}
 
	if (ivec.size() % 2 != 0) // 提示最后一个元素没有求和
	{
		cout << endl
		<< "The last element is not been summed "
		<< "and its value is "
		<< ivec[ivec.size()-1] << endl;
	}
 
	return 0;
}
```

### 迭代器iterator

```cpp
vector<int>::iterator iter = ivec.begin();
vector<int>::iterator iter = ivec.end();
```
由begin返回的迭代器指向第一个元素：假设 vector不空，初始化后，iter 即指该元素为 ivec[0]。
由 end 操作返回的迭代器指向 vector 的“末端元素的下一个”。“超出 末端迭代器”(off-the-end iterator)。表明它指向了一个不存在的元素。 由 end 操作返回的迭代器并不指向 vector 中任何实际的元 素，相反，它只是起一个哨兵(sentinel)的作用，表示我们 已处理完 vector 中所有元素。
如果 vector 为空，begin 返回的迭代器与 end 返回的迭代器相同。

用迭代器编写循环：
```cpp
for(vector<int>::iterator iter = ivec.begin(); iter!=ivec.end(); iter++){
    *iter=0;
}
```
for 循环首先定义了 iter，并将它初始化为指向 ivec 的第一个元素。 for 循环的条件测试 iter 是否与 end 操作返回的迭代器不等。每次迭代 iter 都自增 1，这个 for 循环的效果是从 ivec 第一个元素开始，顺序处 理 vector 中的每一元素。最后， iter 将指向 ivec 中的最后一个元素，处理 完最后一个元素后，iter 再增加 1，就会与 end 操作的返回值相等，在这种情况下，循环终止。

编写程序来创建有 10 个元素的 vector 对象。用迭代器 把每个元素值改为当前值的 2 倍。
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> ivec;//创建了一个名为ivec的vector容器，用于存储整数。
    for(vector<int>::size_type st=0; st<10; st++){ //使用for循环向ivec容器中添加元素。循环变量st的类型是vector<int>::size_type
        ivec.push_back(st);//使用push_back函数将st添加到ivec容器中
        cout<<ivec[st]<<endl;//使用cout语句打印出ivec[st]的值。
    }
    for(vector<int>::iterator iter=ivec.begin(); iter!=ivec.end(); iter++){//使用另一个for循环遍历ivec容器中的元素。循环变量iter的类型是vector<int>::iterator，它是一个迭代器，用于访问容器中的元素。
        *iter*=2;//使用解引用操作符*iter来访问当前元素，并将其乘以2。
        cout<<*iter<<endl;//使用cout语句打印出*iter的值。
    }
}
```


### bitset
```cpp
bitset<n> b; // b有n 位，每位都 0
bitset<n> b(u); //b是unsigned
bitset<n> b(s); //b是string 对象 s 中含有的位串的副本
bitset<n> b(s, pos, n); //s 中从位置 pos 开始的&nbps;n 个位的副本。
b.any() // b 中是否存在置为 1 的二进制位?
b.none() // b 中不存在置为 1 的二进制位吗?
b.count() // b 中置为 1 的二进制位的个数
b.size() // b 中二进制位的个数
b[pos] //访问 b 中在 pos 处二进制位
b.test(pos) //b 中在 pos 处的二进制位置为 1 么?
b.set() //把 b 中所有二进制位都置为 1
b.set(pos) //把 b 中在 pos 处的二进制位置为 1
b.reset() //把 b 中所有二进制位都置为 0
b.reset(pos) //把 b 中在 pos 处的二进制位置为 0 
b.flip() //把 b 中所有二进制位逐位取反
b.flip(pos) //把 b 中在 pos 处的二进制位取反
b.to_ulong() //用 b 中同样的二进制位返回一个 unsigned long 值 
os << b //把 b 中的位集输出到 os 流
```

 考虑这样的序列 1，2，3，5，8，13，21，并初始化一个 将该序列数字所对应的位置置为 1 的 bitset<32> 对 象。然后换个方法，给定一个空的 bitset，编写一小段 程序把相应的数位设置为 1。
 ```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main()
{
    /*
    因为bitset读入位集的顺序是从右向左：最右侧是低阶位，最左是高阶位。
    00000000010000000010000100101110是满足要求的序列，
    其对应的十六进制表示是0x20212e，
    最简单的方法是：
    bitset<32> bitvec("00000000010000000010000100101110");
    或者是：
    bitset<32> bitvec(0x20212e);
    以下使用另一种方法：
    */
    bitset<32> bitvec;
    int x = 0, y = 1;
    int z = x + y;
    while (z <= 21)
    {
        bitvec.set(z);
        // 1,2,3,5,8,13,21 其实是斐波那契数列
        x = y;
        y = z;
        z = x + y;
    }
    cout << bitvec << bitvec.count() << endl;

    return 0;
}
```

## 数组
```cpp
 const unsigned array_size = 3;
int ia[array_size] = {0, 1, 2};
//等价于
int ia[] = {0, 1, 2}; // an array of dimension 3
```

把一个数组复制给另一个数组
```cpp
int main() {
uninitialized
    const size_t array_size = 7;
    int ia1[] = { 0, 1, 2, 3, 4, 5, 6 };
    int ia2[array_size]; // local array, elements
    // copy elements from ia1 into ia2
    for (size_t ix = 0; ix != array_size; ++ix)
          ia2[ix] = ia1[ix];
    return 0;
}
```

## 指针
```cpp
vector<int> *pvec; // pvec can point to a vector<int> 
int *ip1, *ip2; // ip1 and ip2 can point to an int
string  *pstring; // pstring can point to a string
double *dp; // dp can point to a double
```

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout<<"开始运行了"<<endl;
    int a = 2, b = 3, c = 4;
    int *p = &a, *q = &b;
    cout << "初始化时*p的值-----" << *p << endl;
    //改变*p指针所指对象的值
    //下面这一句，把a的值改成了3
    *p = b;
    cout << "改变*p指针所值对象的值---" << *p << endl;
    cout << "改变*p指针所指向对象的值后a的值---" << a << endl;
    //改变*p指针的值，下面这一句将*p指向a，改为了指向c
    p = &c;
    cout << "改变*p指针的值---" << *p << endl;
    system("pause");
    return 0;
}
```
开始运行了
初始化时＊p的值一——2
改变＊p指针所值对象的值——3
改变＊p指针所指向对象的值后a的值———3
改变＊p指针的值——4

  *p = b：改变了指针所指向的变量的值
  p = &c：只改变了指针的值

## 数组
初始化二维数组
```cpp
     const size_t rowSize = 3;
     const size_t colSize = 4;
     int ia [rowSize][colSize];   // 12 uninitialized elements
     // for each row
     for (size_t i = 0; i != rowSize; ++i)
         // for each column within the row
         for (size_t j = 0; j != colSize; ++j)
             // initialize to its positional index
             ia[i][j] = i * colSize + j;
```
