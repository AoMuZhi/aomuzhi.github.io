---
title: 啊哈！算法之栈、队列、链表
author: aogui
avatar: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585588339631&di=6fc163ee2519e0730db31973c2fd3a08&imgtype=0&src=http%3A%2F%2Fpic.38fan.com%2Fallimg%2F170619%2F51_170619104556_1.png
authorLink: 
authorAbout: 一个有梦想的人
authorDesc: 一个有梦想的人
categories: 转载
date: 2020-04-13 23:03:48
comments: true
tags:
 - 算法
 - 学习
keywords: 栈 队列 链表
description: 栈 队列 链表
photos: https://cdn.jsdelivr.net/gh/aogui/source@v1.6.2/aha2.png
---
## 1.解密 QQ 号——队列
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.2/201.png)
```c
#include <stdio.h>
int main()
{
	int q[102]={0,6,3,1,7,5,8,9,2,4},head,tail;
	int i;
	//初始化队列
	head=1;
	tail=10; //队列中已经有9个元素了，tail指向队尾的后一个位置
	while(head<tail) //当队列不为空的时候执行循环
	{
		//打印队首并将队首出队
		printf("%d ",q[head]);
		head++;
		//先将新队首的数添加到队尾
		q[tail]=q[head];
		tail++;
		//再将队首出队
		head++;
	}
	getchar();getchar();
	return 0;
}
```
最后的输出就是 6 1 5 9 4 7 2 8 3
下面这段代码是使用结构体来实现的队列操作:
```c
#include <stdio.h>
struct queue
{
	int data[100];//队列的主体，用来存储内容
	int head;//队首
	int tail;//队尾
};
int main()
{
	struct queue q;
	int i;
	//初始化队列
	q.head=1;
	q.tail=1;
	for(i=1;i<=9;i++)
	{
		//依次向队列插入9个数
		scanf("%d",&q.data[q.tail]);
		q.tail++;
	}
	while(q.head<q.tail) //当队列不为空的时候执行循环
	{
		//打印队首并将队首出队
		printf("%d ",q.data[q.head]);
		q.head++;
		//先将新队首的数添加到队尾
		q.data[q.tail]=q.data[q.head];
		q.tail++;
		//再将队首出队
		q.head++;
	}
	getchar();getchar();
	return 0;
}
```
## 2.解密回文——栈
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.2/202.png)
```c
#include <stdio.h>
#include <string.h>
int main()
{
	char a[101],s[101];
	int i,len,mid,next,top;
	gets(a); //读入一行字符串
	len=strlen(a); //求字符串的长度
	mid=len/2-1; //求字符串的中点
	top=0;//栈的初始化
	//将mid前的字符依次入栈
	for(i=0;i<=mid;i++)
		s[++top]=a[i];
	//判断字符串的长度是奇数还是偶数，并找出需要进行字符匹配的起始下标
	if(len%2==0)
		next=mid+1;
	else
		next=mid+2;
	//开始匹配
	for(i=next;i<=len-1;i++)
	{
		if(a[i]!=s[top])
			break;
		top--;
	}
	//如果top的值为0，则说明栈内所有的字符都被一一匹配了
	if(top==0)
		printf("YES");
	else
		printf("NO");
	getchar();getchar();
	return 0;
}
```
可以输入以下数据进行验证。
ahaha
运行结果是：
YES
## 3.链表
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.2/203.png)
```c
#include <stdio.h>
#include <stdlib.h>
//这里创建一个结构体用来表示链表的结点类型
struct node
{
	int data;
	struct node *next;//下一个结点的类型也是 struct node，所以这个指针的类型也必须是 struct node
* 类型的指针
};
int main()
{
	struct node *head,*p,*q,*t;
	int i,n,a;
	scanf("%d",&n);
	head = NULL;//头指针初始为空
	for(i=1;i<=n;i++)//循环读入n个数
	{
		scanf("%d",&a);
		//动态申请一个空间，用来存放一个结点，并用临时指针p指向这个结点
		p=(struct node *)malloc(sizeof(struct node));
		p->data=a;//将数据存储到当前结点的data域中
		p->next=NULL;//设置当前结点的后继指针指向空，也就是当前结点的下一个结点为空
		if(head==NULL)
			head=p;//如果这是第一个创建的结点，则将头指针指向这个结点
		else
			q->next=p;//如果不是第一个创建的结点，则将上一个结点的后继指针指向当前结点
		q=p;//指针q也指向当前结点
	}
	//输出链表中的所有数
	t=head;
	while(t!=NULL)
	{
		printf("%d ",t->data);
		t=t->next;//继续下一个结点
	}
	getchar();getchar();
	return 0;
}
```
可以输入以下数据进行验证。
9
2 3 5 8 9 10 18 26 32
运行结果是：
2 3 5 8 9 10 18 26 32

