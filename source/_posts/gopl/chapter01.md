---
title: 01 入门
date: 2023-10-19 13:32:12
categories:
- Go 语言圣经
tags:
- golang
- gopl
---

本章介绍 `Go` 语言的基础组件。本章提供了足够的信息和示例程序，希望可以帮你们尽快入门，写出有用的程序。本章和之后章节的示例程序都针对你可能遇到的现实案例。先了解几个 `Go` 程序涉及的主题从简单的文件处理、图像处理到互联网客户端和服务端并发。当然第一章不会解释细枝末节，但用这些程序来学习一门新语言还是很有效的。

学习一门新语言时，会有一种自然的倾向，按照自己熟悉的语言套路写新语言程序，学习 `Go` 语言的过程中，请警惕这种想法，尽量别这么做。我们会演示怎么写好 `Go` 语言程序，所以请用本书的代码作为你写程序时的指南。

## 1.1 Hello World

我们现在以传统的 ”Hello World“ 来开始吧，这个例子首次出现于 1978 年出版的 《The C Programming Language》。`C` 语言是直接影响 `Go` 语言设计的语言之一，这个例子体现了 `Go` 语言的一些核心理念。

我们使用 `go mod` 模式，我们本书的基础目录为 `github.com/hanzhuoxian/study/go/gopl` ，在当前目录下执行  `go mod init github.com/hanzhuoxian/study/go/gopl`,新建目录 `mkdir ch01/helloworld`，在 helloworld 目录下，新建文件 `helloword.go`,文件内容如下：

*github.com/hanzhuoxian/study/go/gopl/ch01/helloworld/helloword.go*

```go
// 声明包

package main

// 导入标准I/O包
import "fmt"

// 程序的入口方法
func main() {
	fmt.Println("Hello，世界")
}

```

`Go` 语言是一门编译型语言，`Go` 语言的工具链将源代码及其依赖转化成计算机的机器指令。`Go` 语言提供的工具都通过单独的命令 `go` 调用，`go` 有一系列子命令。最简单的一个子命令就是 `run` 。这个命令编译一个或多个以 `.go` 结尾的源文件、链接库文件，并运行最终生成的可执行文件（本书使用 $ 表示命令提示符）。

```bash
$ go run helloworld.go
```

毫无意外，这个命令会输出

```bash
Hello，世界
```

`Go` 语言原生支持 Unicode，它可以处理全世界任何语言的文本。
如果不只是一次性实验，你肯定希望能编译这个程序，保存编译结果以备将来之用。可以用 `build` 子命令。

```bash
$ go build helloworld.go
```

这个命令生成一个名为 `helloworld` 的可执行的二进制文件。之后你可以随时运行它，不需任何处理。

```bash
$ ./helloworld
Hello，世界
```

本书中所有示例代码上都有一行标记，利用这些标记可以从 `github.com` 代码仓库中获取代码

```bash
https://github.com/hanzhuoxian/study
```

执行 `git clone https://github.com/hanzhuoxian/study` 命令，就可以将代码下载到本地。

来讨论下程序本身。`Go` 语言代码通过包（package）组织，包类似于其他语言里的库（libraries）或者模块（modules）。一个包由位于单个目录下的一个或多个 `.go` 源代码文件组成，目录定义包的作用。每个源文件都以一条 `package` 语句声明开始，这个例子里就是 `package main` ,表示该文件属于那个包，紧跟着一系列导入（`import`）的包，之后是存储在这个文件里的程序语句。

`Go` 标准库提供了 100 多个包，以支持常见功能，如输入、输出、排序以及文本处理。比如 `fmt` 包就含有格式化输出、接受输入的函数。`Println` 是其中一个基础函数，可以打印以逗号间隔的一个或多个值，并在最后添加一个换行符，从而输出一整行。

`main` 包比较特殊。它定义了一个独立可执行的程序，而不是一个库，在 `main` 包里的 `main` 函数也很特殊，它是整个程序执行时的入口。`main` 函数所做的事情就是程序做的，当然了，`main` 函数一般调用其他包里的函数完成很多工作（如 `fmt.Println`）。

必须告诉编译器源文件需要哪些包，这就是跟随在 `package` 声明后面的 `import` 扮演的角色。hello world 例子只用到了一个包，大多数程序需要导入多个包。

必须恰当导入需要的包，缺少了必要的包或者导入了不需要的包，程序都无法编译通过。这项严格要求避免了程序开发过程中引入未使用的包。

