---
title: 指针
date: 2024-03-15 22:59:03
categories:
- Go 学习笔记
tags:
- golang
---

## 指针概念

一个变量对应一个保存了变量对应类型值的内存空间。普通变量在声明语句创建时被绑定到一个变量名。比如叫 `x` 的变量，但是还有很多变量始终以表达式方式引入 例如 `x[i]` 或 `x.f`。所有这些表达式一般都是读取一个变量的值，除非他们是出现在赋值语句的左边，这时候是给对应变量赋予一个新的值。

一个指针的值是另一个变量的地址，一个指针对应变量在内存中的存储位置。通过指针我们可以直接读取或更新该变量的值，而不需知道该变量的名字（如果变量有名字的话）。

如果用 `var x int` 声明语句声明一个 `x` 变量，那么 `&x` 表达式（取x变量的内存地址）将产生一个指向该整数变量的指针，指针对应的数据类型是 `*int`，指针被称之为“指向int类型的指针”。如果指针名字为 `p`，那么可以说“ `p` 指针指向变量 `x` ”，或者说“ `p` 指针保存了 `x` 变量的内存地址”。同时 `*p` 表达式对应 `p` 指针指向的变量的值。一般 `*p` 表达式读取指针指向的变量的值，这里为 `int` 类型的值，同时因为 `*p` 对应一个变量，所以该表达式也可以出现在赋值语句的左边，表示更新指针所指向的变量的值。

```go
    x := 1
    p := &x         // p 的类型为 *int 指向变量 x
    fmt.Println(*p) // 1

    *p = 2         // 与 x = 2 等价
    fmt.Println(x) // 2
```

对于聚合类型的每个成员，比如结构的每个字段或者数组的每个元素也都是对应一个变量，因此可以被取值。

## 指针零值

任何类型的指针的零值都是 `nil`，如果 `p != nil` 测试成立，那么 `p` 指向某个有效变量。在使用指针时必须判断不是空指针否则会产生运行时 panic。

```go
    var p1 *int
    var p2 *int
    fmt.Println(*p1 + *p2)                  // panic: runtime error: invalid memory address or nil pointer dereference
```

## 指针比较

指针都为 `nil` 或者他们指向相同的变量时这两个指针相等。类型不同的指针不能比较，会报编译错误。

```go
    // 相等比较
    var p1 *int
    var p2 *int
    // var p3 *float32

    fmt.Println(p1, p2, &p1, &p2, p1 == p2) // <nil> <nil> 0xc000058028 0xc000058030 true

    // fmt.Println(p1 == p3) // invalid operation: p1 == p3 (mismatched types *int and *float32)
    x = 1
    p1 = &x
    p2 = &x
    fmt.Println(p1, p2, &p1, &p2, p1 == p2) // 0xc0000120d0 0xc0000120d0 0xc000058028 0xc000058030 true

```

## 闭包

在 Go 语言中，返回函数中局部变量的地址是安全的，调用函数 `f` 时创建局部变量 v，在局部变量地址被返回后仍然有效，因为指针 `p` 仍然使用这个变量，变量逃逸出函数 `f` 的作用域。

```go
var p = f()
func f() *int {
    v := 1
    return &v
}


fmt.Println(f() == f())
```

## 指针在 flag 包中的应用

```go
var n = flag.Bool("n", false, "omit trailing newline")

// 新建 bool 类型变量并将指针返回
func (f *FlagSet) Bool(name string, value bool, usage string) *bool {
    p := new(bool)
    f.BoolVar(p, name, value, usage)
    return p
}
```

`flag.Bool` 使用 `new` 创建变量并将变量地址返回