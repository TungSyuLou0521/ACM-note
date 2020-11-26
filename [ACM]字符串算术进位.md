编写一个程序，输入一个字符串，从字符串中提取有效的数字，输出它们的综合。
例如输入为"123.4ab56 33.2"
输出为212.6
即123.4+56+33.2得结果
要求：1.字符串可以从键盘输入 2.字符串中可以有空格，如例子中6后边就有一个空格

## 判断进位

sum=sum*10+( s[ i ] -'0');

### 代码
```cpp
#include<stdio.h>
#include<string.h>
char s[100];
int main()
{
    gets(s);
    int len;
    len=strlen(s);
    double sum=0;
    double sum2=0;
    double sum3=0;
    double n=10;
    int flag=0;
    for(int i=0; i<len; i++)
    {
        if(s[i]=='.')
        {
            flag=1;
        }
        if(s[i]!='.'&&s[i]!='0'&&s[i]!='1'&&s[i]!='2'&&s[i]!='3'&&s[i]!='4'&&s[i]!='5'&&s[i]!='6'&&s[i]!='7'&&s[i]!='8'&&s[i]!='9')
        {
            flag=0;
            sum3=sum+sum2+sum3;
            sum=0;
            sum2=0;
            n=10;
        }
        if(s[i]>='0'&&s[i]<='9')
        {
            if(flag==0)
            {
                sum=sum*10+(s[i]-'0');
            }
            else
            {
                sum2=sum2+(s[i]-'0')/n;
                n*=10;
            }
        }
        printf("%lf+%lf=%lf\n",sum,sum2,sum3);
    }
    sum3=sum+sum2+sum3;
    printf("%lf+%lf=%lf\n",sum,sum2,sum3);
}

```
