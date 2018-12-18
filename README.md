# nyx
[![Build Status](https://travis-ci.org/racaljk/nyx-lang.svg?branch=master)](https://travis-ci.org/racaljk/nyx) | 
[![Build status](https://ci.appveyor.com/api/projects/status/ptqln5210xp6gupc?svg=true)](https://ci.appveyor.com/project/racaljk/nyx) |
[![Documentation Status](https://readthedocs.org/projects/nyx-lang/badge/?version=latest)](https://nyx-lang.readthedocs.io/zh/latest/?badge=latest) |
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/f75d53319a8f46d3866a41f32b2874a9)](https://www.codacy.com/app/racaljk/nyx?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=racaljk/nyx&amp;utm_campaign=Badge_Grade) |
[![CodeFactor](https://www.codefactor.io/repository/github/racaljk/nyx-lang/badge)](https://www.codefactor.io/repository/github/racaljk/nyx-lang)

对的，**nyx**是又一门看似**动态类型**实则有着**严格类型系统**的脚本语言

希望她仅有`python`的灵活，`c/c++`的实用性和语法形式，`java/`的工程化，以及非理想主义者的哲学 ：——）


# 语言手册
## 1.基础
### 1.1注释 
使用`#`可以注释一行代码。**nyx**不支持多行注释，对于多行需要重复`#`

### 1.2数据类型
+ **int** 整数类型，如`3`,`100000`,`1024`
+ **double** 小数类型，如`3.1415926`,`2.232`，`4.4` 
+ **string** 字符串类型，如`"string"`,`"test"`,`""`
+ **bool** 布尔类型，值域只有字面值`true`和`false`
+ **null** 空值类型，用于指示该变量不具有值，值域只有字面值`null`
+ **char** 字符类型，表示单个字符，如`a`,`Y`

## 2.运算符
### 2.1 四则运算
`+,-,*,/,%`是计算的基石，所以没有不支持的道理。在**nyx**中四则运算的优先级和运算规则与其它语言无二：
```nyx
d = (3+2)*4+(6*5)-8/2+(3+2*(5-4))
c = -7
a = 3+2-5
b = 3+5*2%2
print(a,b,c,d)                 
q = (((((((((((((((((((1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1)+1
print(q)
```
字符串类型的运算符效果不同于数值类型。
对字符串类型进行`+`运算得到的是两个字符串拼接后的结果；
`*`表示N次重复字符串：
```nyx
print("hello,"+"world") # will print hello,world
print("test" * 3 )      # will print testtesttest
```

### 2.2 逻辑运算
`&&`表示逻辑与运算，`||`表示逻辑或运算,`!`表示逻辑非运算。
。由于宿主语言是C++，这些逻辑运算也原生的具有[**短路求值**](https://en.wikipedia.org/wiki/Short-circuit_evaluation)特性。
```nyx
true&&false
false||true
!(false||false||false||(true||false))
```
### 2.3 条件运算
除了逻辑运算外，**nyx**也有完备的条件运算支持：`==`，`!=`，`>`，`>=`，`<`，`<=`:
```nyx
print((true&&false)==false)
print((false&&true)==false)
print((true||false)==true)
print((true||true)==true)
print(5>3 && 6<10 && (14>=13||13<=15))
```
另外值得注意的是`==`,`!=`运算符也支持`null`的条件比较:
+ `null==null`总是为`true`
+ `null!=null`总是为`false`。

### 2.4 位运算
条件运算类似于C系语言：
```
# 位与
print(3&5) # 0011 & 0101 => 1

# 位或
print(4|66) # 00000100 & 01000010 => 70

# 位反
print(~43) # 00101011 =>11010100 => -44
```

## 3. 流程控制
## 3.1 if-else分支跳转
`if`语句可以根据条件进行分支跳转。单个`if`分支跳转和`if-else`分支跳转都是允许的：
```nyx
a = input()
if(a+1 == "whatsup"){
    print("fine")
}
b = 10
if(b <10){
    print("b is less than 10")
}else{
    print("b is greater equal than 10")
}
```

## 3.2 while循环
**nyx**不打算在公共语言基础上标新立异，它的`while`做了与其他大多数语言一样的事情，即根据条件进行循环。
```nyx
a= 1
while(a<100){
    print("counter:"+a)
    a = a+1
}
```
## 3.3 break
`break`跳出最近一层循环：
```nyx
# 输出1-10
func upto10(){
    i=0
    while(true){
        if(i==10){
            break
        }
        print("up")
        i = i+1
    }
}
upto10()
```
## 3.4 continue
`continue`结束本次循环并继续下次循环(会对条件重新求值)：
```nyx
# 过滤奇数，输出limit以内的偶数
func filter_odd(limit)
{
    i = 1
    while(i<limit){
        if(i%2==1){
            i = i+1
            continue
        }
        print(i)
        i = i+1
    }
}

filter_odd(100)
```

## 4.函数
函数几乎是现代编程语言最重要的抽象之一，在nyx可以使用`func`关键字引导函数定义：
```nyx
# 重复输出a次str
func repeat(a,str){
    i = 0
    while(i<a){
        print(str)
        i = i+1
    }
}

repeat(10,"greeting!")

# 判断是否为水仙花数
func isNarcissicsticNumber(num)
{
    old = num
    accumulate = 0
    while(0!=num){
        n = num%10
        accumulate = accumulate + n*n*n
        num = num/10
        
    }
    return accumulate==old
}

isNarcissicsticNumber(153)
```
关键字`return`用于控制返回
```nyx
# 将字符串字符逐个转化为*字符
func toStar(str){
    result = ""
    i =0
    while(i<length(str)){
        result = result+"*"
        i = i+1
    }
    return result
}

print(toStar("i come i see i conquer"))
# **********************
```
这里没有魔法。

## 5.内置函数
```nyx
# 接受任意数目的参数，向stdout输出
func print(a:any,b:any,c:any...)

# 无参数。接受stdin输入并返回输入字符串
func input()

# 接受一个参数，返回一个字符串用以表示实参类型
func typeof(a:any) b:string

# 接受字符串类型，返回字符串长度
func length(a:string) b:int
```

# 开源协议
**nyx**所有代码受[MIT LICENSE](LICENSE)保护。
