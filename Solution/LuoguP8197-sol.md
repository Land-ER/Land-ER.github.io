## 题意简述
给定序列 $a$ 和 $b$，每次操作可以交换序列 $a$ 中相邻的两个数，试将序列 $a$ 变得与序列 $b$ 相同。

## 解题思路
首先，如果两个序列中每个数字出现的次数都相同则有解。

其次，考虑到每次操作是交换相邻的两项，并且次数上限是 $n^2$，那么很容易考虑到冒泡排序的思想。

具体来说，我们通过一个新的序列 $d$ 来完成这一过程。对于序列 $d$，我们使 $d_i$ 为 $a_i$ 在 $b$ 中出现的位置。

样例：
```cpp
a = {1,2,2,3};
b = {3,2,2,1};
d = {4,2,2,1};//由于冒泡排序的原理，即使有相同的元素也能正确处理
```
然后我们直接对 $d$ 进行冒泡排序，并输出过程即可。

## 代码实现
```cpp
#include<bits/stdc++.h>
using namespace std;
int main(void){
    int t,n,a[1005],b[1005],d[1005],f;
    scanf("%d",&t);
    while(t--){
        f = 1;
        scanf("%d",&n);
        for(int i = 0;i < n;++ i)
            scanf("%d",a+i);
        for(int i = 0;i < n;++ i)
            scanf("%d",b+i);
        for(int i = 0;i < n;++ i){
            int j;
            for(j = 0;j < n;++ j){
                if(a[i] == b[j])
                    break;
            }
            if(j == n){
                f = 0;
                break;
            }
            d[i] = j;
        }
        if(!f){
            printf("NO\n");
            continue;
        }
        printf("YES\n");
        for(int i = n;i > 0;-- i){
            for(int j = 0;j < i-1;++ j){
                if(d[j] > d[j+1]){
                    printf("%d %d\n",j+1,j+2);
                    swap(d[j],d[j+1]);
                }
            }
        }
        printf("0 0\n");
    }
    return 0;
}
```