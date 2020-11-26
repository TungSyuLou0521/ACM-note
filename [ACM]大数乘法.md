```cpp
#include<bits/stdc++.h>
using namespace std;
int arr1[201],arr2[201],arr3[456];
char ch[1005],str[205];
int main()
{
    scanf("%[^\n]",ch);
    getchar();
    scanf("%[^\n]",str);
    int len1=strlen(ch);
    int len2=strlen(str);
    int i,j;
    i=0;
    for(j=len1-1; j>=0; j--)
    {
        arr1[i]=ch[j]-'0';
        i++;
    }
    i=0;
    for(j=len2-1; j>=0; j--)
    {
        arr2[i]=str[j]-'0';
        i++;
    }
    
    //运算
    for(i=0; i<len1; i++)
    {
        for(j=0; j<len2; j++)
        {
            arr3[i+j]+=arr1[i]*arr2[j];
        }
    }
    
    //进位
    for(i=0; i<len1+len2; i++)
    {
        if(arr3[i]>=10)
        {
            arr3[i+1]+=arr3[i]/10;
            arr3[i]=arr3[i]%10;
        }
    }
    i=i-1;
    
    //判断前导0
    while(i>=0)
    {
        if(arr3[i]!=0)
            break;
        i--;
    }
    
    //输出
    for(int h=i; h>=0; h--)
    {
        printf("%d",arr3[h]);
    }
    return 0;
}

```