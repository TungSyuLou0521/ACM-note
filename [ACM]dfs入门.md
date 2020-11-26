# 1. 走迷宫

有一个4*4的矩阵迷宫，左上角为起点，0为障碍1为路，
问，有几条路可以走出这个迷宫。

#### 输入

一个4*4的矩阵迷宫，由0和1构成

#### 输出
有几条走出迷宫的路

#### 输入样例

> 1111
> 0101
> 0111
> 0101

#### 输出样例

> 2

#### 题解


    #include <iostream>
    #include <string.h>
    #include <stdio.h>
    
    using namespace std;
    
    int mp[4][4];
    int vis[4][4];
    int ans=0;
    
    int dx[4]= {-1,1,0,0};
    int dy[4]= {0,0,-1,1};
    int sum=0;
    
    void dfs(int x, int y)
    {
        printf("%d %d %d\n",x,y,sum++);
        if(x==3&&y==3)
        {
            ans++;
            return;
        }
        if(mp[x][y]==0)
        {
            return ;
        }
    
        int xx,yy;
    
        for(int i=0; i<4; i++)
        {
            xx=x+dx[i];
            yy=y+dy[i];
            if(xx>=0&&xx<4&&yy>=0&&yy<4&&mp[xx][yy]==1&&vis[xx][yy]==0)
            {
                vis[x][y]=1;
                dfs(xx,yy);
    
                // --
                vis[x][y]=0;
                printf("%d %d %d +++\n",x,y,sum++);
            }
        }
        return ;
    }
    int main()
    {
        for(int i=0; i<4; i++)
        {
            for(int j=0; j<4; j++)
            {
                scanf("%d",&mp[i][j]);
            }
        }
        dfs(0,0);
        printf("%d\n",ans);
        return 0;
    }



------------

# 2.油田
The GeoSurvComp geologic survey company is responsible for detecting underground oil deposits. GeoSurvComp works with one large rectangular region of land at a time, and creates a grid that divides the land into numerous square plots. It then analyzes each plot separately, using sensing equipment to determine whether or not the plot contains oil. A plot containing oil is called a pocket. If two pockets are adjacent, then they are part of the same oil deposit. Oil deposits can be quite large and may contain numerous pockets. Your job is to determine how many different oil deposits are contained in a grid.

#### 输入

The input file contains one or more grids. Each grid begins with a line containing m and n, the number of rows and columns in the grid, separated by a single space. If m = 0 it signals the end of the input; otherwise 1 <= m <= 100 and 1 <= n <= 100. Following this are m lines of n characters each (not counting the end-of-line characters). Each character corresponds to one plot, and is either '*', representing the absence of oil, or '@', representing an oil pocket.

#### 输出

For each grid, output the number of distinct oil deposits. Two different pockets are part of the same oil deposit if they are adjacent horizontally, vertically, or diagonally. An oil deposit will not contain more than 100 pockets.

#### 输入样例

> 1 1
> *
> 3 5
> *@*@*
> **@**
> *@*@*
> 1 8
> @@****@*
> 5 5 
> ****@
> *@@*@
> *@**@
> @@@*@
> @@**@
> 0 0 

#### 输出样例

> 0
> 1
> 2
> 2

#### 题解

```cpp
    #include<cstdio>
    #include<queue>
    #include<cstring>
    #include<algorithm>
    using namespace std;
    int num,i,j,b[105][105],m,n,k;
    char a[105][105];
    void dfs(int x,int y)
    {
      if(a[x][y+1]=='@'&&b[x][y+1]!=1)
    	{
    		b[x][y+1]=1;
    		dfs(x,y+1);
    	}
    	if(a[x][y-1]=='@'&&b[x][y-1]!=1)
    	{
    		b[x][y-1]=1;
    		dfs(x,y-1);
    	}
    		if(a[x-1][y]=='@'&&b[x-1][y]!=1)
    	{
    		b[x-1][y]=1;
    		dfs(x-1,y);
    	}
    		if(a[x+1][y]=='@'&&b[x+1][y]!=1)
    	{
    		b[x+1][y]=1;
    		dfs(x+1,y);
    	}
    	if(a[x-1][y+1]=='@'&&b[x][y+1]!=1)
    	{
    		b[x-1][y+1]=1;
    		dfs(x-1,y+1);
    	}
    	if(a[x-1][y-1]=='@'&&b[x-1][y-1]!=1)
    	{
    		b[x-1][y-1]=1;
    		dfs(x-1,y-1);
    	}
    		if(a[x+1][y+1]=='@'&&b[x+1][y+1]!=1)
    	{
    		b[x+1][y+1]=1;
    		dfs(x+1,y+1);
    	}
    		if(a[x+1][y-1]=='@'&&b[x+1][y-1]!=1)
    	{
    		b[x+1][y-1]=1;
    		dfs(x+1,y-1);
    	}
    }
    int main()
    {
    	while(scanf("%d %d",&m,&n)!=EOF&&m!=0)
    	{
    		memset(b,0,sizeof(b));
            memset(a,'*',sizeof(a));
    		num=0;
    		for(i=0;i<m;i++)
    		scanf("%s",&a[i]);
    		for(i=0;i<m;i++)
    		for(j=0;j<n;j++)
    		{
    			   if(a[i][j]=='@'&&b[i][j]!=1)
    			{
    				b[i][j]=1;
    				dfs(i,j);
    				num++;
    			}
    		}
    		printf("%d\n",num);
    	}
    	return 0;
    }
    
```



