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
