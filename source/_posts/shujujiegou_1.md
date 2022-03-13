---
title: 数据结构之线性表
author: aogui
authorAbout: 一个有梦想的人
authorDesc: 一个有梦想的人
categories: 技术
comments: true
date: 2020-06-20 14:12:40
avatar: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585588339631&di=6fc163ee2519e0730db31973c2fd3a08&imgtype=0&src=http%3A%2F%2Fpic.38fan.com%2Fallimg%2F170619%2F51_170619104556_1.png
authorLink:
tags:
 - 数据结构
 - 学习
keywords: 线性表
description: 线性表学习
photos: https://cdn.jsdelivr.net/gh/aogui/source@v1.6.5/shujujiegou.jpg
---
## 一.顺序表
#1.静态分配
```c
#define Maxsize 100

typedef struct {
    int data[Maxsize];
    int length;
}Sqlist;

int main(){
    Sqlist L;
    L.length=0;
    int n,i=0;
    scanf("%d",&n);
    while(n!=999){
        L.data[i]=n;
        L.length=L.length+1;
        if(L.length==Maxsize)
            break;
        scanf("%d",&n);
        i++;
    }
    printf("输入数据为：");
    for(i=0;i<L.length;i++){
        printf("%d ",L.data[i]);
    }
    printf("\n顺序表长度为：%d ",L.length);
	return 0;
}
```

#2.动态分配
```c
#include<stdio.h>
#define InitSize 5

typedef struct{
    int *data;
    int MaxSize;
    int length;
}*Seqlist;

int main(){
    Seqlist L;
    InitList(L);    //
    int n,i=0;
    scanf("%d",&n);
    while(n!=999){
        L->data[i]=n;
        L->length++;
        if(L->length==L->MaxSize)
            IncreaseSize(L,5);
        scanf("%d",&n);
        i++;
    }
    printf("输入数据为：");
    for(i=0;i<L->length;i++){
        printf("%d ",L->data[i]);
    }
    printf("\n顺序表当前最大容量为：%d ",L->MaxSize);
    printf("\n顺序表长度为：%d ",(*L).length);//(*L).length这种用指针引用结构体变量成员的方式等价于L->length
    return 0;
}

void InitList(Seqlist L){
    L->data=(int *)malloc(InitSize*sizeof(int));
    L->MaxSize=InitSize;
    L->length=0;
}

void IncreaseSize(Seqlist L,int len){
    int *them=L->data;
    L->data=(int *)malloc((InitSize+len)*sizeof(int));
    for(int i=0;i<L->MaxSize;i++){
        L->data[i]=them[i];
    }
    L->MaxSize=L->MaxSize+len;
    free(them);
}
//也可用以下代码实现
/*
#include<stdio.h>
#define InitSize 5

typedef struct{
    int *data;
    int MaxSize;
    int length;
}Seqlist;

int main(){
    Seqlist L;
    InitList(&L);
    int n,i=0;
    scanf("%d",&n);
    while(n!=999){
        L.data[i]=n;
        L.length++;
        if(L.length==L.MaxSize)
            IncreaseSize(&L,5);
        scanf("%d",&n);
        i++;
    }
    printf("输入数据为：");
    for(i=0;i<L.length;i++){
        printf("%d ",L.data[i]);
    }
    printf("\n顺序表长度为：%d ",L.length);
    printf("顺序表当前最大容量为：%d\n",L.MaxSize);
    return 0;
}

void InitList(Seqlist *L){
    L->data=(int *)malloc(InitSize*sizeof(int));
    L->MaxSize=InitSize;
    L->length=0;
}

void IncreaseSize(Seqlist *L,int len){
    int *them=L->data;
    L->data=(int *)malloc((InitSize+len)*sizeof(int));
    for(int i=0;i<L->MaxSize;i++){
        L->data[i]=them[i];
    }
    L->MaxSize=L->MaxSize+len;
    free(them);
}
*/
```
可以输入以下数据进行验证。
1
2
3
4
5
6
999
输入数据为：1 2 3 4 5 6
顺序表当前最大容量为：10
顺序表长度为：6

#3.插入操作
```c
#define Maxsize 100

typedef struct {
    int data[Maxsize];
    int length;
}Sqlist;

int main(){
    Sqlist L;
    for(int i=0;i<10;i++){
        L.data[i]=i+1;
    }
    L.length=9;
    if(ListInsert(&L,2,10)==1){
        for(int i=0;i<L.length;i++){
            printf("%d ",L.data[i]);
        }
        printf("\nInsert succese");
    }
    else
        printf("Insert fail");
}
int ListInsert(Sqlist *L,int n,int e){
    if(n>L->length+1||n<1||L->length>=Maxsize){
        return 0;
    }
    else{
        for(int i=L->length;i>n-1;i--){
            L->data[i]=L->data[i-1];
        }
        L->data[n-1]=e;
        L->length++;
        return 1;
    }
}
```
运行结果
999 1 2 3 4 5 6 7 8 9
Insert succese