------------

# 3.N皇后问题

```cpp
#include <iostream>
#include <cstdio>
#include <cstdlib>
#include <string.h>
#define maxsize 20+7
using namespace std;

int y[maxsize];
int n;
int count=0;

bool judge(int num)
{
    for(int i=0; i<num; i++)
    {
        if(y[i]==y[num] || abs(y[num]-y[i])==num-i)
        {
            return false;
        }

    }
    return true;
}

void RecurBack(int num)
{
    if(num==n)
    {
        count++;
        return;
    }
    for(int i=0; i<n; i++)
    {
        y[num]=i;
        if(judge(num))
        {
            RecurBack(num+1);
        }
    }
}
int main()
{
    while(~scanf("%d",&n))
    {
        count=0;
        if(n==0)
        {
            break;
        }
        RecurBack(0);
        printf("%d\n",count);
    }
    return 0;
}

```

------------

# 4.全排列问题

#### 题目描述

输出自然数1到n所有不重复的排列，即n的全排列，要求所产生的任一数字序列中不允许出现重复的数字。

输入输出格式

输入格式：
n(1≤n≤9)

输出格式：
由1～n组成的所有不重复的数字序列，每行一个序列。每个数字保留5个常宽。

#### 输入样例：

3
#### 输出样例：
​    1    2    3
​    1    3    2
​    2    1    3
​    2    3    1
​    3    1    2
​    3    2    1

#### 题解

```cpp
#include<bits/stdc++.h>
using namespace std;
int n;
int ans[15];//保存当前的方案
int use[15];//表示每个数是否被用过
void dfs(int x) //X表示当前搜索到那个数
{
    if(x>n) //如果N位都搜索完了，就输出方案并返回
    {
        for(int i=1; i<=n; i++)
            printf("% 5d",ans[i]);//输出方案
        puts("");
        return;
    }
    for(int i=1; i<=n; i++) //从小到大枚举
        if(!use[i]) //判断这个数是否用过
        {
            ans[x]=i;//保存到方案中
            use[i]=1;//标记这个数被使用了
            dfs(x+1);//进行下一步搜索
            use[i]=0;//撤销标记
        }
}
int main()
{

    scanf("%d",&n);//输入
    dfs(1);//从第一个数开始搜索；
}

```

------------

# 5.迷宫（一）

一天蒜头君掉进了一个迷宫里面，蒜头君想逃出去，可怜的蒜头君连迷宫是否有能逃出去的路都不知道。
看在蒜头君这么可怜的份上，就请聪明的你告诉蒜头君是否有可以逃出去的路。

#### 输入格式
第一行输入两个整数 n 和 m，表示这是一个 n × m 的迷宫。

接下来的输入一个 n 行 m 列的迷宫。其中 'S' 表示蒜头君的位置，'*'表示墙，蒜头君无法通过，'.'表示路，蒜头君可以通过'.'移动，'T'表示迷宫的出口（蒜头君每次只能移动到四个与他相邻的位置——上，下，左，右）。

#### 输出格式
输出一个字符串，如果蒜头君可以逃出迷宫输出"yes"，否则输出"no"。

#### 数据范围
1 <= n, m <= 10

输出时每行末尾的多余空格，不影响答案正确性

#### 样例输入1

```cpp
 3 4
S**.
..*.
***T
```

#### 样例输出1

> no

#### 样例输入2

```cpp
 3 4
S**.
....
***T
```

#### 样例输出2

> yes

#### 题解

```cpp
#include <iostream>
#include <cstdio>
using namespace std;
int n, m;
bool f;
char mp[15][15];
int vis[15][15];
int dir[4][2] = {{-1, 0}, {0,1}, {1,0}, {0,-1}};
bool in(int x, int y)
{
    return 0<= x && x < n&& 0 <= y && y < m;
}
void dfs(int x, int y)
{
    if (mp[x][y] == 'T')
    {
        f = true;
        return;
    }
    if (!in(x,y)||mp[x][y]=='*'||vis[x][y])
    {
        return;
    }
    vis[x][y] = 1;
    for (int i = 0; i < 4; i++)
    {
        int tx = x + dir[i][0];
        int ty = y + dir[i][1];
        dfs(tx,ty);
    }
    return;
}
int main()
{
    scanf("%d%d", &n, &m);
    for(int i = 0; i < n; i++)
    {
        scanf("%s", mp[i]);
    }
    int x, y;
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {
            if (mp[i][j] == 'S')
            {
                x = i;
                y = j;
            }
        }
    }
    dfs(x, y);
    if (f)
    {
        printf("yes\n");
    }
    else
    {
        printf("no\n");
    }

    return 0;
}

```