malloc 函数：
malloc 函数的作用就是从内存中申请分配指定字节大小的内存空间。上面这行代码就申
请了 4 个字节。如果你不知道 int 类型是 4 个字节的，还可以使用 sizeof(int)获取
int 类型所占用的字节数，如下：
malloc(sizeof(int));
现在你已经成功地从内存中申请了 4 个字节的空间来准备存放一个整数，可是如何来
对这个空间进行操作呢？这里我们就需要用一个指针来指向这个空间，即存储这个空间的
首地址。
int *p;
p=(int *)malloc(sizeof(int));
需要注意，malloc 函数的返回类型是 void * 类型。void * 表示?确定类型的指针。在 C
和 C++中，void * 类型可以强制转换为任何其他类型的指针。上面代码中我们将其强制转化
为整型指针，以便告诉计算机这里的 4 个字节作为一个整体用来存放整数。还记得我们之前
遗留了一个问题：指针就是用来存储内存地址的，为什么要分不同类型的指针呢？因为指针
变量存储的是一个内存空间的首地址（第一个字节的地址），但是这个空间占用了多少个字
节，用来存储什么类型的数，则是由指针的类型来标明的。这样系统才知道应该取多少个连
续内存作为一个数据。
![image](https://cdn.jsdelivr.net/gh/aogui/source@v1.6.2/204.png)
```c
#include <stdio.h>
#include <stdlib.h>
//这里创建一个结构体用来表示链表的结点类型
struct node
{
	int data;
	struct node *next;
};
int main()
{
	struct node *head,*p,*q,*t;
	int i,n,a;
	scanf("%d",&n);
	head = NULL;//头指针初始为空
	for(i=1;i<=n;i++)//循环读入n个数
	{
		scanf("%d",&a);
		//动态申请一个空间，用来存放一个结点，并用临时指针p指向这个结点
		p=(struct node *)malloc(sizeof(struct node));
		p->data=a;//将数据存储到当前结点的data域中
		p->next=NULL;//设置当前结点的后继指针指向空，也就是当前结点的下一个结点为空
		if(head==NULL)
			head=p;//如果这是第一个创建的结点，则将头指针指向这个结点
		else
			q->next=p;//如果不是第一个创建的结点，则将上一个结点的后继指针指向当前结点
		q=p;//指针q也指向当前结点
	}
	scanf("%d",&a);//读入待插入的数
	t=head;//从链表头部开始遍历
	while(t!=NULL)//当没有到达链表尾部的时候循环
	{
		if(t->next->data > a)//如果当前结点下一个结点的值大于待插入数，将数插入到中间
		{
			p=(struct node *)malloc(sizeof(struct node));//动态申请一个空间，
			用来存放新增结点
			p->data=a;
			p->next=t->next;//新增结点的后继指针指向当前结点的后继指针所指向的结点
			t->next=p;//当前结点的后继指针指向新增结点
			break;//插入完毕退出循环
		}
		t=t->next;//继续下一个结点
	}
	//输出链表中的所有数
	t=head;
	while(t!=NULL)
	{
		printf("%d ",t->data);
		t=t->next;//继续下一个结点
	}
	getchar();getchar();
	return 0;
}
```
可以输入以下数据进行验证。
9
2 3 5 8 9 10 18 26 32
6
运行结果是：
2 3 5 6 8 9 10 18 26 32