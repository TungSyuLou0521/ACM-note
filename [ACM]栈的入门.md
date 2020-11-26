## 括号画家

Candela是一名漫画家，她有一个奇特的爱好，就是在纸上画括号。这一天，刚刚起床的Candela画了一排括号序列，其中包含小括号()、中括号[]和大括号{}，总长度为N。这排随意绘制的括号序列显得杂乱无章，于是Candela定义了什么样的括号序列是美观的：
(1) 空的括号序列是美观的；
(2) 若括号序列A是美观的，则括号序列(A)、[A]、{A}也是美观的；
(3) 若括号序列A、B都是美观的，则括号序列AB也是美观的；
例如 [(){}]() 是美观的括号序列，而 )({)[}]( 则不是。
现在Candela想知道她画出的括号序列是不是美观的。你能帮帮她吗？

### 输入
一个括号序列，长度不超过10000。
### 输出
如果它是美观的，输出Yes，否则输出No。
### 样例
#### 样例输入
{}[(){}]()
#### 样例输出
Yes

题目来源：http://dsalgo.openjudge.cn/stackqueue/10/


### 题解
```cpp
#include<bits/stdc++.h>
using namespace std;
stack<int>s;
char ch[12345];
int main()
{
	int i;
	int flag=0;
	gets(ch);
	int len=strlen(ch);
	for(i=0;i<len;i++)
	{
		if(s.empty())
		{
			if(ch[i]=='('||ch[i]==')'||ch[i]=='['||ch[i]==']'||ch[i]=='{'||ch[i]=='}')
			s.push(i);
		}
		else
		{
			if(ch[s.top()]==')'||ch[s.top()]==']'||ch[s.top()]=='}')
			{
				flag=1;
			}
			else if(ch[s.top()]=='(')
			{
				if(ch[i]==')')
				s.pop();
				else
				s.push(i);
			}
			else if(ch[s.top()]=='[')
			{
				if(ch[i]==']')
				s.pop();
				else
				s.push(i);
			}
			else if(ch[s.top()]=='{')
			{
				if(ch[i]=='}')
				s.pop();
				else
				s.push(i);
			}
		}
	}
	if(s.empty()&&flag!=1)
	printf("Yes");
	else if(!s.empty()||flag==1)
	printf("No");
}
```


### 栈的基本实现
| Stack<T>()     | 创建一个空的栈           |
| -------------- | ------------------------ |
| void Push(T s) | 往栈中添加一个新的元素   |
| T.op()         | 移除并返回最近添加的元素 |
| bool IsEmpty() | 栈是否为空               |
| int Size()     | 栈中元素的个数           |