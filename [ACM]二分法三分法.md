### 理论
非线性方程的求根问题
> 非线性方程，是指f(x)中含有三角函数、指数函数或其他超越函数。

实际应用中，只要得到满足一定精度要求的近似解
需要考虑2个问题：
　　（1）根的存在性。用这个定理判定：设函数在闭区间[a, b]上连续，且f(a) ∙ f(b) < 0,则f(x) = 0存在根。
　　（2）求根。一般有两种方法：搜索法、二分法。

**搜索法**：把区间[a, b]分成n等份，每个子区间长度是∆x，计算点xk = a + k∆x (k=0,1,2,3,4,…,n)的函数值f(xk)，若f(xk) = 0，则是一个实根，若相邻两点满足f(xk) ∙ f(xk+1) < 0，则在(xk, xk+1)内至少有一个实根，可以取(xk+ xk+1)/2为近似根。
**二分法**：如果确定f(x)在区间[a, b]内连续，且f(a) ∙ f(b) < 0，则至少有一个实根。二分法的操作，就是把[a, b]逐次分半，检查每次分半后区间两端点函数值符号的变化，确定有根的区间。

#### 什么情况下用二分？
两个条件：上下界[a, b]确定、函数在[a, b]内单调。

复杂度是O(logn)

### 中间值
**中间值写成mid = left + (right-left)/2**
不能写成 mid = (left + right)/2; 在有负数的情况下，会出错。

## STL的lower_bound()和upper_bound()
如果只是简单地找x或x附近的数，就用STL的lower_bound()和upper_bound()函数。有以下情况：
（1）查找第一个大于x的元素的位置：upper_bound()。代码例如：pos = upper_bound(a, a+n, test) - a;
（2）查找第一个等于或者大于x的元素：lower_bound()
（3）查找第一个与x相等的元素：lower_bound()且 = x
（4）查找最后一个与x相等的元素：upper_bound()的前一个且 = x
（5）查找最后一个等于或者小于x的元素：upper_bound()的前一个
（6）查找最后一个小于x的元素：lower_bound()的前一个
（7）单调序列中数x的个数：upper_bound() - lower_bound()

### 例题
1）生成随机数组a[]；
2）用sort()排序；
3）生成一个随机的x；
4）分别用bin_search()和lower_bound()在a[]中找x；
5）比较它们的返回值是否相同。
```cpp
#include<bits/stdc++.h>
using namespace std;
#define MAX   100    //试试10000000
#define MIN  -100
int a[MAX];          //如果MAX超过100万，大数组a[MAX]最好定义为全局。
//大数组定义在全局的原因是：有的评测环境，栈空间很小，大数组定义在局部占用了栈空间导致爆栈。
//现在各大OJ和比赛都会设置编译命令使栈空间等于内存大小，不会出现爆栈。

unsigned long ulrand(){          //生成一个大随机数
    return (
      (((unsigned long)rand()<<24)& 0xFF000000ul)
     |(((unsigned long)rand()<<12)& 0x00FFF000ul)
     |(((unsigned long)rand())    & 0x00000FFFul));
}

int bin_search(int *a, int n, int x){    //a[0]～a[n-1]是有序的
    int left = 0, right = n;             //不是 n-1
    while (left < right) {
        int mid = left+(right-left)/2;   //int mid = (left+ right)>>1;
        if (a[mid] >= x)  right = mid;
        else    left = mid + 1;
    }
   return left;       //特殊情况：如果最后的a[n-1] < key，left = n
}

int main(){
    int n = MAX;
    srand(time(0));
    while(1){
        for(int i=0; i< n; i++)   //产生[MIN, MAX]内的随机数，有正有负
            a[i] = ulrand() % (MAX-MIN + 1) + MIN;
        sort(a, a + n );       //排序，a[0]~a[n-1]

        int test = ulrand() % (MAX-MIN + 1) + MIN; //产生一个随机的x
        int ans = bin_search(a,n,test);
        int pos = lower_bound(a,a+n,test)-a;  

        //比较bin_search()和lower_bound()的输出是否一致：
        if(ans == pos) cout << "!";             //正确
        else        {  cout << "wrong"; break;} //有错，退出
    }
}
```

### 例题
输入n ( n≤100,000)个整数，找出其中的两个数，它们之和等于整数m(假定肯定有解)。题中所有整数都能用int 表示。
### 题解
（1）暴力搜，用两重循环，枚举所有的取数方法，复杂度O(n^2)。超时。
（2）二分法。首先对数组从小到大排序，复杂度O(nlogn)；然后，从头到尾处理数组中的每个元素a[i]，在a[i]后面的数中二分查找是否存在一个等于 m - a[i]的数，复杂度也是O(nlogn)。两部分相加，总复杂度仍然是O(nlogn)。
（3）尺取法/双指针:首先对数组从小到大排序；然后，设置两个变量L和R，分别指向头和尾，L初值是0，R初值是n-1，检查a[L]+a[R]，如果大于m，就让R减1，如果小于m，就让L加1，直至a[L]+a[R] = m。排序复杂度O(nlogn)，检查的复杂度O(n)，总复杂度O(nlogn)。
```cpp
void find_sum(int a[], int n, int m){ 
     sort(a, a + n - 1);      //先排序
     int L = 0, R = n - 1;    //L指向头，R指向尾
     while (L < R){
		    int sum = a[L] + a[R];
		    if (sum > m)   R--;
		    if (sum < m)   L++;
		    if (sum == m){     
			    cout << a[L] << "    " << a[R] << endl;  //打印一种情况
                L++;   //可能有多种情况，继续
		    }
	  }
}
```

