---
title: 变量
date: 2023-11-28 22:59:03
categories:
- Go 学习笔记
tags:
- golang
---

声明语句定义了程序的各种实体对象以及部分或全部的属性。Go 语言的声明有：`var`、`const`、`type`和`func`，分别对应变量、常量、类型和函数实体对象的声明。

### 变量声明

`var` 声明语句可以创建一个特定类型的变量。变量声明的一般语法如下：

```go
var 变量名 类型 = 初始值
```

类型或者初始值可以省略，如果只强调类型不关心初始值那么久省略初始值，Go 语言会使用零值初始化。如果有明确的初始值那么可以省略类型 Go 语言会自动推导变量类型

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