`import` 声明必须跟在文件的 `package` 声明之后。随后，则是组成程序的函数、变量、常量、类型的声明语句（分别由关键字 `func` 、`var` 、`const` 、`type` 定义）。这些内容的声明顺序并不重要。这个例子的程序已经尽可能短了，只声明了一个函数，其中只调用了一个其他函数。为了节省篇幅，有些时候示例程序会省略 `package` 和 `import`  声明，但是这些声明在源代码里有，并且必须得有才能编译。

一个函数的声明由 `func` 关键字、函数名、参数列表、返回值列表（这个例子里的 `main` 函数参数列表和返回值都是空的）以及包含在大括号里的函数体组成。第五章进一步考察函数。

`Go` 语言不需要在语句或者声明的末尾添加分号，除非一行上有多条语句。实际上，编译器会主动把特定符号后的换行符转换为分号，因此换行符添加的位置会影响 `Go` 代码的正确解析（译注：比如行末是标识符、整数、浮点数、虚数、字符或字符串文字、关键字 `break`、`continue`、`fallthrough`或 `return` 中的一个、运算符和分隔符 `++`、`--`、`)`、`]` 或 `}` 中的一个）。举个例子，函数的左括号 `{` 必须和 `func` 函数声明在同一行上，且位于末尾，不能独占一行，而在表达式 `x+y` 中，可在 `+` 后换行，不能在 `+` 前换行（译注：以+结尾的话不会被插入分号分隔符，但是以 x 结尾的话则会被分号分隔符，从而导致编译错误）。

`Go` 语言在代码格式上采取了很强硬的态度。`gofmt`工具把代码格式化为标准格式（译注：这个格式化工具没有任何可以调整代码格式的参数，`Go` 语言就是这么任性），并且 `go` 工具中的 `fmt` 子命令会对指定包，否则默认为当前目录中所有go 源文件应用 `gofmt` 命令。本书中的所有代码都被 gofmt 过。你也应该养成格式化自己的代码的习惯。以法令方式规定标准的代码格式可以避免无尽的无意义的琐碎争执（译注：也导致了 `Go` 语言的 TIOBE 排名较低，因为缺少撕逼的话题）。更重要的是，这样可以做多种自动源码转换，如果放任 `Go` 语言代码格式，这些转换就不大可能了。

很多文本编辑器都可以配置为保存文件时自动执行 `gofmt`，这样你的源代码总会被恰当地格式化。还有个相关的工具：`goimports`，可以根据代码需要，自动地添加或删除 `import` 声明。这个工具并没有包含在标准的分发包中，可以用下面的命令安装：

```bash
$ go install golang.org/x/tools/cmd/goimports@latest
```

对于大多数用户来说，下载、编译包、运行测试用例、查看 `Go` 语言的文档等等常用功能都可以用 go 的工具完成 10.7 详细介绍这些知识。

## 1.2 命令行参数

大多数程序都是处理输入，产生输出；这也正是计算的定义。但是程序如何获取要输入的数据呢？一些程序生成自己的数据，但通常情况下、输入来自于程序外部：文件、网络、连接、其他程序的输出、敲击前盘的用户、命令行参数或其他输入源。下面几个例子会讨论其中几个输入源，首先是命令行参数。

`os` 包以跨平台的方式，提供了一些与操作系统交互的函数和变量。程序的命令行参数可以从 `os` 包的 `Args` 变量获取。`os` 包外部使用 `os.Args` 访问该变量。

`os.Args` 变量是一个一个字符串（string）的*切片*（slice）,切片是 `Go` 语言的基础概念，稍后详细介绍。现在先把切片 `s` 当做数组元素序列，序列的长度动态变化，用 `s[i]` 访问单个元素，用 `s[m:n]` 获取子序列，序列的元素数目为 `len(s)`。和大多数编程语言类似，区间索引时，`Go` 语言也采用作闭右开形式，即区间包括包括第一个索引元素，不包括最后一个索引元素。因为这样可以简化逻辑。比如 `s[m:n]` 这个切片，`0<=m<=n<=len(s)`，包含 `n-m` 个元素。

`os.Args` 变量的第一个元素：`os.Args[0]` 是命令本身的名字；其他元素则是程序启动时传给他的参数。`s[m:n]` 形式的切片表达式，产生从第 `m` 个元素到第 `n-1` 个元素的切片，下个例子用到的元素包含在 `os.Args[1:len(os.Args)]` 切片中。如果省略切片表达式的 `m` 或 `n`，会默认传入 `0` 或 `len(s)`，因此前面的切片可以简写成 `os.Args[1:]`。

