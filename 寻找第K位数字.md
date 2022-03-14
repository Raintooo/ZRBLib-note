- [寻找第K位数字](#寻找第k位数字)
  - [注意点剖析](#注意点剖析)

#  寻找第K位数字

* 在不能排序的情况下对乱序的数组中找到第K位数字

```C++
#include <iostream>

using namespace std;

int partition(int a[], int begin, int end)
{
    int privot = a[begin];

    while(begin < end)
    {
        while(privot < a[end])
        {
            end--;
        }

        std::swap(a[begin], a[end]);

        while(privot > a[begin])
        {
            begin++;
        }

        std::swap(a[begin], a[end]);
    }

    a[begin] = privot;

    return privot;
}

int FindNumK(int a[], int begin, int end, int k)
{
    int ret;

    if(begin == end)
    {
        ret = a[begin];
    }
    else
    {
        int privot = partition(a, begin, end);

        if(privot == k)
        {
            ret = a[privot];
        }
        else if(privot > k)
        {
            ret = FindNumK(a, begin, privot - 1, k);
        }
        else if(privot < k)
        {
            ret = FindNumK(a, privot + 1, end, k);
        }
    }

    return ret;
}

int FindNumK(int a[], int n, int k)
{
    int ret = 0;

    if((0 <= k) && (k < n))
    {
        ret = FindNumK(a, 0, n-1, k);
    }
    else
    {
        ret = -1;
    }

    return ret;
}

int FindMidNum(int a[], int n)
{
    return FindNumK(a, n, (n-1)/2);
}
```

## 注意点剖析

* 利用快速排序的思维, 即```partition```中每次可寻找到一个已经排好序的数字 ```J```, 
* 对```J```与```K```比较判断确定下次是在```J```的左边还是右边继续递归