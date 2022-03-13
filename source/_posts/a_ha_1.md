---
title: 啊哈！算法之排序
author: aogui
avatar: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585588339631&di=6fc163ee2519e0730db31973c2fd3a08&imgtype=0&src=http%3A%2F%2Fpic.38fan.com%2Fallimg%2F170619%2F51_170619104556_1.png
authorLink: 
authorAbout: 一个有梦想的人
authorDesc: 一个有梦想的人
categories: 转载
date: 2020-04-10 20:02:32
comments: true
tags:
 - 算法
 - 学习
keywords: 排序
description: 三种排序对比
photos: https://cdn.jsdelivr.net/gh/aogui/source@v1.6/aha1.png
---
## 1.最快最简单的排序——桶排序
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6/101.png)
```c
#include <stdio.h>
int main()
{
	int book[1001],i,j,t,n;
	for(i=0;i<=1000;i++)
		book[i]=0;
	scanf("%d",&n);//输入一个数n，表示接下来有n个数
	for(i=1;i<=n;i++)//循环读入n个数，并进行桶排序
	{
		scanf("%d",&t); //把每一个数读到变量t中
		book[t]++; //进行计数，对编号为t的桶放一个小旗子
	}
	for(i=1000;i>=0;i--) //依次判断编号1000~0的桶
		for(j=1;j<=book[i];j++) //出现了几次就将桶的编号打印几次
			printf("%d ",i);
	getchar();getchar();
	//这里的getchar();用来暂停程序，以便查看程序输出的内容
	//也可以用system("pause");等来代替
	return 0;
}
```
可以输入以下数据进行验证。
10
8 100 50 22 15 6 1 1000 999 0
运行结果是：
1000 999 100 50 22 15 8 6 1 0
## 2.邻居好说话——冒泡排序
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6/102.png)
```c
#include <stdio.h>
struct student
{
	char name[21];
	char score;
};//这里创建了一个结构体用来存储姓名和分数
int main()
{
	struct student a[100],t;
	int i,j,n;
	scanf("%d",&n); //输入一个数n
	for(i=1;i<=n;i++) //循环读入n个人名和分数
		scanf("%s %d",a[i].name,&a[i].score);
	//按分数从高到低进行排序
	for(i=1;i<=n-1;i++)
	{
		for(j=1;j<=n-i;j++)
		{
			if(a[j].score<a[j+1].score)//对分数进行比较
			{ t=a[j]; a[j]=a[j+1]; a[j+1]=t; }
		}
	}
	for(i=1;i<=n;i++)//输出人名
		printf("%s\n",a[i].name);
	getchar();getchar();
	return 0;
}
```
可以输入以下数据进行验证。
5
huhu 5
haha 3
xixi 5
hengheng 2
gaoshou 8
运行结果是：
gaoshou
huhu
xixi
haha
hengheng
## 3.最常用的排序——快速排序
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6/103.png)
```c
#include <stdio.h>
int a[101],n;//定义全局变量，这两个变量需要在子函数中使用
void quicksort(int left,int right)
{
	int i,j,t,temp;
	if(left>right)
		return;
	temp=a[left]; //temp中存的就是基准数
	i=left;
	j=right;
	while(i!=j)
	{
		//顺序很重要，要先从右往左找
		while(a[j]>=temp && i<j)
			j--;
		//再从左往右找
		while(a[i]<=temp && i<j)
			i++;
		//交换两个数在数组中的位置
		if(i<j)//当哨兵i和哨兵j没有相遇时
		{
			t=a[i];
			a[i]=a[j];
			a[j]=t;
		}
	}
	//最终将基准数归位
	a[left]=a[i];
	a[i]=temp;
	quicksort(left,i-1);//继续处理左边的，这里是一个递归的过程
	quicksort(i+1,right);//继续处理右边的，这里是一个递归的过程
}
int main()
{
	int i,j,t;
	//读入数据
	scanf("%d",&n);
	for(i=1;i<=n;i++)
		scanf("%d",&a[i]);
	quicksort(1,n); //快速排序调用
	//输出排序后的结果
	for(i=1;i<=n;i++)
		printf("%d ",a[i]);
	getchar();getchar();
	return 0;
}
```
可以输入以下数据进行验证。
10
6 1 2 7 9 3 4 5 10 8
运行结果是：
1 2 3 4 5 6 7 8 9 10