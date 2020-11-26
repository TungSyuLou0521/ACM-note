## A  -	Jelly
Nancy喜欢吃果冻！
Nancy钻进了一nn×n×n的果冻里，她想从(1,1,1)一路上、下、左、右、前、后六个方向吃到(n,n,n)。
但果冻毕竟是有许多口味的，标记为*的口味是Nancy不愿意吃的，其余的果冻均标记为.。
Nancy不想吃坏肚子，于是她想尽可能少的吃果冻。
下面给出果冻的情况，请你帮忙计算一下她能吃多少块果冻叭！
### 输入
第一行：一个整数n。
接下来n层，每组n行，每行n列，表示果冻(i,j,k)的情况（如题目描述所述）。
数据满足：1≤n≤100，保证果冻(1,1,1)不是Nancy不愿意吃的。

### 输出
如果可以到达(n,n,n)，请输出路上吃的果冻数量，否则请输出-1。

### 样例
#### 输入
2
.*
..
*.
..

#### 输出
4

### 题解

```cpp
#include<cstdio>
#include<iostream>
#include<queue>
using namespace std;
int n,nx[6]={1,-1,0,0,0,0},ny[6]={0,0,1,-1,0,0},nz[6]={0,0,0,0,1,-1};
char c[105][105][105];
bool vis[105][105][105];
struct node{
    int x,y,z,s;
};
queue<node> q;
int main(){
    scanf("%d",&n);
    for (int i=1;i<=n;i++)
     for (int j=1;j<=n;j++)
      for (int k=1;k<=n;k++)
       cin>>c[i][j][k];
    if (c[n][n][n]=='*') return puts("-1")&0;
    q.push((node){
        1,1,1,1
    }),vis[1][1][1]=1;
    while(!q.empty()){
        node a=q.front();
        q.pop();
        for (int i=0,xx,yy,zz;i<6;i++){
            xx=a.x+nx[i],yy=a.y+ny[i],zz=a.z+nz[i];
            if (vis[xx][yy][zz] || c[xx][yy][zz]=='*' || xx<1 || yy<1 || zz<1 || xx>n || yy>n || zz>n) continue;
            q.push((node){
                xx,yy,zz,a.s+1
            }),vis[xx][yy][zz]=1;
            if (xx==n && yy==n && zz==n) return printf("%d",a.s+1)&0;
        }
    }
    puts("-1");
}
```

## B - 	「木」迷雾森林
赛时提示：保证出发点和终点都是空地

帕秋莉掌握了一种木属性魔法
这种魔法可以生成一片森林（类似于迷阵），但一次实验时，帕秋莉不小心将自己困入了森林
帕秋莉处于地图的左下角，出口在地图右上角，她只能够向上或者向右行走
现在给你森林的地图，保证可以到达出口，请问有多少种不同的方案
答案对2333取模

### 输入
第一行两个整数m , n表示森林是m行n列
接下来m行，每行n个数，描述了地图
0  -  空地
1  -  树（无法通过）
### 输出
一个整数表示答案
### 样例
#### 输入
3 3
0 1 0
0 0 0
0 0 0
#### 输出
3
### 备注
链接：https://ac.nowcoder.com/acm/contest/5338/B
来源：牛客网

对于30%的数据，n,m≤100
对于100%的数据，n,m≤3,000
数据规模较大，请使用较快的输入方式，以下为快速读入模板
```cpp
template<class T>inline void read(T &res)
{
char c;T flag=1;
while((c=getchar())<'0'||c>'9')if(c=='-')flag=-1;res=c-'0';
while((c=getchar())>='0'&&c<='9')res=res*10+c-'0';res*=flag;
}

scanf("%d",&x)  ->  read(x)
cin>>x -> read(x)

```
（调用方式：read(要读入的数)）

### 题解
动态规划
方程 c[ a ] [ b ]=c[ a-1 ] [ b ]+c[ a ] [ b-1 ];

