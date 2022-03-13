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
    int flag=0;
    ListInsert(&L,10,10,&flag);
    if(flag==1){
        for(int i=0;i<L.length;i++){
            printf("%d ",L.data[i]);
        }
        printf("\n插入成功");
    }
    else
        printf("插入失败");
}
void ListInsert(Sqlist *L,int n,int e,int *flag){
    if(n>L->length+1||n<1||L->length>=Maxsize){
        return 0;
    }
    else{
        for(int i=L->length;i>n-1;i--){
            L->data[i]=L->data[i-1];
        }
        L->data[n-1]=e;
        L->length++;
        (*flag)++;
        return 0;
    }
}
```