---
title: 啊哈！算法之枚举
author: aogui
avatar: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585588339631&di=6fc163ee2519e0730db31973c2fd3a08&imgtype=0&src=http%3A%2F%2Fpic.38fan.com%2Fallimg%2F170619%2F51_170619104556_1.png
authorLink: 
authorAbout: 一个有梦想的人
authorDesc: 一个有梦想的人
categories: 转载
comments: true
date: 2020-04-15 22:01:16
comments: true
tags:
 - 算法
 - 学习
keywords: 最短路径
description: 最短路径
photos: https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/aha6.png
---
## 1.最短路径之Floyd
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/601.png)
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/602.png)
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/603.png)
```c
#include <stdio.h>
int main()
{
    int e[10][10],k,i,j,n,m,t1,t2,t3;
    int inf=999999;//用inf(infinity的缩写)存储一个我们认为的正无穷值
    //读入n和m,n表示顶点个数，m表示边的条数
    scanf("%d %d",&n,&m);

    //初始化
    for(i=1;i<=n;i++)
        for(j=1;j<=n;j++)
            if(i==j)
                e[i][j]=0;
            else
                e[i][j]=inf;
    //读入边
    for(i=1;i<=m;i++)
    {
        scanf("%d %d %d",&t1,&t2,&t3);
        e[t1][t2]=t3;
    }

    //Floyd-Warshall算法核心语句
    for(k=1;k<=n;k++)
        for(i=1;i<=n;i++)
            for(j=1;j<=n;j++)
                if(e[i][k]<inf && e[k][j]<inf && e[i][j]>e[i][k]+e[k][j])
                    e[i][j]=e[i][k]+e[k][j];

    //输出最终结果
    for(i=1;i<=n;i++)
    {
        for(j=1;j<=n;j++)
        {
            printf("%10d",e[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```
输入：
4 8
1 2 2
1 3 6
1 4 4
2 3 3
3 1 7
3 4 1
4 1 5
4 3 12
输出：
         0         2         5         4
         9         0         3         4
         6         8         0         1
         5         7        10         0
## 2.最短路径之Dijkstra
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/604.png)
```c
#include <stdio.h>
int main()
{
    int e[10][10],dis[10],book[10],i,j,n,m,t1,t2,t3,u,v,min;
    int inf=9999999;//用inf(infinity的缩写)存储一个我们认为的正无穷值
    //读入n和m,n表示顶点个数，m表示边的条数
    scanf("%d %d",&n,&m);

        //初始化
    for(i=1;i<=n;i++)
        for(j=1;j<=n;j++)
            if(i==j)
                e[i][j]=0;
            else
                e[i][j]=inf;
    //读入边
    for(i=1;i<=m;i++)
    {
        scanf("%d %d %d",&t1,&t2,&t3);
        e[t1][t2]=t3;
    }

    //初始化dis数组，这里是1号顶点到其余各个顶点的初始化路程
    for(i=1;i<=n;i++)
        dis[i]=e[1][i];

    //book数组初始化
    for(i=1;i<=n;i++)
        book[i]=0;
    book[1]=1;

    //Dijkstra算法核心语句
    for(i=1;i<=n-1;i++)
    {
        //找到离1号顶点最近的顶点
        min=inf;
        for(j=1;j<=n;j++)
        {
            if(book[j]==0 && dis[j]<min)
            {
                min=dis[j];
                u=j;
            }
        }
        book[u]=1;
        for(v=1;v<=n;v++)
        {
            if(e[u][v]<inf)
            {
                if(dis[v]>dis[u]+e[u][v])
                    dis[v]=dis[u]+e[u][v];
            }
        }
    }

    //输出最终的结果
    for(i=1;i<=n;i++)
        printf("%d ",dis[i]);

    getchar();
    getchar();
    return 0;
}
```
单源最短路径
输入：
6 9
1 2 1
1 3 12
2 3 9
2 4 3
3 5 5
4 3 4
4 5 13
4 6 15
5 6 4
输出：
0 1 8 4 13 17
## 3.最短路径算法对比分析
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/605.png)