下面是 Unix 里 `echo` 命令的一份实现，`echo` 把它的命令行参数打印成一行。程序导入了两个包，用括号把它们括起来写成列表形式，而没有分开写成独立的 `import` 声明。两种形式都合法，列表形式习惯上用得多。包导入顺序并不重要；`gofmt` 工具格式化时按照字母顺序对包名排序。（示例有多个版本时，我们会对示例编号，这样可以明确当前正在讨论的是哪个。）

*github.com/hanzhuoxian/study/go/gopl/ch01/echo1/main.go*

```go
package main

// echo1 打印命令行的参数

import (
	"fmt"
	"os"
)

func main() {
	// go 在声明变量时没有显示初始化，go 语言会对变量隐式赋 0 值，字符串会赋值空字符串
	var s, sep string
	// 经典的for循环
	for i := 1; i <= len(os.Args[1:]); i++ {
		// += 是一个赋值运算符
		s += sep + os.Args[i]
		sep = " "
	}
	fmt.Println(s)

}
```

注释语句以 `//` 开头。对于程序员来说，`//` 之后到行末之间所有的内容都是注释，被编译器忽略。按照惯例，我们在每个包的包声明前添加注释；对于 `main package`，注释包含一句或几句话，从整体角度对程序做个描述。

`var` 声明定义了两个 `string` 类型的变量 `s` 和 `sep`。变量会在声明时直接初始化。如果变量没有显式初始化，则被隐式地赋予其类型的 *零值*（zero value），数值类型是 `0`，字符串类型是空字符串 `""`。这个例子里，声明把 `s` 和 `sep` 隐式地初始化成空字符串。第 2 章再来详细地讲解变量和声明。

对数值类型，`Go 语言` 提供了常规的数值和逻辑运算符。而对 `string` 类型，`+` 运算符连接字符串。所以表达式：`sep + os.Args[i]` 表示连接字符串 `sep` 和 `os.Args[i]`。程序中使用的语句：`s+=sep+os.Args[i]` 是一条 *赋值语句*，将 `s` 的旧值跟 `sep` 与 `os.Args[i]` 连接后赋值回 `s`，等价于：`s=s+sep+os.Args[i]`。

运算符 `+=` 是赋值运算符（assignment operator），每种数值运算符或逻辑运算符，如 `+` 或 `*`，都有对应的赋值运算符。

`echo` 程序可以每循环一次输出一个参数，这个版本却是不断地把新文本追加到末尾来构造字符串。字符串 `s` 开始为空，即值为 `""`，每次循环会添加一些文本；第一次迭代之后，还会再插入一个空格，因此循环结束时每个参数中间都有一个空格。这是一种二次加工（quadratic process），当参数数量庞大时，开销很大，但是对于 `echo`，这种情形不大可能出现。本章会介绍 `echo` 的若干改进版，下一章解决低效问题。

循环索引变量 `i` 在 `for` 循环的第一部分中定义。符号 `:=` 是 *短变量声明*（short variable declaration）的一部分，这是定义一个或多个变量并根据它们的初始值为这些变量赋予适当类型的语句。下一章有这方面更多说明。

自增语句 `i++` 给 `i` 加 `1`；这和 `i+=1` 以及 `i=i+1` 都是等价的。对应的还有 `i--` 给 `i` 减 `1`。它们是语句，而不像 C 系的其它语言那样是表达式。所以 `j=i++` 非法，而且 `++` 和 `--` 都只能放在变量名后面，因此 `--i` 也非法。

Go 语言只有 `for` 循环这一种循环语句。`for` 循环有多种形式，其中一种如下所示：

```go
for initialization; condition; post {
	// zero or more statements
}
```

`for` 循环三个部分不需括号包围。大括号强制要求，左大括号必须和 *`post`* 语句在同一行。

*`initialization`* 是可选的，在循环开始前执行，*`initialization`* 如果存在，必须是一条简单语句（simple statement），即短变量声明、自增语句、赋值语句或函数调用。`condition` 是一个布尔表达式（boolean expression ），其值在每次循环迭代开始时计算。如果为 `true` 则执行循环体语句。`post` 语句在循环体结束后执行，之后再次对 `condition` 求值。`condition` 为 `false` 时循环结束。

