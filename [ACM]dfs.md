迷宫：由（0，0）走到（3，3）有几种走法？

|  1   |  1   |  1   |  1   |
| :--: | :--: | :--: | :--: |
|  0   |  1   |  0   |  1   |
|  0   |  1   |  1   |  1   |
|  0   |  1   |  0   |  1   |

## 伪代码

```cpp
int mp[4][4];

int dx[4]={-1,1,0,0};
int dy[4]={0,0,-1,1};

void dfs(int x,int y);
{
   if(到达终点)
	{
 		答案++；
		return；
	}
	if(遇到障碍)
	{
		return;
	}
	
	for(int i=0;i<4;i++)
	{
		走迷宫
	}
}

int main()
{
	输入二维数组；
	调用函数，给定起点；
	输出答案；
	return 0；
}
```


## 代码
```cpp
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
            vis[x][y]=0;
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

```