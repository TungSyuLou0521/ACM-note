# 素数筛

## 埃氏筛

对于一个质数p，显然K*P都是合数，其中k=2，3……
        求n以内的素数，则对于小于n的每一个p将它的倍数筛去，最后剩下的都是素数

```cpp
for(int i=2; i<=n; i++)
{
    if(!vis[i])
    {
        prim[++op]=i;
        for(int j=2*i; j<=n; j++)
        {
            vis[j]=1;
        }
    }
}
for(int i=1; i<=op; i++)
{
    cout<<prim[i]<<" ";
}
```
时间复杂度O(nloglogn)

## 欧拉筛(线性筛)
每个数都只被其最小质因子筛一次
时间复杂度O(n)

```cpp
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N=1e8+1;

bool vis[N];
int prim[N],op,n;

void init()
{
    for(int i=2; i<n; i++)
    {
        if(!vis[i])
        {
            prim[++op]=i;
        }
        for(int j=1; j<=op&&i*prim[j]<N; j++)
        {
//            cout<<prim[j]<<" "<<i<<" "<<i*prim[j]<<endl;
            vis[i*prim[j]]=1;
            if(i%prim[j]==0)
            {
                break;
            }
        }
    }
}
int main()
{
    cin>>n;
    init();
    cout<<op<<endl;
}

```



# 积性函数

两个定义
**数论函数**:定义在所有正整数上的函数称为数论函数
**积性函数**:如果数论函数f对任意两个互质的数n和m,均有f(mn)=f(m)f(n),就称为积性函数。如果对任意两个正整数n和m,均有f(mn)=f(m)f(n)，就称为完全积性函数

一些常见的积性函数：
欧拉函数、莫比乌斯函数、整数n的约数个数、整数n的约数和

## 欧拉函数

```cpp
int main()
{
    int n;
    cin>>n;
    ll ans = n;
    for(int i=1;i*i<=n;i++)
    {
        if(n%i) continue;
        ans-=ans/i;
        while(n%i==0)  n/=i;
    }
    if(n>1)  ans-=ans/n;
}

```
## 欧拉筛求欧拉函数

```cpp
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N=1e8+1;

bool vis[N];
int prim[N],op,n,q,phi[N];

void init()
{
    for(int i=2;i<=n;i++)
    {
        if(!vis[i])
        {
            prim[++op]=i;
            phi[i]=i-1;
        }
        for(int j=1lj<=op&&i*prim[j]<=n;j++)
        {
            vis[prim[j]*i]=1;
            if(i%prim[j]==0)
            {
                phi[i*prim[j]]=phi[i]*prim[j];
                break;
            }
            phi[i*prim[j]]=phi[i]*phi[prim[j]];
        }
    }
}
int main()
{
    scanf("%d%d",&n,&q);
    init();
    while(q--)
    {
        int k;
        scanf("%d",&k);
        printf("%d\n",prim[k]);
    }
}

```
# 费马小定理
对于质数p,任意整数a(并且a不为p得倍数) (a^(p-1))%p=1

#### 剩余系和最小剩余系
S={3,7,5,15}; 对于p=3
剩余系为对p取模  {0,1,2,0}
最小/完全 剩余系 没有重复的元素 {0,1,2}

#### 例
a^(p-2)=1/a %p
x/y对于p取模 = x%p*(1/y % p)=x%p*(y^(p-2)%p)