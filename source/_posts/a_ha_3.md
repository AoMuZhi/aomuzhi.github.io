---
title: 啊哈！算法之枚举
author: aogui
avatar: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585588339631&di=6fc163ee2519e0730db31973c2fd3a08&imgtype=0&src=http%3A%2F%2Fpic.38fan.com%2Fallimg%2F170619%2F51_170619104556_1.png
authorLink: 
authorAbout: 一个有梦想的人
authorDesc: 一个有梦想的人
categories: 转载
date: 2020-04-15 21:32:00
comments: true
tags:
 - 算法
 - 学习
keywords: 枚举
description: 枚举
photos: https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/aha3.png
---
## 1.坑爹的奥数
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/301.png)
```c
/***
填1~9不同的数实现：
□ □ □ + □ □ □ = □ □ □
*/
#include <stdio.h>
int main()
{
    int a[10],i,total=0,book[10],sum;
    //这里用a[1]~a[9]来表示九个变量
    for(a[1]=1;a[1]<=9;a[1]++)
     for(a[2]=1;a[2]<=9;a[2]++)
      for(a[3]=1;a[3]<=9;a[3]++)
       for(a[4]=1;a[4]<=9;a[4]++)
        for(a[5]=1;a[5]<=9;a[5]++)
         for(a[6]=1;a[6]<=9;a[6]++)
          for(a[7]=1;a[7]<=9;a[7]++)
           for(a[8]=1;a[8]<=9;a[8]++)
            for(a[9]=1;a[9]<=9;a[9]++)
             {
                 for(i=1;i<=9;i++)
                    book[i]=0;
                 for(i=1;i<=9;i++)
                    book[a[i]]=1;
                 //统计共出现了多少不同的数
                 sum=0;
                 for(i=1;i<=9;i++)
                    sum+=book[i];
                 //如果正好出现了9个不同的数，并且满足等式条件，则输出
                 if(sum==9&&a[1]*100+a[2]*10+a[3]+a[4]*100+a[5]*10+a[6]==a[7]*100+a[8]*10+a[9])
                 {
                     total++;
                     printf("%d%d%d+%d%d%d=%d%d%d\n",a[1],a[2],a[3],a[4],a[5],a[6],a[7],a[8],a[9]);
                 }
             }
    printf("total=%d",total/2);
    return 0;
}
```
此题也可以用深度优先搜索模型实现（转下一章）