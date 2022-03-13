---
title: 啊哈！算法之枚举
author: aogui
avatar: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585588339631&di=6fc163ee2519e0730db31973c2fd3a08&imgtype=0&src=http%3A%2F%2Fpic.38fan.com%2Fallimg%2F170619%2F51_170619104556_1.png
authorLink: 
authorAbout: 一个有梦想的人
authorDesc: 一个有梦想的人
categories: 转载
date: 2020-04-15 21:42:03
comments: true
tags:
 - 算法
 - 学习
keywords: 搜索
description: 搜索
photos: https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/aha4.png
---
## 1.坑爹的奥数
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/301.png)
```c
#include <stdio.h>
int a[10],book[10],total=0;
void dfs(int step)//step表示站在第几个盒子面前
{
    int i;
    if(step==10)
    {
        //判断是否满足等式□ □ □ + □ □ □ = □ □ □
        if(a[1]*100+a[2]*10+a[3]+a[4]*100+a[5]*10+a[6]==a[7]*100+a[8]*10+a[9])
        {
           total++;
           printf("%d%d%d+%d%d%d=%d%d%d\n",a[1],a[2],a[3],a[4],a[5],a[6],a[7],a[8],a[9]);
        }
        return;//返回之前的一步（最近调用的地方）
    }
    //此时站在第step个盒子面前，应该放哪张牌呢？
    //按照1、2、3、、、n的顺序一一尝试
    for(i=1;i<=9;i++)
    {
        //判断扑克牌i是否还在手上
        if(book[i]==0)//book[i]为0表示扑克牌还在手上
        {
            //开始尝试使用扑克牌i
            a[step]=i;//将扑克牌i放入第step个盒子中
            book[i]=1;//将book[i]的值设为1，表示扑克牌i已不在手上

            //第step个盒子已经放置好扑克牌，走到下一个盒子面前
            dfs(step+1);

            //这里是非常重要的一步，一定要将刚才尝试的扑克牌收回，才能进行下一次尝试
            book[i]=0;
        }
    }

    return;

}

int main()
{
    dfs(1);//首先站在第一个盒子面前

    printf("total=%d",total/2);
    return 0;
}
```