```cpp
#include<bits/stdc++.h> 
using namespace std;
#define mid 1000000007  
typedef  long long ll;
int c[3001][3001];
int ans[3001][3001];
int   read()
{
	int X=0; bool flag=1; char ch=getchar();
	while(ch<'0'||ch>'9') {if(ch=='-') flag=0; ch=getchar();}
	while(ch>='0'&&ch<='9') {X=(X<<1)+(X<<3)+ch-'0'; ch=getchar();}
	return X;
}//md为啥这个快读要判断正负这个一步干嘛？，虽然不判断就不对。

int main(){
	int a,b,i,j;
	cin>>a>>b;
	//把他读成从（0，0）开始，（a,b）结束
	//否则后面容易出错
	for(i=a;i>=1;i--){
		for(j=1;j<=b;j++){
			c[i][j]=read();//不用快读也能过
		}
	}
	ans[1][1]=1;
	for(i=1;i<=a;i++){
		for(j=1;j<=b;j++){
			if(c[i][j]==0)
			ans[i][j]+=(ans[i-1][j]+ans[i][j-1])%2333;
			else
			ans[i][j]=0;
		}
	}	
	cout<<ans[a][b];
	return 0;
}
```
## D - 表达式求值
给定一个只包含加法和乘法的算术表达式，请你编程计算表达式的值。
### 输入
输入仅有一行，为需要你计算的表达式，表达式中只包含数字、加法运算符“+”和乘法运算符“*”，且没有括号。
所有参与运算的数字均为 0 到 2^31-1 之间的整数。
输入数据保证这一行只有0~9、+、*这12种字符。
### 输出
输出只有一行，包含一个整数，表示这个表达式的值。
**注意：当答案长度多于4位时，请只输出最后4位，前导0不输出。**
### 样例1
#### 输入
1+1*3+4

#### 输出
8

#### 备注
计算的结果为8，直接输出8。

### 样例2
#### 输入
1+1234567890*1

#### 输出
7891

#### 备注
计算的结果为1234567891，输出后4位，即7891。

### 样例3
#### 输入
1+1000000003*1

#### 输出
4

#### 备注
计算的结果为1000000004，输出后4位，即4。

### 备注
对于30%的数据，0≤表达式中加法运算符和乘法运算符的总数≤100；
对于80%的数据，0≤表达式中加法运算符和乘法运算符的总数≤1000；
对于100%的数据，0≤表达式中加法运算符和乘法运算符的总数≤100000。
### 题解
用一个栈实现 ，用来记录数
有乘法就先计算出结果，结果再放入栈中，最后栈中元素求和
每个数只记录后4位，因为题目要求
因为输入是一个数，一个符号的输入。所以可以很好处理
```cpp
#include<iostream>
#include<algorithm>
#include<cstdio>
#include<cstring>
#include<cmath>
#include<stack>  
using namespace std;
#define mid 1000000007  
typedef  long long ll;
//主要因为题目运算简单 
//思路：用一个栈实现 ，用来记录数
//有乘法就先计算出结果，再放入栈中，最后栈中元素求和 
//每个数只记录后4位，因为题目要求 
//因为输入是一个数，一个符号的输入。所以可以很好处理  
stack<int>c1;
int sum=0;
int main(){
	int i,a,b;
	char ch;
	//模拟输入，符号，数字交替输入
	for(i=1;;i++){
		if(i%2==1){
			cin>>a;
			a=a%10000;
			c1.push(a);
		}
		else{
			ch=getchar();//输入回车符，就断开
			if(ch=='\n')
			break;
			else{
				if(ch=='*'){
					cin>>a;//直接把下一个数读进来，进行计算 
					a=a%10000;
					b=c1.top();
					c1.pop();
					c1.push(a*b%10000);
					i++;//因为多输入了一个 
				}
			}
		}
	}
	//栈中元素求和
	while(!c1.empty()){
		sum=(sum+c1.top())%10000;
		c1.pop();
	} 
	cout<<sum;
	return 0;
	
}
```

#### Python(2.7.3)
```python
print(input()%10000)
```