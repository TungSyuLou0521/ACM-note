## 相反数
为了得到一个数的"相反数",我们将这个数的数字顺序颠倒,然后再加上原先的数得到"相反数"。例如,为了得到1325的"相反数",首先我们将该数的数字顺序颠倒,我们得到5231,之后再加上原先的数,我们得到5231+1325=6556.如果颠倒之后的数字有前缀零,前缀零将会被忽略。例如n = 100, 颠倒之后是1.

#### 输入
输入包括一个整数n,(1 ≤ n ≤ 10^5)
#### 输出
输出一个整数,表示n的相反数

#### 样例
##### 输入
1325
##### 输出
6556

### 自己写的
```cpp
#include<stdio.h>
#include<math.h>
void fun(int n,int t)
{
    int a,b,c,d,e,f;
    a=n/100000;
    b=n/10000%10;
    c=n/1000%10;
    d=n/100%10;
    e=n/10%10;
    f=n%10;
    int ans;
    if(t==1)
    {
        ans=f+n;
        printf("%d\n",ans);
    }
    else if(t==2)
    {
        ans=f*10+e+n;
        printf("%d\n",ans);
    }
    else if(t==3)
    {
        ans=f*100+e*10+d+n;
        printf("%d\n",ans);
    }
    else if (t==4)
    {
        ans=f*1000+e*100+d*10+c+n;
        printf("%d\n",ans);
    }
    else if (t==5)
    {
        ans=f*10000+e*1000+d*100+c*10+b+n;
        printf("%d\n",ans);
    }
    else if(t==6)
    {
        ans=f*100000+e*10000+d*1000+c*100+b*10+a+n;
        printf("%d\n",ans);
    }
}
int main()
{
    int num;
    int t=0;
    scanf("%d",&num);
    int sum=num;
    while(sum>0)
    {
        t++;
        sum/=10;
    }
    fun(num,t);
    return 0;
}
```


### 题解
```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=9;
int sav[N],e;
int main(){
    int n,x;
    scanf("%d",&n);
    x=n;
    while(n){
        sav[++e]=n%10,n/=10;
    }
    int y=0;
    for(int i=1;i<=e;++i){
        y=y*10+sav[i];
    }
    cout<<x+y;
    return 0;
}
```
## 完全平方数
多次查询[l,r]范围内的完全平方数个数
定义整数x为完全平方数当且仅当可以找到整数y使得y*y=x

#### 输入
第一行一个数n表示查询次数
之后n行每行两个数l,r

#### 输出
对于每个查询，输出一个数表示答案

#### 样例
##### 输入
5
1 3
1 4
2 4
4 4
1 1000000000
##### 输出
1
2
1
1
31622

> n <= 100000
> 0<= l <= r <= 1000000000

### 题解

```cpp
#include <math.h>
#include <stdio.h>
#include <iostream>
using namespace std;
int main()
{
    int n;
    scanf("%d" , &n);
    while (n--)
    {
        int l , r;
        scanf("%d%d" , &l , &r);
        if (l != 0)
            printf("%d\n" , (int)sqrt(r) - (int)sqrt(l - 1));
        else
            printf("%d\n" , (int)sqrt(r) + 1);
    }
}
```