`for` 循环的这三个部分每个都可以省略，如果省略  `initialization` 和 `post` 时分号也可以省略 

```go
// a traditional while loop
for condition {
	// zero or more statement
}
```

如果连 `condition` 也省略了，像下面这样：

```go
// a traditional infinite loop
for {
	// zero or more statement
}
```

这就变成一个无限循环，尽管如此，还可以用其他方式终止循环，如一条 `break` 或 `return` 语句。

`for` 循环的另一种形式，在某种数据类型的区间上遍历，如字符串或切片，`echo` 的第二个版本展示了这种形式。

*github.com/hanzhuoxian/study/go/gopl/ch01/echo2/main.go*

```go
package main

// echo2 打印命令行的参数

import (
	"fmt"
	"os"
)

func main() {
	var s, sep string
	for _, arg := range os.Args[1:] {
		s += sep + arg
		sep = " "
	}
	fmt.Println(s)
}

```

每次循环迭代， `range` 产生一对值；索引以及在改索引处的元素值，这个例子不需要索引，但是 `range` 语法要求处理元素必须处理索引。一种思路是把索引值赋值给一个临时变量（比如 temp）然后忽略它的值，但 `Go` 语言不允许使用无用的局部变量（local variables），因为这会导致编译错误。

Go 语言中这种情况的解决方法是用 *空标识符*（blank identifier），即 `_`（也就是下划线）。空标识符可用于在任何语法需要变量名但程序逻辑不需要的时候（如：在循环里）丢弃不需要的循环索引，并保留元素值。大多数的 Go 程序员都会像上面这样使用 `range` 和 `_` 写 `echo` 程序，因为隐式地而非显式地索引 `os.Args`，容易写对。

`echo` 的这个版本使用一条短变量声明来声明并初始化 `s` 和 `seps`，也可以将这两个变量分开声明，声明一个变量有好几种方式，下面这些都等价：

```go
s := ""
var s string
var s = ""
var s string = ""
```

用哪种不用哪种，为什么呢？第一种形式，是一条短变量声明，最简洁，但只能用在函数内部，而不能用于包变量。第二种形式依赖于字符串的默认初始化零值机制，被初始化为 `""`。第三种形式用得很少，除非同时声明多个变量。第四种形式显式地标明变量的类型，当变量类型与初值类型相同时，类型冗余，但如果两者类型不同，变量类型就必须了。实践中一般使用前两种形式中的某个，初始值重要的话就显式地指定变量的值，否则指定类型使用隐式初始化。

如前文所述，每次循环迭代字符串 `s` 的内容都会更新。`+=` 连接原字符串、空格和下个参数，产生新字符串，并把它赋值给 `s`。`s` 原来的内容已经不再使用，将在适当时机对它进行垃圾回收。

如果连接涉及的数据量很大，这种方式代价高昂。一种简单且高效的解决方案是使用 `strings` 包的 `Join` 函数：

*github.com/hanzhuoxian/study/go/gopl/ch01/echo3/main.go*

```go
package main

// echo3 打印命令行的参数

import (
	"fmt"
	"strings"
	"os"
)

func main() {
	fmt.Println(strings.Join(os.Args[1:], " "))
}

```

最后，如果不关心输出格式，只想看看输出值，或许只是为了调试，可以用 `Println` 为我们格式化输出。

```go
fmt.Println(os.Args[1:])
```

这条语句的输出结果跟 `strings.Join` 得到的结果很像，只是被放到了一对方括号里。切片都会被打印成这种格式。

---------

**练习 1.1：** 修改 `echo` 程序，使其能够打印 `os.Args[0]`，即被执行命令本身的名字。

**练习 1.2：** 修改 `echo` 程序，使其打印每个参数的索引和值，每个一行。

**练习 1.3：** 做实验测量潜在低效的版本和使用了 `strings.Join` 的版本的运行时间差异。（[1.6 节]讲解了部分 `time` 包，[11.4 节]展示了如何写标准测试程序，以得到系统性的性能评测。）

## 1.3 查找重复的行

对文件做拷贝、打印、搜索、排序、统计或类似事情的程序都有一个差不多的程序结构：一个处理输入的循环，在每个元素上执行计算处理，在处理的同时或最后产生输出。我们会展示一个名为 `dup` 的程序的三个版本；灵感来自于 Unix 的 `uniq` 命令，其寻找相邻的重复行。该程序使用的结构和包是个参考范例，可以方便地修改。

