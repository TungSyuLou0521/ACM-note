**const int INF=0x3f3f3f3f;**

将某个数组清零，我们通常会使memset(a,0,sizeof(a))
但是当我们想将某个数组全部赋值为无穷大时，就不能使用memset函数而得自己写循环了，
因为memset是按字节操作的，它能够对数组清零是因为0的每个字节都是0（一般我们只有赋值为-1和0的时候才使用它）。
现在好了，如果我们将无穷大设为0x3f3f3f3f，那么奇迹就发生了，0x3f3f3f3f的每个字节都是0x3f！所以要把一段内存全部置为无穷大，我们只需要**memset(a,0x3f,sizeof(a))。**