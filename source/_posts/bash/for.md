---
title: for循环
date: 2024-02-19 10:14:18
tags:
---

## C 语言语法 for 循环

### 语法解释

```bash
# do 与 for 不在一行的写法
for (( expression1; expression2; expression3 ))
do
  commands
done

# do 与 for 在一行的写法
for (( expression1; expression2; expression3 )); do
  commands
done
```

`expression1` 用来初始化循环条件，`expression2` 用来决定循环结束的条件，`expression3` 在每次循环迭代的末尾执行，用于更新值。

循环条件放在双重圆括号之中，变量不需要加美元符号 `$`

### 例子

```bash
# do 与 for 不在一行的写法
for ((i=0;i<10;i++))
do
    echo $i
done

# do 与 for 在一行的写法
for ((i=0;i<10;i++)); do
    echo $i
done
```

### 遍历数组

```bash
declare -a arr=("element1" "element2" "element3")
len=${#arr[@]}
for ((i=0;i < "${len}"; i++)) ;do
    echo "${arr[$i]}"
done
```

## `for...in` 循环

### `for...in` 语法解释

for...in 循环用于遍历列表的每一项

```bash
# for 与 do 不在一行的写法
for var in list
do
command
done

# for 与 do 在一行的写法
for var in list;do
command
done
```

上面的语法中，`for` 会依次从 `list` 中取出一项作为变量 `var` 的值，然后在循环体中进行处理

### `for...in` 例子

#### 数组例子

```bash
for i in 1 2 3
do
    echo $i
done
```

#### 列表可以由通配符产生

```bash
for conf in /etc/*conf;do
    echo "$conf"
done
```

#### in list 省略的情况

脚本参数或者函数参数 in $@ 可以省略

```bash

forignoreinlist() {
    for i in "$@";do
        echo "$i"
    done
    # 省略 in list
    for i;do
        echo "$i"
    done
}

forignoreinlist a b c d
```

#### 遍历数组元素

```bash
declare -a arr=("element1" "element2" "element3")
for element in "${arr[@]}";do
    echo "$element"
done
```
