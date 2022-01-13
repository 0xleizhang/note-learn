# 基础

## 背景知识
[理解结构体：](https://juejin.im/post/6844903814168838151)

[理解指针：](https://studygolang.com/articles/7412)

[基础语法](https://juejin.im/post/6844903585252278279#heading-1)

## 基础语法

### 包
main main方法包名定义程序入库

[init 函数](https://zhuanlan.zhihu.com/p/34211611)

[可见性](https://studygolang.com/articles/6212)

### 函数

#### 多返回值
func swap(x, y string) (string, string) {

 return y, x

}

实现原理：将函数结果压入栈中 而不是存入寄存器。

#### 方法与指针重定向
\`\`\`
var v Vertex
v.Scale(5) // OK
p := &v
p.Scale(10) // OK
 // v.Scale(5) 解释为 (&v).Scale(5)

var v Vertex
fmt.Println(v.Abs()) // OK
p := &v
fmt.Println(p.Abs()) // OK
//p.Abs() 会被解释为 (\*p).Abs()。
\`\`\`

### 单元测试

[test语法](https://codeplayer.vip/p/j7tek)

##

## 语言核心

### 数据结构

#### 切片

#### map

### 语言特性

#### 反射

#### new 与 make

\- \`make\` 的作用是初始化内置的数据结构，也就是我们在前面提到的切片、哈希表和 Channel[2](https://draveness.me/golang/docs/part2-foundation/ch05-keyword/golang-make-and-new/#fn:2)；
\- \`new\` 的作用是根据传入的类型分配一片内存空间并返回指向这片内存空间的指针[3](https://draveness.me/golang/docs/part2-foundation/ch05-keyword/golang-make-and-new/#fn:3)；

new的过程中涉及逃逸分析，如果未逃逸分配在栈上

make 只能是 slice，map,channel

### 标准库

## 错误处理

## 并发编程

# 运行时

## 内存分配

## 并发调度

##

## 垃圾回收

# 工具链

## 代码分析

## 依赖管理

[go mod](https://juejin.im/post/6844903798658301960)

## 编译技术

# 生态库

## web框架
[echo](https://echo.labstack.com/)

### 中间件
 函数式编程 闭包 类似于React中的高阶组件

## 数据库驱动