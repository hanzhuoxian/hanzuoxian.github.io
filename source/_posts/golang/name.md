---
title: 命名
date: 2023-11-28 19:34:27
categories:
- Go 学习笔记
tags:
- golang
- 命名
---

## 命名字符组成

Go 语言中的函数名、变量名、常量名、类型名、语句标号和包名等所有的命名，都遵循一个简单的命名规则：一个名字必须以一个字母（Unicode字母）或下划线开头，后面可以跟任意数量的字母、数字或下划线。名字的长度没有限制，尽量使用短小的名字。

```go
// 正确示例
姓名 := "娃哈哈"
name := "哇哈哈"
_name := "娃哈哈"
_name1 := "娃哈哈"
_name姓名 := "娃哈哈"

// 错误示例
1name := "娃哈哈"
```

## 命名大小写敏感

大写字母和小写字母是不同的：`heapSort`和`Heapsort`是两个不同的名字。

## 关键字不能用于自定义名字

关键字不能用于自定义的名字只能在特定的语法结构中使用，下面是所有关键字：

```go
break      default       func     interface   select
case       defer         go       map         struct
chan       else          goto     package     switch
const      fallthrough   if       range       type
continue   for           import   return      var
```

## 预定义名字可以使用，但不推荐

预定义的名字，包括内建常量、类型和函数；预定义名字可以重新使用，但是最好不要这么做。

```golang
// 内建常量
true false iota nil

// 内建类型
int int8 int16 int32 int64
uint uint8 uint16 uint32 uint64 uintptr
float32 float64 complex128 complex64
bool byte rune string error

// 内建函数
make len cap new append copy close delete
complex real imag
panic recover
```

## 可见性

如果名字是在函数内定义，那么只在函数内有效，如果是在函数外定义的，那么在当前包内的所有文件都可以访问。名字开头字母的大小写决定了在包外的可见性。如果一个名字是大写字母开头的那么就可以被外部的包访问。中文认为是小写字母，不能被导出

## 使用驼峰命名

当名字由几个单词组成时优先使用大小写分隔，而不是优先用下划线分隔。因此，在标准库有QuoteRuneToASCII和parseRequestLine这样的函数命名，但是一般不会用quote_rune_to_ASCII和parse_request_line这样的命名。而像ASCII和HTML这样的缩略词则避免使用大小写混合的写法，它们可能被称为htmlEscape、HTMLEscape或escapeHTML，但不会是escapeHtml。

## 编程规范

[顶层变量声明](https://github.com/xxjwxc/uber_go_guide_cn#%E9%A1%B6%E5%B1%82%E5%8F%98%E9%87%8F%E5%A3%B0%E6%98%8E)
[本地变量声明](https://github.com/xxjwxc/uber_go_guide_cn#%E6%9C%AC%E5%9C%B0%E5%8F%98%E9%87%8F%E5%A3%B0%E6%98%8E)
[函数名](https://github.com/xxjwxc/uber_go_guide_cn#%E5%87%BD%E6%95%B0%E5%90%8D)
[错误命名](https://github.com/xxjwxc/uber_go_guide_cn#%E9%94%99%E8%AF%AF%E5%91%BD%E5%90%8D)
[包名](https://github.com/xxjwxc/uber_go_guide_cn#%E5%8C%85%E5%90%8D)

## 参考

[Uber Go 语言编码规范](https://github.com/xxjwxc/uber_go_guide_cn)，by Uber
