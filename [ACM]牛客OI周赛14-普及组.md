## B题

#### 题目描述
牛能有n个数字分别为a1、a2、a3....an，他认为一个数字是好的，当且仅当他可以表示为自己每一位上的数的k次方和，例如153=1^3+5^3+3^3=1，此时k=3，其中k是个自然数，现在牛能请你帮他算出，这n个数字中，有几个数字是好的？

#### 输入描述:
> 第一行，一个数n
> 接下来n行，每行一个数，第i行的数代表ai

#### 输出描述:
> 一行，一个数，代表好的数字的个数

#### 示例1

> 输入
> 3
> 1
> 2
> 153

> 输出
> 3

#### 备注:
> 对于30%的数据，1<=n<=100,1<=ai<=100;
> 对于100%的数据，1<=n<=100,1<=ai<=1e6;

#### 题解

#### 1
```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=1e5+7;
int q_pow(int a,int x)
{
    int res=1;
    while(x){
        if(x&1) res=res*a;
        a=a*a;
        x>>=1;
    }
    return res;
}
int main()
{
    int n; scanf("%d",&n);
    int res=0;
    for(int i=1;i<=n;i++){
        int a; scanf("%d",&a);
        int tmp=a,sum=0,k=0;
        while(tmp){
            tmp/=10;
            k++;
        }
        tmp=a;
        while(tmp){
            sum+=q_pow(tmp%10,k);
            tmp/=10;
        }
        if(sum==a) res++;
    }
    cout<<res<<endl;
}
```
 #### 2
```cpp
#include<bits/stdc++.h>
using namespace std;
inline int read(){
    int x=0,f=1;
    char ch=getchar();
    while(ch<'0'||ch>'9'){
        ch=getchar();
    }
    while(ch>='0'&&ch<='9'){
        x=(x<<1)+(x<<3)+(ch^48);
        ch=getchar();
    }
    return x*f;
}
int quickPower(int a, int b)//求a的b次方 结果对mod取模
{
    int ans = 1, base = a;//ans为答案，base为a^(2^n)
    while(b > 0)//b是一个变化的二进制数，如果还没有用完
    {
        if(b & 1)//&是位运算，b&1表示b在二进制下最后一位是不是1，如果是：
            ans = ans*base; //把ans乘上对应的a^(2^n)
  
        base = base*base ;//base自乘，由a^(2^n)变成a^(2^(n+1))
        b >>= 1;//位运算，b右移一位，如101变成10（把最右边的1移掉了），10010变成1001。现在b在二进制下最后一位是刚刚的倒数第二位。结合上面b & 1食用更佳
    }
    return ans;
}
int ans=0;
int main()
{
    int n;
    n=read();
    while(n--){
        int x,y;
        y=read();
        int sum=0;
        for(int k=0;k<=30;++k){
            sum=0;
            x=y;
            while(x){
                sum+=pow(x%10,k);
                x/=10;
            }
            if(sum==y){
                ans++;
                break;
            }
            if(sum>y){
                break;
            }
        }
    }
    printf("%d",ans);
}
```
#### 3

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=256;
int a[N];
void solve()
{
    int n,data,count=0;
    cin>>n;
    while(n--)
    {
        cin>>data;
        int a=data,b=data,k=0;
        while(a)
        {
            k++;
            a=a/10;
        }
        int sum=0;
        while(b)
        {
            sum+=pow(b%10,k);
            b=b/10;
        }
        if(sum==data) count++;
    }
    cout<<count;
}
int main()
{
    solve();
    return 0;
}
```

## D题

#### 题目描述：
众所周知，牛可乐 的口胡能力十分强大
牛可乐 要讲 n 件事情，我们把这些事情从 1~n 标号。
牛可乐每讲一件事需要耗费一个单位的时间，但是 牛可乐讲事情和普通人不同：牛可乐在 **讲完** 第 i 件事时，只有Pi的概率继续讲下一件事（第i+1件），也就是说，牛可乐讲完第i件事后有（1-Pi）的概率从第 i-1 件事开始讲！
当 牛可乐讲完第 n 件事，**并且决定讲下一件事时**，牛可乐才算是把这 n 件事讲完了。
牛妹是个不耐烦的女孩子，她想问问你 牛可乐期望要讲多久才能把 n 件事情全部讲完。

#### 输入描述：

> 第一行一个整数 n
> 第二行 n 个浮点数，代表Pi，保证P1=1

#### 输出描述：

> 一行一个浮点数，表示 牛可乐期望要多久才能把全部事情讲完（保留到小数点后 3 位）

#### 示例：

> 输入
> 4
> 1 0.6 0.4 0.2

> 输出
> 38.333

#### 备注:

对于 20% 的数据，1<=n<=20
对于 100% 的数据，1<=n<=1e5

#### 题解

#### 1

```cpp
#include<bits/stdc++.h>
using namespace std;
 
double dp[100005],p[100005],ans=0;
 
int main()
{
    int n;
    scanf("%d",&n);
    for(int i=1;i<=n;++i)
    {
        scanf("%lf",&p[i]);
        dp[i]=1+(1-p[i])/p[i]*(1+dp[i-1]);
        ans+=dp[i];
    }
    printf("%.3f\n",ans);
    return 0;
}
```

#### 2

```cpp
#include <bits/stdc++.h>
using namespace std;
   
typedef long long ll;
   
const int maxn=1e5+5;
double ex[maxn];
   
int main() {
    int n;cin>>n;double p,sum=0;
    for(int i=1;i<=n;i++){
        cin>>p;
        ex[i]+=(1+(1-p)*ex[i-1])/p;
        sum+=ex[i];
    }
    printf("%.3f",sum);
    return 0;
}
```

#### 3

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1e5+10;
double p[N],dp[N];
int main()
{
    ios::sync_with_stdio(false),cin.tie(0),cout.tie(0);
    int n;
    scanf("%d",&n);
    for(int i=1;i<=n;i++){
        scanf("%lf",&p[i]);
    }
    dp[1]=0;
    for(int i=1;i<=n;i++)
    dp[i+1]=((1-dp[i-1])*(1-p[i])+dp[i]+p[i])/p[i];
    printf("%.3f\n",dp[n+1]);
    return 0;
}
```