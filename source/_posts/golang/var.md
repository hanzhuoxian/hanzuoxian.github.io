---
title: 变量
date: 2023-11-28 22:59:03
categories:
- Go 学习笔记
tags:
- golang
---

## 什么是变量

变量是指一个抽象的存储地址，它含有被称为一个值的某种已知或未知信息量，并且配对了关联的符号名称（变量名）。变量的主要作用是代表数据，让程序设计者在编写代码时无需关心具体的数值，只需要通过这个符号来操作数据。

## 变量声明

`var` 声明语句可以创建一个特定类型的变量。变量声明的一般语法如下：

```go
var 变量名 类型 = 初始值
```

类型或者初始值可以省略，如果只强调类型不关心初始值那么就省略初始值，Go 语言会使用零值初始化。如果有明确的初始值那么可以省略类型 Go 语言会自动推导变量类型

|类型|零值|
|-----|------|
|数值类型|0|
|字符串|""|
|布尔类型|false|
|接口|nil|
|引用类型（slice、map、chan、func）|nil|
|数组|对应类型的0值|
|结构体|结构体字段对应的0值|

```go
package main

import (
	"fmt"
)

func main() {
	var defaultInt int64
	var defaultString string
	var defaultBool bool
	var defaultSlice []int
	var defaultMap map[string]int
	var defaultChan chan int
	var defaultFunc func()
	var defaultInterface interface{}
	var defaultArray [3]int
	var defaultStruct struct{ name string }
	fmt.Println(defaultInt)
	fmt.Println(defaultString)
	fmt.Println(defaultBool)
	fmt.Println(defaultSlice == nil)
	fmt.Println(defaultMap == nil)
	fmt.Println(defaultChan)
	fmt.Println(defaultFunc)
	fmt.Println(defaultInterface)
	fmt.Println(defaultArray)
	fmt.Println(defaultStruct)
}

```

输出

```bash
0

false
true
map[]
<nil>
<nil>
<nil>
[0 0 0]
{}
```

可以声明一组变量

```go
var i, j, k int                 // int, int, int
var b, f, s = true, 2.3, "four" // bool, float64, string
```

## 简短变量声明

在函数内部，有一种称为简短变量声明语句的形式可用于声明和初始化局部变量。它以 `name := value` 的形式声明变量，变量的类型根据表达式来自动推导。

简短变量的组声明

```go
i, j := 0, 1
```

声明和赋值的区别：声明会分配内存空间，赋值只是改变内存空间的值。


## new 函数

另一个创建变量的方法是调用内建的`new`函数。表达式`new(T)`将创建一个`T`类型的匿名变量，初始化为`T`类型的零值，然后返回变量地址，返回的指针类型为`*T`。

## 变量生命周期

变量生命周期指的是变量在程序运行期间存在的有效时间段。对于包一级变量来说他们和程序的运行周期是一致的。对于局部变量来说，每次从创建一个变量的声明语句开始，直到不在引用这个变量为止，然后变量的存储空间可能会被回收。对于局部变量来说存在逃逸为全局变量。

## 变量作用域

一个声明语句将程序中的实体和一个名字关联，比如一个函数或一个变量。声明语句的作用域是指源代码中可以有效使用这个名字的范围。

不要将作用域和生命周期混为一谈。声明语句的作用域对应的是一个源代码的文本区域；它是一个编译时的属性。一个变量的生命周期是指程序运行时变量存在的有效时间段，在此时间区域内它可以被程序的其他部分引用；是一个运行时的概念。

句法块：由花括号包含的一些列语句，句法块内部声明的名字是无法被外部块访问的。
词法块：虽然没有括号包含，但是他们是一个声明群组。全局的源代码在一个全局词法块中。对于每个包，每个 for、if 和 switch 语句 也都有对应的词法块。每个 switch 和 select 的分支也有独立的词法块。