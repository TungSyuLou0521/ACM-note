## G-做题
有 nn 个题目，mm 分钟，做完每个题目所花费的时间是不一样的，求牛可乐最多可以做出多少个题目。

### 输入：
第一行是空格分隔的两个整数 n,mn,m，表示有 nn 个题目和 mm 分钟。

第二行有 nn 个非负整数 a1,a2,a3,...,ana1,a2,a3,...,an，表示牛可乐 做出第 ii 个题目所需要的时间

### 输出：
输出一行一个整数表示牛可乐能做出的最多的题目数量

### 样例
#### 样例输入
5 2
2 3 0 1 1

#### 样例输出
3

#### 注
1≤n≤5e5,1≤m≤5e10
0≤ai≤1e5
建议使用 scanf 读入


### 题解
先从小到大排序，然后从前往后减，直到m<=0。

### 代码
```cpp
#include<bits/stdc++.h>
using namespace std;
long long n,m,a[500010],sum,i;
int main(){
    cin>>n>>m;
    for(i=1;i<=n;i++){
        cin>>a[i];
    }
    sort(a+1,a+n+1);
    for(i=1;i<=n;i++){
        if(a[i]<=m) m-=a[i];
        else{
            cout<<i-1<<"\n";
            return 0;
        }
    }
}
```

## B-组队
你的团队中有 nn 个人，每个人有一个能力值ai，现在需要选择若干个人组成一个团队去参加比赛，由于比赛的规则限制，一个团队里面任意两个人能力的差值必须要小于等于 k，为了让更多的人有参加比赛的机会，你最多能选择多少个人参加比赛？

### 输入
第一行一个整数 TT，表示案例组数。
每个案例有两行：
第一行两个正整数 n,kn,k ，表示人的数量。
第二行n个以空格分隔的整数 ai，表示每个人的能力值。

### 输出
每个案例输出一行，表示可以参加比赛的最多人数。

### 样例
#### 输入
1
5 3
8 3 5 1 6
#### 输出
3

#### 说明
选择能力值为3,5,6 或者5,6,8
#### 注
T≤10
1≤n≤2e5,1≤k≤1e9
1 ≤i≤1e9

### 题解
sort deque
排个序，从小到大将元素放入双端队列队尾，若头尾差大于kk，则去掉队头，记录最大的队伍元素个数即可。

### 代码
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef pair<int,int>P;
const double eps = 1e-8;
const int NINF = 0xc0c0c0c0;
const int INF  = 0x3f3f3f3f;
const ll  mod  = 1e9 + 7;
const ll  maxn = 1e6 + 5;
const int N = 2e5 + 5;
 
ll n,k,a[N];
 
void solve(){
    cin>>n>>k;
    for(int i=1;i<=n;i++){
        cin>>a[i];
    }
    sort(a+1,a+1+n);
    deque<int>q;
    ll ans=0;
    for(int i=1;i<=n;i++){
        q.push_back(a[i]);
        while(q.back()-q.front()>k) q.pop_front();
        ans=max(ans,(ll)(q.size()));
    }
    cout<<ans<<'\n';
}
 
int main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    int T;cin>>T;
    while(T--){
        solve();
    }
    return 0;
}
```