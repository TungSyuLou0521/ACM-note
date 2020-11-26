### sort函数
sort函数用于C++中，对给定区间所有元素进行排序，默认为升序，也可进行降序排序。
时间复杂度为n*log2n
#### 示例
sort函数没有第三个参数，实现的是从小到大（升序）排列：
```cpp
#include<iostream>
#include<algorithm>
using namespace std;
int main()
{
    int a[10]={9,6,3,8,5,2,7,4,1,0};
    for(int i=0;i<10;i++)
    cout<<a[i]<<endl;
    sort(a,a+10);//指针
    for(int i=0;i<10;i++)
    cout<<a[i]<<endl;
    return 0;
}
```
#### 示例
从大到小排序，需要加入一个比较函数compare()，此函数的实现过程如下：
```cpp
bool compare(int a,int b)
{
    return a>b;
}
```


完整

```cpp
#include<iostream>
#include<algorithm>
using namespace std;
bool compare(int a,int b)
{   
return a>b;
}
int main()
{
int a[10]={9,6,3,8,5,2,7,4,1,0};
for(int i=0;i<10;i++)
cout<<a[i]<<endl;  
sort(a,a+10,compare);//在这里就不需要对compare函数传入参数了   
for(int i=0;i<10;i++)
cout<<a[i]<<endl;
return 0;
}
```

#### 示例
假设自己定义了一个结构体node
```cpp
struct node
{
int a;
int b;
double c;
}
```
有一个node类型的数组node arr[100]，想对它进行排序：先按a值升序排列，如果a值相同，再按b值降序排列，如果b还相同，就按c降序排列。就可以写一个比较函数：
```cpp
bool cmp(node x,node y)
{
if(x.a!==y.a) return x.a<y.a;
if(x.b!==y.b) return x.b>y.b;
return x.c>y.c;
}
```