`dup` 的第一个版本打印标准输入中多次出现的行，以重复次数开头。该程序将引入 `if` 语句，`map` 数据类型以及 `bufio` 包。


*github.com/hanzhuoxian/study/go/gopl/ch01/dup1/main.go*

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	count := make(map[string]int)
	input := bufio.NewScanner(os.Stdin)
	for input.Scan() {
		count[input.Text()]++
		if input.Err() != nil {
			panic("input is error")
		}
	}

	for line, n := range count {
		if n > 1 {
			fmt.Printf("%d\t%s\n", n, line)
		}
	}
}

```

正如 `for` 循环一样，`if` 语句条件两边也不加括号，但是主体部分需要加。`if` 语句的 `else` 部分是可选的，在 `if` 的条件为 `false` 时执行。

**map** 存储了键/值（key/value）的集合，对集合元素，提供常数时间的存、取或测试操作。键可以是任意类型，只要其值能用 `==` 运算符比较，最常见的例子是字符串；值则可以是任意类型。这个例子中的键是字符串，值是整数。内置函数 `make` 创建空 `map`，此外，它还有别的作用。4.3 节讨论 `map`。

每次 `dup` 读取一行输入，该行被当做键存入 `map`，其对应的值递增。`counts[input.Text()]++` 语句等价下面两句：

```go
line = input.Text()
counts[line] = counts[like] + 1
```

`map` 中不含某个键时不用担心，首次读到新行时，等号右边的表达式 `counts[line]` 的值将被计算为其类型的零值，对于 `int` 即 `0`。

为了打印结果，我们使用了基于 `range` 的循环，并在 `counts` 这个 `map` 上迭代。跟之前类似，每次迭代得到两个结果，键和其在 `map` 中对应的值。`map` 的迭代顺序并不确定，从实践来看，该顺序随机，每次运行都会变化。这种设计是有意为之的，因为能防止程序依赖特定遍历顺序，而这是无法保证的。

继续来看 `bufio` 包，它使处理输入和输出方便又高效。`Scanner` 类型是该包最有用的特性之一，它读取输入并将其拆成行或单词；通常是处理行形式的输入最简单的方法。

程序使用短变量声明创建 `bufio.Scanner` 类型的变量 `input`。

```go
input := bufio.NewScanner(os.Stdin)
```

该变量从程序的标准输入中读取内容。每次调用 `input.Scan()`，即读入下一行，并移除行末的换行符；读取的内容可以调用 `input.Text()` 得到。`Scan` 函数在读到一行时返回 `true`，不再有输入时返回 `false`。

类似于 C 或其它语言里的 `printf` 函数，`fmt.Printf` 函数对一些表达式产生格式化输出。该函数的首个参数是个格式字符串，指定后续参数被如何格式化。各个参数的格式取决于“转换字符”（conversion character），形式为百分号后跟一个字母。举个例子，`%d` 表示以十进制形式打印一个整型操作数，而 `%s` 则表示把字符串型操作数的值展开。

`Printf` 有一大堆这种转换，Go程序员称之为*动词（verb）*。下面的表格虽然远不是完整的规范，但展示了可用的很多特性：

```text
%d          十进制整数
%x, %o, %b  十六进制，八进制，二进制整数。
%f, %g, %e  浮点数： 3.141593 3.141592653589793 3.141593e+00
%t          布尔：true或false
%c          字符（rune） (Unicode码点)
%s          字符串
%q          带双引号的字符串"abc"或带单引号的字符'c'
%v          变量的自然形式（natural format）
%T          变量的类型
%%          字面上的百分号标志（无操作数）
```

`dup1` 的格式字符串中还含有制表符`\t`和换行符`\n`。字符串字面上可能含有这些代表不可见字符的**转义字符（escape sequences）**。默认情况下，`Printf` 不会换行。按照惯例，以字母 `f` 结尾的格式化函数，如 `log.Printf` 和 `fmt.Errorf`，都采用 `fmt.Printf` 的格式化准则。而以 `ln` 结尾的格式化函数，则遵循 `Println` 的方式，以跟 `%v` 差不多的方式格式化参数，并在最后添加一个换行符。（译注：后缀 `f` 指 `format`，`ln` 指 `line`。）

很多程序要么从标准输入中读取数据，如上面的例子所示，要么从一系列具名文件中读取数据。`dup` 程序的下个版本读取标准输入或是使用 `os.Open` 打开各个具名文件，并操作它们。


*github.com/hanzhuoxian/study/go/gopl/ch01/dup2/main.go*

```go
package main

