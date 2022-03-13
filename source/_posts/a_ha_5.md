---
title: 啊哈！算法之枚举
author: aogui
avatar: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585588339631&di=6fc163ee2519e0730db31973c2fd3a08&imgtype=0&src=http%3A%2F%2Fpic.38fan.com%2Fallimg%2F170619%2F51_170619104556_1.png
authorLink: 
authorAbout: 一个有梦想的人
authorDesc: 一个有梦想的人
categories: 转载
date: 2020-04-15 21:51:55
comments: true
tags:
 - 算法
 - 学习
keywords: 图 遍历
description: 图的遍历
photos: https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/aha5.png
---
## 1.图的深度优先遍历
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/501.png)
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/502.png)
```c
#include <stdio.h>
int book[101],sum,n,e[101][101];
void dfs(int cur)//cur是当前所在的顶点编号
{
    int i;
    printf("%d ",cur);
    sum++;//每访问一个顶点sum就加1
    if(sum==n)
        return;//所有顶点都已经访问过则直接退出
    for(i=1;i<=n;i++)//从1号顶点到n号顶点依次尝试，看哪些顶点与当前顶点cur有边相连
    {
        //判断当前顶点cur到顶点i是否有边，及顶点i是否已经访问过
        if(e[cur][i]==1 && book[i]==0)
        {
            book[i]=1;//标记顶点i已经访问过
            dfs(i);//从顶点i再出发继续遍历
        }
    }
    return;
}
int main()
{
    int i,j,m,a,b;
    scanf("%d %d",&n,&m);
    //初始化二维矩阵
    for(i=1;i<=n;i++)
    {
        for(j=1;j<=n;j++)
        {
             if(i==j)
                e[i][j]=0;
            else
                e[i][j]=9999999;//这里假设9999999为正无穷
        }
    }

    //读入顶点之间的边
    for(i=1;i<=m;i++)
    {
        scanf("%d %d",&a,&b);
        e[a][b]=1;
        e[b][a]=1;//这里是无向图，所以也为1
    }

    //从1号城市出发
    book[1]=1;//标记1号顶点已经访问
    dfs(1);//从1号顶点开始遍历

    getchar();getchar();
    return 0;
}
```
输入验证：
5 5
1 2
1 3
1 5
2 4
3 5
运行结果：
1 2 3 4 5

## 2.图的广度优先遍历
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.3/503.png)
```c
#include <stdio.h>
int main()
{
    int i,j,n,m,a,b,cur,book[101]={0},e[101][101];
    int que[10001],head,tail;
    scanf("%d %d",&n,&m);
    //初始化二维矩阵
    for(i=1;i<=n;i++)
        for(j=1;j<=n;j++)
            if(i==j)
                e[i][j]=0;
            else
                e[i][j]=9999999;

    //读入顶点之间的边
    for(i=1;i<=m;i++)
    {
        scanf("%d %d",&a,&b);
        e[a][b]=1;
        e[b][a]=1;
    }

    //队列初始化
    head=1;
    tail=1;

    //从1号顶点出发，将1号顶点加入队列
    que[tail]=1;
    tail++;
    book[1]=1;//标记1号顶点已访问

    //当前队列不为空的时候循环
    while(head<tail)
    {
        cur=que[head];//当前正在访问的顶点编号
        for(i=1;i<=n;i++)//从1~n依次尝试
        {
            //判断从顶点cur到顶点i是否有边，及顶点i是否已经访问过
            if(e[cur][i]==1&&book[i]==0)
            {
                //如果从顶点cur到i有边，并且顶点i没有被访问过，则将顶点i入队
                que[tail]=i;
                tail++;
                book[i]=1;//标记顶点i已访问
            }
            //如果tail大于n,则表明所有顶点都已经被访问过
            if(tail>n)
            {
                break;
            }
        }
        head++;//注意这地方，千万不能忘记当一个顶点扩展结束后，head++,然后才能继续往下扩展
    }

    for(i=1;i<tail;i++)
        printf("%d ",que[i]);

    getchar();getchar();
    return 0;
}
```
输入验证：
5 5
1 2
1 3
1 5
2 4
3 5
运行结果：
1 2 3 5 4