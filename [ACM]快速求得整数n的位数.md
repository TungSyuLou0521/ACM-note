```cpp
#include<stdio.h>
#include<math.h>
int main()
{
    int n;
    scanf("%d",&n);
    if(n<0)
        n*=-1;
    int ans = floor(log10(n))+1;
    printf("%d\n",ans);
    return 0;
}

```