import (
	"bufio"
	"fmt"
	"log"
	"os"
)

func main() {
	// 定义缓存行次数的map
	counts := make(map[string]int)
	// 获取命令行
	files := os.Args[1:]
	if len(files) == 0 {
		// 使用标准输入
		countLines(os.Stdin, counts)
	} else {
		// 循环读取文件
		for _, filePath := range files {
			// 打开文件
			file, err := os.Open(filePath)
			if err != nil {
				fmt.Fprintf(os.Stderr, "dup2: %v\n", err)
				continue
			}
			countLines(file, counts)
			file.Close()
		}
	}

	for line, n := range counts {
		if n > 1 {
			fmt.Printf("%d\t%s\n", n, line)
		}
	}

}

func countLines(f *os.File, counts map[string]int) {
	input := bufio.NewScanner(f)
	for input.Scan() {
		counts[input.Text()]++
	}
	
	// NOTE: ignoring potential errors from input.Err()
}

```


`os.Open` 函数返回两个值。第一个值是被打开的文件（`*os.File`），其后被 `Scanner` 读取。

`os.Open` 返回的第二个值是内置 `error` 类型的值。如果 `err` 等于内置值`nil`（译注：相当于其它语言里的 `NULL`），那么文件被成功打开。读取文件，直到文件结束，然后调用 `Close` 关闭该文件，并释放占用的所有资源。相反的话，如果 `err` 的值不是 `nil`，说明打开文件时出错了。这种情况下，错误值描述了所遇到的问题。我们的错误处理非常简单，只是使用 `Fprintf` 与表示任意类型默认格式值的动词 `%v`，向标准错误流打印一条信息，然后 `dup` 继续处理下一个文件；`continue` 语句直接跳到 `for` 循环的下个迭代开始执行。

为了使示例代码保持合理的大小，本书开始的一些示例有意简化了错误处理，显而易见的是，应该检查 `os.Open` 返回的错误值，然而，使用 `input.Scan` 读取文件过程中，不大可能出现错误，因此我们忽略了错误处理。我们会在跳过错误检查的地方做说明。5.4 节中深入介绍错误处理。

注意 `countLines` 函数在其声明前被调用。函数和包级别的变量（package-level entities）可以任意顺序声明，并不影响其被调用。

`map` 是一个由 `make` 函数创建的数据结构的引用。`map` 作为参数传递给某函数时，该函数接收这个引用的一份拷贝（copy，或译为副本），被调用函数对 `map` 底层数据结构的任何修改，调用者函数都可以通过持有的 `map` 引用看到。在我们的例子中，`countLines` 函数向 `counts` 插入的值，也会被 `main` 函数看到。

`dup` 的前两个版本以"流”模式读取输入，并根据需要拆分成多个行。理论上，这些程序可以处理任意数量的输入数据。还有另一个方法，就是一口气把全部输入数据读到内存中，一次分割为多行，然后处理它们。下面这个版本，`dup3`，就是这么操作的。这个例子引入了 `ReadFile` 函数（来自于`io/ioutil`包），其读取指定文件的全部内容，`strings.Split` 函数把字符串分割成子串的切片。（`Split` 的作用与前文提到的 `strings.Join` 相反。）

我们略微简化了 `dup3`。首先，由于 `ReadFile` 函数需要文件名作为参数，因此只读指定文件，不读标准输入。其次，由于行计数代码只在一处用到，故将其移回 `main` 函数。

```go
package main

import (
	"fmt"
	"os"
	"strings"
)

func main() {
	counts := make(map[string]int)
	for _, filename := range os.Args[1:] {
		data, err := os.ReadFile(filename)
		if err != nil {
			fmt.Fprintf(os.Stderr, "dup3: %v\n", err)
			continue
		}
		for _, line := range strings.Split(string(data), "\n") {
			counts[line]++
		}

	}
	for line, n := range counts {
		if n > 1 {
			fmt.Printf("%d\t%s\n", n, line)
		}
	}
}

```

`ReadFile` 函数返回一个字节切片（byte slice），必须把它转换为 `string`，才能用 `strings.Split` 分割。我们会在3.5.4 节详细讲解字符串和字节切片。

---------

**练习 1.4：** 修改 `dup2`，出现重复的行时打印文件名称。