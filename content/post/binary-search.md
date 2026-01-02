---
title: 二分查找实现
date: 2018-01-13 16:36:44
tags: [算法, C]
---

二分查找应该是一个比较简单的查找方法，但也是最之容易有bug的算法了。好吧，说得新看C语法总得有个交待吧，现在交上一个二分查找算法的实现吧。自己曾经写过一个，但给出的这个应该是非常正确的一个了。

二分查找的先决条件是啥呢，有是查找的数据必需是一个有序数组。否则无效.

好吧上代码了。

```c

    #include <stdio.h>
    
    #define SIZE 10
    
    int binary_search(int sorted_list[], int low, int high, int element);
    
    int main()
    {
        int a[ SIZE ] = { 1,2,3,4,5,6,7,8,9,10 };
        int e, i, p;
        printf("Array:");
        for (i=0; i< SIZE ;i++)
        {
            printf("%d ", a[i]);
        }
        printf("\n");
        printf("please input a integer:");
        scanf("%d", &e);
        p = binary_search(a, 0, SIZE, e);
    
        if(p >= 0)
        {
            printf("The key %d was found at %d\n", e, p);
        }
        else
        {
            printf("The key %d was not found\n", e);
        }
        return 0;
    }
    
    int binary_search(int sorted_list[], int low, int high, int element)
    {
        int middle;
        while(low <= high)
        {
            middle = (high-low)/2 +low;
            if(element < sorted_list[middle])
                high = middle - 1;
            else if( element > sorted_list[middle])
                low = middle + 1;
            else
                return middle;
    
        }
        return -1;
    }
```

其中核心部份应该是`middle = (high-low)/2 +low`了。这个作用是防止溢出
