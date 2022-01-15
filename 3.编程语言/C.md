# 语法基础

if 与 `#if` 区别

if runtime 运行时

`#if` compile 编译期

```c
struct Books
{
 char title[50];
 char author[50];
 char subject[100];
 int book\_id;
} book;
//定义结构体 并生命变量

struct\_pointer->title;//指针结构体访问通过：->

struct bs{
 int a:8;
 int b:2;
 int c:6;
}data; //位域 data 为 bs 变量，共占两个字节。其中位域 a 占 8 位，位域 b 占 2 位，位域 c 占 6 位

```

## 预处理 C Preprocessor
实际编译之前文本替换