#4.查找操作
```c
#define Maxsize 100

typedef struct {
    int data[Maxsize];
    int length;
}Sqlist;

int main(){
    Sqlist L;
    for(int i=0;i<10;i++){
        L.data[i]=i+1;
    }
    L.length=9;
    int e;
    scanf("%d",&e);
    if(LocateElem(L,e)==0){
        printf("查找失败");
    }
    else
        printf("查找成功,所查数据为第%d位",LocateElem(L,e));
    return 0;
}

int LocateElem(Sqlist L,int e){
    for(int i=0;i<L.length;i++){
        if(L.data[i]==e)
            return i+1;
    }
    return 0;
}
```
运行结果
输入：
5
输出：
查找成功,所查数据为第5位

## 二.链表
#1.头插法建立单链表
```c
#include<stdio.h>

typedef struct LNode{
    int data;
    struct LNode *next;
}LNode,*LinkList;

LinkList List_HeadInsert();//将该函数声明为指针函数，返回值为创建链表的链头指针。(关键md)

int main(){
    LinkList L,head;
    head=List_HeadInsert(L);//接受返回链头指针
    printf("插入数据为：\n");
    while(head!=NULL){
        printf("%d ",head->next->data);
        head=head->next;
    }
    return 0;
}

LinkList List_HeadInsert(LinkList L){
    LNode *s;
    int x;
    L=(LinkList)malloc(sizeof(LNode));
    L->next=NULL;
    scanf("%d",&x);
    while(x!=999){
        s=(LNode *)malloc(sizeof(LNode));
        s->data=x;
        s->next=L->next;
        L->next=s;
        scanf("%d",&x);
    }
    return L;
}
```
运行结果
输入：
1 2 3 4 5 6 999
输出：
插入数据为：
6 5 4 3 2 1

#2.尾插法建立单链表
```c
#include<stdio.h>

typedef struct LNode{
    int data;
    struct LNode *next;
}LNode,*LinkList;

LinkList List_FailInsert();

int main(){
    LinkList L,head;
    head=List_FailInsert(L);
    printf("插入数据为：\n");
    while(head!=NULL){
        printf("%d ",head->next->data);
        head=head->next;
    }
    return 0;
}

LinkList List_FailInsert(LinkList L){
    LNode *s,*r;//r为表尾指针
    int x;
    L=(LinkList)malloc(sizeof(LNode));
    r=L;
    scanf("%d",&x);
    while(x!=999){
        s=(LNode *)malloc(sizeof(LNode));
        s->data=x;
        r->next=s;
        r=s;
        scanf("%d",&x);
    }
    r->next=NULL;//尾结点指针一定记得置空，不然没有结束输出的条件。
    return L;
}
```
运行结果
输入：
1 2 3 4 5 6 999
输出：
插入数据为：
1 2 3 4 5 6

#3.单链表数据查找
```c
#include<stdio.h>

typedef struct LNode{
    int data;
    struct LNode *next;
}LNode,*LinkList;

LinkList List_FailInsert();
LNode *GetElem();
LNode *LocateElem();

int main(){
    LinkList L,head;
    LNode *p,*q;
    int x,e;
    head=List_FailInsert(L);
    
	//按位查找
	printf("输入要查的位数:\n");
    scanf("%d",&x);
    p=GetElem(head,x);
    if(p==NULL)
        printf("查询数据不存在");
    else if(p==1)
        printf("所查数据为头结点");
    else
        printf("第%d位为:%d",x,p->data);



    //按值查找
    printf("\n输入要查的数:\n");
    scanf("%d",&e);
        q=LocateElem(head,e);
    if(q==NULL)
        printf("查询数据不存在");
    else
        printf("数据%d存在",q->data);
    return 0;
}

LinkList List_FailInsert(LinkList L){
    LNode *s,*r;//r为表尾指针
    int x;
    L=(LinkList)malloc(sizeof(LNode));
    r=L;
    scanf("%d",&x);
    while(x!=999){
        s=(LNode *)malloc(sizeof(LNode));
        s->data=x;
        r->next=s;
        r=s;
        scanf("%d",&x);
    }
    r->next=NULL;//尾结点指针一定记得置空，不然没有结束输出的条件。
    return L;
}

LNode *GetElem(LinkList L,int i){
    int j=1;
    LNode *p=L->next;
    if(i==0)
        return 1;
    if(i<0)
        return NULL;
    while(p!=NULL&&j<i){
        p=p->next;
        j++;
    }
    return p;
}

LNode *LocateElem(LinkList L,int i){
    LNode *p=L->next;
    while(p!=NULL&&p->data!=i){
        p=p->next;
    }
    return p;
}

```
运行结果
1 2 3 4 5 6 7 8 999
输入要查的位数:
6
第6位为:6
输入要查的数:
8
数据8存在