### 最小值最大化（最小值尽量大）
Farmer John建造了一个有N(2<=N<=100,000)个隔间的牛棚，这些隔间分布在一条直线上，坐标是x1,...,xN (0<=xi<=1,000,000,000)。

他的C(2<=C<=N)头牛不满于隔间的位置分布，它们为牛棚里其他的牛的存在而愤怒。为了防止牛之间的互相打斗，Farmer John想把这些牛安置在指定的隔间，所有牛中相邻两头的最近距离越大越好。那么，这个最大的最近距离是多少呢？

#### 输入
第1行：两个用空格隔开的数字N和C。
第2~N+1行：每行一个整数，表示每个隔间的坐标。
#### 输出
输出只有一行，即相邻两头牛最大的最近距离。

#### 样例
##### 输入
5 3
1 
2 
8 
4 
9 
##### 输出
3
### 题解
（1）暴力法。从小到大枚举最小距离的值dis，然后检查，如果发现有一次不行，那么上次枚举的就是最大值。如何检查呢？用贪心法：第一头牛放在x1，第二头牛放在xj≥x1+dis的点xi,第三头牛放在xk≥xj+dis的点xk，等等，如果在当前最小距离下，不能放c条牛，那么这个dis就不可取。复杂度O(nc)。
（2）二分。分析从小到大检查dis的过程，发现可以用二分的方法找这个dis。这个dis符合二分法：它有上下边界、它是单调递增的。复杂度O(nlogn)。
```cpp
#include<bits/stdc++.h>
using namespace std;
int n,c,x[100005];//牛棚数量，牛数量，牛棚坐标

bool check(int dis){     //当牛之间距离最小为dis时，检查牛棚够不够
    int cnt=1, place=0;  //第1头牛，放在第1个牛棚
    for (int i = 1; i < n; ++i)     //检查后面每个牛棚
        if (x[i] - x[place] >= dis){ //如果距离dis的位置有牛棚
            cnt++;      //又放了一头牛
            place = i;  //更新上一头牛的位置
        }
    if (cnt >= c) return true;   //牛棚够
    else          return false;  //牛棚不够
}

int main(){
    scanf("%d%d",&n, &c);
    for(int i=0;i<n;i++)    scanf("%d",&x[i]);
    sort(x,x+n);             //对牛棚的坐标排序
    int left=0, right=x[n-1]-x[0];  //R=1000000也行，因为是log(n)的，很快
							        //优化：把二分上限设置为1e9/c
    int ans = 0;
    while(left < right){
        int mid = left + (right - left)/2;     //二分
        if(check(mid)){       //当牛之间距离最小为mid时，牛棚够不够?
            ans = mid;        //牛棚够，先记录mid
            left = mid + 1;   //扩大距离
           }
        else
            right = mid;      //牛棚不够，缩小距离
    }

    cout << ans;              //打印答案
    return 0;
}
```

### 三分法求极值
三分法求单峰（或者单谷）的极值，是二分法的一个简单扩展。
单峰函数和单谷函数如下图，函数f(x)在区间[l, r]内，只有一个极值v，在极值点两边，函数是单调变化的。以单峰函数为例，在v的左边，函数是严格单调递增的，在v右边是严格单调递减的。
![](http://www.wangyinboy.com/function/photo/55.JPG)
以求单峰极值为例。
如何求单峰函数最大值的近似值？虽然不能直接用二分法，不过，只要稍微变形一下，就能用了。
在[l, r]上任取2个点，mid1和mid2，把函数分成三段。有以下情况：
（1）若f(mid1) < f(mid2)，极值点v一定在mid1的右侧。此时，mid1和mid2要么都在v的左侧，要么分别在v的两侧。![](http://www.wangyinboy.com/function/photo/66.JPG)
下一步，令l = mid1，区间从[l, r]缩小为[mid1, r]，然后再继续把它分成三段。
（2）同理，若f(mid1) > f(mid2)，极值点v一定在mid2的左侧。如下图所示。下一步，令 r = mid2，区间从[l, r]缩小为[l, mid2]。
![](http://www.wangyinboy.com/function/photo/77.JPG)
不断缩小区间，就能使得区间[l, r]不断逼近v，从而得到近似值。
如何取mid1和mid2？
三等分：mid1和mid2为[l, r]的三等分点。那么区间每次可以减少三分之一。

### 例题
给出一个N次函数，保证在范围[l, r]内存在一点x，使得[l, x]上单调增，[x, r]上单调减。试求出x的值。
```cpp
#include<bits/stdc++.h>
using namespace std;
const double eps = 1e-6;
int n;
double a[15];
double f(double x){       //计算函数值
    double s=0;
    for(int i=n;i>=0;i--) //注意函数求值的写法
        s = s*x + a[i];
    return s;
}
int main(){
    double L,R;
    scanf("%d%lf%lf",&n,&L,&R);
    for(int i=n;i>=0;i--) scanf("%lf",&a[i]);
    while(R-L > eps){  // for(int i = 0; i<100; i++){   //用for也行
        double k =(R-L)/3.0;
        double mid1 = L+k, mid2 = R-k;
        if(f(mid1) > f(mid2)) 
               R = mid2;
        else   L = mid1;
    }
    printf("%.5f\n",L);
    return 0;
}
```