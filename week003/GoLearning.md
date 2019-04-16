# Go 语言学习

## 简介

Go是一门编译型的和静态的编程语言。 Go诞生于谷歌研究院。 Go的核心设计成员中包括很多有着数十年编程语言研究领域经验的研究者。

Go有很多特性，有一些是独特的，有一些借鉴于一些其它编程语言。

- 内置并发编程支持：
  - 使用**协程**（goroutine）做为基本的计算单元。轻松地创建协程。
  - 使用**数据通道**（channels）来实现协程间的同步和通信。
- 内置了映射（map）和切片（slice）类型。
- 支持多态（polymorphism）。
- 使用接口（interface）来实现裝盒（value boxing）和反射（reflection）。
- 支持指针。
- 支持函数闭包（closure）。
- 支持方法。
- 支持延迟函数调用（defer）。
- 支持类型内嵌（type embedding）。
- 支持类型推断（type deduction or type inference）。
- 内存安全。
- 自动垃圾回收。
- 良好的代码跨平台性。

第一，语言简单，上手快。Go 语言的语法特性简直是太简单了，简单到你几乎玩不出什么花招，直来直去的，学习难度很低，容易上手。

第二，并行和异步编程几乎无痛点。Go 语言的 Goroutine 和 Channel 这两个神器简直就是并发和异步编程的巨大福音。像 C、C++、Java、Python 和 JavaScript 这些语言的并发和异步的编程方式控制起来就比较复杂了，并且容易出错，但 Go 语言却用非常优雅和流畅的方式解决了这个问题。这对于编程多年受尽并发和异步折磨的我来说，完全就是眼前一亮的感觉。

第三，Go 语言的 lib 库“麻雀虽小，五脏俱全”。Go 语言的 lib 库中基本上有绝大多数常用的库，虽然有些库还不是很好，但我觉得这都不是主要问题，因为随着技术的发展和成熟，这些问题肯定也都会随之解决。

第四，C 语言的理念和 Python 的姿态。C 语言的理念是信任程序员，保持语言的小巧，不屏蔽底层且对底层友好，关注语言的执行效率和性能。而 Python 的姿态是用尽量少的代码完成尽量多的事。于是我能够感觉到，Go 语言是想要把 C 和 Python 统一起来，这是多棒的一件事。

## 关键字和标识符

### 关键字

这些关键字可以分为四组：

- const、func、import、package、type和var用来声明各种代码元素。
- chan、interface、map和struct用做一些组合类型的字面表示中。
- break、case、continue、default、else、fallthrough、for、goto、if、range、return、select和switch用在流程控制语句中。
- defer和go也可以看作是流程控制关键字， 与协程和延迟函数调用有关。

### 标识符

一个标识符是一个以*Unicode字母*或者 _ **开头**并且完全由**Unicode字母**和**Unicode数字**组成的单词。

注意：**关键字不能被用做标识符**

标识符 _ 是一个特殊字符，叫做空标识符

一个由Unicode大写字母开头的标识符称为**导出标识符**。 这里**导出**可以被理解为**公开**（public）。 其它（即非Unicode大写字母开头的）标识符称为**非导出标识符**。 **非导出**可以被理解为**私有**（private），包内公开，对其它包不可见。

## 基本类型和它们的值的字面表示形式

类型（type）可以被看作是值（value）的模板，值可以被看作是类型的实例。

### 基本内置类型

Go支持如下内置基本类型：

- 一种内置布尔类型：bool。
- 11种内置整数类型：int8、uint8、int16、uint16、int32、uint32、int64、uint64、int、uint和uintptr。
- 两种内置浮点数类型：float32和float64。
- 两种内置复数类型：complex64和complex128。
- 一种内置字符串类型：string。

Go中有两种内置别名类型（alias type）：

- byte是uint8的内置别名类型。 我们可以将byte和uint8看作是同一个类型。
- rune是int32的内置别名类型。 我们可以将rune和int32看作是同一个类型。

一个complex64复数值的实部和虚部都是float32类型的值。 一个complex128复数值的实部和虚部都是float64类型的值。

### 零值

每种类型都有一个零值。一个类型的零值可以看作是此类型的默认值。

- 一个布尔类型的零值表示真假中的假。
- 数值类型的零值都是零（但是不同类型的零在内存中占用的空间可能不同）。
- 一个字符串类型的零值是一个空字符串。

### 基本类型的值的字面表示形式

一个值的字面表示形式是指在代码中这个值的文字体现形式。 一个值可能会有很多种字面表示形式。

一个基本类型的值的字面表示形式也称为一个**字面常量**，或者叫一个**无名常量**。

#### 布尔值的字面表示形式

Go白皮书没有定义布尔类型值字面表示形式。 我们可以将false和true这两个预声明的有名常量当作布尔类型值字面表示形式。

布尔类型的零值可以使用预声明的false来表示。

#### 整数类型值的字面表示形式

整数类型值有三种字面表示形式：十进制形式（decimal）、八进制形式（octal）和十六进制形式（hex）。 比如，下面的三个字面值均表示十进制的15：

```go
0xF // 十六进制表示（必须使用0x或者0X开头）
017 // 八进制表示（必须使用0开头）
15  // 十进制表示（必须不能用0开头）
```

整数类型的零值的字面形式一般使用0表示。 当然，00和0x0也是合法的整数类型零值的字面表示形式。

#### 浮点数类型值的字面表示形式

一个浮点数的完整字面表示形式包含一个整数部分、一个小数点、一个小数部分和一个指数部分。 常常地，某些部分可以根据情况省略掉。一些例子：

```go
    1.23
    01.23 // == 1.23
    .23
    1.
    // 一个e或者E随后的数值是指数值。指数值
    // 必须为一个可以带符号的十进制整数字面值。
    1.23e2  // == 123.0
    123E2   // == 12300.0
    123.E+2 // == 12300.0
    1e-1    // == 0.1
    .1e0    // == 0.1
    0e+5    // == 0.0
```

浮点类型的零值的标准字面表示形式为0.0。 当然其它很多形式也是合法的，比如0.、.0、0e0等。

#### 虚部的字面表示形式

一个虚部值的字面表示形式由一个浮点数字面值或者一个整数字面值加一个小写的i组成。 一些例子：

```go
1.23i
1.i
.23i
123i
0123i   // == 123i
1.23E2i // == 123i
1e-1i
```

虚部字面值用来表示复数的虚部。下面是一些复数值的字面表示形式：

```go
1 + 2i       // == 1.0 + 2.0i
1. - .1i     // == 1.0 + -0.1i
1.23i - 7.89 // == -7.89 + 1.23i
1.23i        // == 0.0 + 1.23i
```

复数零值的标准字面表示为0.0+0.0i。 当然0i、.0i、0+0i等表示也是合法的。

#### rune值的字面形式

在Go中，一个rune值表示一个Unicode码点。 一般说来，我们可以将一个Unicode码点看作是一个Unicode字符。 但是，我们也应该知道，有些Unicode字符由多个Unicode码点组成。 每个英文或中文Unicode字符值含有一个Unicode码点。

```go
'a' // 一个英文字符
'π'
'众' // 一个中文字符

'\141'   // 141是97的八进制表示
'\x61'   // 61是97的十六进制表示
'\u0061'
'\U00000061'
```

它们多用做字符串的双引号字面形式中的转义字符。

如果一个rune字面形式中被单引号包起来的部分含有两个字符， 并且第一个字符是 \ ，第二个字符不是x、 u和U，那么这两个字符将被转义为一个特殊字符。 目前支持的转义组合为：

    \a   (rune值：0x07) 铃声字符
    \b   (rune值：0x08) 退格字符（backspace）
    \f   (rune值：0x0C) 换页符（form feed）
    \n   (rune值：0x0A) 换行符（line feed or newline）
    \r   (rune值：0x0D) 回车符（carriage return）
    \t   (rune值：0x09) 水平制表符（horizontal tab）
    \v   (rune值：0x0b) 竖直制表符（vertical tab）
    \\   (rune值：0x5c) 一个反斜杠（backslash）
    \'   (rune值：0x27) 一个单引号（single quote）

rune类型的零值常用 '\000'、'\x00'或'\u0000'等来表示。

#### 字符串值的字面表示形式

在Go中，字符串值是UTF-8编码的， 甚至所有的Go源代码都必须是UTF-8编码的。

Go字符串的字面表示形式有两种。 一种是解释型字面表示（interpreted string literal，双引号风格）。 另一种是直白字面表示（raw string literal，反引号风格）。 下面的两个字符串表示形式是等价的：

```go
// 解释形式
"Hello\nworld!\n\"你好世界\""

// 直白形式
`Hello
world!
"你好世界"`
```

以\、\x、\u和\U开头的rune字面形式（不包括两个单引号）也可以出现在双引号风格的字符串字面形式中。比如：

```go
// 这几个字符串字面形式是等价的。
"\141\142\143"
"\x61\x62\x63"
"abc"

// 这几个字符串字面形式是等价的。
"\u4f17\xe4\xba\xba"
    // “众”的Unicode值为4f17，它的UTF-8
    // 编码为三个字节：0xe4 0xbc 0x97。
"\xe4\xbc\x97\u4eba"
    // “人”的Unicode值为4eba，它的UTF-8
    // 编码为三个字节：0xe4 0xba 0xba。
"\xe4\xbc\x97\xe4\xba\xba"
"众人"
```

在UTF-8编码中，一个Unicode码点（rune）可能由1到4个字节组成。 每个英文字母的UTF-8编码只需要一个字节。 每个中文字符的UTF-8编码需要三个字节。

直白反引号风格的字面表示中是不支持转义字符的。 除了首尾两个反引号，直白反引号风格的字面表示中不能包含反引号。 为了跨平台兼容性，直白反引号风格的字面表示中的回车符（Unicode码点为0x0D） 将被忽略掉。

字符串类型的零值在代码里用 ""或``表示。

### 基本类型字面值的适用范围

我们常常把一个值的字面形称为一个字面值。

任何字符串的字面形式都可以表示任何字符串类型的值。

预声明的两个常量false和true都可以表示任何布尔类型的值。

只有在不需要四舍五入的情况下，数字才可以表示为整数值。例如，1.23e2可以表示为任何基本整数类型的值，但是1.23不能表示为任何基本整数类型的值。当一个数值型的字面值用来表示一个非整数基本类型的值时，舍入（或者精度丢失）是允许的。

每种数值类型有一个能够表示的数值范围。 如果一个字面值超出了一个类型能够表示的数值范围（溢出），则在编译时刻，此字面值不能用来表示此类型的值。

## 常量和变量

各种基本类型的字面表示形式 （除了false和true）都属于**无名常量**（unnamed constant），或者叫**字面常量**（literal constant）。 false和true是预声明的两个有名常量。

### 类型不确定值（untyped value）和类型确定值（typed value）

在Go中，有些值的类型是不确定的。换句话说，有些值的类型有很多可能性。 这些值称为类型不确定值。对于大多数类型不确定值来说，它们各自都有一个默认类型， 除了预声明的nil。nil是没有默认类型的。

与类型不确定值相对应的概念称为类型确定值。

一个字面常量的默认类型取决于它的字面表示形式：

- 一个字符串字面值的默认类型是预声明的string类型。
- 一个布尔字面值的默认类型是预声明的bool类型。
- 一个整数型字面值的默认类型是预声明的int类型。
- 一个rune字面值的默认类型是预声明的rune（亦即int32）类型。
- 一个浮点数字面值的默认类型是预声明的float64类型。
- 如果一个字面值含有虚部字面形式，则此字面值的默认类型是预声明的complex128类型。

### 类型不确定常量的显式类型转换

一个显式类型转换的形式为T(v)，其表示将一个值v转换为类型T。 编译器将T(v)的转换结果视为一个类型为T的类型确定值。 当然，对于一个特定的类型T，T(v)并非对任意的值v都合法。

对于一个类型不确定常量值v，有两种情形显式转换T(v)是合法的：

1. v**可以表示**为T类型的一个值。 转换结果为一个类型为T的类型确定常量值。
2. v的默认类型是一个整数类型（int或者rune） 并且T是一个字符串类型。 转换T(v)将v看作是一个Unicode码点。 转换结果为一个类型为T的字符串常量。 此字符串常量只包含一个Unicode码点，并且可以看作是此Unicode码点的UTF-8表示形式。 对于不在合法的Unicode码点取值范围内的整数v， 转换结果等同于字符串字面值"\uFFFD"（亦即"\xef\xbf\xbd"）。 0xFFFD是Unicode标准中的（非法码点的）替换字符值。

一些合法的转换例子：

```go
complex128(1 + -1e-1000i)  // 结果为complex128类型的1.0+0.0i。虚部被舍入了。
float32(0.49999999)        // 结果为float32类型的0.5。这里也舍入了。
float32(17000000000000000) // 只要目标类型不是整数类型，舍入都是允许的。
float32(123)
uint(1.0)
int8(-123)
int16(6+0i)
complex128(789)

string(65)          // "A"
string('A')         // "A"
string('\u68ee')    // "森"
string(-1)          // "\uFFFD"
string(0xFFFD)      // "\uFFFD"
string(0x2FFFFFFFF) // "\uFFFD"
```

下面是一些非法的转换：

```go
int(1.23)     // 1.23不能被表示为int类型值。
uint8(-1)     // -1不能被表示为uint8类型值。
float64(1+2i) // 1+2i不能被表示为float64类型值。

float64(-1e1000)         // -1e+1000不能被表示为float64类型值。不允许溢出。
int(0x10000000000000000) // 0x10000000000000000做为int值将溢出。

string(65.0)  // 字面值65.0的默认类型是float64（不是一个整数类型）。
string(66+0i) // 66+0i的默认类型是complex128（不是一个整数类型）。
```

### 类型推断介绍

Go支持类型推断（type deduction or type inference）。 类型推断是指在某些场合下，程序员可以在代码中使用一些类型不确定值， 编译器会自动推断出这些类型不确定值在特定情景下应被视为某些特定类型的值。

如果某处需要一个特定类型的值并且一个类型不确定值可以表示为此特定类型的值， 则此类型不确定值可以使用在此处。

有些场景对某些类型不确定值并没有特定的类型要求。 在这种情况下，Go编译器将这些类型不确定值视为类型为它们各自的默认类型的类型确定值。

### （有名）常量声明（constant declaration）

有名常量必须都是布尔、数字或者字符串值。 在Go中，关键字const用来声明有名常量。 下面是一些常量声明的例子。

```go
package main
// 声明了两个单独的有名常量。（是的，非ASCII字符可以用做标识符。）
const π = 3.1416
const Pi = π // 等价于：Pi == 3.1416

// 声明了一组有名常量。
const (
    No         = !Yes
    Yes        = true
    MaxDegrees = 360
    Unit       = "弧度"
)

func main() {
    // 声明了三个局部有名常量。
    const DoublePi, HalfPi, Unit2 = π * 2, π * 0.5, "度"
}
```

每行含有一个等号 `=` 的语句称为一个**常量描述**（constant specification）。

每个`const`关键字对应一个**常量声明**。一个常量声明中可以有若干个常量描述。

常量声明中的等号=表示“绑定”而非“赋值”。每个常量描述将一个或多个字面值绑定到各自对应的有名常量上。

常量可以直接声明在包中，也可以声明在函数体中。 声明在函数体中的常量称为**局部常量**（local constant），直接声明在包中的常量称为**包级常量**（package-level constant）。包级常量也常常被称为全局常量。

包级常量声明中的常量描述的顺序并不重要。

#### 类型确定有名变量

我们可以在声明一些常量的时候指定这些常量的确切类型。 这样声明的常量称为类型确定有名常量。

```go
const X float32 = 3.14

const (
    A, B int64   = -3, 5
    Y    float32 = 2.718
)
```

欲将一个字面常量绑定到一个类型确定有名常量上，此字面常量必须能够表示为此常量的确定类型的值。 否则，编译将报错。

下面这个类型确定常量声明在64位的操作系统上是合法的，但在32位的操作系统上是非法的。 因为一个uint值在32位操作系统上的尺寸是32位， (1 << 64) - 1将溢出uint。（这里，符号<<为左移位运算符。）

```go
const MaxUint uint = (1 << 64) - 1
```

那么如何声明一个代表着最大uint值的常量呢？ 我们可以用下面这个常量声明来替换上面这个。下面这个声明在在64位和32位的操作系统上都是合法的。

```go
const MaxUint = ^uint(0)
```

类似地，我们可以使用下面这个常量声明来声明一个有名常量来表示最大的int值。（这里，符号>>为右移位运算符。）

```go
const MaxInt = int(^uint(0) >> 1)
```

使用类似的方法，我们可以声明一个常量来表示当前操作系统的位数，或者检查当前操作系统是32位的还是64位的。

```go
const NativeWordBits = 32 << (^uint(0) >> 63) // 64 or 32
const Is64bitOS = ^uint(0) >> 63 != 0
const Is32bitOS = ^uint(0) >> 32 == 0
```

#### 常量声明中的自动补全

在一个包含多个常量描述的常量声明中，除了第一个常量描述，其它后续的常量描述都可以只有标识符部分。 Go编译器将通过**照抄前面最紧挨的一个完整的常量描述来自动补全不完整的常量描述**。

在编译阶段，编译器会将下面的代码

```go
const (
    X float32 = 3.14
    Y                // 这里必须只有一个标识符
    Z                // 这里必须只有一个标识符

    A, B = "Go", "language"
    C, _
    // 上一行中的空标识符是必需的（如果上一行是一个不完整的常量描述）。
)
```

自动补全为

```go
const (
    X float32 = 3.14
    Y float32 = 3.14
    Z float32 = 3.14

    A, B = "Go", "language"
    C, _ = "Go", "language"
)
```

#### 在常量声明中使用iota

iota是Go中预声明（内置）的一个特殊的有名常量。 iota被预声明为0，但是它的值在编译阶段并非恒定。 *当此预声明的iota出现在一个常量声明中的时候，它的值在第n个常量描述中的值为n（从0开始）。*

```go
func main() {
    const (
        k = 3 // 在此处，iota == 0

        m float32 = iota + .5 // m float32 = 1 + .5
        n                     // n float32 = 2 + .5

        p = 9             // 在此处，iota == 3
        q = iota * 2      // q = 4 * 2
        _                 // _ = 5 * 2
        r                 // r = 6 * 2
        s, t = iota, iota // s, t = 7, 7
        u, v              // u, v = 8, 8
        _, w              // _, w = 9, 9
    )

    const x = iota // x = 0 （iota == 0）
    const (
        y = iota // y = 0 （iota == 0）
        z        // z = 1
    )

    println(m)             // +1.500000e+000
    println(n)             // +2.500000e+000
    println(q, r)          // 8 12
    println(s, t, u, v, w) // 7 7 8 8 9
    println(x, y, z)       // 0 0 1
}
```

```go
const (
    Failed = iota - 1 // == -1
    Unknown           // == 0
    Succeeded         // == 1
)

const (
    Readable = 1 << iota // == 1
    Writable             // == 2
    Executable           // == 4
)
```

### 变量声明和赋值操作语句

变量可以被看作是在运行时刻存储在内存中并且可以被更改的有名字的值。

所有的变量值都是类型确定值。当声明一个变量的时候，我们必须在代码中给编译器提供足够的信息来让编译器推断出此变量的确切类型。

在一个函数体内声明的变量称为局部变量。 在任何函数体内声明的变量称为包级或者全局变量。

Go语言有两种变量声明形式。一种称为标准形式，另一种称为短声明形式。 **短声明形式只能用来声明局部变量**。

#### 标准变量声明形式

每条标准变量声明形式语句起始于一个var关键字。 每个var关键字跟随着一个变量名。 每个变量名必须为一个标识符。

两种变种形式：

1. 省略了变量类型（但仍指定了变量的初始值）, 编译器将根据初始值的字面形式来推断出变量的类型。
2. 省略了初始值（但仍指定了变量类型）, 编译器将使用变量类型的零值做为变量的初始值

和常量声明一样，多个变量可以用一对小括号组团在一起被声明。

```go
var (
    lang, bornYear, compiled     = "Go", 2007, true
    announceAt, releaseAt    int = 2009, 2012
    createdBy, website       string
)
```

#### 纯赋值语句

在上面展示的变量声明的例子中，等号=表示赋值。 一旦一个变量被声明之后，它的值可以被通过纯赋值语句来修改。 多个变量可以同时在一条赋值语句中被修改。

一个赋值语句等号左边的表达式必须是一个可寻址的值、一个映射元素或者一个空标识符。

空标识符也可以出现在纯赋值语句的左边，表示不关心对应的目标值。 空标识符不可被用做源值。

一个包含了很多（合法或者不合法的）纯赋值语句的例子：

```go
const N = 123
var x int
var y, z float32

N = 789 // error: N是一个不可变量
y = N   // ok: N被隐式转换为类型float32（或者N的类型被推断为float32）
x = y   // error: 类型不匹配
x = N   // ok: N被隐式转换为类型int（或者N的类型被推断为int）
y = x   // error: 类型不匹配
z = y   // ok
_ = y   // ok

z, y = y, z               // ok
_, y = y, z               // ok
z, _ = y, z               // ok
_, _ = y, z               // ok
x, y = 69, 1.23           // ok
x, y = y, x               // error: 类型不匹配
x, y = int(y), float32(x) // ok
```

Go不支持连等语法

#### 短变量声明形式

**短声明形式只能用来声明局部变量**。

每个短声明语句中必须至少有一个新声明的变量。

短声明形式不包含var关键字，并且不能指定变量的类型。

短变量声明中的赋值符号必须为:=。

在一个短声明语句的左侧，已经声明过的变量和新声明的变量可以共存。 但在一个标准声明语句中，所有左侧出现在的变量必须都为新声明的变量。

目前短声明语句有一个限制：出现在一个短声明左侧的项必须都为纯标识符。不能出现结构体值的字段，指针的解引用和容器类型值的元素索引项等

知变量声明示例：

```go
package main

func main() {
    // 变量lang和year都为新声明的变量。
    lang, year := "Go language", 2007

    // 这里，只有变量createdBy是新声明的变量。
    // 变量year已经在上面声明过了，所以这里仅仅
    // 改变了它的值，或者说它被重新声明了。
    year, createdBy := 2009, "Google Research"

    // 这是一个纯赋值语句。
    lang, year = "Go", 2012

    print(lang, "由", createdBy, "发明")
    print("并发布于", year, "年。")
    println()
}
```

#### 关于“赋值”这个术语

当“赋值”这个术语被提到的时候，它可以指一个纯赋值、一个短变量声明或者是一个初始值未省略的标准变量声明语句。

当y = x是一条合法的赋值语句时，我们可以说**x可以被赋给y**。 假设y的类型为Ty，有时为了叙述方便，我们也可以说**x可以被赋给类型Ty**。

#### 每个局部声明的变量至少要被有效使用一次

一个局部变量被声明之后至少要被有效使用一次，否则编译器将报错。 包级变量无此限制。

如果一个变量总是被当作赋值语句中的目标值，那么我们认为这个变量没有被有效使用过。

#### 若干包级变量在声明时刻的依赖关系将影响它们的初始化顺序

下面这个例子中的声明的变量的初始化顺序为`y = 5、c = y、b = c+1、a = b+1、x = a+1`。

```go
var x, y = a+1, 5         // 8 5
var a, b, c = b+1, c+1, y // 7 6 5
```

包级变量在初始化的时候不能相互依赖。比如，下面这个变量声明语句编译不通过。

```go
var x, y = y, x
```

### 值的可寻址性

在Go中，有些值是可以被寻址的。所有变量都是可以寻址的，所有常量都是不可被寻址。

### 非常量数字值相关的显式类型转换规则

在Go中，两个类型不一样的基本类型值是不能相互赋值的。 我们必须使用显式类型转换将一个值转换为另一个值的类型之后才能进行赋值。

- 一个非常量浮点数和整数可以显式转换到其它任何一个浮点数和整数类型。
- 一个非常量复数可以显式转换到其它任何一个复数类型。

上面已经提到，常量数字值的类型转换不能溢出。此规则不适用于非常量数字值的类型转换。 非常量数字值的类型转换中，溢出是允许的。 另外当将一个浮点数非常量值（比如一个变量）转换为一个整数类型的时候，舍入（或者精度丢失）也是允许的。 具体规则如下：

- 当从一个比特位数多的整数类型的非常量整数值向一个比特位数少的整数类型转换的时候，高位的比特将被舍弃，低位的比特将被保留。 我们称这种处理方式为截断（truncated）或者回绕（wrapped around）。
- 当从一个非常量的浮点数向一个整数类型转换的时候，浮点数的小数部分将被舍弃（向零靠拢）。
- 当一个非常量整数或者浮点数向一个浮点数类型转换的时候，精度丢失是可以发生的。
- 当一个非常量复数向另一个复数类型转换的时候，精度丢失也是可以发生的。
- 当一个非常量复数向另一个复数类型转换的时候，精度丢失也是可以发生的。
- 当一个显式转换涉及到非常量浮点数或者复数数字值时，如果源值溢出了目标类型的表示范围，则转换结果取决于具体编译器实现（即行为未定义）。

### 变量和常量的作用域

在Go中，我们可以使用一对大括号来显式形成一个（局部）代码块。一个代码块可以内嵌另一个代码块。 最外层的代码块称为包级代码块。 一个声明在一个内层代码块中的常量或者变量将遮挡另一个外层代码块中声明的同名变量或者常量。 比如，下面的代码中声明了3个名为x的变量。 内层的x将遮挡外层的x， 从而外层的x在内层的x声明之后在内层中将不可见。

```go
package main

const y = 70
var x int = 123 // 包级变量

func main() {
    // 此x变量遮挡了包级变量x。
    var x = true

    // 一个内嵌代码块。
    {
        x, y := x, y-10 // 这里，左边的x和y均为新声明的变量。
                        // 右边的x为外层声明的bool变量。
                        // 右边的y为包级变量。

        // 在此内层代码块中，从此开始，刚声明的x和y将遮挡外层声明x和y。

        x, z := !x, y/10 // z是一个新声明的变量。
                            // x和y是上一句中声明的变量。
        println(x, y, z) // false 60 6
    }
    println(x) // true
    println(y) // 70 （包级变量y从未修改）
    /*
    println(z) // error: z未定义。z的作用域仅限于上面的最内层代码块。
    */
}
```

### 更多关于常量声明

#### 一个类型不确定常量所表示的值在可以溢出其默认类型

比如，下例中的三个类型不确定常量均溢出了它们各自的默认类型，但是此程序编译和运行都没问题。

```go
package main

// 三个类型不确定常量。
const n = 1 << 64          // 默认类型为int
const r = 'a' + 0x7FFFFFFF // 默认类型为rune
const x = 2e+308           // 默认类型为float64

func main() {
    _ = n >> 2
    _ = r - 0x7FFFFFFF
    _ = x / 2
}
```

#### 每个常量标识符将在编译的时候被其绑定的字面值所替代

常量声明可以看作是增强型的C语言中的#define宏。 在编译阶段，所有的标识符将被它们各自绑定的字面值所替代。

如果一个运算中的所有运算数都为常量，则此运算的结果也为常量。

一个例子：

```go
package main

const X = 3
const Y = X + X
var a = X

func main() {
    b := Y
    println(a, b, X, Y)
}
```

上面这段程序代码将在编译阶段被重写为下面这样：

```go
package main

var a = 3

func main() {
    b := 6
    println(a, b, 3, 6)
}
```

## 运算操作符

算术运算符、位运算符、比较运算符、布尔运算符和字符串衔接运算符。 这些运算符要么是二元的（需要两个操作数），要么是一元的（需要一个操作数）。 所有这些运算符运算都只返回一个结果。

二元运算符运算需要其涉及的两个操作数类型必须一样

- 如果这两个操作数都是类型确定值，则它们的类型必须相同，或者其中一个操作数可以被隐式转换到另一个操作数的类型。
- 如果其中只有一个操作数是类型确定的，则要么另外一个类型不确定操作数可以表示为此类型确定操作数的类型的值，要么此类型不确定操作数的默认类型的任何值可以被隐式转换到此类型确定操作数的类型。
- 如果这两个操作数都是类型不确定的，则它们必须同时都为两个布尔值，同时都为两个字符串值，或者同时都为两个基本数字值。

一个运算符（一元或者二元）运算要求其涉及的某个操作数的类型必须为某个特定类型

- 如果这个操作数是类型确定的，则它的类型必须为所要求的特定类型，或者此操作数可以被隐式转换为所要求的特定类型。
- 如果一个操作数是类型不确定的，则要么此操作数可以表示为所要求的特定类型值，要么此操作数的默认类型的任何值可以被隐式转换为所要求的特定类型。

### 常量表达式

当一个表达式中涉及到的所有操作数都是常量时，此表达式称为一个常量表达式。 一个常量表达式的*估值是在编译阶段进行的*。一个常量表达式的估值结果依然是一个常量。 如果一个表达式中涉及到的操作数中至少有一个不为常量，则此表达式称为非常量表达式。

### 算术运算符

五个基本二元算术运算符：

<table class="table table-bordered text-center" style="width:100%;">
<thead>
<tr class="active">
<th class="text-center" style="white-space: nowrap;">字面形式</th>
<th class="text-center" style="white-space: nowrap;">名称</th>
<th class="text-center">对两个运算数的要求</th>
</tr>
</thead>
<tbody>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">+</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        加法
    </td>
    <td style="vertical-align: middle;" class="text-left" rowspan="4">
        两个运算数的类型必须相同并且为基本数值类型。
    </td>
</tr>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">-</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        减法
    </td>
</tr>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">*</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        乘法
    </td>
</tr>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">/</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        除法
    </td>
</tr>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">%</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        余数
    </td>
    <td style="vertical-align: middle;" class="text-left">
        两个运算数的类型必须相同并且为基本整数数值类型。
    </td>
</tr>
</tbody>
</table>

六种位运算符（也属于算术运算）：

<table class="table table-bordered text-center" style="width:100%;">
<thead>
<tr class="active">
<th class="text-center" style="white-space: nowrap;">字面形式</th>
<th class="text-center" style="white-space: nowrap;">名称</th>
<th class="text-center">对两个操作数的要求以及机制解释</th>
</tr>
</thead>
<tbody>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">&amp;</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        位与
    </td>
    <td style="vertical-align: middle;" class="text-left" rowspan="4">
        <p>
        两个操作数的类型必须相同并且为基本<b>整数</b>数值类型。
        </p>
        机制解释（下标<code>2</code>表明一个字面形式为二进制）：
        <ul>
        <li>
            <code>1100<sub>2</sub> &amp; 1010<sub>2</sub></code>
            得到 <code>1000<sub>2</sub></code>
        </li>
        <li>
            <code>1100<sub>2</sub> | 1010<sub>2</sub></code>
            得到 <code>1110<sub>2</sub></code>
        </li>
        <li>
            <code>1100<sub>2</sub> ^ 1010<sub>2</sub></code>
            得到 <code>0110<sub>2</sub></code>
        </li>
        <li>
            <code>1100<sub>2</sub> &amp;^ 1010<sub>2</sub></code>
            得到 <code>0100<sub>2</sub></code>
        </li>
        </ul>
    </td>
</tr>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">|</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        位或
    </td>
</tr>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">^</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        （位）异或
    </td>
</tr>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">&amp;^</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        清位
    </td>
</tr>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">&lt;&lt;</th>
    <td style="vertical-align: middle; white-space: nowrap;">
        左移位
    </td>
    <td style="vertical-align: middle;" class="text-left" rowspan="2">
        <p>
        左操作数必须为一个<b>整数</b>，右操作数必须为一个<b>无符号整数</b>类型的类型确定值或者一个可以表示成<code>uint</code>值的类型不确定（常数）值<sup>(1)</sup>。
        </p>
        机制解释：
        <ul>
        <li>
            <code>1100<sub>2</sub> &lt;&lt; 3</code>
            得到 <code>1100000<sub>2</sub></code>（低位补零）
        </li>
        <li>
            <code>1100<sub>2</sub> &gt;&gt; 3</code>
            得到 <code>1<sub>2</sub></code>（低位被舍弃）
        </li>
        </ul>
        <p>
        如果左操作数的类型为一个有符号整数，则在右移位运算中，左操作数的符号位（即最高位）将总是保留在结果中。
        比如如果左操作数<code>-128</code>的类型为<code>int8</code>（二进制表示为<code>10000000<sub>2</sub></code>），
        则<code>10000000<sub>2</sub> &gt;&gt; 1</code>的结果为<code>11000000<sub>2</sub></code>（即<code>-64</code>）。
        </p>
    </td>
</tr>
<tr>
    <th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">&gt;&gt;</th>
    <td style="vertical-align: middle; white-space: nowrap;" class="text-center">
        右移位
    </td>
</tr>
</tbody>
</table>

三个一元算术运算符

<table class="table table-bordered text-center" style="width:100%;">
<thead>
	<tr class="active">
	<th class="text-center" style="white-space: nowrap;">字面形式</th>
	<th class="text-center" style="white-space: nowrap;">名称</th>
	<th class="text-center">解释</th>
	</tr>
</thead>
<tbody>
	<tr>
		<th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">+</th>
		<td style="vertical-align: middle; white-space: nowrap;" class="text-center">
			取正数
		</td>
		<td style="vertical-align: middle;" class="text-left">
			<code>+n</code>等价于<code>0 + n</code>.
		</td>
	</tr>
	<tr>
		<th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">-</th>
		<td style="vertical-align: middle; white-space: nowrap;" class="text-center">
			取负数
		</td>
		<td style="vertical-align: middle;" class="text-left">
			<code>-n</code>等价于<code>0 - n</code>.
		</td>
	</tr>
	<tr>
		<th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">^</th>
		<td style="vertical-align: middle; white-space: nowrap;" class="text-center">
			位反（或位补）
		</td>
		<td style="vertical-align: middle;" class="text-left">
			<code>^n</code>等价于<code>m ^ n</code>，<code>m</code>是一个和<code>n</code>同类型并且它的二进制表示中所有比特位均为1。
			比如如果<code>n</code>的类型为<code>int8</code>，则<code>m</code>的值为<code>-1</code>；如果<code>n</code>的类型为<code>uint8</code>，则<code>m</code>的值为<code>255</code>。
		</td>
	</tr>
</tbody>
</table>

注意：

- 在很多其它流行语言中，位反运算符是用~表示的。
- 和一些其它流行语言一样，加号运算符+也可用做字符串衔接运算符。
- 和C及C++语言一样，*除了可以当作乘号运算符，它也可以用做指针解引用运算符； &除了可以当作位与运算符，它也可以用做取地址运算符。
- 和Java不一样，Go支持无符号数，所以Go不需要无符号右移运算符>>>。
- Go不支持幂运算符， 我们必须使用math标准库包中的Pow函数来进行幂运算。
- 清位运算符`&^`是Go中特有的一个运算符。 `m &^ n`等价于`m & (^n)`。

示例：

```go
func main() {
    var (
        a, b    float32 = 12.0, 3.14
        c, d    int16   = 15, -6
        e       uint8   = 7
    )

    // 这些行编译没问题。
    _ = 12 + 'A' // 两个类型不确定操作数（都为数值类型）
    _ = 12 - a   // 类型不确定值12将被当做a的类型（float32）使用。
    _ = a * b    // 两个同类型的类型确定操作数。
    _ = c % d
    _, _ = c + int16(e), uint8(c) + e
    _, _, _, _ = a / b, c / d, -100 / -9, 1.23 / 1.2
    _, _, _, _ = c | d, c & d, c ^ d, c &^ d
    _, _, _, _ = d << e, 123 >> e, e >> 3, 0xF << 0
    _, _, _, _ = -b, +c, ^e, ^-1

    // 这些行编译将失败。
    _ = a % b   // error: a和b都不是整数
    _ = a | b   // error: a和b都不是整数
    _ = c + e   // error: c和e的类型不匹配
    _ = b >> 5  // error: b不是一个整数
    _ = c >> -5 // error: -5不是一个无符号整数
    _ = e << c  // error: c不是一个无符号整数
}
```

#### 关于算术运算的结果

除了移位运算，对于一个二元算术运算，

- 如果它的两个操作数都为类型确定值，则此运算的结果也是一个和这两个操作数类型相同的类型确定值。
- 如果只有一个操作数是类型确定的，则此运算的结果也是一个和此类型确定操作数类型相同的类型确定值。 另一个类型不确定操作数的类型将被推断为（或隐式转换为）此类型确定操作数的类型。
- 如果它的两个操作数均为类型不确定值，则此运算的结果也是一个类型不确定值。 在运算中，两个操作数的类型将被设想为它们的默认类型中一个（按照此优先级来选择：complex128高于float64高于rune高于int）。 结果的默认类型同样为此设想类型。 比如，如果一个类型不确定操作数的默认类型为int，另一个类型不确定操作数的默认类型为rune， 则前者的类型在运算中也被视为rune，运算结果为一个默认类型为rune的类型不确定值。

```go
fmt.Println(reflect.TypeOf(12 + 'a'))
fmt.Println(reflect.TypeOf(12 + 1))
```

对于移位运算，首先移位运算的结果肯定都是整数。

- 如果左操作数是一个类型确定值（则它的类型必定为整数），则此移位运算的结果也是一个和左操作数类型相同的类型性确定值。
- 如果左操作数是一个类型不确定值并且右操作数是一个**常量**，则左操作数将总是被视为一个整数。 如果它的默认类型不是一个整数（rune或int），则它的默认类型将被视为int。 此移位运算的结果也是一个类型不确定值并且它的的默认类型和左操作数的默认类型一致。
- 如果左操作数是一个类型不确定值并且右操作数是一个**非常量**，则左操作数将被首先*转化为运算结果的期待设想类型*。 如果期待设想类型并没有被指定，则左操作数的默认类型将被视为它的期待设想类型。 如果此*期待设想类型不是一个基本整数类型，则编译报错*。 当然最终运算结果是一个类型为此期待设想类型的类型确定值。

一些非移位算术运算的例子：

```go
func main() {
    const X, Y, Z = 2, 'A', 3i // 三个类型不确定常量。它们的默认类型
                                // 分别为：int、rune和complex64.

    var a, b int = X, Y // 两个类型确定值

    d := X + Y // 变量d的类型被推断为Y的默认类型：rune（亦即int32）。
    e := Y - a // 变量e的类型被推断为a的类型：int。
    f := a * b // 变量f的类型和a及b的类型一样：int。
    g := Z * Y // 变量g的类型被推断为Z的默认类型：complex64。

    println(X, Y, Z)    // 2 65 (+0.000000e+000+3.000000e+000i)
    println(d, e, f, g) // 67 63 130 (+0.000000e+000+1.950000e+002i)
}
```

一个移位算术运算的例子：

```go
const N = 2
const A = 3.0 << N       // A == 6，它是一个默认类型为int的类型不确定值。
const B = int8(3.0) << N // B == 6，它是一个类型为int8的类型确定值。

var m = uint(32)
// 下面的三行是相互等价的。
var x int64 = 1 << m  // 1的类型将被设想为int64，而不是int。
var y = int64(1 << m) // 同上，1的类型将被设想为int64，而不是int。
var z = int64(1) << m // 同上

// 下面这两行编译不通过。
/*
var _ = 1.23 << m // error: shift of type float64
const _ = 1 << B  // error: the right operand must be unsigned.
*/
```

```go
const n = uint(2)
var m = uint(2)

// 这两行编译没问题。
var _ float64 = 1 << n
var _ = float64(1 << n)

// 这两行编译失败。
var _ float64 = 1 << m  // error
var _ = float64(1 << m) // error
//上面两行编译失败是因为它们都等价于下面这两行：
var _ = float64(1) << m
var _ = 1.0 << m // error: shift of type float64
```

#### 关于溢出

- 一个类型确定数字型常量所表示的值是不能溢出它的类型的表示范围的。
- 一个类型不确定数字型常量所表示的值是可以溢出它的默认类型的表示范围的。 当一个类型不确定数字常量值溢出它的默认类型的表示范围时，此数值不会被截断（亦即回绕）。
- 将一个非常量数字值转换为其它数字类型时，此非常量数字值可以溢出转化结果的类型。 在此转换中，当溢出发生时，转化结果为此非常量数字值的截断（亦即回绕）表示。

```go
// 结果为非常量
var a, b uint8 = 255, 1
var c = a + b  // c==0。a+b是一个非常量表达式，
               // 结果中溢出的高位比特将被截断舍弃。
var d = a << b // d == 254。同样，结果中溢出的高位比特将被截断舍弃。

// 结果为类型不确定常量
const X = 0x1FFFFFFFF * 0x1FFFFFFFF // 没问题，尽管X溢出它的默认类型int。
const R = 'a' + 0x7FFFFFFF          // 没问题，尽管R溢出它的默认类型rune。

// 运算结果或者转换结果为类型确定常量
var e = X                // error: X溢出int。
var h = R                // error: R溢出rune。
const Y = 128 - int8(1)  // error: 128溢出int8。
const Z = uint8(255) + 1 // error: 256溢出uint8。
```

#### 关于除法和余数运算

假设两个操作数x和y的类型为同一个整数类型， 则它们通过除法和余数运算得到的商`q（= x / y）`和余数`r（= x % y）`满足`x == q*y + r`（`|r| < |y|`）。如果余数`r`不为零，则它的符号和被除数`x`相同。商`q`的结果为`x / y`向零靠拢截断。

如果除数`y`是一个常量，则它必须不为0，否则编译不通过。如果除数`y`在运行时为零且为整数，则会发生运行时恐慌（panic）。恐慌类似与某些其它语言中的异常（exception）。

```go
println( 5/3,   5%3)  // 1 2
println( 5/-3,  5%-3) // -1 2
println(-5/3,  -5%3)  // -1 -2
println(-5/-3, -5%-3) // 1 -2

println(5.0 / 3.0)     // 1.666667
println((1-1i)/(1+1i)) // -1i

var a, b = 1.0, 0.0
println(a/b, b/b) // +Inf NaN

_ = int(a)/int(b) // 编译没问题，但在运行时刻将造成恐慌。

// 这两行编译不通过。
println(1.0/0.0) // error: 除数为0
println(0.0/0.0) // error: 除数为0
```

#### `op=` 运算符

对于一个二元算数运算符op，语句x = x op y可以被简写为x op= y。 在这个简写的语句中，**x只会被估值一次**。

#### 自增和自减操作符

和很多其它流行语言一样，Go也支持自增（++）和自减（--）操作符。 不过和其它语言不一样的是，**自增（aNumber++）和自减（aNumber--）操作操作没有返回值， 所以它们不能当做表达式来使用**。 另一个显著区别是，在Go中，自增（++）和自减（--）操作符只能后置，不能前置。

### 字符串衔接运算符

上面已经提到了，加法运算符也可用做字符串衔接运算符。

| 字面形式 | 名称       | 对两个操作数的要求                   |
| -------- | ---------- | ------------------------------------ |
| +    | 字符串衔接 | 两个操作数必须为同一类型的字符串值。 |

### 布尔运算符

Go支持两种布尔二元运算符和一种布尔一元运算符。

<table class="table table-bordered text-center" style="width:100%;">
<thead>
	<tr class="active">
	<th class="text-center" style="white-space: nowrap;">字面形式</th>
	<th class="text-center" style="white-space: nowrap;">名称</th>
	<th class="text-center">对操作值的要求</th>
	</tr>
</thead>
<tbody>
	<tr>
		<th scope="row" class="text-center" style="vertical-align: middle; white-space: nowrap;">&amp;&amp;</th>
		<td style="vertical-align: middle;" class="text-center">
			布尔与（二元）
		</td>
		<td style="vertical-align: middle;" class="text-left" rowspan="2">
			两个操作值的类型必须为同一布尔类型。
		</td>
	</tr>
	<tr>
		<th scope="row" class="text-center" style="vertical-align: middle; white-space: nowrap;">||</th>
		<td style="vertical-align: middle;" class="text-center">
			布尔或（二元）
		</td>
	</tr>
	<tr>
		<th scope="row" class="text-center" style="vertical-align: middle; white-space: nowrap;">!</th>
		<td style="vertical-align: middle;" class="text-center">
			布尔否（一元）
		</td>
		<td style="vertical-align: middle;" class="text-left">
			唯一的一个操作值的类型必须为一个布尔类型。
		</td>
	</tr>
</tbody>
</table>

### 比较运算符

Go支持6种比较运算符：

<table class="table table-bordered text-center" style="width:100%;">
<thead>
	<tr class="active">
	<th class="text-center" style="white-space: nowrap;">字面形式</th>
	<th class="text-center" style="white-space: nowrap;">名称</th>
	<th class="text-center">对两个操作值的要求</th>
	</tr>
</thead>
<tbody>
	<tr>
		<th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">==</th>
		<td style="vertical-align: middle; white-space: nowrap;">
			等于
		</td>
		<td style="vertical-align: middle;" class="text-left" rowspan="2">
			<p>
			如果两个操作数都为类型确定的，则它们的类型必须一样，或者其中一个操作数可以隐式转换为另一个操作数的类型。
			两者的类型必须都为可比较类型（将在以后的文章中介绍）。
			</p>
			<p>
			如果只有一个操作数是类型确定的，则另一个类型不确定操作数必须可以隐式转换到类型确定操作数的类型。
			</p>
			<p>
			如果两个操作数都是类型不确定的，则它们必须同时为两个类型不确定布尔值、两个类型不确定字符串值或者另个类型不确定数字值。
			</p>
		</td>
	</tr>
	<tr>
		<th scope="row" style="vertical-align: middle;" class="text-center">!=</th>
		<td style="vertical-align: middle; white-space: nowrap;" class="text-center">
			不等于
		</td>
	</tr>
	<tr>
		<th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">&lt;</th>
		<td style="vertical-align: middle; white-space: nowrap;" class="text-center">
			小于
		</td>
		<td style="vertical-align: middle;" class="text-left" rowspan="4">
			两个操作值的类型必须相同并且它们的类型必须为整数类型、浮点数类型或者字符串类型。
		</td>
	</tr>
	<tr>
		<th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">&lt;=</th>
		<td style="vertical-align: middle; white-space: nowrap;" class="text-center">
			小于或等于
		</td>
	</tr>
	<tr>
		<th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">&gt;</th>
		<td style="vertical-align: middle; white-space: nowrap;" class="text-center">
			大于
		</td>
	</tr>
	<tr>
		<th scope="row" style="vertical-align: middle; white-space: nowrap;" class="text-center">&gt;=</th>
		<td style="vertical-align: middle; white-space: nowrap;" class="text-center">
			大于或等于
		</td>
	</tr>
</tbody>
</table>

### 操作符运算的优先级

Go中的操作符运算的优先级和其它流行语言有一些差别。 下面列出了本文介绍的操作符的优先级。 每行中的操作符的优先级是一样的。优先级逐行递减。

    *   /   %   <<  >>  &   &^
    +   -   |   ^
    ==  !=  <   <=  >   >=
    &&
    ||

一个和其它流行语言明显的差别是，移位运算<<和>>的优先级比加减法+和-的优先级要高。

一个表达式（做为一个子表达式）可以出现在另一个表达式中。 这个子表达式的估值结果将成为另一个表达式的一个操作数。 在这样的复杂表达式中，对于相同优先级的运算，它们将从左到右进行估值。 和很多其它语言一样，我们也可用一对小括号()来提升一个子运算的优先级。

## 函数声明和调用

### 函数声明

一个函数声明从左到右由以下部分组成：

1. 第一部分是func关键字。
2. 第二部分是函数名称。函数名称必须是一个标识符。
3. 第三部分是输入参数列表。输入参数声明列表必须用一对小括号括起来。输入参数声明有时也称为形参声明。
4. 第四部分是输出结果声明列表。在Go中，一个函数可以有多个返回值。当一个函数的输出结果声明列表包含多个标识符时，此输出结果声明列表必须用一对小括号括起来。否则，小括号是可选的。返回值可以被命名，并且像变量一样使用。
5. 最后一部分是函数体。函数体必须用一对大括号括起来。 一对大括号和它其间的代码形成了一个显式代码块。 在一个函数体内，return关键字可以用来结束此函数的正常向前执行流程并进入此函数的退出阶段

```go
func SquaresOfSumAndDiff(a int64, b int64) (s int64, d int64) {
    x, y := a + b, a - b
    s = x * x
    d = y * y
    return // <=> return s, d
}
```

输出结果声明列表中的所有声明中的结果名称可以（而且必须）同时出现或者同时省略。 这两种方式在实践中都使用得很广泛。 如果一个返回结果声明中的结果名称没有省略，则这个返回结果称为有名返回结果。否则称为匿名返回结果。

如果一个函数声明的所有返回结果均为匿名的，则在此函数体内的返回语句return关键字后必须跟随一系列返回值，这些返回值和此函数的各个返回结果声明一一对应。

```go
func SquaresOfSumAndDiff(a int64, b int64) (int64, int64) {
    return (a+b) * (a+b), (a-b) * (a-b)
}
```

尽管一个函数声明中的输入参数和返回结果看上去是声明在这个函数体的外部，但是在此函数体内，这些输入参数和输出结果被当作局部变量来使用。 但输入参数和输出结果和普通局部变量还是有一点区别的：目前的主流Go编译器不允许一个名称不为_的普通局部变量被声明而不有效使用。

Go不支持输入参数默认值。每个返回结果的默认值是它的类型的零值。

和普通的变量声明一样，如果若干连续的输入参数或者返回结果的类型相同，则在它们的声明中可以共用一个类型。

```go
func SquaresOfSumAndDiff(a, b int64) (s, d int64) {
    return (a+b) * (a+b), (a-b) * (a-b)
    // 上面这行等价于下面这行：
    // s = (a+b) * (a+b); d = (a-b) * (a-b); return
}
```

### 函数调用

一个声明的函数可以通过它的名称和一个实参列表来调用之。 一个实参列表必须用小括号括起来。 实参列表中的每一个单值实参对应一个形参声明。

一个实参值的类型不必一定要和其对应的形参声明的类型一样。 但如果一个实参值的类型和其对应的形参声明的类型不一致，则此实参必须能够隐式转换到其对应的形参的类型。

```go
package main

func SquaresOfSumAndDiff(a int64, b int64) (int64, int64) {
    return (a+b) * (a+b), (a-b) * (a-b)
}

func CompareLower4bits(m, n uint32) (r bool) {
    r = m&0xF > n&0xf
    return
}

// 使用一个函数调用的返回结果来初始化一个包级变量。
var v = VersionString()

func main() {
    println(v) // v1.0
    x, y := SquaresOfSumAndDiff(3, 6)
    println(x, y) // 81 9
    b := CompareLower4bits(uint32(x), uint32(y))
    println(b) // false
    // "Go"的类型被推断为string；1的类型被推断为int32。
    doNothing("Go", 1)
}

func VersionString() string {
    return "v1.0"
}

func doNothing(string, int32) {
}
```

### 函数调用的退出阶段

在Go中，当一个函数调用返回后（比如执行了一个return语句或者函数中的最后一条语句执行完毕）， 此调用可能并未立即退出。一个函数调用从返回开始到最终退出的阶段称为此函数调用的退出阶段（exiting phase）。

### 匿名函数

Go支持匿名函数。定义一个匿名函数和声明一个函数类似，但是一个匿名函数的定义中不包含函数名称部分。 注意匿名函数定义不是一个函数声明。

```go
package main

func main() {
    // 这个匿名函数没有输入参数，但有两个返回结果。
    x, y := func() (int, int) {
        println("This fucntion has no parameters.")
        return 3, 4
    }() // 一对小括号表示立即调用此函数。不需传递实参。

    // 下面这些匿名函数没有返回结果。

    func(a, b int) {
        println("a*a + b*b =", a*a + b*b) // a*a + b*b = 25
    }(x, y) // 立即调用并传递两个实参。

    func(x int) {
        // 形参x遮挡了外层声明的变量x。
        println("x*x + y*y =", x*x + y*y) // x*x + y*y = 32
    }(y) // 将实参y传递给形参x。

    func() {
        println("x*x + y*y =", x*x + y*y) // x*x + y*y = 25
    }() // 不需传递实参。
}
```

注意，上例中的最后一个匿名函数处于变量x和y的作用域内，所以在它的函数体内可以直接使用这两个变量。 这样的函数称为闭包（closure）。事实上，Go中的所有的自定义函数（包括声明的函数和匿名函数）都可以被视为闭包。 这就是为什么Go中的函数使用起来为什么像动态语言中的函数一样灵活。

## 代码包和包引入

和很多现代编程语言一样，Go代码包（package）来组织管理代码。 我们必须先引入一个代码包（除了builtin标准库包）才能使用其中导出的资源（比如函数、类型、变量和有名常量等）。

### 包引入

- `package` 指定所处包，程序入口main函数必须处于一个名为main的代码包中。
- `import` 关键字引入包
- 在调用包中资源时必需加上包引入名称。`aImportName.AnExportedIdentifier`这种形式称为一个限定标识符。
- 当一个代码包被引入一个Go源文件时，只有此代码包中的导出资源（名称为大写字母的变量、常量、函数和类型等）可以在此源文件被使用。
- 一个包引入也可称为一个包声明。一个包声明只在当前包含此声明的源文件内可见。
- 多个包引入语句可以用一对小括号来合并成一个包引入语句。比如下面这例。

```go
package main

import "fmt"

func main() {
    fmt.Println("Go has", 25, "keywords.")
}
```

```go
package main

// 一条包引入语句引入了三个代码包。
import (
    "fmt"
    "math/rand"
    "time"
)

func main() {
    rand.Seed(time.Now().UnixNano()) // 设置随机数种子
    fmt.Printf("下一个伪随机数总是%v。\n", rand.Uint32())
}
```

### 关于`fmt.Printf`函数调用的输出格式

下面是一些常用的占位字符组合：

- %v：将被替换为**对应实参字符串**表示形式。
- %T：将替换为对应实参的**类型**的字符串表示形式。
- %x：将替换为对应实参的**十六进制**表示。实参的类型必须为整数，整数数组（array）或者整数切片（slice）等。
- %s：将被替换为对应实参的**字符串**表示形式。实参的类型必须为*字符串或者字节切片*（byte slice）类型。
- %%：将被替换为一个百分号。

一个例子：

```go
package main

import "fmt"

func main() {
    a, b := 123, "Go"
    fmt.Printf("a == %v == 0x%x, b == %s\n", a, a, b)
    fmt.Printf("type of a: %T, type of b: %T\n", a, b)
}
```

输出：

    a == 123 == 0x7b, b == Go
    type of a: int, type of b: string
    1% 50% 99%

### 代码包文件夹、代码包引入路径、和代码包依赖关系

一个代码包可以由若干Go源文件组成。一个代码包的源文件须都处于同一个文件夹下。 一个文件夹（不包含子文件夹）下的所有源文件必须都处于同一个代码包中，亦即这些源文件开头的package pkgname语句必须一致。 所以，一个代码包对应着一个文件夹（不包含子文件夹），反之亦然。 对应着一个代码包的文件夹称为此代码包的文件夹。 一个代码包文件夹下的每个子文件夹对应的都是另外一个独立的代码包。

一个Go代码包可以选择是否支持模块模式。Go SDK 1.11引入了一个环境变量GO111MODULE。这个环境变量的默认值是auto，它的其它两个可能取值为on和off。 如果此环境变量取值为on，则所有的代码包都支持模块模式； 如果此环境变量取值为off，则所有的代码包都不支持模块模式； 如果此环境变量取值为auto，则只有同时满足下面两个条件的代码包才支持模块模式：

1. 代码包文件夹必须处于GOPATH环境变量指定的所有路径的src子目录以外。
2. 代码包文件夹或者它的某个上级目录文件夹中含有一个名为go.mod文件。

对于一个不支持模块模式的代码包，通常它应该处于某个GOPATH/src路径之下。 它的包引入路径为此包的文件夹相对于GOPATH/src或者某个vendor目录的相对路径。

在不支持模块模式的情形下，假设有一个如下的包层级结构，则：

- 两个foo包的引入路径均为w/foo。
- x包、y包和z包的引入路径均分别为x、x/y和x/z。

注意：

- 当在y.go文件中引入一个引入路径均为w/foo的包的时候，被引入的包为GOPATH/src/x/y/vendor/w/foo文件夹中的包。
- 当在x.go或者z.go文件中引入一个引入路径为w/foo的包的时候，被引入的包为GOPATH/src/x/vendor/w/foo文件夹中的包。

```text
_ GOPATH
  |_ src
     |_ x
        |_ vendor
        |  |_ w
        |     |_ foo
        |        |_ foo.go    // package foo
        |_ y
        |  |_ vendor
        |  |  |_ w
        |  |     |_ foo
        |  |        |_ foo.go // package foo
        |  |_ y.go            // package y
        |_ z
        |  |_ z.go            // package z
        |_ x.go               // package x
```

对于一个支持模块模式的代码包，其对应的go.mod文件中必须指定此go.mod文件所处的最内层文件夹对应的代码包的引入路径。 指定引入路径的格式为module ImportPath。 在这种模式下，只有和与此go.mod文件处于同一文件夹下的vendor文件夹才被视为特殊的文件夹。 并且请注意，如果go命令的选项-mod=vendor未提供，则此vendor文件夹的包将被忽略，而下载缓存（处于项目代码包之外）中相应的代码包将被使用。

在支持模块模式的情形下，假设有一个如下的包层级结构，则：

- 第一个foo包的引入路径均为w/foo。 此包的父目录vendor文件夹被视为一个特殊的文件夹。
- 另外一个foo包的引入路径均为`example.com/mypkg/x/y/vendor/w/foo`。 注意这里的vendor文件夹被视为一个普通的包文件夹。
- x包、y包和z包的引入路径均分别为`example.com/mypkg/x、example.com/mypkg/x/y`和`example.com/mypkg/x/z`。

注意：当在x.go、y.go或者z.go文件中引入一个引入路径均为w/foo的包的时候，被引入的包均为MyProject/vendor/w/foo文件夹中的包。

```text
_ MyProject
     |_ go.mod                // module example.com/mypkg
     |_ vendor
     |  |_ w
     |     |_ foo
     |        |_ foo.go       // package foo
     |_ x
        |_ y
        |  |_ vendor
        |  |  |_ w
        |  |     |_ foo
        |  |        |_ foo.go // package foo
        |  |_ y.go            // package y
        |_ z
        |  |_ z.go            // package z
        |_ x.go               // package x
```

如果一个包文件夹含有一个go.mod文件，则请不要在它的任何（直接或间接）子包文件夹中也放置一个go.mod文件。

当一个代码包中的某个文件引入了另外一个代码包，则我们说前者代码包依赖于后者代码包。

Go不支持循环引用（依赖）。 如果一个代码包a依赖于代码包b，同时代码包b依赖于代码包c，则代码包c中的源文件不能引入代码包a和代码包b，代码包b中的源文件也不能引入代码包a。

当然，一个代码包中的源文件不能也没必要引入此代码包本身。

今后，我们称一个程序中含有main入口函数的名称为main的代码包为程序代码包，称其它代码包为库代码包。 一个程序只能有一个程序代码包。程序代码包不能被其它代码包引入。

代码包文件夹的名称并不要求一定要和其对应的代码包的名称相同。 但是，库代码包文件夹的名称最好设为和其对应的代码包的名称相同。 因为一个代码包的引入路径中包含的是此包的文件夹名，但是此包的默认引入名为此包的名称。 如果两者不一致，会使人感到困惑。

另一方面，最好给每个程序代码包指定一个有意义的名字，而不是它的包名main。

> 此项为Go Modules为Go包管理工具的之一，后续研究

### `init`函数

在一个代码包中，甚至一个源文件中，可以声明**若干名为init的函数**。 这些init函数必须不带任何输入参数和返回结果。

注意，我们不能声明名为init的包级变量、常量或者类型。

在程序运行时刻，在进入main入口函数之前，每个init函数在此包加载的时候将被**串行执行**并且只执行一遍。

### 程序资源初始化顺序

包的执行顺序：

- 在 main 包中的 go 文件默认总是会被执行
- 同包下的不同 go 文件，按照文件名“从小到大”排序顺序执行
- 其他的包只有被 main 包 import 才会执行，按照 import 的先后顺序执行
- 被递归 import 的包的初始化顺序与 import 顺序相反，例如：导入顺序 main –> A –> B –> C，则初始化顺序为 C –> B –> A –> main
- 一个包被其它多个包 import，但只能被初始化一次
- main 包总是被最后一个初始化，因为它总是依赖别的包
- 避免出现循环 import，例如：A –> B –> C –> A

init()、main() 是 go 语言中的保留函数，两个函数在 go 语言中的区别如下：
相同点：

- 两个函数在定义时不能有任何的参数和返回值
- 该函数只能由 go 程序自动调用，不可以被引用

不同点：

- init 可以应用于任意包中，且可以重复定义多个。
- main 函数只能用于 main 包中，且只能定义一个。

两个函数的执行顺序：

- 对同一个 go 文件的 init( ) 调用顺序是从上到下的
- 对同一个 package 中的不同文件，将文件名按字符串进行“从小到大”排序，之后顺序调用各文件中的init()函数
- 对于不同的 package，如果不相互依赖的话，按照 main 包中 import 的顺序调用其包中的 init() 函数
- 如果 package 存在依赖，调用顺序为最后被依赖的最先被初始化，例如：导入顺序 main –> A –> B –> C，则初始化顺序为 C –> B –> A –> main，一次执行对应的 init 方法。

在同一个文件中，包级常量、变量、init()、main() 依次进行初始化。

### 完整的引入声明语句形式

一个引入声明语句的完整形式为：

`import importname "path/to/package"`

其中引入名importname是可选的，它的默认值为被引入的包的包名（不是文件夹名）。

如果一个包引入声明中的importname没有省略，则限定标识符使用的前缀必须为importname，而不是被引入的包的名称。

```go
package main

import (
    format "fmt"
    random "math/rand"
    "time"
)

func main() {
    random.Seed(time.Now().UnixNano())
    format.Print("一个随机数:", random.Uint32(), "\n")

    // 下面这两行编译不通过，因为rand不可识别。
    /*
    rand.Seed(time.Now().UnixNano())
    fmt.Print("一个随机数:", rand.Uint32(), "\n")
    */
}
```

一个完整引入声明语句形式的引入名importname可以是一个句点(.)。 这样的引入称为句点引入。使用被句点引入的包中的导出资源时，限定标识符的前缀必须省略。

```go
package main

import (
    . "fmt"
    . "time"
)

func main() {
    Println("Current time:", Now())
}
```

一个完整引入声明语句形式的引入名importname可以是一个空标识符(_)。 这样的引入称为匿名引入。一个包被匿名引入的目的主要是为了加载这个包，从而使得这个包中的资源得以初始化。 被匿名引入的包中的init函数将被执行并且仅执行一遍。

### 每个非匿名引入必须至少被使用一次

除了匿名引入，其它引入必须在代码中被使用一次。

## 表达式、语句和简单语句

简单说来，一个表达式表示一个值，而一条语句表示一个操作。有些个表达式可能同时表示多个值，有些语句可能是由很多更基本的语句组成的。

Go中有六种简单语句类型：

1. 变量短声明语句。
2. 纯赋值语句，包括x op= y这种运算形式。
3. 有返回结果的函数或方法调用，以及数据通道的接收数据操作。
4. 数据通道的发送数据操作。
5. 空语句。
6. 自增（x++）和自减（x--）语句。

注意：和C/C++不一样，在Go中，自增和自减语句**不能被当作表达式**使用。

一些非简单语句

- 标准变量声明语句。是的，短声明语句属于简单语句，但是标准变量声明语句不属于。
- （有名）常量声明语句。
- 类型声明语句。
- （代码）包引入语句。
- 显式代码块。一个显式代码块起始于一个左大括号{，终止于一个右大括号}。 一个显式代码块中可以包含若干子语句。
- 函数声明。 一个函数声明中可以包含若干子语句。
- 流程控制跳转语句。
- 函数返回（return）语句。
- 延迟函数调用和协程创建语句。

一些表达式和语句的例子

```go
// 一些非简单语句：
import "time"
var a = 123
const B = "Go"
type Choice bool
func f() int {
    for a < 10 {
        break
    }

    // 这是一个显式代码块。
    {
        // ...
    }
    return 567
}

// 一些简单语句的例子：
c := make(chan bool) // 数据通道将在以后讲解
a = 789
a += 5
a = f() // 这是一个纯赋值语句
a++
a--
c <- true // 一个数据通道发送操作
z := <-c  // 一个使用数据通道接收操作
        // 做为源值的变量短声明语句

// 一些表达式的例子：
123
true
B
B + " language"
a - 789
a > 0 // 一个类型不确定布尔值
f     // 一个类型为“func ()”的表达式

// 下面这些即可以被视为简单语句，也可被视为表达式。
f() // 函数调用
<-c // 数据通道接收操作
```

## 基本流程控制语法

Go语言中有三种基本的流程控制代码块：

- if-else条件分支代码块；
- for循环代码块；
- switch-case多条件分支代码块。

Go中另外还有几种和特定种类的类型相关的流程控制代码块：

- 容器类型相关的for-range循环代码块。
- 接口类型相关的type-switch多条件分支代码块。
- 数据通道类型相关的select-case多分支代码块。

和很多其它流行语言一样，Go也支持break、continue和goto等跳转语句。 另外，Go还支持一个特有的fallthrough跳转语句。

除了if-else条件分支代码块，其它五种称为可跳出代码块。 我们可以在一个可跳出代码块中使用break语句以跳出此代码块。

我们可以在for和for-range两种循环代码块中使用continue语句提前结束一个循环步。 除了这两种循环代码块，其它四种代码块称为分支代码块。

### if-else条件分支控制代码块

一个if-else条件分支控制代码块的完整形式如下：

```go
if InitSimpleStatement; Condition {
    // do something
} else {
    // do something
}
```

- InitSimpleStatement部分是可选的，如果它没被省略掉，则它必须为一条简单语句。 如果它被省略掉，它可以被视为一条空语句（简单语句的一种）。 在实际编程中，InitSimpleStatement常常为一条变量短声明语句。
- Condition必须为一个结果为布尔值的表达式（它被称为条件表达式）。 Condition部分可以用一对小括号括起来，但大多数情况下不需要。

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    if h := time.Now().Hour(); h < 12 {
        fmt.Println("现在为上午。")
    } else if h > 19 {
        fmt.Println("现在为晚上。")
    } else {
        fmt.Println("现在为下午。")
        // 左h是一个新声明的变量，右h已经在上面声明了。
        h := h
        // 刚声明的h遮掩了上面声明的h。
        _ = h
    }

    // 上面声明的两个h在此处都不可见。
}
```

### for循环代码块

for循环代码块的完整形式如下：

```go
for InitSimpleStatement; Condition; PostSimpleStatement {
    // do something
}
```

其中for是一个关键字。在一个for循环代码块中，

- InitSimpleStatement（初始化语句）和PostSimpleStatement（步尾语句）两个部分必须均为简单语句，并且PostSimpleStatement不能为一个变量短声明语句。
- Condition必须为一个结果为布尔值的表达式（它被称为条件表达式）。

在一个for循环流程控制中，初始化语句（InitSimpleStatement）将被率先执行，并且只会被执行一次。

```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

在每个循环步的开始，Condition条件表达式将被估值。如果估值结果为false，则循环立即结束；否则循环体（即显式代码块）将被执行。

在每个循环步的结尾，步尾语句（PostSimpleStatement）将被执行。

在一个for循环流程控制中，如果InitSimpleStatement和PostSimpleStatement两部分同时被省略（可将它们视为空语句），则和它们相邻的两个分号也可被省略。 这样的形式被称为只有条件表达式的for循环。只有条件表达式的for循环和很多其它语言中的while循环类似。

```go
for i < 20 {
    fmt.Println(i)
    i++
}
```

在一个for循环流程控制中，如果条件表达式部分被省略，则编译器视其为true。

一条break语句可以用来提前跳出包含此break语句的最内层for循环。

```go
i := 0
for {
    if i >= 10 {
        break
    }
    i++
    fmt.Println(i)
}
```

一条continue语句可以被用来提前结束包含此continue语句的最内层for循环的当前循环步（步尾语句仍将得到执行）。

```go
for i := 0; i < 10; i++ {
    if i % 2 == 0 {
        continue
    }
    fmt.Print(i)
}
```

### switch-case流程控制代码块

一个switch-case流程控制代码块的完整形式为：

```go
switch InitSimpleStatement; CompareOperand0 {
case CompareOperandList1:
    // do something
case CompareOperandList2:
    // do something
...
case CompareOperandListN:
    // do something
default:
    // do something
}
```

- InitSimpleStatement部分必须为一条简单语句，它是可选的。
- CompareOperand0部分必须为一个表达式。 此表达式的估值结果总是被视为一个类型确定值。如果它是一个类型不确定值，则它被视为类型为它的默认类型的类型确定值。 因为这个原因，此表达式不能为类型不确定的nil值。 CompareOperand0常被称为switch表达式。
- 每个CompareOperandListX部分（X表示1到N）必须为一个用（英文）逗号分隔开来的表达式列表。 其中每个表达式都必须能和CompareOperand0表达式进行比较。 每个这样的表达式常被称为case表达式。 如果其中case表达式是一个类型不确定值，则它必须能够自动隐式转化为对应的switch表达式的类型，否则编译将失败。

switch-case代码块属于可跳出流程控制。 break可以使用在一个switch-case流程控制的任何分支代码块之中以提前跳出此switch-case流程控制。

当一个switch-case流程控制被执行到的时候，其中的简单语句InitSimpleStatement将率先被执行。 随后switch表达式CompareOperand0将被估值（仅一次）。上面已经提到，此估值结果一定为一个类型确定值。 然后此结果值将从上到下从左到右和各个CompareOperandListX表达式列表中的各个case表达式逐个依次比较（使用==运算符）。 一旦发现某个表达式和CompareOperand0相等，比较过程停止并且此表达式对应的分支代码块将得到执行。 如果没有任何一个表达式和CompareOperand0相等，则default默认分支将得到执行（如果此分支存在的话）。

**每个分支代码块的结尾不需要一条break语句就可以自动跳出当前的switch-case流程控制**。fallthrough关键字可以从一个case分支代码块的结尾跳入下一个分支代码块。

请注意：

- 一条fallthrough语句必须为一个分支代码块中的最后一条语句。
- 一条fallthrough语句不能出现在一个switch-case流程控制中的最后一个分支代码块中。

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

func main() {
    rand.Seed(time.Now().UnixNano())
    switch n := rand.Intn(100); n%9 {
    case 0:
        fmt.Println(n, "is a multiple of 9.")

        // 和很多其它语言不一样，程序不会自动从一个分支代码块跳到
        // 下一个分支代码块去执行。所以，这里不需要一个break语句。
    case 1, 2, 3:
        fmt.Println(n, "mod 9 is 1, 2 or 3.")
        break // 这里的break语句可有可无的，效果是一样的。
            // 执行不会跳到下一个分支。
    case 4, 5, 6:
        fmt.Println(n, "mod 9 is 4, 5 or 6.")
    // case 6, 7, 8:
        // 上一行行可能编译不过，因为6和上一个case中的6重复了。
        // 是否能编译通过取决于具体编译器实现。
    default:
        fmt.Println(n, "mod 9 is 7 or 8.")
    }
}
```

```go
rand.Seed(time.Now().UnixNano())
switch n := rand.Intn(100) % 5; n {
case 0, 1, 2, 3, 4:
    fmt.Println("n =", n)
    fallthrough // 跳到下个代码块
case 5, 6, 7, 8:
    // 一个新声明的n，它只在当前分支代码快内可见。
    n := 99
    fmt.Println("n =", n) // 99
    fallthrough
default:
    // 下一行中的n和第一个分支中的n是同一个变量。
    // 它们均为switch表达式"n"。
    fmt.Println("n =", n)
}
```

```go
switch n := rand.Intn(100) % 5; n {
case 0, 1, 2, 3, 4:
    fmt.Println("n =", n)
    // 此整个if代码块为当前分支中的最后一条语句
    if true {
        fallthrough // error: 不是当前分支中的最后一条语句
    }
case 5, 6, 7, 8:
    n := 99
    fallthrough // error: 不是当前分支中的最后一条语句
    _ = n
default:
    fmt.Println(n)
    fallthrough // error: 不能出现在最后一个分支中
}
```

一个switch-case流程控制中的InitSimpleStatement语句和CompareOperand0表达式都是可选的。 如果CompareOperand0表达式被省略，则它被认为类型为bool类型的true值。 如果InitSimpleStatement语句被省略，其后的分号也可一并被省略。

### goto跳转语句和跳转标签声明

Go支持goto跳转语句。 在一个goto跳转语句中，goto关键字后必须跟随一个表明跳转到何处的跳转标签。 我们使用LabelName:这样的形式来声明一个名为LabelName的跳转标签，其中LabelName必须为一个标识符。 一个不为空标识符的跳转标签声明后必须被使用至少一次。

一条跳转标签声明之后必须立即跟随一条语句。 如果此声明的跳转标签使用在一条goto语句中，则当此条goto语句被执行的时候，执行将跳转到此跳转标签声明后跟随的语句。

一个跳转标签必须声明在一个函数体内，此跳转标签的使用可以在此跳转标签的声明之后或者之前，但是此跳转标签的使用不能出现在此跳转标签声明所处的最内层代码块之外。

```go
package main

import "fmt"

func main() {
    i := 0

Next: // 跳转标签声明
    fmt.Println(i)
    i++
    if i < 5 {
        goto Next // 跳转
    }
}
```

```go
package main

func main() {
goto Label1 // error
    {
        Label1:
        goto Label2 // error
    }
    {
        Label2:
    }
}
```

如果一个跳转标签声明在某个变量的作用域内，则此跳转标签的使用不能出现在此变量的声明之前。

```go
package main

import "fmt"

func main() {
    i := 0
Next:
    if i >= 5 {
        // error: goto Exit jumps over declaration of k
        goto Exit
    }

    k := i + i
    fmt.Println(k)
    i++
    goto Next
Exit: // 此标签声明在k的作用域内，但它的使用再在k的作用域之外。
}
```

解决方案

```go
func main() func main() {
    i := 0
Next:
    if i >= 5 {
        goto Exit
    }
    // 创建一个显式代码块以缩小k的作用域。
    {
        k := i + i
        fmt.Println(k)
    }
    i++
    goto Next
Exit:
}
```

```go
func main() {
    var k int // 将变量k的声明移到此处。
    i := 0
Next:
    if i >= 5 {
        goto Exit
    }

    k = i + i
    fmt.Println(k)
    i++
    goto Next
Exit:
}
```

### 跟随跳转标签的break和continue跳转语句

一个break或者continue语句也可以包含一个跳转标签名，但此跳转标签名是可选的。 包含跳转标签名的break语句一般用于可跳出外层的嵌套可跳出流程控制代码块。 包含跳转标签名的continue语句一般用于提前结束外层的嵌套循环流程控制代码块。

```go
package main

import "fmt"

func FindSmallestPrimeLargerThan(n int) int {
Outer:
    for n++; ; n++{
        for i := 2; ; i++ {
            switch {
            case i * i > n:
                break Outer
            case n % i == 0:
                continue Outer
            }
        }
    }
    return n
}

func main() {
    for i := 90; i < 100; i++ {
        n := FindSmallestPrimeLargerThan(i)
        fmt.Print("最小的比", i, "大的素数为", n)
        fmt.Println()
    }
}
```

## 协程、延迟函数调用、以及恐慌和恢复

### 协程

协程有时也被称为绿色线程。绿色线程是由程序的运行时（runtime）维护的线程。一个绿色线程的开销（比如内存消耗和情景转换）比一个系统线程常常小得多。 只要内存充足，一个程序可以轻松支持上万个并发（concurrent）协程。

Go不支持创建系统线程，所以协程是一个Go程序内部唯一的并发实现方式。

每个Go程序启动的时候只有一个对用户可见的协程，我们称之为主协程。 一个协程可以开启更多其它新的协程。在Go中，开启一个新的协程是非常简单的。 我们只需在一个函数调用之前使用一个go关键字，即可让此函数调用运行在一个新的协程之中。当此函数调用退出后，这个新的协程也随之结束了。我们可以称此函数调用为一个协程调用（或者为此协程的启动调用）。 一个协程调用的所有返回值（如果存在的话）必须被全被舍弃。

```go
package main

import (
    "log"
    "math/rand"
    "time"
)

func SayGreetings(greeting string, times int) {
    for i := 0; i < times; i++ {
        log.Println(greeting)
        d := time.Second * time.Duration(rand.Intn(5)) / 2
        time.Sleep(d) // 睡眠片刻（随机0到2.5秒）
    }
}

func main() {
    rand.Seed(time.Now().UnixNano())
    log.SetFlags(0)
    go SayGreetings("hi!", 10)
    go SayGreetings("hello!", 10)
    time.Sleep(2 * time.Second)
}
```

### 并发同步（concurrency synchronization）

上面这个并发程序是有缺陷的。我们本期望每个新创建的协程打印出10条问候语，但是主协程（和程序）在这20条问候语还未都打印出来的时候就退出了。 如何确保主协程在这20条问候语都打印完毕之后才退出呢？我们必须使用某种并发同步技术来达成这一目标。

sync标准库包中的WaitGroup来同步程序中的主协程和协程。

WaitGroup类型有三个方法：Add、Done和Wait。

- Add方法用来注册新的需要完成的任务数。
- Done方法用来通知某个任务已经完成了。
- 一个Wait方法调用将阻塞（等待）到所有任务都已经完成之后才继续执行其后的语句。

```go
package main

import (
    "log"
    "math/rand"
    "time"
    "sync"
)

var wg sync.WaitGroup

func SayGreetings(greeting string, times int) {
    for i := 0; i < times; i++ {
        log.Println(greeting)
        d := time.Second * time.Duration(rand.Intn(5)) / 2
        time.Sleep(d)
    }
    wg.Done() // 通知当前任务已经完成。
}

func main() {
    rand.Seed(time.Now().UnixNano())
    log.SetFlags(0)
    wg.Add(2) // 注册两个新任务。
    go SayGreetings("hi!", 10)
    go SayGreetings("hello!", 10)
    wg.Wait() // 阻塞在这里，直到所有任务都已完成。
}
```

### 协程的状态

一个活动中的协程可以处于两个状态：**运行状态**和**阻塞状态**。一个协程可以在这两个状态之间切换。

![goroutine-states](https://i.imgur.com/0oDkEJ3.png)

一个处于睡眠中的（通过调用time.Sleep）或者在等待系统调用返回的协程被认为是处于运行状态，而不是阻塞状态。

协程创建时自动进入运行状态，一个协程只能从运行状态退出。

### 协程的调度

并非所有处于运行状态的协程都在执行。在任一时刻，只能最多有和逻辑CPU数目一样多的协程在同时执行。 我们可以调用runtime.NumCPU函数来查询当前程序可利用的逻辑CPU数目。 每个逻辑CPU在同一时刻只能最多执行一个协程。Go运行时（runtime）必须让逻辑CPU频繁地在不同的处于运行状态的协程之间切换，从而每个处于运行状态的协程都有机会得到执行。 这和操作系统执行系统线程的原理是一样的。

![goroutine-schedule](https://i.imgur.com/VcOhOH8.png)

标准编译器采纳了一种被称为M-P-G模型的算法来实现协程调度。 其中，M表示系统线程，P表示逻辑处理器（并非上述的逻辑CPU），G表示协程。 大多数的调度工作是通过逻辑处理器（P）来完成的。 逻辑处理器像一个监工一样通过将不同的处于运行状态协程（G）交给不同的系统线程（M）来执行。 一个协程在同一时刻只能在一个系统线程中执行。一个执行中的协程运行片刻后将自发地脱离让出一个系统线程，从而使得其它处于等待子状态的协程得到执行机会。

### 延迟函数调用（deferred function call）

在Go中，一个函数调用可以跟在一个defer关键字后面，形成一个延迟函数调用。 和协程调用类似，被延迟的函数调用的所有返回值必须全部被舍弃。

当一个函数调用被延迟后，它不会立即被执行。它将被推入由当前协程维护的一个延迟调用堆栈。 当一个函数调用（可能是也可能不是一个延迟调用）返回并进入它的退出阶段后，所有在此函数调用中已经被推入的延迟调用将被按照它们被推入堆栈的顺序逆序执行。 当所有这些延迟调用执行完毕后，此函数调用也就真正退出了。

```go
package main

import "fmt"

func main() {
    defer fmt.Println("The third line.")
    defer fmt.Println("The second line.")
    fmt.Println("The first line.")
}
```

- 一个是正常的函数调用堆栈。在此堆栈中，相邻的的两个调用存在着调用关系。晚进入堆栈的调用被早进入堆栈的调用所调用。 此堆栈的中最早被推入的调用是对应协程的启动调用。
- 另一个堆栈是上面提到的延迟调用堆栈。处于延迟调用堆栈中的任意两个调用之间不存在调用关系。

一个延迟调用可以修改包含此延迟调用的最内层函数的返回值

```go
package main

import "fmt"

func Triple(n int) (r int) {
    defer func() {
        r += n // 修改返回值
    }()

    return n + n // <=> r = n + n; return
}

func main() {
    fmt.Println(Triple(5)) // 15
}
```

### 协程和延迟调用的实参的估值时刻

一个协程调用或者延迟调用的实参是在此调用发生时被估值的。更具体地说，

- 对于一个延迟函数调用，它的实参是在*此调用被推入延迟调用堆栈的时候被估值*的。
- 对于一个协程调用，它的实参是在此协程被创建的时候估值的。
- 一个匿名函数体内的表达式是在此函数被执行的时候才会被逐个估值的，不管此函数是被普通调用还是延迟/协程调用。

```go
package main

import "fmt"

func main() {
    func() {
        for i := 0; i < 3; i++ {
            defer fmt.Println("a:", i)
        }
    }()
    fmt.Println()
    func() {
        for i := 0; i < 3; i++ {
            defer func() {
                fmt.Println("b:", i)
            }()
        }
    }()
}
```

```go
package main

import "fmt"
import "time"

func main() {
    var a = 123
    go func(x int) {
        time.Sleep(time.Second)
        fmt.Println(x, a)
    }(a)

    a = 789

    time.Sleep(2 * time.Second)
}
```

### 恐慌（panic）和恢复（recover）

Go不支持异常抛出和捕获，而是推荐使用返回值显式返回错误。 不过，Go支持一套和异常抛出/捕获类似的机制。此机制称为恐慌/恢复（panic/recover）机制。

我们可以调用内置函数panic来产生一个恐慌以使当前协程进入恐慌状况。一个恐慌不会蔓延到其它协程。

进入恐慌状况是另一种使当前函数调用开始返回的途径。 一旦一个函数调用产生一个恐慌，此函数调用将立即进入返回阶段，在此函数调用中被推入堆栈的延迟调用将按照它们被推入的顺序逆序执行。

通过在一个延迟函数调用之中调用内置函数recover，当前协程中的一个恐慌可以被消除，从而使得当前协程重新进入正常状况。

在一个panic函数调用中，我们可以传任何实参值。

一个recover函数的返回值为其所恢复的恐慌在产生时被一个panic函数调用所消费的参数。

```go
package main

import "fmt"

func main() {
    defer func() {
        fmt.Println("正常退出")
    }()
    fmt.Println("嗨！")
    defer func() {
        v := recover()
        fmt.Println("恐慌被恢复了：", v)
    }()
    panic("拜拜！") // 产生一个恐慌
    fmt.Println("执行不到这里")
}
```

## Go类型系统概述

### 基本类型

### 组合类型

- 指针类型 - 类C指针
- 结构体类型 - 类C结构体
- 函数类型 - 函数类型在Go中是一种一等公民类别
- 容器类型，包括:
  - 数组类型 - 定长容器类型
  - 切片类型 - 动态长度和容量容器类型
  - 映射类型（map）- 也常称为字典类型。在标准编译器中映射是使用哈希表实现的。
- 数据通道类型 - 数据通道用来同步并发的协程
- 接口类型 - 接口在反射和多态中发挥着重要角色

```go
// 假设T为任意一个类型，Tkey为一个支持比较的类型。

*T         // 一个指针类型
[5]T       // 一个元素类型为T、元素个数为5的数组类型
[]T        // 一个元素类型为T的切片类型
map[Tkey]T // 一个键值类型为Tkey、元素类型为T的映射类型

// 一个结构体类型
struct {
    name string
    age  int
}

// 一个函数类型
func(int) (bool, string)

// 一个接口类型
interface {
    Method0(string) int
    Method1() (int, bool)
}

// 几个数据通道类型
chan T
chan<- T
<-chan T
```

### 类型定义

在Go中，我们可以用如下形式来定义新的类型。在此语法中，type为一个关键字。

```go
// 定义单个类型。
type NewTypeName SourceType

// 定义多个类型。
type (
    NewTypeName1 SourceType1
    NewTypeName2 SourceType2
)
```

- 一个新定义的类型和它的源类型为两个不同的类型。
- 在两个不同的类型定义中的定义的两个类型肯定为两个不同的类型。
- 一个新定义的类型和它的源类型的底层类型一致并且它们的值可以相互显式转换。
- 类型定义可以出现在函数体内。

```go
// 下面这些新定义的类型和它们的源类型都是基本类型。
type (
    MyInt int
    Age   int
    Text  string
)

// 下面这些新定义的类型和它们的源类型都是组合类型。
type IntPtr *int
type Book struct{author, title string; pages int}
type Convert func(in0 int, in1 bool)(out0 int, out1 string)
type StringArray [5]string
type StringSlice []string

func f() {
    // 这三个新定义的类型名称只能在此函数内使用。
    type PersonAge map[string]int
    type MessageQueue chan string
    type Reader interface{Read([]byte) int}
}
```

### 类型别名声明（type alias declaration）

从Go 1.9开始，我们可以使用下面的语法来声明自定义类型别名。此语法和类型定义类似，但是请注意其中多了一个等号=。

```go
type (
    Name = string
    Age  = int
)

type table = map[string]int
type Table = map[Name]Age
```

类型定义是完全定义了一种新的类型，而类型别名只是给现有的类型取了一个别名alias，类似与C语言的typedef和#define

### 定义类型和非定义类型

一个定义类型是一个在某个类型定义声明中定义的类型。

所有的基本类型都是定义类型。一个非定义类型一定是一个组合类型。

在下面的例子中，别名C和类型字面表示[]string都表示同一个非定义类型。 类型A和别名B均表示同一个定义类型。

```go
type A []string
type B = A
type C = []string
```

### 底层类型

- 一个内置类型的底层类型为它自己。
- 所有非类型安全类型的底层类型均为unsafe标准库包中定义的Pointer类型。
- 一个非定义类型（必为一个组合类型）的底层类型为它自己。
- 在一个类型声明中，新声明的类型和源类型共享底层类型。

```go
// 这四个类型的底层类型均为内置类型int。
type (
    MyInt int
    Age   MyInt
)

// 下面这三个新声明的类型的底层类型各不相同。
type (
    IntSlice   []int   // 底层类型为[]int
    MyIntSlice []MyInt // 底层类型为[]MyInt
    AgeSlice   []Age   // 底层类型为[]Age
)

// 类型[]Age、Ages和AgeSlice的底层类型均为[]Age。
type Ages AgeSlice
```

- 底层类型为内置类型bool的类型称为布尔类型；
- 底层类型为任一内置整数类型的类型称为整数类型；
- 底层类型为内置类型float32或者float64的类型称为浮点数类型；
- 底层类型为内置类型complex64或complex128的类型称为复数类型；
- 整数类型、浮点数类型和复数类型统称为数字值类型；
- 底层类型为内置类型string的类型称为字符串类型。

### 值

一个类型的一个实例称为此类型的一个值。一个类型可以有很多不同的值，其中一个为它的零值。 同一类型的不同值共享很多相同的属性。

组合字面表示形式（composite literal）和函数字面表示形式。

函数字面表示形式用来表示函数值。事实上，一个函数声明是由一个标识符（函数名）和一个函数字面表示形式组成。

组合字面表示形式用来表示结构体类型值和容器类型（数组、切片和映射）值。

指针类型、数据通道类型和接口类型的值没有字面表示形式。

### 值部简介

在运行时刻，很多值是存储在内存的。每个这样的值都有一个直接部分，但是有一些值还可能有一个或多个间接部分。 每个值部分在内存中都占据一段连续空间。通过指针，一个值的间接部分被此值的直接部分所引用。

### 值尺寸

一个值存储在在内存中是要占据一定的空间的。此空间的大小称为此值的尺寸。值尺寸是用字节数来衡量的。

我们可以用unsafe标准库包中的Sizeof函数来取得任何一个值的尺寸。

### 可比较类型和不可比较类型

下面这些类型的值不支持（使用==和!=运算标识符）比较。这些类型称为不可比较类型。

- 切片类型
- 映射类型
- 函数类型
- 任何包含有不可比较类型的字段的结构体类型和任何元素类型为不可比较类型的数组类型。

## 指针

### 内存地址

一个内存地址表示操作系统管理的整个内存的中一个偏移量。

一个内存地址用一个操作系统原生字（native word）来存储。 一个原生字在32位操作系统上占4个字节，在64位操作系统上占8个字节。 所以，32位操作系统上的理论最大支持内存容量为4GB，64位操作系统上的理论最大支持内存容量为2<sup>34</sup>GB。

内存地址的字面形式常用整数的十六进制字面值来表示，比如0x1234CDEF。

### 值的地址

一个值的地址是指此值的直接部分占据的内存的起始地址。在Go中，每个值都包含一个直接部分，但有些值可能还包含一个或多个间接部分。

### 什么是指针

一个指针是某个指针类型的一个值。一个指针可以存储一个内存地址。

### 指针类型和值

一个非定义指针类型的字面形式为`*T`，其中T为一个任意类型。类型T称为指针类型`*T`的基类型（base type）。 如果一个指针类型的基类型为T，则我们可以称此指针类型为一个T指针类型。

指针类型的零值的字面形式使用预声明的nil来表示。

如果一个指针类型的基类型为T，则此指针类型的值只能存储类型为T的值的地址。

术语“引用”暗示着一个关系。比如，如果一个指针中存储着另外一个值的地址，则我们可以说此指针值引用着另外一个值；同时另外一个值当前至少有一个引用。

### 如何获取一个指针值？

有两种方式来得到一个指针值：

1. 我们可以用内置函数new来为任何类型的值开辟一块内存并将此内存块的起始地址做为此值的地址返回。 假设T是任一类型，则函数调用new(T)返回一个类型为*T的指针值。 存储在返回指针值所表示的地址处的值（可被看作是一个匿名变量）为T的零值。
2. 我们也可以使用前置取地址操作符&来获取一个可寻址的值的地址。 对于一个类型为T的可寻址的值t，我们可以用&t来取得它的地址。&t的类型为*T。

### 指针（地址）解引用

我们可以使用前置解引用操作符`*`来访问存储在一个指针所表示的地址处的值（即此指针所引用着的值）。 比如，对于基类型为T的指针类型的一个指针值p，我们可以用`*p`来表示地址p处的值。 此值的类型为T。`*p`称为指针p的解引用。解引用是取地址的逆过程。

```go
package main

import "fmt"

func main() {
    p0 := new(int)   // p0指向一个int类型的零值
    fmt.Println(p0)  // （将打印出一个十六进制字符串形式的地址）
    fmt.Println(*p0) // 0

    x := *p0              // x是p0所引用的值的一个复制。
    p1, p2 := &x, &x      // p1和p2中都存储着x的地址。
                        // x、*p1和*p2表示着同一个int值。
    fmt.Println(p1 == p2) // true
    fmt.Println(p0 == p1) // false
    p3 := &*p0            // <=> p3 := &(*p0)
                        // <=> p3 := p0
                        // p3和p0中存储的地址是一样的。
    fmt.Println(p0 == p3) // true
    *p0, *p1 = 123, 789
    fmt.Println(*p2, x, *p3) // 789 789 123

    fmt.Printf("%T, %T \n", *p0, x) // int, int
    fmt.Printf("%T, %T \n", p0, p1) // *int, *int
}
```

```go
package main

import "fmt"

func double(x *int) {
    *x += *x
    x = nil // 此行仅为讲解目的
}

func main() {
    var a = 3
    double(&a)
    fmt.Println(a) // 6
    p := &a
    double(p)
    fmt.Println(a, p == nil) // 12 false
}
```

和C不一样，Go是支持**垃圾回收**的，所以一个函数**返回其内声明的局部变量的地址是绝对安全的**。

```go
func newInt() *int {
    a := 3
    return &a
}
```

### Go指针的一些限制

为了安全起见，Go指针在使用上相对于C指针有很多限制。 通过施加这些限制，Go指针保留了C指针的好处，同时也避免了C指针的危险性。

#### Go指针不支持算术运算

在Go中，指针是不能参与算术运算的。比如，对于一个指针p， 运算p++和p-2都是非法的。

如果p为一个指向一个数值类型值的指针，`*p++`将被编译器认为是合法的并且等价于`(*p)++`。 换句话说，取地址操作符&和解引用操作符*的优先级都高于自增++和自减--操作符。

```go
package main

import "fmt"

func main() {
    a := int64(5)
    p := &a

    // 下面这两行编译不通过。
    /*
    p++
    p = (&a) + 8
    */

    *p++
    fmt.Println(*p, a)   // 6 6
    fmt.Println(p == &a) // true

    *&a++
    *&*&a++
    **&p++
    *&*p++
    fmt.Println(*p, a) // 10 10
}
```

#### 一个指针类型的值不能被随意转换为另一个指针类型

在Go中，只有如下某个条件被满足的情况下，一个类型为T1的指针值才能被显式转换为另一个指针类型T2：

1. 类型T1和T2的底层类型必须一致（忽略结构体字段的标签）。 特别地，如果类型T1和T2中只要有一个是非定义类型并且它们的底层类型一致（考虑结构体字段的标签），则此转换可以是隐式的。
2. 类型T1和T2都为非定义类型并且它们的底层类型的基类型一致（忽略结构体字段的标签）。

#### 一个指针值不能和其它任一指针类型的值进行比较

Go指针值是支持（使用比较运算符==和!=）比较的。 但是，两个指针只有在下列任一条件被满足的时候才可以比较：

1. 这两个指针的类型相同。
2. 其中一个指针可以被隐式转换为另一个指针的类型。换句话说，这两个指针的类型的底层类型必须一致并且其中一个指针类型为非定义的（考虑结构体字段的标签）。
3. 其中一个并且只有一个指针用类型不确定的nil标识符表示。

```go
package main

func main() {
    type MyInt int64
    type Ta    *int64
    type Tb    *MyInt

    // 4个不同类型的指针：
    var pa0 Ta
    var pa1 *int64
    var pb0 Tb
    var pb1 *MyInt

    // 下面这6行编译没问题。它们的比较结果都为true。
    _ = pa0 == pa1
    _ = pb0 == pb1
    _ = pa0 == nil
    _ = pa1 == nil
    _ = pb0 == nil
    _ = pb1 == nil

    // 下面这三行编译不通过。
    /*
    _ = pa0 == pb0
    _ = pa1 == pb1
    _ = pa0 == Tb(nil)
    */
}
```

#### 一个指针值不能被赋值给其它任意类型的指针值

一个指针值可以被赋值给另一个指针值的条件和这两个指针值可以比较的条件是一致的。

## 结构体

### 结构体类型和结构体类型的字面表示形式

每个非定义结构体类型的字面形式均由struct关键字开头，后面跟着用一对大括号{}，其中包裹着的一系列字段（field）声明。 一般来说，每个字段声明由一个字段名和字段类型组成。一个结构体类型的字段数目可以为0。相邻的同类型字段可以声明在一起。

```go
struct {
    title, author string
    pages         int
}
```

一个结构体类型的尺寸为它的所有字段的（类型）尺寸之和加上一些填充字节的数目。一个零字段结构体的尺寸为零。

每个结构体字段在它的声明中可以被指定一个标签（tag）。字段标签可以是任意字符串，它们是可选的，默认为空字符串。每个字段标签的目的取决于具体应用。它是一个附属于字段的字符串，可以是文档或其他的重要标记。标签的内容不可以在一般的编程中使用，只有包 reflect 能获取它。

```go
struct {
    Title  string `json:"title"`
    Author string `json:"author,omitempty"`
    Pages  int    `json:"pages,omitempty"`
}
```

两个声明在不同的代码包中的非导出字段将总被认为是不同的字段。

### 结构体值的字面表示形式和结构体值的使用

在Go中，语法形式`T{...}`称为一个组合字面形式（composite literal），其中T必须为一个类型名或者类型字面形式。 组合字面形式可以用来表示结构体类型和内置容器类型的值。

假设S是一个结构体类型并且它的底层类型为struct{ x int; y bool}，S的零值可以表示成下面所示的组合字面形式两种变种形式：

1. `S{0, false}`。在此变种形式中，所有的字段名称均不出现，但每个字段的值必须指定，并且每个字段的出现顺序和它们的声明顺序必须一致。
2. `S{x: 0, y: false}`、`S{y: false, x: 0}`、`S{x: 0}`、`S{y: false}`和`S{}`。 在此变种形式中，字段的名称和值必须成对出现，但是每个字段都不是必须出现的，并且字段的出现顺序并不重要。 没有出现的字段的值被编译器认为是它们各自类型的零值。`S{}`是最常用的类型S的零值的表示形式。

对于类型S的一个值v，我们可以用v.x和v.y来表示它的字段。 v.x这种形式称为一个选择器（selector）。 选择器中的句点.为属性选择操作符。

```go
package main

import (
    "fmt"
)

type Book struct {
    title, author string
    pages         int
}

func main() {
    book := Book{"Go语言101", "老貘", 256}
    fmt.Println(book) // {Go语言101 老貘 256}

    // 使用带字段名的组合字面形式来表示结构体值。
    book = Book{author: "老貘", pages: 256, title: "Go语言101"}
    // title和author字段的值都为空字符串""，pages字段的值为0。
    book = Book{}
    // title字段空字符串""，pages字段为0。
    book = Book{author: "老貘"}

    // 使用选择器来访问和修改字段值。
    var book2 Book // <=> book2 := Book{}
    book2.author = "Tapir"
    book2.pages = 300
    fmt.Println(book.pages) // 300
}
```

如果一个组合字面形式中最后一项和结尾的}处于同一行，则此项后的逗号,是可选的；否则此逗号不可省略。

```go
var _ = Book {
    author: "老貘",
    pages: 256,
    title: "Go语言101", // 这里行尾的逗号不可省略
}

// 下行}前的逗号可以省略。
var _ = Book{author: "老貘", pages: 256, title: "Go语言101",}
```

### 关于结构体值的赋值

当一个（源）结构体值被赋值给另外一个（目标）结构体值时，其效果和逐个将源结构体值的各个字段赋值给目标结构体值的各个对应字段的效果是一样的。

```go
func f() {
    book1 := Book{pages: 300}
    book2 := Book{"Go语言101", "老貘", 256}

    book2 = book1
    // 上面这行和下面这三行是等价的。
    book2.title = book1.title
    book2.author = book1.author
    book2.pages = book1.pages
}
```

两个结构体值只有在它们的类型的底层类型一样（要考虑字段标签）并且其中至少有一个结构体值的类型为非定义类型时才可以互相赋值。？？

### 结构体字段的可寻址性

如果一个结构体值是可寻址的，则它的字段也是可寻址的；反之，一个不可寻址的结构的字段也是不可寻址的。 不可寻址的字段的值是不可更改的。所有的组合字面值都是不可寻址的。

```go
package main

import "fmt"

func main() {
    type Book struct {
        Pages int
    }
    var book = Book{} // 变量值book是可寻址的
    p := &book.Pages
    *p = 123
    fmt.Println(book) // {123}

    // 下面这两行编译不通过，因为Book{}.Pages是不可寻址的。
    /*
    Book{}.Pages = 123
    p = &Book{}.Pages // <=> p = &(Book{}.Pages)
    */
}
```

### 组合字面值不可寻址但可被取地址

虽然所有的组合字面值都是不可寻址的，但是它们都可被取地址，虽然所有的组合字面值都是不可寻址的，但是它们都可被取地址。

```go
func main() {
    type Book struct {
        Pages int
    }
    // Book{100}是不可寻址的，但是它可以被取地址。
    p := &Book{100} // <=> tmp := Book{100}; p := &tmp
    p.Pages = 200
}
```

### 选择器中结构体值的指针可以当作结构值来使用

和C语言不同，Go中没有->操作符用来通过一个结构体值的指针来访为此结构体值的字段。 在Go中，->操作符也是用句点.来表示的。

```go
func main() {
    type Book struct {
        pages int
    }
    book1 := &Book{100} // book1是一个指针
    book2 := new(Book)  // book2是另外一个指针
    // 像使用结构值一样来使用结构体值的指针。
    book2.pages = book1.pages
}
```

### 关于结构体值的比较

大多数的结构体类型都是可比较类型，除了少数含有不可比较字段的结构体类型。

和结构体值的赋值规则类似，如果两个结构体值的类型均为可比较类型，则它们仅在它们的类型的底层类型一样（要考虑字段标签）并且其中至少有一个结构体值的类型为非定义类型时才可以互相比较。

如果两个结构体值可以相互比较，则它们的比较结果等同于逐个比较它们的相应字段。 两个结构体值只有在它们的相应字段都相等的情况下才相等。

### 关于结构体值的类型转换

两个类型分别为S1和S2的结构体值只有在S1和S2的底层类型相同（忽略掉字段标签）的情况下才能相互转换为对方的类型。 特别地，如果S1和S2的底层类型相同（要考虑字段标签）并且只要它们其中有一个为非定义类型，则此转换可以是隐式的。

### 匿名结构体类型可以使用在结构体字段声明中

匿名结构体类型允许出现在结构体字段声明中。匿名结构体类型也允许出现在组合字面形式中。

```go
var aBook = struct {
    author struct { // 此字段的类型为一个匿名结构体类型
        firstName, lastName string
        gender              bool
    }
    title string
    pages int
}{
    author: struct {
        firstName, lastName string
        gender              bool
    }{
        firstName: "Mark",
        lastName: "Twain",
    }, // 此组合字面形式中的类型为一个匿名结构体类型
    title: "The Million Pound Note",
    pages: 96,
}
```

## 值部

### Go类型分为两个类别

第一个类别中的类型种类包括：布尔类型、各种数值类型、结构体类型、指针类型、数组类型和非类型安全指针类型。此类别类型的值与C语言中值类似，在内存中只含有一个透明的直接部分。

第二个类别中的值在内存中可以包含若干间接部分，并且它们的直接部分是不透明的。包括：

- 切片类型
- 映射类型
- 数据通道类型
- 函数类型
- 接口类型
- 字符串类型

### Go中的两种指针类型

除了一般用到的指针，Go还支持另一种称为非类型安全的指针类型。 非类型安全的指针类型提供在unsafe标准库包中。 非类型安全指针类型通常使用unsafe.Pointer来表示。 unsafe.Pointer类似于C语言中的void*。 底层类型为unsafe.Pointer类型都是非类型安全指针类型。

我们将一个含有（直接或者间接）指针字段的结构体类型称为一个**指针包裹类型**，将一个含有（直接或者间接）指针的类型称为**指针持有者类型**。

### 第二类类型内部实现结构

#### 映射、数据通道和函数类型的内部定义

```go
// 映射类型
type _map *hashtableImpl // 目前，官方标准编译器是使用
                        // 哈希表来实现映射的。

// 数据通道类型
type _channel *channelImpl

// 函数类型
type _function *functionImpl
```

#### 切片类型的内部定义

```go
type _slice struct {
    elements unsafe.Pointer // 引用着底层的元素
    len      int            // 当前的元素个数
    cap      int            // 切片的容量
}
```

#### 字符串类型内部结构

```go
type _string struct {
    elements *byte // 引用着底层的byte元素
    len      int   // 字符串的长度
}
```

#### 接口类型的内部定义

空接口内部结构

```go
type _interface struct {
    dynamicType  *_type         // 引用着接口值的动态类型
    dynamicValue unsafe.Pointer // 引用着接口值的动态值
}
```

接口类型也可以看作是一个指针包裹类型。一个接口类型含有两个指针字段。 每个非零接口值的（两个）间接部分分别存储着此接口值的动态类型和动态值。 这两个间接部分被此接口值的直接字段dynamicType和dynamicValue所引用。

非空接口类型的内部定义

```go
type _interface struct {
    dynamicTypeInfo *struct {
        dynamicType *_type       // 引用着接口值的动态类型
        methods     []*_function // 引用着动态类型的对应方法列表
    }
    dynamicValue unsafe.Pointer // 引用着动态值
}
```

一个非空接口类型的值的dynamicTypeInfo字段的methods字段引用着一个方法列表。 此列表中的每一项为此接口值的动态类型上定义的一个方法，此方法对应着此接口类型所指定的一个的同原型的方法。

### 在赋值中，底层间接值部将不会被复制

每个赋值操作（包括函数调用传参等）都是一个值的浅复制过程（假设源值和目标值的类型相同）。 换句话说，在一个赋值操作中，只有源值的直接部分被复制给了目标值。 如果源值含有间接部分，则在此赋值操作完成之后，目标值和源值的直接部分将引用着相同的间接部分。 换句话说，两个值将共享底层的间接值部，如下图所示：

![value-parts-copy](https://i.imgur.com/YQp4K08.png)

在Go中，所有的函数调用的参数都是通过值复制的方式来传递的。

## 数组、切片和映射

### 容器类型和容器值概述

每个容器（值）用来表示和存储一个元素（element）序列或集合。一个容器中的所有元素的类型是相同的。此相同的类型称为此容器的类型的元素类型（或简称此容器的元素类型）。

存储在一个容器中的每个元素值都关联着着一个键值（key）。每个元素可以通过它的键值而被访问到。 一个映射类型的键值类型必须为一个可比较类型。 数组和切片类型的键值类型均为内置类型int。

一个切片或者映射值是由一个直接部分和一个可能的被此直接部分引用着的间接部分组成。

一个数组或者切片的所有元素紧挨着存放在一块连续的内存中。一个数组中的所有元素均存放在此数组值的直接部分，一个切片中的所元素均存放在此切片值的间接部分。

可以通过一个元素的键值来访问此元素。 对于这三种容器，元素访问的时间复杂度均为O(1)。 但是一般来说，映射元素访问消耗的时长要数倍于数组和切片元素访问消耗的时长。 但是映射相对于数组和切片有两个优点：

- 映射的键值类型可以是任何可比较类型。
- 相对于使用含有大量稀疏索引的数组和切片，使用映射可以节省大量的内存。

### 非定义容器类型的字面表示形式

非定义容器类型的字面表示形式如下：

- 数组类型：`[N]T`
- 切片类型：`[]T`
- 映射类型：`map[K]T`

其中，

- T可为任意类型。它表示一个容器类型的元素类型。某个特定容器类型的值中只能存储此容器类型的元素类型的值。
- N必须为一个非负整数常量。它指定了一个数组类型的长度，或者说它指定了此数组类型的任何一个值中存储了多少个元素。 一个数组类型的长度是此数组类型的一部分。比如`[5]int`和`[8]int`是两个不同的类型。
- K必须为一个可比较类型。它指定了一个映射类型的键值类型。

```go
const Size = 32

type Person struct {
    name string
    age  int
}

// 数组类型
[5]string
[Size]int
[16][]byte  // 此数组类型的元素类型为一个切片类型：[]byte
[100]Person // 此数组类型的元素类型为一个结构体类型：Person

// 切片类型
[]bool
[]int64
[]map[int]bool // 此切片类型的元素类型为一个映射类型：map[int]bool
[]*int         // 此切片类型的元素类型为一个指针类型：*int

// 映射类型
map[string]int
map[int]bool
map[int16][6]string     // 此映射类型的元素类型为一个数组类型：[6]string
map[bool][]string       // 此映射类型的元素类型为一个切片类型：[]string
map[struct{x int}]*int8 // 此映射类型的元素类型为一个指针类型：*int8，
                        // 它的键值类型为一个结构体类型。
```

所有切片类型的尺寸都是一致的，所有映射类型的尺寸也都是一致的。 一个数组类型的尺寸等于它的元素类型的尺寸和它的长度的乘积。长度为零的数组的尺寸为零；元素类型尺寸为零的任意长度的数组类型的尺寸也为零。

### 容器类型值的字面表示形式

容器值的文字表示也可以用组合字面形式（composite literal）来表示。 比如对于一个容器类型T，它的值可以用形式T{...}来表示（除了切片和映射的零值外）。

映射值的组合字面形式中大括号中的每一项称为一个键值对（key-value pair），或者称为一个条目（entry）。

`...`表示让编译器推断出相应数组值的类型的长度。

```go
// 一个含有4个布尔元素的数组值。
[4]bool{false, true, true, false}

// 一个含有三个字符串值的切片值。
[]string{"break", "continue", "fallthrough"}

// 一个映射值。
map[string]int{"C": 1972, "Python": 1991, "Go": 2009}

// 下面这些切片的字面表示形式都是等价的。
[]string{"break", "continue", "fallthrough"}
[]string{0: "break", 1: "continue", 2: "fallthrough"}
[]string{2: "fallthrough", 1: "continue", 0: "break"}
[]string{2: "fallthrough", 0: "break", "continue"}

// 下面这些数组的字面表示形式都是等价的。
[4]bool{false, true, true, false}
[4]bool{0: false, 1: true, 2: true, 3: false}
[4]bool{1: true, true}
[4]bool{2: true, 1: true}
[...]bool{false, true, true, false}
[...]bool{3: false, 1: true, true}

```

- 如果一个索引下标出现，它的类型不必是数组和切片类型的键值类型int，但它必须是一个可以表示为int值的非负常量； 如果它是一个类型确定值，则它的类型必须为一个基本整数类型。
- 在一个数组和切片组合字面形式中，如果一个元素的索引下标缺失，则编译器认为它的索引*下标为出现在它之前的元素的索引下标加一*。
- 如果出现的第一个元素的索引下标缺失，则它的索引下标被认为是0。

映射组合字面形式中元素对应的键值不可缺失，并且它们可以为非常量。

```go
var a uint = 1
var _ = map[uint]int {a : 123} // 没问题
var _ = []int{a: 100}          // error: 下标必须为常量
var _ = [5]int{a: 100}         // error: 下标必须为常量
```

### 容器类型零值的字面表示形式

和结构体类似，一个数组类型A的零值可以表示为`A{}`。 比如，数组类型`[100]int`的零值可以表示为`[100]int{}`。 一个数组零值中的所有元素均为对应数组元素类型的零值。

和指针一样，所有切片和映射类型的零值均用预声明的标识符nil来表示。

在运行时刻，即使一个数组变量在声明的时候未指定初始值，它的元素所占的内存空间也已经被开辟出来。 但是一个nil切片或者映射值的元素的内存空间尚未被开辟出来。

### 容器字面值是不可寻址的但可以被取地址

```go
package main

import "fmt"

func main() {
    pm := &map[string]int{"C": 1972, "Go": 2009}
    ps := &[]string{"break", "continue"}
    pa := &[...]bool{false, true, true, false}
    fmt.Printf("%T\n", pm) // *map[string]int
    fmt.Printf("%T\n", ps) // *[]string
    fmt.Printf("%T\n", pa) // *[4]bool
}
```

### 内嵌组合字面形式可以被简化

在某些情形下，内嵌在其它组合字面值中的组合字面形式可以简化为{...}（即类型部分被省略掉了）。 内嵌组合字面值前的取地址操作符&有时也可以被省略。

```go
// heads为一个切片值。它的类型的元素类型为*[4]byte。
// 此元素类型为一个基类型为[4]byte的指针类型。
// 此指针基类型为一个元素类型为byte的数组类型。
var heads = []*[4]byte{
    &[4]byte{'P', 'N', 'G', ' '},
    &[4]byte{'G', 'I', 'F', ' '},
    &[4]byte{'J', 'P', 'E', 'G'},
}
```

可以被简化为

```go
var heads = []*[4]byte{
    {'P', 'N', 'G', ' '},
    {'G', 'I', 'F', ' '},
    {'J', 'P', 'E', 'G'},
}
```

下面这个数组组合字面值

```go
type language struct {
    name string
    year int
}

var _ = [...]language{
    language{"C", 1972},
    language{"Python", 1991},
    language{"Go", 2009},
}
```

可以被简化为

```go
var _ = [...]language{
    {"C", 1972},
    {"Python", 1991},
    {"Go", 2009},
}
```

下面这个映射组合字面值

```go
type LangCategory struct {
    dynamic bool
    strong  bool
}

// 此映射值的类型的键值类型为一个结构体类型，
// 元素类型为另一个映射类型：map[string]int。
var _ = map[LangCategory]map[string]int{
    LangCategory{true, true}: map[string]int{
        "Python": 1991,
        "Erlang": 1986,
    },
    LangCategory{true, false}: map[string]int{
        "JavaScript": 1995,
    },
    LangCategory{false, true}: map[string]int{
        "Go":   2009,
        "Rust": 2010,
    },
    LangCategory{false, false}: map[string]int{
        "C": 1972,
    },
}
```

可以被简化为

```go
var _ = map[LangCategory]map[string]int{
    {true, true}: {
        "Python": 1991,
        "Erlang": 1986,
    },
    {true, false}: {
        "JavaScript": 1995,
    },
    {false, true}: {
        "Go":   2009,
        "Rust": 2010,
    },
    {false, false}: {
        "C": 1972,
    },
}
```

### 容器值的比较

映射和切片类型都属于不可比较类型。 所以任意两个映射值（或切片值）是不能相互比较的。

尽管两个映射值和切片值是不能比较的，但是一个映射值或者切片值可以和预声明的nil标识符进行比较以检查此映射值或者切片值是否为一个零值。

大多数数组类型都是可比较类型，除了元素类型为不可比较类型的数组类型。

当比较两个数组值时，它么的对应元素将逐一被比较。这两个数组只有在它们的对应元素都相等的情况下才相等。

```go
func main() {
    var a [16]byte
    var s []int
    var m map[string]int

    fmt.Println(a == a)   // true
    fmt.Println(m == nil) // true
    fmt.Println(s == nil) // true
    fmt.Println(nil == map[string]int{}) // false
    fmt.Println(nil == []int{})          // false

    // 下面这些行编译不通过。
    /*
    _ = m == m
    _ = s == s
    _ = m == map[string]int(nil)
    _ = s == []int(nil)
    var x [16][]int
    _ = x == x
    var y [16]map[int]bool
    _ = y == y
    */
}
```

### 查看容器值的长度和容量

除了已提到的容器长度属性（此容器中含有有多少个元素），每个容器值还有一个容量属性。 一个数组值的容量总是和它的长度相等；一个非零映射值的容量可以被认为是无限大的。一个切片值的容量总是不小于此切片值的长度。

可以调用内置函数len来获取一个容器值的长度，或者调用内置函数cap来获取一个容器值的容量。 这两个函数都返回一个int结果值。 因为非零映射值的容量是无限大，所以cap并不适用于映射值。

一个数组值的长度和容量永不改变。同一个数组类型的所有值的长度和容量都总是和此数组类型的长度相等。 切片值的长度和容量可在运行时刻改变。因为此原因，切片可以被认为是动态数组。

```go
func main() {
    var a [5]int
    fmt.Println(len(a), cap(a)) // 5 5
    var s []int
    fmt.Println(len(s), cap(s)) // 0 0
    s, s2 := []int{2, 3, 5}, []bool{}
    fmt.Println(len(s), cap(s), len(s2), cap(s2)) // 3 3 0 0
    var m map[int]bool
    fmt.Println(len(m)) // 0
    m, m2 := map[int]bool{1: true, 0: false}, map[int]int{}
    fmt.Println(len(m), len(m2)) // 2 0
}
```

### 读取和修改容器的元素

一个容器值v中存储的对应着键值`k`的元素用语法形式`v[k]`来表示。 今后我们称`v[k]`为一个元素索引表达式。

假设`v`是一个数组或者切片，在`v[k]`中，

- 如果`k`是一个常量，则它必须满足上面列出的对出现在组合字面值中的索引的要求。 另外，如果`v`是一个数组，则`k`必须小于此数组的长度。
- 如果`k`不是一个常量，则它必须为一个整数。 另外它必须为一个非负数并且小于`len(v)`，否则，在运行时刻将产生一个恐慌。
- 如果`v`是一个零值切片，则在运行时刻将产生一个恐慌。

假设`v`是一个映射值，在`v[k]`中，k的类型必须为（或者可以隐式转换为）`v`的类型的元素类型。另外，

- 如果`k`是一个动态类型为不可比较类型的接口值，则`v[k]`在运行时刻将造成一个恐慌；
- 如果`v[k]`被用做一个**赋值**语句中的目标值并且`v`是一个零值**nil映射**，则`v[k]`在运行时刻将造成一个**恐慌**；
- 如果`v[k]`用来表示**读取**映射值`v`中键值`k`对应的元素，则它无论如何都**不会产生一个恐慌**，即使v是一个零值`nil`映射（假设k的估值没有造成恐慌）；
- 如果`v[k]`用来表示读取映射值`v`中键值`k`对应的元素，并且映射值`v`中并不含有对应着键值k的条目，则`v[k]`返回一个此映射值的类型的元素类型的**零值**。 一般情况下，`v[k]`被认为是一个单值表达式。但是在一个`v[k]`被用为唯一源值的赋值语句中，`v[k]`可以返回一个**可选的第二个返回值**。 此第二个返回值是一个类型不确定布尔值，用来**表示是否有对应着键值**`k`的条目存储在映射值`v`中。

```go
func main() {
    a := [3]int{-1, 0, 1}
    s := []bool{true, false}
    m := map[string]int{"abc": 123, "xyz": 789}
    fmt.Println (a[2], s[1], m["abc"])    // 读取
    a[2], s[1], m["abc"] = 999, true, 567 // 修改
    fmt.Println (a[2], s[1], m["abc"])    // 读取

    n, present := m["hello"]
    fmt.Println(n, present, m["hello"]) // 0 false 0
    n, present = m["abc"]
    fmt.Println(n, present, m["abc"]) // 567 true 567
    m = nil
    fmt.Println(m["abc"]) // 0

    // 下面这两行编译不同过。
    /*
    _ = a[3]  // 下标越界
    _ = s[-1] // 下标越界
    */

    // 下面这几行每行都会造成一个恐慌。
    _ = a[n]         // panic: 下标越界
    _ = s[n]         // panic: 下标越界
    m["hello"] = 555 // panic: m为一个零值映射
}
```

### 切片的内部结构

```go
type _slice struct {
    elements unsafe.Pointer // 引用着底层存储在间接部分上的元素
    len      int            // 长度
    cap      int            // 容量
}
```

上面展示的切片的内部定义为切片的直接部分的定义。直接部分的len字段表示一个切片当前存储了多少个元素；直接部分的cap表示一个切片的容量。 下面这张图描绘了一个切片值的内存布局。

![slice-internal](https://i.imgur.com/xvcdtav.png)

从下标len（包含）到下标cap（不包含）对应的元素并不属于图中所示的切片值。 它们只是此切片之中的一些冗余元素槽位，但是它们可能是其它切片（或者数组）值中的有效元素。

当一个切片被用做一个append函数调用中的基础切片，

- 如果添加的元素数量大于此（基础）切片的冗余元素槽位的数量，则一个新的底层内存片
段将被开辟出来并用来存放结果切片的元素。 这时，基础切片和结果切片不共享任何底层元素。
- 否则，不会有底层内存片段被开辟出来。这时，基础切片中的所有元素也同时属于结果切片。两个切片的元素都存放于同一个内存片段上。

### 容器赋值

当一个映射赋值语句执行完毕之后，目标映射值和源映射值将共享底层的元素。 向其中一个映射中添加（或从一个映射中删除）元素将体现在另一个映射中。

和映射一样，当一个切片赋值给另一个切片后，它们将共享底层的元素。 它们的长度和容量也相等。但是如果以后其中一个切片*改变了长度或者容量*（？？），此变化不会影响到另一个切片。

当一个数组被赋值给另一个数组，所有的元素都将被从*源数组复制到目标数组*。赋值完成之后，这两个数组不共享任何元素。

```go
func main() {
    m0 := map[int]int{0:7, 1:8, 2:9}
    m1 := m0
    m1[0] = 2
    fmt.Println(m0, m1) // map[0:2 1:8 2:9] map[0:2 1:8 2:9]

    s0 := []int{7, 8, 9}
    s1 := s0
    s1[0] = 2
    fmt.Println(s0, s1) // [2 8 9] [2 8 9]

    a0 := [...]int{7, 8, 9}
    a1 := a0
    a1[0] = 2
    fmt.Println(a0, a1) // [7 8 9] [2 8 9]
}
```

### 添加和删除容器元素

向一个映射中添加一个条目的语法和修改一个映射元素的语法是一样的。 比如，对于一个非零映射值m，如果当前m中尚未存储条目(k, e)，则下面的语法形式将把此条目存入m；否则，下面的语法形式将把键值k对应的元素值更新为e。

`m[k] = e`

内置函数delete用来从一个映射中删除一个条目。比如，下面的delete调用将把键值k对应的条目从映射m中删除。 如果映射m中未存储键值为k的条目，则此调用为一个空操作，它不会产生一个恐慌，即使m是一个nil零值映射。

`delete(m, k)`

一个数组中的元素个数总是恒定的，我们无法向其中添加元素，也无法从其中删除元素。但是可寻址的数组值中的元素是可以被修改的。

通过调用内置append函数，以一个切片为基础，来添加不定数量的元素并返回一个新的切片。 此新的结果切片包含着基础切片中所有的元素和所有被添加的元素。 注意，基础切片并未被此append函数调用所修改。

Go中并未提供一个内置方式来从一个切片中删除一个元素。 我们必须使用append函数和后面将要介绍的子切片语法一起来实现元素删除操作。

```go
func main() {
    s0 := []int{2, 3, 5}
    fmt.Println(s0, cap(s0)) // [2 3 5] 3
    s1 := append(s0, 7)      // 添加一个元素
    fmt.Println(s1, cap(s1)) // [2 3 5 7] 6
    s2 := append(s1, 11, 13) // 添加两个元素
    fmt.Println(s2, cap(s2)) // [2 3 5 7 11 13] 6
    s3 := append(s0)         // <=> s3 := s0
    fmt.Println(s3, cap(s3)) // [2 3 5] 3
    s4 := append(s0, s0...)  // 以s0为基础添加s0中所有的元素
    fmt.Println(s4, cap(s4)) // [2 3 5 2 3 5] 6

    s0[0], s1[0] = 99, 789
    fmt.Println(s2[0], s3[0], s4[0]) // 789 99 2
}
```

### 使用内置make函数来创建切片和映射

除了使用组合字面值来创建映射和切片，我们还可以使用内置make函数来创建映射和切片。 数组不能使用内置make函数来创建。

假设M是一个映射类型并且n是一个非负整数，我们可以用下面的两种函数调用来各自生成一个类型为M的映射值。

`make(M, n)`
`make(M)`

`make(S, length, capacity)`
`make(S, length) // <=> make(S, length, length)`

```go
func main() {
    // 创建映射。
    fmt.Println(make(map[string]int)) // map[]
    m := make(map[string]int, 3)
    fmt.Println(m, len(m)) // map[] 0
    m["C"] = 1972
    m["Go"] = 2009
    fmt.Println(m, len(m)) // map[C:1972 Go:2009] 2

    // 创建切片。
    s := make([]int, 3, 5)
    fmt.Println(s, len(s), cap(s)) // [0 0 0] 3 5
    s = make([]int, 2)
    fmt.Println(s, len(s), cap(s)) // [0 0] 2 2
}
```

### 使用内置new函数来创建容器值

内置new函数可以用来为一个任何类型的值开辟内存并返回一个存储有此值的地址的指针。 用new函数开辟出来的值均为零值。

```go
func main() {
    m := *new(map[string]int)   // <=> var m map[string]int
    fmt.Println(m == nil)       // true
    s := *new([]int)            // <=> var s []int
    fmt.Println(s == nil)       // true
    a := *new([5]bool)          // <=> var a [5]bool
    fmt.Println(a == [5]bool{}) // true
}
```

### 容器元素的可寻址性

一些关于容器元素的可寻址性的事实：

- 可寻址的数组的元素也是可寻址的。不可寻址的数组的元素也是不可寻址的。 原因很简单，因为一个数组中的所有元素均处于此数组的直接部分。
- 一个切片值的任何元素都是可寻址的，即使此切片本身是不可寻址的。 这是因为一个切片的底层元素总是存储在一个被开辟出来的内存片段上。
- 任何映射元素都是不可寻址的。
  - 如果映射元素可以被取地址，则每个映射元素的地址在它的生命期内必须保持不变。 这阻碍了Go编译器在实现映射时使用更加有效率的算法。 对于标准编译器，映射元素的内部地址在运行时刻有可能发生改变。

```go
func main() {
    a := [5]int{2, 3, 5, 7}
    s := make([]bool, 2)
    pa2, ps1 := &a[2], &s[1]
    fmt.Println(*pa2, *ps1) // 5 false
    a[2], s[1] = 99, true
    fmt.Println(*pa2, *ps1) // 99 true
    ps0 := &[]string{"Go", "C"}[0]
    fmt.Println(*ps0) // Go

    m := map[int]bool{1: true}
    _ = m
    // 下面这几行编译不通过。
    /*
    _ = &[3]int{2, 3, 5}[0]
    _ = &map[int]bool{1: true}[1]
    _ = &m[1]
    */
}
```

每个数组或者结构体值都是仅含有一个直接部分。所以

- 如果一个映射类型的元素类型为一个结构体类型，则我们无法修改此映射类型的值中的每个结构体元素的单个字段。 我们必须整体地同时修改所有结构体字段。
- 如果一个映射类型的元素类型为一个数组类型，则我们无法修改此映射类型的值中的每个数组元素的单个元素。 我们必须整体地同时修改所有数组元素。

```go
func main() {
    type T struct{age int}
    mt := map[string]T{}
    mt["John"] = T{age: 29} // 整体修改是允许的
    ma := map[int][5]int{}
    ma[1] = [5]int{1: 789} // 整体修改是允许的

    // 这两个赋值编译不通过，因为部分修改一个映射
    // 元素是非法的。这看上去确实有些反直觉。
    /*
    ma[1][1] = 123      // error
    mt["John"].age = 30 // error
    */

    // 读取映射元素的元素或者字段是没问题的。
    fmt.Println(ma[1][1])       // 789
    fmt.Println(mt["John"].age) // 29
}
```

```go
func main() {
    type T struct{age int}
    mt := map[string]T{}
    mt["John"] = T{age: 29}
    ma := map[int][5]int{}
    ma[1] = [5]int{1: 789}

    t := mt["John"] // 临时变量
    t.age = 30
    mt["John"] = t // 整体修改

    a := ma[1] // 临时变量
    a[1] = 123
    ma[1] = a // 整体修改

    fmt.Println(ma[1][1], mt["John"].age) // 123 30
}
```

### *从数组或者切片派生切片（取子切片）

我们可以从一个基础切片或者一个可寻址的基础数组派生出另一个切片。此派生操作也常称为一个取子切片操作。 派生出来的切片的元素和基础切片（或者数组）的元素位于同一个内存片段上。或者说，派生出来的切片和基础切片（或者数组）将共享一些元素。

Go中有两种取子切片的语法形式（假设baseContainer是一个切片或者数组）：

`baseContainer[low : high]       // 双下标形式`

`baseContainer[low : high : max] // 三下标形式`

上面所示的双下标形式等价于下面的三下标形式：

`baseContainer[low : high : cap(baseContainer)]`

上面所示的取子切片表达式的语法形式中得下标必须满足下列关系，否则代码要么编译不通过，要么在运行时刻将造成恐慌。

```go
// 双下标形式
0 <= low <= high <= cap(baseContainer)

// 三下标形式
0 <= low <= high <= max <= cap(baseContainer)
```

- 只要上述关系均满足，下标low和high都可以大于len(baseContainer)。但是它们一定不能大于cap(baseContainer)。
- 如果baseContainer是一个零值nil切片，只要上面所示的子切片表达式中下标的值均为0，则此这两个子切片表达式不会造成恐慌。 在这种情况下，结果切片也是一个nil切片。

子切片表达式的结果切片的长度为high - low、容量为max - low。 派生出来的结果切片的长度可能大于基础切片的长度，但结果切片的容量绝不可能大于基础切片的容量。

- 如果*下标low为零，则它可被省略*。此条规则同时适用于双下标形式和三下标形式。
- 如果*下标high等于len(baseContainer)，则它可被省略*。此条规则同时只适用于双下标形式。
- 三下标形式中的下标max在任何情况下都不可被省略。

下面的子切片表达式都是相互等价的：

```go
baseContainer[0 : len(baseContainer)]
baseContainer[: len(baseContainer)]
baseContainer[0 :]
baseContainer[:]
baseContainer[0 : len(baseContainer) : cap(baseContainer)]
baseContainer[: len(baseContainer) : cap(baseContainer)]
```

```go
func main() {
    a := [...]int{0, 1, 2, 3, 4, 5, 6}
    s0 := a[:]     // <=> s0 := a[0:7:7]
    s1 := s0[:]    // <=> s1 := s0
    s2 := s1[1:3]  // <=> s2 := a[1:3]
    s3 := s1[3:]   // <=> s3 := s1[3:7]
    s4 := s0[3:5]  // <=> s4 := s0[3:5:7]
    s5 := s4[:2:2] // <=> s5 := s0[3:5:5]
    s6 := append(s4, 77)
    s7 := append(s5, 88)
    s8 := append(s7, 66)
    s3[1] = 99
    fmt.Println(len(s2), cap(s2), s2) // 2 6 [1 2]
    fmt.Println(len(s3), cap(s3), s3) // 4 4 [3 99 77 6]
    fmt.Println(len(s4), cap(s4), s4) // 2 4 [3 99]
    fmt.Println(len(s5), cap(s5), s5) // 2 2 [3 99]
    fmt.Println(len(s6), cap(s6), s6) // 3 4 [3 99 77]
    fmt.Println(len(s7), cap(s7), s7) // 3 4 [3 4 88]
    fmt.Println(len(s8), cap(s8), s8) // 4 4 [3 4 88 66]
}

```

### 使用内置copy函数来复制切片元素

我们可以使用内置copy函数来将一个切片中的元素复制到另一个切片。 这两个切片的类型可以不同，但是它们的**元素类型必须相同**。 换句话说，这两个切片的类型的**底层类型必须相同**。copy函数的第一个参数为目标切片，第二个参数为源切片。copy函数返回复制了多少个元素，此值（int类型）为这两个切片的长度的较小值。

```go
func main() {
    type Ta []int
    type Tb []int
    dest := Ta{1, 2, 3}
    src := Tb{5, 6, 7, 8, 9}
    n := copy(dest, src)
    fmt.Println(n, dest) // 3 [5 6 7]
    n = copy(dest[1:], dest)
    fmt.Println(n, dest) // 2 [5 5 6]

    a := [4]int{} // 一个数组
    n = copy(a[:], src)
    fmt.Println(n, a) // 4 [5 6 7 8]
    n = copy(a[:], a[2:])
    fmt.Println(n, a) // 2 [7 8 7 8]
}
```

### 遍历容器元素

在Go中，我们可以使用下面的语法形式来遍历一个容器中的键值和元素：

```go
for key, element = range aContainer {
    // 使用key和element ...
}
```

`for`和`range`为两个关键字，`key`和`element`称为循环变量。 如果`aContainer`是一个切片或者数组（或者数组指针，见后），则`key`的类型必须为内置类型`int`。

上面所示的`for-range`语法形式中的等号`=`也可以是一个变量短声明符号`:=`。 当短声明符号被使用的时候，`key`和`element`总是两个新声明的变量，这时如果`aContainer`是一个切片或者数组（或者数组指针），则`key`的类型被推断为内置类型`int`。

```go
func main() {
    m := map[string]int{"C": 1972, "C++": 1983, "Go": 2009}
    for lang, year := range m {
        fmt.Printf("%v: %v \n", lang, year)
    }

    a := [...]int{2, 3, 5, 7, 11}
    for i, prime := range a {
        fmt.Printf("%v: %v \n", i, prime)
    }

    s := []string{"go", "defer", "goto", "var"}
    for i, keyword := range s {
        fmt.Printf("%v: %v \n", i, keyword)
    }
}
```

```go
// 忽略键值循环变量。
for _, element = range aContainer {
    // ...
}

// 忽略元素循环变量。
for key, _ = range aContainer {
    element = aContainer[key]
    // ...
}

// 舍弃元素循环变量。此形式和上一个变种等价。
for key = range aContainer {
    element = aContainer[key]
    // ...
}

// 键值和元素循环变量均被忽略。
for _, _ = range aContainer {
    // 这个变种形势没有太大实用价值。
}

// 键值和元素循环变量均被舍弃。此形式和上一个变种等价。
for range aContainer {
    // 这个变种形势没有太大实用价值。
}

```

- 映射中的条目的遍历顺序是不确定的（可以认为是随机的）。或者说，同一个映射中的条目的两次遍历中，条目的顺序很可能是不一致的，即使在这两次遍历之间，此映射并未发生任何改变。
- 如果在一个映射中的条目的遍历过程中，一个还没有被遍历到的条目被删除了，则此条目保证不会被遍历出来。
- 如果在一个映射中的条目的遍历过程中，一个新的条目被添加入此映射，则此条目并不保证将在此遍历过程中被遍历出来。

- 被遍历的容器值是aContainer的一个**副本**。 注意，只有aContainer的直接部分被复制了。 此副本是一个**匿名**的值，所以它是不可被修改的。
  - 如果aContainer是一个数组，那么在遍历过程中对此数组元素的修改不会体现到**当前循环变量**中。 原因是此数组的副本（被真正遍历的容器）和此数组不共享任何元素。
  - 如果aContainer是一个切片（或者映射），那么在遍历过程中对此切片（或者映射）元素的修改将体现到循环变量中。 原因是此切片（或者映射）的副本和此切片（或者映射）共享元素（或条目）。
- 在遍历中的每个循环步，aContainer副本中的一个键值元素对将被赋值（复制）给循环变量。 所以对循环变量的直接部分的修改将不会体现在aContainer中的对应元素中。
- 所有被遍历的键值对将被赋值给**同一对**循环变量实例。

### 把数组指针当做数组来使用

通过在range关键字后跟随一个数组的指针来遍历此数组中的元素。 对于大尺寸的数组，这种方法比较高效，因为复制一个指针比复制一个大尺寸数组的代价低得多。

```go
func main() {
    var a [100]int

    for i, n := range &a { // 复制一个指针的开销很小
        fmt.Println(i, n)
    }

    for i, n := range a[:] { // 复制一个切片的开销很小
        fmt.Println(i, n)
    }
}
```

如果一个for-range循环中的**第二个循环变量**既没有被忽略，也没有被舍弃，并且range关键字后跟随一个nil数组指针，则此循环将造成一个恐慌。

可以通过数组的指针来访问和修改此数组中的元素。如果此指针是一个nil指针，将导致一个恐慌。

从一个nil数组指针派生切片将导致一个恐慌。

### memclr优化

假设t0是一个类型T的零值的字面表示形式，并且a是一个元素类型为T的数组，则官方标准编译器将把下面的单循环变量for-range代码块优化为一个[内部的memclr调用](https://github.com/golang/go/issues/5373)。 大多数情况下，此memclr调用比一个一个地重置元素要快。

此优化也适用于a为一个切片的情形。但是，有点遗憾，此优化不适用于a为一个数组指针的情形，至少到目前（Go 1.12）为止。 所以，如果你打算重置一个数组，最好不要在range关键字后跟随此数组的指针。 特别地，推荐在range关键字后跟随一个从此数组派生出来的切片。

```go
s := a[:]
for i := range s {
    s[i] = t0
}
```

### 内置函数len和cap的调用可能会在编译时刻被估值

如果传递给内置函数len或者cap的一个调用的实参是一个数组或者数组指针，则此调用将在编译时刻被估值。 此估值结果是一个类型为内置类型int的类型确定常量值。

```go
var a [5]int
var p *[7]string

// N和M都是类型为int的类型确定值。
const N = len(a)
const M = cap(p)

func main() {
    fmt.Println(N) // 5
    fmt.Println(M) // 7
}
```

### 单独修改一个切片的长度或者容量

可以通过反射的途径来单独修改一个切片的长度或者容量。

```go
func main() {
    s := make([]int, 2, 6)
    fmt.Println(len(s), cap(s)) // 2 6

    reflect.ValueOf(&s).Elem().SetLen(3)
    fmt.Println(len(s), cap(s)) // 3 6

    reflect.ValueOf(&s).Elem().SetCap(5)
    fmt.Println(len(s), cap(s)) // 3 5
}

```

### 更多切片操纵

#### 切片克隆

`sClone := append(s[:0:0], s...)`

对于长度较大（并且元素值的直接部分不含有指针）的切片，上面这种方法比下面这种方法效率更高。

```go
sClone := make([]T, len(s))
copy(sClone, s)
```

#### 删除一段切片元素

切片的元素在内存中是连续存储的，相邻元素之间是没有间隙的。所以，当切片的一个元素段被删除时，

- 如果剩余元素的次序必须保持原样，则被删除的元素段后面的每个元素都得前移。
- 如果剩余元素的次序不需要保持原样，则我们可以将尾部的一些元素移到被删除的元素的位置上。

在下面的例子中，假设from（包括）和to（不包括）是两个合法的下标，并且from不大于to。

```go
// 第一种方法（保持剩余元素的次序）：
s = append(s[:from], s[to:]...)

// 第二种方法（保持剩余元素的次序）：
s = s[:from + copy(s[from:], s[to:])]

// 第三种方法（不保持剩余元素的次序）：
copy(s[from:to], s[len(s)+from-to:])
s = s[:len(s)+from-to]
```

如果切片的元素可能引用着其它值，则我们应该重置因为删除元素而多出来的元素槽位上的元素值，以避免暂时性的内存泄露：

```go
// "len(s)+to-from"是删除操作之前切片s的长度。
temp := s[len(s):len(s)+to-from]
for i := range temp {
    temp[i] = t0
}
```

#### 删除一个元素

在下面的例子中，假设i将被删除的元素的下标，并且它是一个合法的下标。

```go
// 第一种方法（保持剩余元素的次序）：
s = append(s[:i], s[i+1:]...)

// 第二种方法（保持剩余元素的次序）：
s = s[:i + copy(s[i:], s[i+1:])]

// 上面两种方法都需要复制len(s)-i-1个元素。

// 第三种方法（不保持剩余元素的次序）：
s[i] = s[len(s)-1]
s = s[:len(s)-1]
```

如果切片的元素可能引用着其它值，则我们应该重置刚多出来的元素槽位上的元素值，以避免暂时性的内存泄露：

```go
s[len(s):len(s)+1][0] = t0
// 或者
s[:len(s)+1][len(s)] = t0
```

#### 条件性的删除切片元素

```go
// 假设T是一个小尺寸类型。
func DeleteElements(s []T, keep func(T) bool, clear bool) []T {
    result := make([]T, 0, len(s))
    for _, v := range s {
        if keep(v) {
            result = append(result, v)
        }
    }
    if clear { // 避免暂时性的内存泄露。
        temp := s[len(result):]
        for i := range temp {
            temp[i] = t0 // t0是类型T的零值的字面表示形式
        }
    }
    return result
}
```

#### 将一个切片中的所有元素插入到另一个切片中

```go
// 第一种方法:一行实现。
s = append(s[:i], append(elements, s[i:]...)...)

// 另一种效率更高的但较为繁琐的实现。
if cap(s)-len(s) >= len(elements) {
    s = s[:len(s)+len(elements)]
    copy(s[i+len(elements):], s[i:])
    copy(s[i:], elements)
} else {
    x := make([]T, 0, len(elements)+len(s))
    x = append(x, s[:i]...)
    x = append(x, elements...)
    x = append(x, s[i:]...)
    s = x
}

// Push（插入到结尾）。
s = append(s, elements...)

// Unshift（插入到开头）。
s = append(elements, s...)
```

#### 插入若干独立的元素

插入若干独立的元素和插入一个切片中的所有元素类似。 我们可以使用切片组合字面形式构建一个临时切片，然后使用上面的方法插入这些元素。

特殊的插入和删除：前推/后推，前弹出/后弹出
假设被推入和弹出的元素为e并且切片s拥有至少一个元素。

```go
// 前弹出（pop front，又称shift）
s, e = s[1:], s[0]
// 后弹出（pop back）
s, e = s[:len(s)-1], s[len(s)-1]
// 前推（push front）
s = append([]T{e}, s...)
// 后推（push back）
s = append(s, e)
```

### 用映射来模拟集合（set）

Go不支持内置集合（set）类型。但是，集合类型可以用轻松使用映射类型来模拟。 在实践中，我们常常使用映射类型map[K]struct{}来模拟一个元素类型为K的集合类型。 类型struct{}的尺寸为零，所以此映射类型的值中的元素不消耗内存。

## 字符串

字符串类型的内部结构声明如下：

```go
type _string struct {
    elements *byte // 引用着底层的字节
    len      int   // 字符串中的字节数
}
```

### 关于字符串的一些简单事实

- 字符串值（和布尔以及各种数值类型的值）可以被用做常量。
- Go支持两种风格的字符串字面表示形式：双引号风格（解释型字面表示）和反引号风格（直白字面表示）。
- 字符串类型的零值为空字符串。一个空字符串在字面上可以用""或者``来表示。
- 我们可以用运算符+和+=来衔接字符串。
- 字符串类型都是可比较类型。同一个字符串类型的值可以用==和!=比较运算符来比较。 并且和整数/浮点数一样，同一个字符串类型的值也可以用>、<、>=和<=比较运算符来比较。 当比较两个字符串值的时候，它们的底层字节将逐一进行比较。如果一个字符串是另一个字符串的前缀，并且另一个字符串较长，则另一个字符串为两者中的较大者。

```go
func main() {
    const World = "world"
    var hello = "hello"

    // 衔接字符串。
    var helloWorld = hello + " " + World
    helloWorld += "!"
    fmt.Println(helloWorld) // hello world!

    // 比较字符串。
    fmt.Println(hello == "hello")   // true
    fmt.Println(hello > helloWorld) // false
}
```

- 和Java语言一样，字符串值的内容（即底层字节）是不可更改的。 字符串值的长度也是不可独立被更改的。 一个可寻址的字符串只能通过将另一个字符串赋值给它来整体修改它。
- 字符串类型没有内置的方法。我们可以
  - 使用`strings`标准库提供的函数来进行各种字符串操作。
  - 调用内置函数`len`来获取一个字符串值的长度（此字符串中存储的字节数）。
  - 使用容器元素索引语法`aString[i]`来获取`aString`中的第`i`个字节。 表达式`aString[i]`是不可寻址的。换句话说，`aString[i]`不可被修改。
  - 使用子切片语法`aString[start:end]`来获取`aString`的一个子字符串。 这里，`start`（包括）和`end`（不包括）均为`aString`中存储的字节的下标。
- 对于标准编译器来说，一个字符串的赋值完成之后，此赋值中的目标值和源值将共享底层字节。 一个子切片表达式`aString[start:end]`的估值结果也将和基础字符串`aString`共享一部分底层字节。

```go
func main() {
    var helloWorld = "hello world!"

    var hello = helloWorld[:5] // 取子字符串
    // 104是英文字符h的ASCII（和Unicode）码。
    fmt.Println(hello[0])         // 104
    fmt.Printf("%T \n", hello[0]) // uint8

    // hello[0]是不可寻址和不可修改的，所以下面
    // 两行编译不通过。
    /*
    hello[0] = 'H'         // error
    fmt.Println(&hello[0]) // error
    */

    // 下一条语句将打印出：5 12 true
    fmt.Println(len(hello), len(helloWorld),
            strings.HasPrefix(helloWorld, hello))
}
```

### 字符串相关的类型转换

- 一个字符串值可以被显式转换为一个字节切片（byte slice），反之亦然。 一个字节切片类型是一个元素类型为内置类型byte的切片类型。 或者说，一个字节切片类型的底层类型为`[]byte`（亦即[]uint8）。
- 一个字符串值可以被显式转换为一个码点切片（rune slice），反之亦然。 一个码点切片类型是一个元素类型为内置类型rune的切片类型。 或者说，一个码点切片类型的底层类型为`[]rune`（亦即[]int32）。
- 在一个从**码点切片到字符串**的转换中，码点切片中的每个码点值将被UTF-8编码为一到四个字节至结果字符串中。 如果一个码点值是一个不合法的Unicode码点值，则它将被视为Unicode替换字符（码点）值`0xFFFD`（Unicode replacement character）。 替换字符值`0xFFFD`将被UTF-8编码为三个字节`0xef` `0xbf` `0xbd`。
- 当一个**字符串被转换为一个码点切片**时，此字符串中存储的字节序列将被解读为一个一个码点的UTF-8编码序列。 非法的UTF-8编码字节序列将被转化为Unicode替换字符值0xFFFD。
- 当一个字符串被转换为一个字节切片时，结果切片中的底层字节序列是此字符串中存储的字节序列的一份**深复制**。 即Go运行时将为结果切片开辟一块足够大的内存来容纳被复制过来的所有字节。当此字符串的长度较长时，此转换开销是比较大的。同样，当一个字节切片被转换为一个字符串时，此字节切片中的字节序列也将被深复制到结果字符串中。 当此字节切片的长度较长时，此转换开销同样是比较大的。在这两种转换中，必须使用深复制的原因是字节切片中的字节元素是可修改的，但是字符串中的字节是不可修改的，所以一个字节切片和一个字符串是不能共享底层字节序列的。
- 在字符串和字节切片之间的转换中，非法的UTF-8编码字节序列将被保持原样不变。
- Go并不支持字节切片和码点切片之间的直接转换。我们可以用下面列出的方法来实现这样的转换：
  - 利用字符串做为中间过渡。这种方法相对方便但效率较低，因为需要做两次深复制。
  - 使用unicode/utf8标准库包中的函数来实现这些转换。 这种方法效率较高，但使用起来不太方便。
  - 使用bytes标准库包中的Runes函数来将一个字节切片转换为码点切片。 但此包中没有将码点切片转换为字节切片的函数。

```go
func Runes2Bytes(rs []rune) []byte {
    n := 0
    for _, r := range rs {
        n += utf8.RuneLen(r)
    }
    n, bs := 0, make([]byte, n)
    for _, r := range rs {
        n += utf8.EncodeRune(bs[n:], r)
    }
    return bs
}

func main() {
    s := "颜色感染是一个有趣的游戏。"
    bs := []byte(s) // string -> []byte
    s = string(bs)  // []byte -> string
    rs := []rune(s) // string -> []rune
    s = string(rs)  // []rune -> string
    rs = bytes.Runes(bs) // []byte -> []rune
    bs = Runes2Bytes(rs) // []rune -> []byte
}
```

### 字符串和字节切片之间的转换的编译器优化

上面已经提到了字符串和字节切片之间的转换将深复制它们的底层字节序列。 标准编译器做了一些优化，从而在某些情形下避免了深复制。 至少这些优化在当前（Go SDK 1.12）是存在的。 这样的情形包括：

- 一个for-range循环中跟随range关键字的从字符串到字节切片的转换；
- 一个在映射元素索引语法中被用做映射主健的从字节切片到字符串的转换；
- 一个字符串比较表达式中被用做两个比较值之一的从字节切片到字符串的转换；
- 一个（至少有一个被衔接的字符串值为非空字符串常量的）字符串衔接表达式中的从字节切片到字符串的转换。

```go
func main() {
    var str = "world"
    // 这里，转换[]byte(str)将不需要一个深复制。
    for i, b := range []byte(str) {
        fmt.Println(i, ":", b)
    }

    key := []byte{'k', 'e', 'y'}
    m := map[string]string{}
    // 这里，转换string(key)将不需要一个深复制。
    // 即使key是一个包级变量，此优化仍然有效。
    m[string(key)] = "value"
    fmt.Println(m[string(key)]) // value
}
```

```go
var s string
var x = []byte{1024: 'x'}
var y = []byte{1024: 'y'}

func fc() {
    // 下面的四个转换都不需要深复制。
    if string(x) != string(y) {
        s = (" " + string(x) + string(y))[1:]
    }
}

func fd() {
    // 两个在比较表达式中的转换不需要深复制，
    // 但两个字符串衔接中的转换仍需要深复制。
    // 请注意此字符串衔接和fc中的衔接的差别。
    if string(x) != string(y) {
        s = string(x) + string(y)
    }
}

func main() {
    fmt.Println(testing.AllocsPerRun(1, fc)) // 1
    fmt.Println(testing.AllocsPerRun(1, fd)) // 3
}
```

### 使用for-range循环遍历字符串中的码点

```go
func main() {
    s := "éक्षिaπ囧"
    for i, rn := range s {
        fmt.Printf("%2v: 0x%x %v \n", i, rn, string(rn))
    }
    fmt.Println(len(s))
}
```

下标循环变量的值并非连续。原因是下标循环变量为字符串中字节的下标，而一个码点可能需要多个字节进行UTF-8编码。

### 字符串衔接方法

除了使用+运算符来衔接字符串，我们也可以用下面的方法来衔接字符串：

- fmt标准库包中的`Sprintf/Sprint/Sprintln`函数可以用来衔接各种类型的值的字符串表示，当然也包括字符串类型的值。
- 使用strings标准库包中的Join函数。
- bytes标准库包提供的Buffer类型可以用来构建一个字节切片，然后我们可以将此字节切片转换为一个字符串。
- 从Go 1.10开始，strings标准库包中的Builder类型可以用来拼接字符串。 和bytes.Buffer类型类似，此类型内部也维护着一个字节切片，但是它在将此字节切片转换为字符串时避免了底层字节的深复制。

### 语法糖：将字符串当作字节切片使用

内置函数copy和append可以用来复制和添加切片元素。如果这两个函数的调用中的第一个实参为一个字节切片的话，那么第二个实参可以是一个字符串。 （对于append函数调用，字符串实参后必须跟随三个点...。）

```go
func main() {
    hello := []byte("Hello ")
    world := "world!"

    // helloWorld := append(hello, []byte(world)...) // 正常的语法
    helloWorld := append(hello, world...)            // 语法糖
    fmt.Println(string(helloWorld))

    helloWorld2 := make([]byte, len(hello) + len(world))
    copy(helloWorld2, hello)
    // copy(helloWorld2[len(hello):], []byte(world)) // 正常的语法
    copy(helloWorld2[len(hello):], world)            // 语法糖
    fmt.Println(string(helloWorld2))
}
```

### 字符串比较优化

Go编译器一般会对字符串比较做出如下的优化：

- 对于==和!=比较，如果这两个字符串的长度不相等，则这两个字符串肯定不相等（无需进行字节比较）。
- 如果这两个字符串底层引用着字符串切片的指针相等，则比较结果等同于比较这两个字符串的长度。

所以两个相等的字符串的比较的时间复杂度取决于它们是否引用着同一个底层字节序列。 如果它们引用着同一个底层字节序列，则对它们的比较的时间复杂度为O(1)，否则时间复杂度为O(n)。

```go
func main() {
    bs := make([]byte, 1<<26)
    s0 := string(bs)
    s1 := string(bs)
    s2 := s1

    // s0、s1和s2是三个相等的字符串。
    // s0的底层字节序列是bs的一个深复制。
    // s1的底层字节序列也是bs的一个深复制。
    // s0和s1底层字节序列为两个不同的字节序列。
    // s2和s1共享同一个底层字节序列。

    startTime := time.Now()
    _ = s0 == s1
    duration := time.Now().Sub(startTime)
    fmt.Println("duration for (s0 == s1):", duration)

    startTime = time.Now()
    _ = s1 == s2
    duration = time.Now().Sub(startTime)
    fmt.Println("duration for (s1 == s2):", duration)
}
```

## 函数

在Go中，函数是一种一等公民类型。换句话说，我们可以把函数当作值来使用。 尽管Go是一门静态语言，但是Go函数的灵活性宛如甚至超越了很多动态语言。

### 函数签名（function signature）和函数类型

一个函数类型的字面表示形式由一个func关键字和一个函数签名字面表示表示形式组成。

一个函数签名由一个输入参数类型列表和一个输出结果类型列表组成。

```go
func (a int, b string, c string) (x int, y int, z bool)
func (a int, b, c string) (x, y int, z bool)
func (x int, y, z string) (a, b int, c bool)
func (_ int, _, _ string) (_, _ int, _ bool)
func (int, string, string) (int, int, bool) // 标准函数字面形式
func (a int, b string, c string) (int, int, bool)
func (x int, _ string, z string) (int, int, bool)
func (int, string, string) (x int, y int, z bool)
func (int, string, string) (a int, b int, _ bool)
// 这三个函数类型字面形式是等价的。
func () (x int)
func () (int)
func () int

// 这两个函数类型字面形式是等价的。
func (a int, b string) ()
func (a int, b string)
```

#### 变长参数和变长参数函数类型

一个函数的最后一个参数可以是一个变长参数。一个函数可以**最多有一个变长参数**。一个变长参数的类型总为一个**切片类型**。 变长参数在声明的时候必须在它的（切片）类型的元素类型前面前置三个点...，以示这是一个变长参数。

```go
func (values ...int64) (sum int64)
func (separator string, tokens ...string) string
```

#### 所有的函数类型都属于不可比较类型

### 函数原型

一个函数原型由一个函数名称和一个函数类型（或者说一个函数签名）组成。 它的字面形式由一个`func`关键字、一个函数名和一个函数签名字面形式组成。

`func Double(n int) (result int)`

### 变长函数声明和变长函数调用

#### 变长函数声明

变长函数声明和普通函数声明类似，只不过最后一个参数必须为变长参数。 一个变长参数在函数体内将被视为一个切片。

```go
// Sum返回所有输入实参的和。
func Sum(values ...int64) (sum int64) {
    // values的类型为int64。
    sum = 0
    for _, v := range values {
        sum += v
    }
    return
}

// Concat是一个低效的字符串拼接函数。
func Concat(separator string, tokens ...string) string {
    // tokens的类型为[]string。
    r := ""
    for i, t := range tokens {
        if i != 0 {
            r += separator
        }
        r += t
    }
    return r
}
```

#### 变长参数函数调用

在变长参数函数调用中，可以使用两种风格的方式将实参传递给类型为`[]T`的变长形参：

1. 传递一个切片做为实参。此切片必须可以被赋值给类型为`[]T`的值（或者说此切片可以被隐式转换为类型`[]T`）。 此**实参切片后必须跟随三个点`...`**。
2. 传递零个或者多个可以被隐式转换为`T`的实参（或者说这些实参可以赋值给类型为`T`的值）。 这些实参将被添加入一个匿名的在运行时刻创建的类型为`[]T`的切片中，然后此切片将被传递给此函数调用。

```go
func Sum(values ...int64) (sum int64) {
    sum = 0
    for _, v := range values {
        sum += v
    }
    return
}

func main() {
    a0 := Sum()
    a1 := Sum(2)
    a3 := Sum(2, 3, 5)
    // 上面三行和下面三行是等价的。
    b0 := Sum([]int64{}...) // <=> Sum(nil...)
    b1 := Sum([]int64{2}...)
    b3 := Sum([]int64{2, 3, 5}...)
    fmt.Println(a0, a1, a3) // 0 2 10
    fmt.Println(b0, b1, b3) // 0 2 10
}
```

```go
func Concat(separator string, tokens ...string) (r string) {
    for i, t := range tokens {
        if i != 0 {
            r += separator
        }
        r += t
    }
    return
}

func main() {
    tokens := []string{"Go", "C", "Rust"}
    langsA := Concat(",", tokens...)        // 风格1
    langsB := Concat(",", "Go", "C","Rust") // 风格2
    fmt.Println(langsA == langsB)           // true
}
```

下面这个例子编译不通过，因为两种调用风格混用了。

```go
// 这两个函数的声明见前面几例。
func Sum(values ...int64) (sum int64) {......}
func Concat(separator string, tokens ...string) string {......}

func main() {
    // 下面两行报同样的错：实参数目太多了。
    _ = Sum(2, []int64{3, 5}...)
    _ = Concat(",", "Go", []string{"C", "Rust"}...)
}
```

### 一此关于函数声明和函数调用的概念

#### 同一个包中可以同名的函数

一般来说，同一个包中声明的函数的名称不能重复，但有两个例外：

1. 同一个包内可以声明若干个原型为`func ()`的名称为`init`的函数。
2. 多个函数的名称可以被声明为空标识符`_`。这样声明的函数不可被调用。

#### 某些函数调用是在编译时刻被估值的

大多数函数调用都是在运行时刻被估值的。 但unsafe标准库包中的函数的调用都是在编译时刻估值的。 另外，某些其它内置函数（比如len和cap等）的调用在所传实参满足一定的条件的时候也将在编译时刻估值。

#### 所有的函数调用的传参均属于值复制

和赋值一样，传参也属于值（浅）复制。当一个值被复制时，只有它的直接部分被复制了。

#### 不含函数体的函数声明

我们可以使用Go汇编（Go assembly）来实现一个Go函数。 Go汇编代码放在后缀为.a的文件中。 一个使用Go汇编实现的函数依旧必须在一个*.go文件中声明，但是它的声明必须不能含有函数体。 换句话说，一个使用Go汇编实现的函数的声明中只含有它的原型。

#### 某些有返回值的函数可以不必返回

如果一个函数有返回值，则它的函数体内的最后一条语句必须为一条终止语句。 Go中有多种终止语句，return语句只是其中一种。所以一个有返回值的函数的体内不一定需要一个return语句。 比如下面两个函数（它们均可编译通过）：

```go
func fa() int {
    a:
    goto a
}

func fb() bool {
    for{}
}
```

#### 某些函数调用的返回结果不可被舍弃

自定义函数的调用结果都是可以被舍弃掉的。 大多数内置函数（除了recover和copy）的调用结果都是不可被舍弃的。 调用结果不可被舍弃的函数是不可以被用做延迟调用函数和协程起始函数的，比如`append`函数。

#### 有返回值的函数的调用是一种表达式

一个有且只有一个返回值的函数的每个调用总可以被当成一个单值表达式使用。 比如，它可以被内嵌在其它函数调用中当作实参使用，或者可以被当作其它表达式中的操作数使用。

如果一个有多个返回结果的函数的一个调用的返回结果没有被舍弃，则此调用可以当作一个多值表达式使用在两种场合：

1. 此调用可以在一个赋值语句中当作源值来使用，但是它**不能和其它源值掺和到一块**。
2. 此调用可以内嵌在另一个函数调用中中当作实参来使用，但是它**不能和其它实参掺和到一块**。

```go
func HalfAndNegative(n int) (int, int) {
    return n/2, -n
}

func AddSub(a, b int) (int, int) {
    return a+b, a-b
}

func Dummy(values ...int) {}

func main() {
    // 这几行编译没问题。
    AddSub(HalfAndNegative(6))
    AddSub(AddSub(AddSub(7, 5)))
    AddSub(AddSub(HalfAndNegative(6)))
    Dummy(HalfAndNegative(6))
    _, _ = AddSub(7, 5)

    // 下面这几行编译不通过。
    /*
    _, _, _ = 6, AddSub(7, 5)
    Dummy(AddSub(7, 5), 9)
    Dummy(AddSub(7, 5), HalfAndNegative(6))
    */
}
```

### 函数值

函数类型是Go中天然支持的一种类型。函数类型的值称为函数值。 在字面上，函数类型的零值也使用预定义的nil来表示。

内置函数和init函数不可被用做函数值。

任何函数值都可以被当作普通声明函数来调用。 调用一个nil函数来开启一个协程将产生一个致命的不可恢复的错误，此错误将使整个程序崩溃。 在其它情况下调用一个nil函数将产生一个可恢复的恐慌。

当一个函数值被赋给另一个函数值后，这两个函数值将共享底层部分（内部的函数结构）。

```go
func Double(n int) int {
    return n + n
}

func Apply(n int, f func(int) int) int {
    return f(n) // f的类型为"func(int) int"
}

func main() {
    fmt.Printf("%T\n", Double) // func(int) int
    // Double = nil // error: Double是不可修改的

    var f func(n int) int // 默认值为nil
    f = Double
    g := Apply
    fmt.Printf("%T\n", g) // func(int, func(int) int) int

    fmt.Println(f(9))         // 18
    fmt.Println(g(6, Double)) // 12
    fmt.Println(Apply(6, f))  // 12
}
```

```go
func main() {
    // 此函数返回一个函数类型的结果，亦即闭包（closure）。
    isMultipleOfX := func (x int) func(int) bool {
        return func(n int) bool {
            return n%x == 0
        }
    }

    var isMultipleOf3 = isMultipleOfX(3)
    var isMultipleOf5 = isMultipleOfX(5)
    fmt.Println(isMultipleOf3(6))  // true
    fmt.Println(isMultipleOf3(8))  // false
    fmt.Println(isMultipleOf5(10)) // true
    fmt.Println(isMultipleOf5(12)) // false

    isMultipleOf15 := func(n int) bool {
        return isMultipleOf3(n) && isMultipleOf5(n)
    }
    fmt.Println(isMultipleOf15(32)) // false
    fmt.Println(isMultipleOf15(60)) // true
}
```

## 数据通道

### 并发编程和并发同步

现代CPU一般含有多个核，并且一个核可能支持多线程。换句话说，现代CPU可以同时执行多条指令流水线。 为了将CPU的能力发挥到极致，我们常常需要使我们的程序支持并发计算。

并发计算是指若干计算可能在某些时间片段内同时运行的情形。 下面这两张图描绘了两种并发计算的场景。在此图中，A和B表示两个计算。 在第一种情形中，两个计算只在某些时间片段同时运行。 第二种情形称为并行计算。在并行计算中，多个计算在任何时间点都在同时运行。并行计算是一种特殊的并发计算。

![concurrent-vs-parallel](https://i.imgur.com/hKV47xb.png)

不同的并发计算可能共享一些资源，其中**共享内存资源**最为常见。 在一个并发程序中，常常会发生下面的情形：

- 在一个计算向一段内存写数据的时候，另一个计算从此内存段读数据，结果导致读出的数据的完整性得不到保证。
- 在一个计算向一段内存写数据的时候，另一个计算也向此段内存写数据，结果导致被写入的数据的完整性得不到保证。

这些情形被称为数据竞争（data race）。并发编程的一大任务就是要调度不同计算，控制它们对资源的访问时段，以使数据竞争的情况不会发生。 此任务常称为并发同步（或者数据同步）。

并发编程中的其它任务包括：

- 决定需要开启多少计算；
- 决定何时开启、阻塞、解除阻塞和结束哪些计算；
- 决定如何在不同的计算中分担工作负载。

Go中大多数的操作都是未同步的。换句话说，它们都不是并发安全的。 这些操作包括赋值、传参、和各种容器值操作等。

在Go中，每个计算都是一个协程。所以以后我们也常常用协程来表示计算。

### 数据通道介绍

Go语言设计团队的首任负责人Rob Pike对并发编程的一个建议是**不要让计算通过共享内存来通讯，而应该让它们通过通讯来共享内存**。 数据通道机制就是这种哲学的一个设计结果。

当通过共享内存来通讯的时候，我们需要一些传统的并发同步技术（比如互斥锁）来避免数据竞争。

把一个数据通道看作是在一个程序内部的一个先进先出（FIFO：first in first out）数据队列。 一些协程可以向此数据通道发送数据，另外一些协程可以从此数据通道接收数据。

随着一个数据值的传递（发送和接收），一些数据值的所有权从一个协程转移到了另一个协程。 当一个协程发送一个值到一个数据通道，我们可以认为此协程释放了一些值的所有权。 当一个协程从一个数据通道接收到一个值，我们可以认为此协程获取了一些值的所有权。

### 数据通道类型和值

和数组、切片以及映射类型一样，每个数据通道类型也有一个元素类型。 一个数据通道只能传送它的（数据通道类型的）元素类型的值。

数据通道可以是双向的，也可以是单向的。

- 字面形式`chan T`表示一个元素类型为`T`的双向数据通道类型。 编译器允许从此类型的值中接收和向此类型的值中发送数据。
- 字面形式`chan<- T`表示一个元素类型为T的单向发送数据通道类型。 编译器不允许从此类型的值中接收数据。
- 字面形式`<-chan T`表示一个元素类型为`T`的单向接收数据通道类型。 编译器不允许向此类型的值中发送数据。

双向数据通道`chan T`的值可以被隐式转换为单向数据通道类型`chan<- T`和`<-chan T`，但反之不行（即使显式也不行）。 类型`chan<- T`和`<-chan T`的值也不能相互转换。

每个数据通道值有一个容量属性。一个容量为0的数据通道值称为一个非缓冲数据通道（unbuffered channel），一个容量不为0的数据通道值称为一个缓冲数据通道（buffered channel）。

数据通道类型的零值也使用预声明的`nil`来表示。 一个非零数据通道值必须通过内置的`make`函数来创建。 比如`make(chan int, 10)`将创建一个元素类型为`int`的数据通道值。 第二个参数指定了欲创建的数据通道的容量。此第二个实参是可选的，它的默认值为`0`。

### 数据通道值的比较

所有数据通道类型均为可比较类型。一个数据通道值可能含有底层部分。 当一个数据通道值被赋给另一个数据通道值后，这两个数据通道值将共享相同的底层部分。 换句话说，这两个数据通道引用着同一个底层的内部数据通道对象。 比较这两个数据通道的结果为true。

### 数据通道操作

假设一个数据通道（值）为ch，下面列出了这五种操作的语法或者函数调用。

1. 调用内置函数`close`来关闭一个数据通道：

   `close(ch)`

   传给close函数调用的实参必须为一个数据通道值，并且此数据通道值不能为单向接收的。

2. 使用下面的语法向数据通道ch发送一个值v：

    `ch <- v`

    v必须能够赋值给数据通道ch的元素类型。 ch不能为单向接收数据通道。 <-称为数据发送操作符。

3. 使用下面的语法从数据通道ch接收一个值：

    `<-ch`

    如果一个数据通道操作不永久阻塞，它总会返回至少一个值，此值的类型为数据通道ch的元素类型。 ch不能为单向发送数据通道。 <-称为数据接收操作符，是的它和数据发送操作符的表示形式是一样的。

    在大多数场合下，一个数据接收操作可以被认为是一个单值表达式。 但是，当一个数据接收操作被用做一个赋值语句中的唯一的源值的时候，它可以返回第二个可选的类型不确定的布尔值返回值从而成为一个多值表达式。 此类型不确定的布尔值表示第一个接收到的值是否是在数据通道被关闭前发送的。

    `v = <-c`

    `v, sentBeforeClosed = <-ch`

4. 查询一个数据通道的容量：

    `cap(ch)`

5. 查询一个数据通道的长度：

    `len(ch)`

    一个数据通道的长度是指当前有多少个已被发送到此数据通道但还未被接收出去的元素值。

### 数据通道操作详解

数据通道类型的大致内部实现：

我们可以认为一个数据通道内部维护了三个队列（均可被视为先进先出队列）：

- **接收数据协程队列**。此队列是一个没有长度限制的链表。 *此队列中的协程均处于阻塞状态*，它们正等待着从此数据通道*接收数据*。
- **发送数据协程队列**。此队列也是一个没有长度限制的链表。 *此队列中的协程亦均处于阻塞状态*，它们正等待着向此数据通道*发送数据*。 此队列中的每个协程将要发送的值（或者此值的指针，取决于具体编译器实现）和此协程一起存储在此队列中。
- **数据缓冲队列**。这是一个循环队列，它的长度为此数据通道的容量。此队列中*存放的值的类型都为此数据通道的元素类型*。 如果此队列中当前存放的值的个数已经达到此数据通道的容量，则我们说此数据通道已经处于满槽状态。 如果此队列中当前存放的值的个数为零，则我们说此数据通道处于空槽状态。 对于一个非缓冲数据通道（容量为零），它总是同时处于满槽状态和空槽状态。

每个数据通道内部维护着一个互斥锁用来在各种数据通道操作中防止数据竞争。

下表简单地描述了三种数据通道操作施加到三类数据通道的结果。

| 操作     | 一个零值nil数据通道 | 一个非零值但已关闭的数据通道 | 一个非零值且尚未关闭的数据通道 |
| -------- | ------------------- | ---------------------------- | ------------------------------ |
| 关闭     | 产生恐慌            | 产生恐慌                     | 成功关闭<sup>(C)</sup>         |
| 发送数据 | 永久阻塞            | 产生恐慌                     | 阻塞或者成功发送<sup>(B)</sup> |
| 接收数据 | 永久阻塞            | 永不阻塞<sup>(D)</sup>       | 阻塞或者成功接收<sup>(A)</sup> |

上表中的五种未打上标的情形，规则很简单：

- 关闭一个nil数据通道或者一个已经关闭的数据通道将产生一个恐慌。
- 向一个已关闭的数据通道发送数据也将导致一个恐慌。属于一个**非阻塞操作**。
- 向一个nil数据通道发送数据或者从一个nil数据通道接收数据将使当前协程永久阻塞。

**数据通道操作情形A**： 当一个协程Gr尝试从一个非零且尚未关闭的数据通道接收数据的时候，此协程Gr将首先尝试获取此数据通道的锁，成功之后将执行下列步骤，直到其中一个步骤的条件得到满足。

1. 如果此数据通道的*缓冲队列不为空*（这种情况下，接收数据协程队列必为空，（如果不为空的话就会接收缓冲队列中的数据）），此协程Gr将从缓冲队列取出接收一个值。 如果发送数据协程队列不为空，一个发送协程将从此队列中弹出，此协程欲发送的值将被推入缓冲队列。此发送协程将恢复至运行状态。 接收数据协程Gr继续运行，不会阻塞。对于这种情况，此数据接收操作为一个**非阻塞操作**。
2. 否则（即此数据通道的*缓冲队列为空*），如果发送数据协程队列不为空（这种情况下，此数据通道必为一个非缓冲数据通道）， 一个发送数据协程将从此队列中弹出，此协程欲发送的值将被接收数据协程Gr接收。此发送协程将恢复至运行状态。 接收数据协程Gr继续运行，不会阻塞。对于这种情况，此数据接收操作为一个**非阻塞操作**。
3. 对于剩下的情况（即此数据通道的*缓冲队列和发送数据协程队列均为空*），此接收数据协程Gr将被推入接收数据协程队列，并进入**阻塞状态**。 它以后*可能会被另一个发送数据协程唤醒而恢复运行*。 对于这种情况，此数据接收操作为一个**阻塞操作**。

**数据通道操作情形B**： 当一个协程Gs尝试向一个非零且尚未关闭的数据通道发送数据的时候，此协程Gs将首先尝试获取此数据通道的锁，成功之后将执行下列步骤，直到其中一个步骤的条件得到满足。

1. 如果此数据通道的*接收数据协程队列不为空*（这种情况下，缓冲队列必为空）， 一个接收数据协程将从此队列中弹出，此协程将接收到发送协程Gs发送的值。此接收协程将恢复至运行状态。 发送数据协程Gs继续运行，不会阻塞。对于这种情况，此数据发送操作为一个**非阻塞操作**。
2. 否则（*接收数据协程队列为空*），如果缓冲队列未满（这种情况下，发送数据协程队列必为空）， 发送协程欲Gs发送的值将被*推入缓冲队列*，发送数据协程Gs继续运行，不会阻塞。 对于这种情况，此数据发送操作为一个**非阻塞操作**。
3. 对于剩下的情况（*接收数据协程队列为空，并且缓冲队列已满*），此*发送协程Gs将被推入发送数据协程队列，并进入阻塞状态*。 它以后可能会被另一个接收数据协程唤醒而恢复运行。 对于这种情况，此数据发送操作为一个**阻塞操作**。

**数据通道操作情形C**： 当一个协程成功获取到一个非零且尚未关闭的数据通道的锁并且准备关闭此数据通道时，下面两步将依次执行：

1. 如果此数据通道的*接收数据协程队列不为空*（这种情况下，缓冲队列必为空），此队列中的所有协程将被*依个弹出*，并且每个协程将接收到此数据通道的元素类型的一个**零值**，然后**恢复至运行状态**。
2. 如果此数据通道的*发送数据协程队列不为空*，此队列中的所有协程将被*依个弹出*，并且每个协程中将产生一个**恐慌**（因为向已关闭的数据通道发送数据）， 如果**缓冲队列**不为空，它**不会被清空**，其中的数据仍然**可以被后续的数据接收操作所接收到**。

**数据通道操作情形D**： 一个非零数据通道被关闭之后，此数据通道上的后续数据接收操作将永不会阻塞。

- 此数据通道的**缓冲队列中存储数据仍然可以被接收出来**。 一旦此**缓冲队列变为空**，后续的数据接收操作将永不阻塞并且**总会接收到一个此数据通道的元素类型的零值**。 上面已经提到了，一个接收操作的**第二个可选返回**（类型不确定布尔）值表示一个接收到的值是否是在此数据通道被关闭之前发送的。 如果此返回值为false，则第一个返回值必然是一个此数据通道的元素类型的零值。

![Channel_queue](https://i.imgur.com/gsfIIWS.png)

小结：

- 如果一个数据通道已经关闭了，则它的发送数据协程队列和接收数据协程队列肯定都为空，但是它的缓冲队列可能不为空。
- 在任何时刻，如果缓冲队列不为空，则接收数据协程队列必为空。
- 在任何时刻，如果缓冲队列未满，则发送数据协程队列必为空。
- 如果一个数据通道是缓冲的，则在任何时刻，它的发送数据协程队列和接收数据协程队列之一必为空。
- 如果一个数据通道是非缓冲的，则在任何时刻，一般说来，它的发送数据协程队列和接收数据协程队列之一必为空， 但是有一个例外：一个协程可能在一个select流程控制中同时被推入到此数据通道的发送数据协程队列和接收数据协程队列中。
- 向此类通道发送元素值的操作会被阻塞，直到至少有一个针对该通道的接收操作开始进行为止。
- 从此类通道接收元素值的操作会被阻塞，直到至少有一个针对该通道的发送操作开始进行为止。
- 针对非缓冲通道的接收操作会在与之相应的发送操作完成之前完成。
- 缓冲通道中，由于元素值的传递是异步的，所以发送操作在成功向通道发送元素值之后就会立即结束。

### 数据通道的使用例子

一个简单的通过一个非缓冲数据通道实现的请求/响应的例子：

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    c := make(chan int) // 一个非缓冲数据通道
    go func(ch chan<- int, x int) {
        time.Sleep(time.Second)
        // <-ch    // 此操作编译不通过
        ch <- x*x  // 阻塞在此，直到发送的值被接收
    }(c, 3)
    done := make(chan struct{})
    go func(ch <-chan int) {
        n := <-ch      // 阻塞在此，直到有值发送到c
        fmt.Println(n) // 9
        // ch <- 123   // 此操作编译不通过
        time.Sleep(time.Second)
        done <- struct{}{}
    }(c)
    <-done // 阻塞在此，直到有值发送到done
    fmt.Println("bye")
}
```

一个缓冲数据通道例子：

```go
package main

import "fmt"

func main() {
    c := make(chan int, 2) // 一个容量为2的缓冲数据通道
    c <- 3
    c <- 5
    close(c)
    fmt.Println(len(c), cap(c)) // 2 2
    x, ok := <-c
    fmt.Println(x, ok) // 3 true
    fmt.Println(len(c), cap(c)) // 1 2
    x, ok = <-c
    fmt.Println(x, ok) // 5 true
    fmt.Println(len(c), cap(c)) // 0 2
    x, ok = <-c
    fmt.Println(x, ok) // 0 false
    x, ok = <-c
    fmt.Println(x, ok) // 0 false
    fmt.Println(len(c), cap(c)) // 0 2
    close(c) // 此行将产生一个恐慌
    c <- 7   // 如果上一行不存在，此行也将产生一个恐慌。
}
```

一场永不休场的足球比赛：

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    var ball = make(chan string)
    kickBall := func(playerName string) {
        for {
            fmt.Print(<-ball, "传球", "\n")
            time.Sleep(time.Second)
            ball <- playerName
        }
    }
    go kickBall("张三")
    go kickBall("李四")
    go kickBall("王二麻子")
    go kickBall("刘大")
    ball <- "裁判"   // 开球
    var c chan bool // 一个零值nil数据通道
    <-c             // 永久阻塞在此
}
```

### 数据通道的元素值的传递都是复制过程

在一个值被从一个协程传递到另一个协程的过程中，此值将被复制至少一次。 如果此传递值曾经在某个数据通道的缓冲队列中停留过，则它在此传递过程中将被复制两次。 一次复制发生在从发送协程向缓冲队列推入此值的时候，另一个复制发生在接收协程从缓冲队列取出此值的时候。 和赋值以及函数调用传参一样，当一个值被传递时，只有它的直接部分被复制。

对于官方标准编译器，最大支持的数据通道的元素类型的尺寸为65535。

为了在数据传递过程中避免过大的复制成本，我们不应该使用尺寸很大的数据通道元素类型。 如果欲传送的值的尺寸较大，应该改用指针类型做为数据通道的元素类型。

### 关于数据通道和协程的垃圾回收

一个数据通道被其发送数据协程队列和接收数据协程队列中的所有协程引用着。因此，如果一个数据通道的这两个队列只要有一个不为空，则此数据通道肯定不会被垃圾回收。 另一方面，如果一个协程处于一个数据通道的某个协程队列之中，则此协程也肯定不会被垃圾回收，即使此数据通道仅被此协程所引用。 事实上，一个协程只有退出后才能被垃圾回收。

### 数据接收和发送操作都属于简单语句

数据接收和发送操作都属于简单语句， 另外一个数据接收操作总是可以被用做一个单值表达式。

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    fibonacci := func() chan uint64 {
        c := make(chan uint64)
        go func() {
            var x, y uint64 = 0, 1
            for ; y < (1 << 63); c <- y { // 步尾语句
                x, y = y, x+y
            }
            close(c)
        }()
        return c
    }
    c := fibonacci()
    for x, ok := <-c; ok; x, ok = <-c { // 初始化和步尾语句
        time.Sleep(time.Second)
        fmt.Println(x)
    }
}
```

### `for-range`应用于数据通道

for-range循环控制流程也适用于数据通道。 此循环将不断地尝试从一个数据通道接收数据，直到此数据通道关闭并且它的缓冲队列中为空为止。 和应用于数组/切片/映射的for-range语法不同，应用于数据通道的for-range语法中最多只能出现一个循环变量，此循环变量用来存储接收到的值。

```go
for
 v = range aChannel {
    // 使用v
}
```

等价于

```go
for {
    v, ok = <-aChannel
    if !ok {
        break
    }
    // 使用v
}
```

这里的数据通道aChannel一定不能为一个单向发送数据通道。 如果它是一个nil零值，则此for-range循环将使当前协程永久阻塞。

### `select-case`分支流程控制代码块

Go中有一个专门为数据通道设计的select-case分支流程控制语法。 此语法和switch-case分支流程控制语法很相似。 比如，select-case流程控制代码块中也可以有若干case分支和最多一个default分支。 但是，这两种流程控制也有很多不同点。在一个select-case流程控制中，

- `select`关键字和`{`之间不允许存在任何表达式和语句。
- `fallthrough`语句不能被使用.
- 每个`case`关键字后必须跟随一个数据通道接收数据操作或者一个数据通道发送数据操作。 数据通道接收数据操作可以做为源值出现在一条简单赋值语句中。 以后，一个`case`关键字后跟随的数据通道操作将被称为一个`case`操作。
- 所有的**非阻塞case操作**中将有一个被**随机选择执行**（而不是按照从上到下的顺序），然后执行此操作对应的case分支代码块。
- 在**所有的case操作均为阻塞的情况下，如果default分支存在，则default分支代码块将得到执行**； 否则，当前协程将被推入所有阻塞操作中相关的数据通道的发送数据协程队列或者接收数据协程队列中，并进入阻塞状态。

一个不含任何分支的select-case代码块select{}将使当前协程处于永久阻塞状态。

```go
package main

import "fmt"

func main() {
    var c chan struct{} // nil
    select {
    case <-c:             // 阻塞操作
    case c <- struct{}{}: // 阻塞操作
    default:
        fmt.Println("Go here.")
    }
}
```

```go
package main

import "fmt"

func main() {
    c := make(chan string, 2)
    trySend := func(v string) {
        select {
        case c <- v:
        default: // 如果c的缓冲已满，则执行默认分支。
        }
    }
    tryReceive := func() string {
        select {
        case v := <-c: return v
        default: return "-" // 如果c的缓冲为空，则执行默认分支。
        }
    }
    trySend("Hello!") // 发送成功
    trySend("Hi!")    // 发送成功
    trySend("Bye!")   // 发送失败，但不会阻塞。
    // 下面这两行将接收成功。
    fmt.Println(tryReceive()) // Hello!
    fmt.Println(tryReceive()) // Hi!
    // 下面这行将接收失败。
    fmt.Println(tryReceive()) // -
}
```

```go
package main

func main() {
    c := make(chan struct{})
    close(c)
    select {
    case c <- struct{}{}: // 如果此分支被选中，则产生一个恐慌
    case <-c:
    }
}
```

### `select-case`流程控制的实现机理

select-case流程控制是Go中的一个重要和独特的特性。 下面列出了官方标准运行时中select-case流程控制的实现步骤。

1. 将所有case操作中涉及到的数据通道表达式和发送值表达式按照从上到下，从左到右的顺序一一估值。 在赋值语句中做为源值的*数据接收操作对应的目标值在此时刻不需要被估值*。
2. 将所有分支的随机排序。default分支总是排在最后。 所有case操作中相关的数据通道可能会有重复的。
3. 为了防止在下一步中造成死锁，对所有case操作中相关的数据通道进行排序。 排序依据并不重要，可以按照它们的地址顺序进行排序。 排序结果中前N个数据通道不存在重复的情况。 N为所有case操作中不重复的数据通道的数量。 下面，通道锁顺序是针对此排序结果中的前N个数据通道来说的，通道锁逆序是指此顺序的逆序。
4. 按照上一步中的生成通道锁顺序获取所有相关的数据通道的锁。
5. 按照第2步中生成的分支顺序检查相应分支：
   1. 如果这是一个case分支并且相应的数据通道操作是一个向关闭了的数据通道发送数据操作，则按照通道锁逆序解锁所有的数据通道并在当前协程中产生一个恐慌。 跳到第12步。
   2. 如果这是一个case分支并且相应的数据通道操作是非阻塞的，则按照通道锁逆序解锁所有的数据通道并执行相应的case分支代码块。 （此相应的数据通道操作可能会唤醒另一个处于阻塞状态的协程。） 跳到第12步。
   3. 如果这是default分支，则按照通道锁逆序解锁所有的数据通道并执行此default分支代码块。 跳到第12步。

    （到这里，default分支肯定是不存在的，并且所有的case操作均为阻塞的。）
6. 将当前协程（和对应case分支信息）推入到每个case操作中对应的数据通道的发送数据协程队列或接收数据协程队列中。 当前协程可能会被多次推入到同一个数据通道的这两个队列中，因为多个case操作中对应的数据通道可能为同一个。
7. 使当前协程进入阻塞状态并则按照通道锁逆序解锁所有的数据通道。
8. 当前协程处于阻塞状态，等待其它协程通过数据通道操作唤醒当前协程
9. 当前协程被另一个协程中的一个数据通道操作唤醒。 此唤醒数据通道操作可能是一个数据通道关闭操作，也可能是一个数据发送/接收操作。 如果它是一个数据发送/接收操作，则（当前正被解释的select-case流程中）肯定有一个相应case操作与之配合传递数据。 在此配合过程中，当前协程将从相应case操作相关的数据通道的接收/发送数据协程队列中弹出。
10. 按照第3步中的生成的通道锁顺序获取所有相关的数据通道的锁。
11. 将当前协程从各个case操作中对应的数据通道的发送数据协程队列或接收数据协程队列中（可能以非弹出的方式）移除。
    1. 如果当前协程时被一个数据通道关闭操作所唤醒，则跳到第5步。
    2. 如果当前协程时被一个数据发送/接收操作所唤醒，则相应的case分支已经在第9步中知晓。 按照通道锁逆序解锁所有的数据通道并执行此case分支代码块。
12. 完毕。

小结：

1. 一个协程可能同时多次处于同一个数据通道的发送数据协程队列或接收数据协程队列中。
2. 当一个协程被阻塞在一个select-case流程控制中并在以后被唤醒时，它可能会从多个数据通道的发送数据协程队列和接收数据协程队列中被移除。

## 方法

### 方法声明

在Go中，我们可以为类型`T`和`*T`显式地声明一个方法，其中类型T必须满足四个条件：

1. T必须是一个**定义类型**；
2. T必须和此方法声明定义在**同一个代码包中**；
3. T不能是一个指针类型；
4. T不能是一个接口类型。

类型`T`和`*T`称为它们各自的方法的属主类型（receiver type）。 类型T被称作为类型T和*T声明的所有方法的属主基类型（receiver base type)

一个方法声明和一个函数声明很相似，但是比函数声明多了一个额外的参数声明部分。 此额外的参数声明部分只能含有一个类型为此方法的**属主类型的参数**，此参数称为此方法声明的属主参数（receiver parameter）。 此属主参数声明必须包裹在一对小括号`()`之中。 此属主参数声明部分必须**处于func关键字和方法名之间**。

```go
type Age int
func (age Age) LargerThan(a Age) bool {
    return age > a
}
func (age *Age) Increase() {
    *age++
}

// 为自定义的函数类型FilterFunc声明方法。
type FilterFunc func(in int) bool
func (ff FilterFunc) Filte(in int) bool {
    return ff(in)
}

// 为自定义的映射类型StringSet声明方法。
type StringSet map[string]struct{}
func (ss StringSet) Has(key string) bool {
    _, present := ss[key]
    return present
}
func (ss StringSet) Add(key string) {
    ss[key] = struct{}{}
}
func (ss StringSet) Remove(key string) {
    delete(ss, key)
}

// 为自定义的结构体类型Book和它的指针类型*Book声明方法。
type Book struct {
    pages int
}
func (b Book) Pages() int {
    return b.pages
}
func (b *Book) SetPages(pages int) {
    b.pages = pages
}
```

### 方法对应的隐式声明函数

```go
func Book.Pages(b Book) int {
    return b.pages // 此函数体和Book类型的Pages方法体一样
}

func (*Book).SetPages(b *Book, pages int) {
    b.pages = pages // 此函数体和*Book类型的SetPages方法体一样
}

func (b Book) Pages() int {
    return Book.pages(b)
}
func (b *Book) SetPages(pages int) {
    (*Book).SetPages(b, pages)
}
```

### 为指针类型属主隐式声明的方法

对每一个为值类型属主`T`声明的方法，编译器将自动隐式地为其对应的指针类型属主`*T`声明一个相应的同名方法。 以上面的为类型Book声明的Pages方法为例，编译器将自动为类型`*Book`声明一个同名方法：

```go
func (b *Book) Pages() int {
    return Book.Pages(*b) // 调用上节中隐式声明的函数
}

func (*Book).Pages(b *Book) int {
    return Book.Pages(*b)
}

```

### 方法原型（method prototype）和方法集（method set）

一个方法原型可以看作是一个不带func关键字的函数原型。 我们可以把每个方法声明看作是由一个func关键字、一个属主参数声明部分、一个方法原型和一个方法体组成。

```go
Pages() int
SetPages(pages int)
```

每个类型都有个方法集。一个非接口类型的方法集由所有为它声明的（不管是显式的还是隐式的，但不包含方法名为空标识符的）方法的原型组成。

比如，在上面的例子中，Book类型的方法集为：

```go
Pages() int
```

而*Book类型的方法集为：

```go
Pages() int
SetPages(pages int)
```

类型T的方法集总是类型*T的方法集的子集。

不同代码包中的同名非导出方法将总被认为是不同名的。

### 方法值和方法调用

方法事实上是特殊的函数。方法也常被称为成员函数。 当一个类型拥有一个方法，则此类型的每个值将拥有一个不可修改的函数类型的成员（类似于结构体的字段）。

```go
package main

import "fmt"

type Book struct {
    pages int
}

func (b Book) Pages() int {
    return b.pages
}

func (b *Book) SetPages(pages int) {
    b.pages = pages
}

func main() {
    var book Book

    fmt.Printf("%T \n", book.Pages)       // func() int
    fmt.Printf("%T \n", (&book).SetPages) // func(int)
    // &book值有一个隐式方法Pages。
    fmt.Printf("%T \n", (&book).Pages)    // func() int

    // 调用这三个方法。
    (&book).SetPages(123)
    book.SetPages(123)           // 等价于上一行
    fmt.Println(book.Pages())    // 123
    fmt.Println((&book).Pages()) // 123
}
```

事实上，上例中的`(&book).SetPages(123)`一行可以被简化为`book.SetPages(123)`。 为什么呢？毕竟，类型`book`并不拥有一个`SetPages`方法。 啊哈，这是Go中特别设计的为了让代码看上去更简洁并方便了编程的**语法糖**。此语法糖只对可寻址的值类型的属主有效。 编译器会自动将`book.SetPages(123)`改写为`(&book).SetPages(123)`。

每个此类型的值将拥有一个和此方法同名的成员函数。 此类型的零值也不例外，不论此类型的零值是否用nil来表示。

```go
package main

type StringSet map[string]struct{}
func (ss StringSet) Has(key string) bool {
    _, present := ss[key] // 永不会产生恐慌，即使ss为nil。
    return present
}

type Age int
func (age *Age) IsNil() bool {
    return age == nil
}
func (age *Age) Increase() {
    *age++ // 如果age是一个空指针，则此行将产生一个恐慌。
}

func main() {
    _ = (StringSet(nil)).Has   // 不会产生恐慌
    _ = ((*Age)(nil)).IsNil    // 不会产生恐慌
    _ = ((*Age)(nil)).Increase // 不会产生恐慌

    _ = (StringSet(nil)).Has("key") // 不会产生恐慌
    _ = ((*Age)(nil)).IsNil()       // 不会产生恐慌

    // 下面这行将产生一个恐慌，但是此恐慌不是在调用方法的时
    // 候产生的，而是在此方法体内解引用空指针的时候产生的。
    ((*Age)(nil)).Increase()
}
```

### 属主参数的传参是一个值复制过程

和普通参数传参一样，属主参数的传参也是一个值复制过程。 所以，在方法体内对属主参数的**直接部分**的修改将不会反映到方法体外。

```go
package main

import "fmt"

type Book struct {
    pages int
}

func (b Book) SetPages(pages int) {
    b.pages = pages
}

func main() {
    var b Book
    b.SetPages(123)
    fmt.Println(b.pages) // 0
}
```

```go
package main

import "fmt"

type Book struct {
    pages int
}

type Books []Book

func (books Books) Modify() {
    // 对属主参数的间接部分的修改将反映到方法之外。
    books[0].pages = 500
    // 对属主参数的直接部分的修改不会反映到方法之外。
    books = append(books, Book{789})
}

func main() {
    var books = Books{{123}, {456}}
    books.Modify()
    fmt.Println(books) // [{500} {456}]
}
```

为了将此两处修改反映到Modify方法之外，Modify方法的属主类型应该改为指针类型：

```go
func (books *Books) Modify() {
    *books = append(*books, Book{789})
    (*books)[0].pages = 500
}

func main() {
    var books = Books{{123}, {456}}
    books.Modify()
    fmt.Println(books) // [{500} {456} {789}]
}
```

### 如何决定一个方法声明使用值类型属主还是指针类型属主？

对于值类型属主还是指针类型属主都可以接受的方法声明，下面列出了一些考虑因素：

- 太多的指针可能会增加垃圾回收器的负担。
- 如果一个值类型的尺寸太大，那么属主参数在传参的时候的复制成本将不可忽略。
- 在并发场合下，同时调用为值类型属主和指针类型属主方法比较易于产生数据竞争。
- sync标准库包中的类型的值不应该被复制，所以如果一个结构体类型内嵌了这些类型，则不应该为这个结构体类型声明值类型属主的方法。

如果实在拿不定主意在一个方法声明中应该使用值类型属主还是指针类型属主，那么请使用指针类型属主。

## 接口

### 什么是接口类型？

一个接口类型指定了一个方法原型的集合。 换句话说，一个接口类型定义了一个方法集。 事实上，我们可以把一个接口类型看作是一个方法集。 接口类型中指定的任何方法原型中的方法名称都不能为空标识符_。

```go
// 一个非定义接口类型。
interface {
    About() string
}

// ReadWriter是一个定义的接口类型。
type ReadWriter interface {
    Read(buf []byte) (n int, err error)
    Write(buf []byte) (n int, err error)
}

// Runnable是一个非定义接口类型的别名。
type Runnable = interface {
    Run()
}
```

error类型为一个内置接口类型。 它的定义声明如下：

```go
type error interface {
    Error() string
}
```

一个没有指定任何方法原型的接口类型称为一个空接口类型。

### 类型的方法集

每个类型都有一个方法集。

- 对于一个非接口类型，它的方法集由所有为它声明的（包括显式和隐式的）方法的原型组成。
- 对于一个接口类型，它的方法集就是它所指定的方法集。

### 什么是实现（implementation）？

如果一个任意类型T的方法集为一个接口类型的方法集的**超集**，则我们说类型T实现了此接口类型。 T可以是一个非接口类型，也可以是一个接口类型。

**实现关系在Go中是隐式的**。两个类型之间的实现关系不需要在代码中显式地表示出来。Go中没有类似于implements的关键字。 Go编译器将自动在需要的时候检查两个类型之间的实现关系。

一个接口类型总是实现了它自己。两个指定了一个相同的方法集的接口类型相互实现了对方。

因为任何方法集都是一个空方法集的超集，所以**任何类型都实现了任何空接口类型**。

在下面的例子中，类型`*Book`、`MyInt`和`*MyInt`都拥有一个原型为`About() string`的方法，所以它们都实现了接口类型`interface {About() string}`。

```go
type Book struct {
    name string
    // 更多其它字段……
}

func (book *Book) About() string {
    return "Book: " + book.name
}

type MyInt int

func (MyInt) About() string {
    return "我是一个自定义整数类型"
}
```

### 值包裹

每个接口值都可以看作是一个用来*包裹一个非接口值的盒子*。 欲将一个非接口值包裹在一个接口值中，此*非接口值的类型必须实现了此接口值的类型*。

如果类型T实现了一个接口类型I，则类型T的值都可以隐式转换到类型I。 换句话说，类型T的值可以赋给类型I的可修改值。 当一个T值被转换到类型I（或者赋给一个I值）的时候，

- 如果类型T是一个**非接口类型**，则此T值的一个**复制**将被包裹在结果（或者目标）I值中。 此操作的**时间复杂度为O(n)**，其中n为T值的尺寸。
- 如果类型T也为一个**接口类型**，则此T值中**当前包裹的（非接口）值将被复制**一份到结果（或者目标）I值中。 官方标准编译器为此操作做了优化，使得此操作的**时间复杂度为O(1)**，而不是O(n)。

当一个非接口值被包裹在一个接口值中，此非接口值称为此接口值的**动态值**，此非接口值的类型称为此接口值的**动态类型**。

接口值的动态值的直接部分是不可修改的的，除非它的动态值被整体替换为另一个动态值。

接口类型的零值也用预声明的nil标识符来表示。 一个nil接口值中什么也没包裹。将一个接口值修改为nil将清空包裹在此接口值中的非接口值。

因为任何类型都实现了空接口类型，所以任何非接口值都可以被包裹在任何一个空接口类型的接口值中（可接收任何参数的函数fmt.Println）。

当一个类型不确定值（除了类型不确定的nil）被转换为一个空接口类型（或者赋给一个空接口值），此类型不确定值将首先转换为它的默认类型。

```go
package main

import "fmt"

type Aboutable interface {
    About() string
}

// 类型*Book实现了接口类型Aboutable。
type Book struct {
    name string
}
func (book *Book) About() string {
    return "Book: " + book.name
}

func main() {
    // 一个*Book值被包裹在了一个Aboutable值中。
    var a Aboutable = &Book{"Go语言101"}
    fmt.Println(a) // &{Go语言101}

    // i是一个空接口值。类型*Book实现了任何空接口类型。
    var i interface{} = &Book{"Rust 101"}
    fmt.Println(i) // &{Rust 101}

    // Aboutable实现了空接口类型interface{}。
    i = a
    fmt.Println(i) // &{Go语言101}
}
```

在编译时刻，Go编译器将构建一个全局表用来存储代码中要用到的各个类型的信息。 对于一个类型来说，这些信息包括：此类型的种类（kind）、此类型的所有方法和字段信息、此类型的尺寸，等等。 这个全局表将在程序启动的时候被加载到内存中。

在运行时刻，当一个非接口值被包裹到一个接口值，Go运行时（至少对于官方标准运行时来说）将*分析和构建这两个值的类型的实现关系信息*，并将此实现关系信息存入到此接口值内。 对每一对这样的类型，它们的实现关系信息将仅被最多构建一次。并且为了程序效率考虑，此实现关系信息将被缓存在内存中的一个全局映射中，以备后用。 所以此全局映射中的条目数永不减少。 事实上，一个非零接口值在内部只是使用一个指针字段来引用着此全局映射中的一个实现关系信息条目。

对于一个非接口类型和接口类型对，它们的实现关系信息包括两部分的内容：

1. 动态类型（即此非接口类型）的信息。
2. 一个方法表（切片类型），其中存储了所有此接口类型指定的并且为此非接口类型（动态类型）声明的方法。

### 多态（polymorphism）

当非接口类型T的一个值t被包裹在接口类型I的一个接口值i中，通过i调用接口类型I指定的一个方法时，事实上为非接口类型T声明的对应方法将通过非接口值t被调用。 换句话说，**调用一个接口值的方法实际上将调用此接口值的动态值的对应方法**。一个接口值可以通过包裹不同动态类型的动态值来表现出各种不同的行为，这称为多态。

```go
package main

import "fmt"

type Filter interface {
    About() string
    Process([]int) []int
}

// UniqueFilter用来删除重复的数字。
type UniqueFilter struct{}
func (UniqueFilter) About() string {
    return "删除重复的数字"
}
func (UniqueFilter) Process(inputs []int) []int {
    outs := make([]int, 0, len(inputs))
    pusheds := make(map[int]bool)
    for _, n := range inputs {
        if !pusheds[n] {
            pusheds[n] = true
            outs = append(outs, n)
        }
    }
    return outs
}

// MultipleFilter用来只保留某个整数的倍数数字。
type MultipleFilter int
func (mf MultipleFilter) About() string {
    return fmt.Sprintf("保留%v的倍数", mf)
}
func (mf MultipleFilter) Process(inputs []int) []int {
    var outs = make([]int, 0, len(inputs))
    for _, n := range inputs {
        if n % int(mf) == 0 {
            outs = append(outs, n)
        }
    }
    return outs
}

// 在多态特性的帮助下，只需要一个filteAndPrint函数。
func filteAndPrint(fltr Filter, unfiltered []int) []int {
    // 在fltr参数上调用方法其实是调用fltr的动态值的方法。
    filtered := fltr.Process(unfiltered)
    fmt.Println(fltr.About() + ":\n\t", filtered)
    return filtered
}

func main() {
    numbers := []int{12, 7, 21, 12, 12, 26, 25, 21, 30}
    fmt.Println("过滤之前：\n\t", numbers)

    // 三个非接口值被包裹在一个Filter切片的三个接口元素中。
    filters := []Filter{
        UniqueFilter{},
        MultipleFilter(2),
        MultipleFilter(3),
    }

    // 每个切片元素将被赋值给类型为Filter的循环变量fltr。
    // 每个元素中的动态值也将被同时复制并被包裹在循环变量fltr中。
    for _, fltr := range filters {
        numbers = filteAndPrint(fltr, numbers)
    }
}
```

### 反射（reflection）

一个接口值中存储的动态类型信息可以被用来*检视此接口值的动态值和操纵此动态值所引用的值*。 这称为反射。

#### 类型断言

Go中有四种接口相关的类型转换情形：

- 将一个非接口值转换为一个接口类型。在这样的转换中，此非接口值的类型必须实现了此接口类型。
- 将一个接口值转换为另一个接口类型（前者接口值的类型实现了后者目标接口类型）。
- 将一个接口值转换为一个非接口类型（此非接口类型必须实现了此接口值的接口类型）。
- 将一个接口值转换为另一个接口类型（前者接口值的类型可以实现了*也可以未实现后者目标接口类型*）。

一个类型断言表达式的语法为`i.(T)`，其中`i`为一个接口值，`T`为一个类型名或者类型字面表示。 类型`T`可以为

- 任意一个非接口类型。
- 或者一个任意接口类型。

在一个类型断言表达式`i.(T)`中，`i`称为**断言值**，`T`称为**断言类型**。 一个断言可能成功或者失败。

- 对于T是一个**非接口类型**的情况，如果**断言值i的动态类型存在并且此动态类型和T为同一类型**，则此**断言将成功**；否则，此断言失败。 当此断言成功时，此类型断言表达式的估值结果为断言值i的**动态值的一个复制**。 我们可以把此种情况看作是一次拆封动态值的尝试。
- 对于T是一个**接口类型**的情况，当断言值i的动态类型存在并且此动态类型**实现了接口类型T**，则此**断言将成功**；否则，此断言失败。 当此断言成功时，此类型断言表达式的估值结果为一个包裹了断言值i的动态值的一个**复制的T值**。

一个**失败的类型断言**的估值结果为断言类型的**零值**。

此断言可以返回一个可选的第二个结果并被视作为一个多值表达式。 此可选的第二个结果为一个类型不确定的布尔值，用来表示此断言是否成功了。

如果一个断言失败并且它的可选的第二个结果未呈现，则此断言将造成一个恐慌。

```go
func main() {
    // 编译器将把123的类型推断为内值类型int。
    var x interface{} = 123

    // 情形一：
    n, ok := x.(int)
    fmt.Println(n, ok) // 123 true
    n = x.(int)
    fmt.Println(n) // 123

    // 情形二：
    a, ok := x.(float64)
    fmt.Println(a, ok) // 0 false

    // 情形三：
    a = x.(float64) // 将产生一个恐慌
}
```

```go
package main

import "fmt"

type Writer interface {
    Write(buf []byte) (int, error)
}

type DummyWriter struct{}
func (DummyWriter) Write(buf []byte) (int, error) {
    return len(buf), nil
}

func main() {
    var x interface{} = DummyWriter{}
    var y interface{} = "abc" // y的动态类型为内置类型string
    var w Writer
    var ok bool

    // DummyWriter既实现了Writer，也实现了interface{}。
    w, ok = x.(Writer)
    fmt.Println(w, ok) // {} true
    x, ok = w.(interface{})
    fmt.Println(x, ok) // {} true

    // y的动态类型为string。string类型并没有实现Writer。
    w, ok = y.(Writer)
    fmt.Println(w, ok) // <nil> false
    w = y.(Writer)     // 将产生一个恐慌
}
```

对于一个动态类型为T的接口值i，方法调用`i.m(...)`等价于`i.(T).m(...)`。

#### `type-switch`流程控制代码块

可以被看作是类型断言的增强版。它和switch-case流程控制代码块有些相似。 一个type-switch流程控制代码块的语法如下所示

```go
switch aSimpleStatement; v := x.(type) {
case TypeA:
    ...
case TypeB, TypeC:
    ...
case nil:
    ...
default:
    ...
}
```

其中`aSimpleStatement;`部分是可选的。 aSimpleStatement必须是一个`简单语句`。 x必须为一个估值结果为**接口值**的表达式，它称为此代码块中的断言值。 v称为此代码块中的**断言结果**，它必须出现在一个**短变量声明形式**中。

如果我们不关心一个`type-switch`代码块中的断言结果，则此`type-switch`代码块可简写为`switch x.(type) {...}`。

在一个`type-switch`代码块中，每个`case`关键字后可以跟随一个`nil`标识符和若干个**类型名**或**类型字面表示形式**。 在同一个`type-switch`代码块中，这些跟随在所有`case`关键字后的**条目不可重复**。

如果跟随在某个`case`关键字后的条目为一个非接口类型（用一个类型名或类型字面表示），则此非接口类型必须实现了断言值x的（接口）类型。

```go
func main() {
    values := []interface{}{
        456, "abc", true, 0.33, int32(789),
        []int{1, 2, 3}, map[int]bool{}, nil,
    }
    for _, x := range values {
        // 这里，虽然变量v只被声明了一次，但是它在
        // 不同分支中可以表现为多个类型的变量值。
        switch v := x.(type) {
        case []int: // 一个类型字面表示
            // 在此分支中，v的类型为[]int。
            fmt.Println("int slice:", v)
        case string: // 一个类型名
            // 在此分支中，v的类型为string。
            fmt.Println("string:", v)
        case int, float64, int32: // 多个类型名
            // 在此分支中，v的类型为x的类型interface{}。
            fmt.Println("number:", v)
        case nil:
            // 在此分支中，v的类型为x的类型interface{}。
            fmt.Println(v)
        default:
            // 在此分支中，v的类型为x的类型interface{}。
            fmt.Println("others:", v)
        }
        // 注意：在最后的三个分支中，v均为接口值x的一个复制。
    }
}
```

上面例子逻辑等价于：

```go
func main() {
    values := []interface{}{
        456, "abc", true, 0.33, int32(789),
        []int{1, 2, 3}, map[int]bool{}, nil,
    }
    for _, x := range values {
        if v, ok := x.([]int); ok {
            fmt.Println("int slice:", v)
        } else if v, ok := x.(string); ok {
            fmt.Println("string:", v)
        } else if x == nil {
            v := x
            fmt.Println(v)
        } else {
            _, isInt := x.(int)
            _, isFloat64 := x.(float64)
            _, isInt32 := x.(int32)
            if isInt || isFloat64 || isInt32 {
                v := x
                fmt.Println("number:", v)
            } else {
                v := x
                fmt.Println("others:", v)
            }
        }
    }
}
```

type-switch代码块和switch-case代码块有很多共同点：

- 在一个type-switch代码块中，最多只能有一个default分支存在。
- 在一个type-switch代码块中，如果default分支存在，它可以为最后一个分支、第一个分支或者中间的某个分支。
- 一个type-switch代码块可以不包含任何分支，它可以被视为一个空操作。

但是，和switch-case代码块不一样，fallthrough语句不能使用在type-switch代码块中。

#### 接口类型内嵌

一个接口类型可以内嵌另一个接口类型的名称。 此内嵌的效果相当于将此被内嵌的接口类型所指定的**所有方法原型展开到内嵌它的接口类型的定义体内**。

如果两个接口类型都**指定了一个同名方法**，则这两个接口类型**不可被同时被内嵌在同一个接口类型中**，即使它们指定的同名方法的原型也一致。

```go
type Ia interface {
    fa()
}

type Ib = interface {
    fb()
}

type Ic interface {
    fa()
    fb()
}

type Id = interface {
    Ia // 内嵌Ia
    Ib // 内嵌Ib
}

type Ie interface {
    Ia // 内嵌Ia
    fb()
}

//反例
type Ix interface {
    Ia
    Ic
}

type Iy = interface {
    Ib
    Ic
}

type Iz interface {
    Ic
    fa()
}
```

#### 接口值相关的比较

- 比较一个非接口值和接口值；
- 比较两个接口值。

非接口值的类型必须实现了接口值的类型（假设此接口类型为I），所以此非接口值可以被隐式转化为（包裹到）一个I值中。 这意味着非接口值和接口值的比较可以转化为两个接口值的比较。

比较两个接口值其实是比较这两个接口值的动态类型和和动态值。

下面是（使用==比较运算符）比较两个接口值的步骤：

1. 如果其中一个接口值是一个nil接口值，则比较结果为另一个接口值是否也为一个nil接口值。
2. 如果这两个接口值的**动态类型不一样**，则比较结果为**false**。
3. 对于这两个接口值的动态类型一样的情形，
    - 如果它们的动态类型为一个不可比较类型，则将产生一个恐慌。
    - 否则，比较结果为它们的动态值的比较结果。

简而言之，两个接口值的比较结果只有在下面两种任一情况下才为true：

1. 这两个接口值都为nil接口值。
2. 这两个接口值的**动态类型相同**、**动态类型为可比较类型**、并且**动态值相等**。

两个包裹了不同非接口类型的nil零值的接口值是不相等的。

```go
func main() {
    var a, b, c interface{} = "abc", 123, "a"+"b"+"c"
    fmt.Println(a == b) // 第二步的情形。 输出"false"。
    fmt.Println(a == c) // 第三步的情形。 输出"true"。

    var x *int = nil
    var y *bool = nil
    var ix, iy interface{} = x, y
    var i interface{} = nil
    fmt.Println(ix == iy) // 第二步的情形。 输出"false"。
    fmt.Println(ix == i)  // 第一步的情形。 输出"false"。
    fmt.Println(iy == i)  // 第一步的情形。 输出"false"。

    var s []int = nil // []int为一个不可比较类型。
    i = s
    fmt.Println(i == nil) // 第一步的情形。 输出"false"。
    fmt.Println(i == i)   // 第三步的情形。 将产生一个恐慌。
}
```

#### 指针动态值和非指针动态值

标准编译器/运行时对接口值的动态值为指针类型的情况做了特别的优化。 此优化使得**接口值包裹指针动态值比包裹非指针动态值的效率更高**。

#### 一个`[]T`类型的值不能直接被转换为类型`[]I`，即使类型`T`实现了接口类型`I`

#### 一个接口类型每个指定的每一个方法都对应着一个隐式声明的函数

如果接口类型I指定了一个名为`m`的方法原型，则编译器将隐式声明一个与之对应的函数名为`I.m`的函数。 此函数比m的方法原型中的参数多一个。此多出来的参数为函数`I.m`的第一个参数，它的类型为I。 对于一个类型为I的值i，方法调用`i.m(...)`和函数调用`I.m(i, ...)`是等价的。

```go
type I interface {
    m(int)bool
}

type T string
func (t T) m(n int) bool {
    return len(t) > n
}

func main() {
    var i I = T("gopher")
    fmt.Println(i.m(5))                          // true
    fmt.Println(I.m(i, 5))                       // true
    fmt.Println(interface {m(int) bool}.m(i, 5)) // true

    // 下面这几行被执行的时候都将会产生一个恐慌。
    I(nil).m(5)
    I.m(nil, 5)
    interface {m(int) bool}.m(nil, 5)
}
```

## 类型内嵌

结构体中一个字段可以仅由一个字段类型组成。 这样的字段声明方式称为类型内嵌（type embedding）

### 类型内嵌语法

```go

import "net/http"

func main() {
    type P = *bool
    type M = map[int]int
    var x struct {
        string // 一个定义的非指针类型
        error  // 一个定义的接口类型
        *int   // 一个非定义指针类型
        P      // 一个非定义指针类型的别名
        M      // 一个非定义类型的别名

        http.Header // 一个定义的映射类型
    }
    x.string = "Go"
    x.error = nil
    x.int = new(int)
    x.P = new(bool)
    x.M = make(M)
    x.Header = http.Header{}
}
```

内嵌字段有时也称为匿名字段。但是，事实上，每个内嵌字段有一个（隐式的）名字。 此字段的非限定（unqualified）类型名即为此字段的名称。 比如，上例中的六个内嵌字段的名称分别为string、error、int、P、M和Header。

### 哪些类型可以被内嵌？

一个内嵌字段必须被声明为形式`T`或者`*T`，其中T为一个类型名并且`T`和`*T`**不能表示基类型为指针类型或者接口类型的指针类型**。

```go
type Encoder interface {Encode([]byte) []byte}
type Person struct {name string; age int}
type Alias = struct {name string; age int}
type AliasPtr = *struct {name string; age int}
type IntPtr *int
type AliasPP = *IntPtr

// 这些类型或别名都可以被内嵌。
Encoder
Person
*Person
Alias
*Alias
AliasPtr
int
*int

// 这些类型或别名都不能被内嵌。
AliasPP          // 基类型为一个指针类型
*Encoder         // 基类型为一个接口类型
*AliasPtr        // 基类型为一个指针类型
IntPtr           // 定义的指针类型
*IntPtr          // 基类型为一个指针类型
*chan int        // 基类型为一个非定义类型
struct {age int} // 非定义非指针类型
map[string]int   // 非定义非指针类型
[]int64          // 非定义非指针类型
func()           // 非定义非指针类型
```

一个结构体类型中不允许有两个同名字段，此规则对匿名字段同样适用。

一个结构体类型不能内嵌（无论间接还是直接）它自己。

### 类型内嵌的意义是什么？

类型内嵌的主要目的是为了将**被内嵌类型的功能扩展到内嵌它的结构体类型中**，从而我们不必再为此结构体类型重复实现一下被内嵌类型的功能。

与其他语言继承类似，不同点在于：

- 如果类型T继承了另外一个类型，则类型T获取了另外一个类型的能力。 同时，一个T类型的值也可以被当作另外一个类型的值来使用。
- 如果一个类型T内嵌了另外一个类型，则另外一个类型变成了类型T的一部分。 类型T获取了另外一个类型的能力，但是T类型的任何值都不能被当作另外一个类型的值来使用。

```go
type Person struct {
    Name string
    Age  int
}
func (p Person) PrintName() {
    fmt.Println("Name:", p.Name)
}
func (p *Person) SetAge(age int) {
    p.Age = age
}

type Singer struct {
    Person // 通过内嵌Person类型来扩展之
    works  []string
}

func main() {
    var gaga = Singer{Person: Person{"Gaga", 30}}
    gaga.PrintName() // Name: Gaga
    gaga.Name = "Lady Gaga"
    (&gaga).SetAge(31)
    (&gaga).PrintName()   // Name: Lady Gaga
    fmt.Println(gaga.Age) // 31
}
```

### 选择器的缩写形式

如果一个选择器中的中部某项对应着一个内嵌字段，则此项可被省略掉。

```go
type A struct {
    x int
}
func (a A) MethodA() {}

type B struct {
    A
}
type C struct {
    B
}

func main() {
    var c C

    // 下面的赋值语句中的选择器都是相互等价的。
    _ = c.B.A.x
    _ = c.B.x
    _ = c.A.x
    _ = c.x // x被称为类型C的一个提升字段

    // 这下面的几个方法调用都是互相等价的。
    c.B.A.MethodA()
    c.B.MethodA()
    c.A.MethodA()
    c.MethodA()
}
```

### 选择器遮挡和碰撞

一个值x可能同时有多个最后一项相同的选择器，并且这些选择器的中间项均对应着一个内嵌字段。 对于这种情形（假设最后一项为y）：

- **只有深度最浅的一个完整形式的选择器**（并且最浅者只有一个）**可以被缩写为x.y**。 换句话说，x.y表示**深度最浅的一个选择器**。其它完整形式的选择器被此最浅者所**遮挡**（压制）。
- 如果有**多个完整形式的选择器同时拥有最浅深度**，则任何完整形式的选择器都**不能被缩写为x.y**。 我们称这些同时拥有最浅深度的完整形式的选择器发生了**碰撞**。

如果一个方法选择器被另一个方法选择器所遮挡，并且它们对应的方法原型是一致的，那么我们可以说第一个方法被第二个覆盖（overridden）了。

举个例子，假设`A`、`B`和`C`为三个定义的类型：

```go
type A struct {
    x string
}
func (A) y(int) bool {
    return false
}

type B struct {
    y bool
}
func (B) x(string) {}

type C struct {
    B
}
```

下面这段代码编译不通过，原因是选择器`v1.A.x`和`v1.B.x`发生了碰撞，结果导致它们都不能被缩写为`v1.x`。 同样的情况发生在选择器`v1.A.y`和`v1.B.y`身上。

```go
var v1 struct {
    A
    B
}

func f1() {
    _ = v1.x
    _ = v1.y
}
```

下面的代码编译没问题。选择器`v2.C.B.x`被另一个选择器`v2.A.x`遮挡了，所以`v2.x`实际上是选择器`v2.A.x`的缩写形式。 因为同样的原因，`v2.y`是选择器`v2.A.y`（而不是选择器`v2.C.B.y`）的缩写形式。

```go
var v2 struct {
    A
    C
}

func f2() {
    fmt.Printf("%T \n", v2.x) // string
    fmt.Printf("%T \n", v2.y) // func(int) bool
}
```

### 为内嵌了其它类型的结构体类型声明的隐式方法

假设结构体类型`S`内嵌了一个类型`T`，并且此内嵌是合法的，

- 对内嵌类型`T`的每一个方法，如果此方法对应的选择器既不和其它选择器碰撞也未被其它选择器遮挡，则编译器将会隐式地为结构体类型`S`声明一个同样原型的方法。 继而，编译器也将为指针类型`*S`隐式声明一个相应的方法。
- 对类型`*T`的每一个方法，如果此方法对应的选择器既不和其它选择器碰撞也未被其它选择器遮挡，则编译器将会隐式地为类型`*S`声明一个同样原型的方法。

在类型`*T`不可内嵌的情况下即`T`是一个指针或者接口类型时，如果即`T`是一个指针或者接口类型时，则类型`*T`的方法集为空。

简单说来，如果没有发生选择器碰撞和遮挡，

- 类型`struct{T}`和`*struct{T}`将获取类型T的所有方法。
- 类型`*struct{T}`、`struct{*T}`和`*struct{*T}`将获取类型`*T`的所有方法。

如果一个结构体类型内嵌了一个实现了一个接口类型的类型（此内嵌类型可以是此接口类型自己），则一般说来，此结构体类型也实现了此接口类型，除非发生了选择器碰撞和遮挡。

一个类型将只会获取它（直接或者间接）内嵌了的类型的方法。

## 非类型安全指针

Go也支持限制较少的非类型安全指针。 非类型安全指针和C指针类似，它们都很强大，但同时也都很危险。 在某些情形下，通过非类型安全指针的帮助，我们可以写出效率更高的代码； 但另一方面，使用非类型安全指针也导致我们可能轻易地写出潜在的不安全的代码，这些潜在的不安全点很难在它们产生危害之前被及时发现。

### 关于unsafe标准库包

非类型安全指针在Go中为一种特别的类型。 我们必须引入unsafe标准库包来使用非类型安全指针。 非类型安全指针unsafe.Pointer被声明定义为：

`type Pointer *ArbitraryType`

这里的`ArbitraryType`仅仅是暗示`unsafe.Pointer`类型值可以被转换为任意类型安全指针（反之亦然）。 换句话说，`unsafe.Pointer`类似于C语言中的`void*`。

unsafe标准库包提供了三个函数：

- `func Alignof(variable ArbitraryType) uintptr`。 此函数用来取得一个值在内存中的**地址对齐保证**（address alignment guarantee）。 注意，同一个类型的值做为结构体字段和非结构体字段时地址对齐保证可能是不同的。 当然，这和具体编译器的实现有关。对于目前的标准编译器，同一个类型的值做为结构体字段和非结构体字段时的地址对齐保证总是相同的。 gccgo编译器对这两种情形是区别对待的。
- `func Offsetof(selector ArbitraryType) uintptr`。 此函数用来取得一个结构体值的某个字段的地址**相对于此结构体值的地址的偏移**。 在一个程序中，对于同一个结构体类型的不同值的对应相同字段，此函数的返回值总是相同的。
- `func Sizeof(variable ArbitraryType) uintptr`。 此函数用来**取得一个值的尺寸**（亦即此值的类型的尺寸）。 在一个程序中，对于同一个类型的不同值，此函数的返回值总是相同的。

```go
func main() {
    var x struct {
        a int64
        b bool
        c string
    }
    const M, N = unsafe.Sizeof(x.c), unsafe.Sizeof(x)
    fmt.Println(M, N) // 16 32

    fmt.Println(unsafe.Alignof(x.a)) // 8
    fmt.Println(unsafe.Alignof(x.b)) // 1
    fmt.Println(unsafe.Alignof(x.c)) // 8

    fmt.Println(unsafe.Offsetof(x.a)) // 0
    fmt.Println(unsafe.Offsetof(x.b)) // 8
    fmt.Println(unsafe.Offsetof(x.c)) // 16
}
```

### 非类型安全指针相关的类型转换

- 一个类型安全指针值可以被显式转换为一个非类型安全指针类型，反之亦然。
- 一个uintptr值可以被显式转换为一个非类型安全指针类型，反之亦然。 但是，注意，一个nil非类型安全指针类型不应该被转换为uintptr并进行算术运算后再转换回来。

### 与指针相关的一此事实

#### 事实一：非类型安全指针值是指针但uintptr值是整数

每一个非零安全或者不安全指针值均引用着另一个值。但是一个uintptr值并不引用任何值，它被看作是一个整数，尽管常常它存储的是一个地址的数字表示。

Go是一门支持垃圾回收的语言。 当一个Go程序在运行中，Go运行时（runtime）将不时地检查哪些内存块将不再被程序中的任何仍在使用中的值所引用并且回收这些内存块。值与值之间和内存块与值之间的引用关系是通过指针来表征的。

#### 事实二：不再被使用的内存块的回收时间点是不确定的

在运行时刻，一次新的垃圾回收过程可能在一个不确定的时间启动，并且此过程可能需要一段不确定的时长才能完成。 所以一个不再被使用的内存块的回收时间点是不确定的。

```go
func createInt() *int {
    return new(int)
}

func foo() {
    p0, y, z := createInt(), createInt(), createInt()
    var p1 = unsafe.Pointer(y) // 和y一样引用着同一个值
    var p2 = uintptr(unsafe.Pointer(z))

    // 此时，即使z指针值所引用的int值的地址仍旧存储在p2值中，但是此
    // int值已经不再被使用了，所以垃圾回收器认为可以回收它所占据的
    // 内存块了。另一方面，p0和p1各自所引用的int值仍旧将在下面被使用。

    // uintptr值可以参与算术运算。
    p2 += 2; p2--; p2--

    *p0 = 1                          // okay
    *(*int)(p1) = 2                  // okay
    *(*int)(unsafe.Pointer(p2))) = 3 // 危险操作！
}
```

值p2仍旧在使用这个事实并不能保证曾经被z指针值所引用的int值所占的内存块一定还没有被回收。 换句话说，当*(*T)(unsafe.Pointer(p2))) = 3被执行的时候，此内存块有可能已经被回收了。 所以，继续通过解引用值p2中存储的地址是非常危险的，因为此内存块可能已经被重新分配给其它值使用了。

#### 事实三：我们可以将一个值的指针传递给`runtime.KeepAlive`函数调用来确保此值在此调用之前仍然处于被使用中

为了确保一个值部和它所引用着的值部仍然被认为在使用中，我们应该将引用着此值的另一个值传给一个`runtime.KeepAlive`函数调用。 在实践中，我们常常将此值的指针传递给一个`runtime.KeepAlive`函数调用。

通过在上一小节的例子中的最后添加一个`runtime.KeepAlive(z)`调用， `*(*int)(unsafe.Pointer(p2))) = 3`可以被安全地执行了。

#### 事实四：一个值的可被使用范围可能并没有代码中看上去的大

```go
type T struct {
    x int
    y *[1<<23]byte
}

func bar() {
    t := T{y: new([1<<23]byte)}
    p := uintptr(unsafe.Pointer(&t.y[0]))

    ... // 使用t.x和t.y

    // 一个聪明的编译器能够觉察到值t.y将不会再被用到，
    // 所以认为t.y值所占的内存块可以被回收了。

    *(*byte)(unsafe.Pointer(p))) = 1 // 危险操作！

    println(t.x) // ok。继续使用值t，但只使用t.x字段。
}
```

#### 事实五：`*unsafe.Pointer`是一个类型安全指针类型

类型*unsafe.Pointer是一个类型安全指针类型。 它的基类型为unsafe.Pointer。 既然它是一个类型安全指针类型，根据上面列出的类型转换规则，它的值可以转换为类型unsafe.Pointer，反之亦然。

```go
func main() {
    x := 123                // 类型为int
    p := unsafe.Pointer(&x) // 类型为unsafe.Pointer
    pp := &p                // 类型为*unsafe.Pointer
    p = unsafe.Pointer(pp)
    pp = (*unsafe.Pointer)(p)
}
```

### 如何正确地使用非类型安全指针？

#### 使用模式一：将类型`*T1`的一个值转换为非类型安全指针值，然后将此非类型安全指针值转换为类型`*T2`。

只有在`T1`的尺寸不大于`T2`并且此转换具有实际意义的时候才应该实施这样的转换。

```go
func Float64bits(f float64) uint64 {
    return *(*uint64)(unsafe.Pointer(&f))
}

func Float64frombits(b uint64) float64 {
    return *(*float64)(unsafe.Pointer(&b))
}
```

```go
func main() {
    type MyString string
    ms := []MyString{"C", "C++", "Go"}
    fmt.Printf("%s\n", ms)  // [C C++ Go]
    // ss := ([]string)(ms) // 编译错误
    ss := *(*[]string)(unsafe.Pointer(&ms))
    ss[1] = "Rust"
    fmt.Printf("%s\n", ms) // [C Rust Go]
    // ms = []MyString(ss) // 编译错误
    ms = *(*[]MyString)(unsafe.Pointer(&ss))
}
```

#### 使用模式二：将一个非类型安全指针值转换为一个uintptr值，然后使用此uintptr值。

一般我们将最终的转换结果uintptr值输出到日志中用来调试

```go
func main() {
    type T struct{a int}
    var t T
    fmt.Println(&t)                                 // &{0}
    fmt.Printf("%x\n", uintptr(unsafe.Pointer(&t))) // c6233120a8
    println(&t)                                     // 0xc6233120a8
}
```

#### 使用模式三：将一个非类型安全指针转换为一个uintptr值，然后此uintptr值参与各种算术运算，再将算术运算的结果uintptr值转回非类型安全指针。

```go
type T struct {
    x bool
    y [3]int16
}

const N = unsafe.Offsetof(T{}.y)
const M = unsafe.Sizeof([3]int16{}[0])

func main() {
    t := T{y: [3]int16{123, 456, 789}}
    p := unsafe.Pointer(&t)
    // "uintptr(p) + N + M + M"为t.y[2]的内存地址。
    ty2 := (*int16)(unsafe.Pointer(uintptr(p)+N+M+M))
    fmt.Println(*ty2) // 789
}
```

注意：在上面这个例子中，转换unsafe.Pointer(uintptr(p) + N + M + M)不应该被拆成两行

```go
func main() {
    t := T{y: [3]int16{123, 456, 789}}
    p := unsafe.Pointer(&t)
    // ty2 := (*int16)(unsafe.Pointer(uintptr(p)+N+M+M))
    addr := uintptr(p) + N + M + M
    // 从这里到下一行代码执行之前，t值将不再被任何值引用，所以
    // 垃圾回收器认为它可以被回收了。一旦它真得被回收了，下面
    // 继续使用t.y[2]值的曾经的地址是非法和危险的！
    ty2 := (*int16)(unsafe.Pointer(addr))
    fmt.Println(*ty2)
}
```

如果我们确实希望将上面提到的转换拆成两行，我们应该在拆分后的两行后添加一条`runtime.KeepAlive`函数调用并将（直接或间接）引用着`t.y[2]`值的一个值传递给此调用做为实参。

```go
func main() {
    t := T{y: [3]int16{123, 456, 789}}
    p := unsafe.Pointer(t)
    addr := uintptr(p) + N + M + M
    ty2 := (*int16)(unsafe.Pointer(addr))
    // 下面这条调用将确保整个t值的内存在此时刻不会被回收。
    runtime.KeepAlive(p)
    fmt.Println(*ty2)
}
```

#### 使用模式四：将非类型安全指针值转换为`uintptr`值并传递给`syscall.Syscall`函数调用。

函数本身不能保证传递进来的地址处的内存块一定没有被回收。 如果此内存块已经被回收了或者被重新分配给了其它值，那么此函数内部的操作将是非法和危险的。

然而，syscall标准库包中的Syscall函数的原型为：

`func Syscall(trap, a1, a2, a3 uintptr) (r1, r2 uintptr, err Errno)`

我们可以认为编译器在每个syscall.Syscall函数调用后面为在此调用中的每个被转换为uintptr类型的非类型安全指针实参添加了一条runtime.KeepAlive调用，从而确保被此非类型安全指针实参引用着的值在此syscall.Syscall函数调用中不会被垃圾回收掉

```go
u := uintptr(unsafe.Pointer(p))
// 被p所引用着的值在此时有可能会被回收掉。
syscall.Syscall(SYS_READ, uintptr(fd), u, uintptr(n))
// 这里编译器不会自动添加runtime.KeepAlive调用。
```

#### 使用模式五：将`reflect.Value.Pointer`或者`reflect.Value.UnsafeAddr`方法的`uintptr`返回值转换为非类型安全指针。

reflect标准库包中的Value类型的Pointer和UnsafeAddr方法都返回一个uintptr值。

这样的设计需要我们将这两个方法的调用的uintptr结果立即转换为非类型安全指针。 否则，将出现一个短暂的可能导致处于返回的地址处的内存块被回收掉的时间窗。 此时间窗是如此短暂以至于此内存块被回收掉的几率非常之低，因而这样的编程错误造成的bug的重现几率亦十分得低。

比如，下面这个调用是安全的：

```go
p := (*int)(unsafe.Pointer(reflect.ValueOf(new(int)).Pointer()))
```

而下面这个调用是危险的：

```go
u := reflect.ValueOf(new(int)).Pointer()
// 在这个时刻，处于存储在u中的地址处的内存块可能会被回收掉。
p := (*int)(unsafe.Pointer(u))
```

#### 使用模式六：将一个`reflect.SliceHeader`或者`reflect.StringHeader`值的`Data`字段转换为非类型安全指针，以及其逆转换。

`reflect`标准库包中的`SliceHeader`和`StringHeader`类型的`Data`字段的类型被指定为`uintptr`，而不是`unsafe.Pointer`。

我们可以将一个字符串的指针值转换为一个`*reflect.StringHeader`指针值，从而可以对此字符串的内部进行修改。类似地，我们可以将一个切片的指针值转换为一个`*reflect.SliceHeader`指针值，从而可以对此切片的内部进行修改。

```go
func main() {
    a := [...]byte{'G', 'o', 'l', 'a', 'n', 'g'}
    s := "Java"
    hdr := (*reflect.StringHeader)(unsafe.Pointer(&s))
    hdr.Data = uintptr(unsafe.Pointer(&a))
    hdr.Len = len(a)
    fmt.Println(s) // Golang
    // 现在，字符串s和切片a共享着底层的byte字节序列，
    // 从而使得此字符串中的字节变得可以修改。
    a[2], a[3], a[4], a[5] = 'o', 'g', 'l', 'e'
    fmt.Println(s) // Google
}
```

```go
func main() {
    a := [6]byte{'G', 'o', '1', '0', '1'}
    bs := []byte("Golang")
    hdr := (*reflect.SliceHeader)(unsafe.Pointer(&bs))
    hdr.Data = uintptr(unsafe.Pointer(&a))
    runtime.KeepAlive(&a) // 必不可少！
    hdr.Len = 2
    hdr.Cap = len(a)
    fmt.Printf("%s\n", bs) // Go
    bs = bs[:cap(bs)]
    fmt.Printf("%s\n", bs) // Go101
}
```

```go
func String2ByteSlice(str string) (bs []byte) {
    strHdr := (*reflect.StringHeader)(unsafe.Pointer(&str))
    sliceHdr := (*reflect.SliceHeader)(unsafe.Pointer(&bs))
    sliceHdr.Data = strHdr.Data
    sliceHdr.Len = strHdr.Len
    sliceHdr.Cap = strHdr.Len
    // 下面的KeepAlive是必要的。
    runtime.KeepAlive(&str)
    return
}

func main() {
    str := strings.Join([]string{"Go", "land"}, "")
    s := String2ByteSlice(str)
    fmt.Printf("%s\n", s) // Goland
    s[5] = 'g'
    fmt.Println(str) // Golang
}
```

### 非类型安全指针总结

对于某些情形，非类型安全机制可以帮助我们写出运行效率更高的代码。 但是，使用非类型安全指针也使得我们可能轻易地写出一些重现几率非常低的微妙的bug。 一个含有这样的bug的程序很可能在很长一段时间内都运行正常，但是突然变得不正常甚至崩溃。 这样的bug很难发现和调试。

我们只应该在不得不使用非类型安全机制的时候才使用它们。 特别地，当我们使用非类型安全机制时，请务必遵循上面列出的使用模式。

## 内置范型

Go语言目前不支持自定义范型，只支持一等公民组合类型的内值范型。 我们可以用各种一等公民组合类型来组合出无穷个类型。

### 一些自定义组合类型的例子

`[3][4]int`

当解读一个类型的字面形式时，我们应该从**左到右进行解读**。 左边开头的`[3]`表示着这个类型为一个数组类型，它右边的整个部分为它的元素类型。 对于这个例子，它的元素类型为另外一个数组类型`[4]int`。 此另外一个数组类型的元素类型为为内值类型`int`。 第一个数组类型可以被看作是一个二维数组类型。

```go
func main() {
    matrix := [3][4]int{
        {1, 0, 0, 1},
        {0, 1, 0, 1},
        {0, 0, 1, 1},
    }

    matrix[1][1] = 3
    a := matrix[1] // 变量a的类型为[4]int
    fmt.Println(a) // [0 3 0 1]
}
```

- `[][]string`是一个元素类型为另一个切片类型`[]string`的切片类型。
- `**bool`是一个基类型为另一个指针类型`*bool`的指针类型。
- `chan chan int`是一个元素类型为另一个数据通道类型的`chan int`的数据通道类型。
- `map[int]map[int]string`是一个元素类型为另一个映射类型`map[string]int`的映射类型。 这两个映射类型的键值类型均为内置类型`int`。
- `func(int32) func(int32)`是一个只有一个输入参数和一个返回值的函数类型，此返回值的类型为一个只有一个输入参数的函数类型。 这两个函数类型的输入参数的类型均为内置类型`int32`。
- `chan *[16]byte` 最左边的`chan`关键字表明此类型是一个数据通道类型。 `chan`关键字右边的整个部分`*[16]byte`表示此数据通道类型的元素类型，此元素类型是一个指针类型。 此指针类型的基类型为`*`右边的整个部分：`[16]byte`，此基类型为一个数组类型。 此数组类型的元素类型为内置类型`byte`。

```go
func main() {
    c := make(chan *[16]byte)

    go func() {
        // 使用两个数组以避免数据竞争。
        var dataA, dataB = new([16]byte), new([16]byte)
        for {
            _, err := rand.Read(dataA[:])
            if err != nil {
                close(c)
            } else {
                c <- dataA
                dataA, dataB = dataB, dataA
            }
        }
    }()

    for data := range c {
        fmt.Println((*data)[:])
        time.Sleep(time.Second / 2)
    }
}
```

- `map[string][]func(int) int`为一个映射类型。 此映射类型的键值类型为内值类型`string`，右边剩余的部分为此映射类型的元素类型。 `[]`表明此映射的元素类型为一个切片类型，此切片类型的元素类型为一个函数类型`func(int) int`

```go
func main() {
    addone := func(x int) int {return x + 1}
    square := func(x int) int {return x * x}
    double := func(x int) int {return x + x}

    transforms := map[string][]func(int) int {
        "inc,inc,inc": {addone, addone, addone},
        "sqr,inc,dbl": {square, addone, double},
        "dbl,sqr,sqr": {double, double, square},
    }

    for _, n := range []int{2, 3, 5, 7} {
        fmt.Println(">>>", n)
        for name, transfers := range transforms {
            result := n
            for _, xfer := range transfers {
                result = xfer(result)
            }
            fmt.Printf(" %v: %v \n", name, result)
        }
    }
```

```go
[]map[struct {
    a int
    b struct {
        x string
        y bool
    }
}]interface {
    Build([]byte, struct {x string; y bool}) error
    Update(dt float64)
    Destroy()
}
```

```go
type B = struct {
    x string
    y bool
}

type K = struct {
    a int
    b B
}

type E = interface {
    Build([]byte, B) error
    Update(dt float64)
    Destroy()
}

type T = []map[K]E
```

## 反射

### 反射概述

通过`reflect`库包中`Type`和`Value`两个类型提供的功能来观察不同的Go值。

Go反射机制设计的目标之一是任何非反射操作都可以通过反射机制来完成。此目标目前（Go 1.12）并没有得到100%的实现。 但是，目前大部分的非反射操作都可以通过反射机制来完成。

### `reflect.Type`类型和值

通过调用`reflect.TypeOf`函数，我们可以从一个任何非接口类型的值创建一个`reflect.Type`值。 此`reflect.Type`值表示着此非接口值的类型。通过此值，我们可以得到很多此非接口类型的信息。

也可以将一个*接口*值传递给一个`reflect.TypeOf`函数调用，但是此调用将返回一个表示着此*接口值的动态类型*的`reflect.Type`值。

类型reflect.Type为一个接口类型，它指定了若干方法。 通过这些方法，我们能够观察到一个reflect.Type值所表示的Go类型的各种信息。这些方法中的有的适用于所有种类的类型，有的只适用于一种或几种类型。 通过不合适的reflect.Type属主值调用某个方法将在运行时产生一个恐慌。

```go
func main() {
    type A = [16]int16
    var c <-chan map[A][]byte
    tc := reflect.TypeOf(c)
    fmt.Println(tc.Kind())    // chan
    fmt.Println(tc.ChanDir()) // <-chan
    tm := tc.Elem()
    ta, tb := tm.Key(), tm.Elem()
    fmt.Println(tm.Kind(), ta.Kind(), tb.Kind()) // map array slice
    tx, ty := ta.Elem(), tb.Elem()

    // byte是uint8类型的别名。
    fmt.Println(tx.Kind(), ty.Kind()) // int16 uint8
    fmt.Println(tx.Bits(), ty.Bits()) // 16 8
    fmt.Println(tx.ConvertibleTo(ty)) // true
    fmt.Println(tb.ConvertibleTo(ta)) // false

    // 切片类型和映射类型都是不可比较类型。
    fmt.Println(tb.Comparable()) // false
    fmt.Println(tm.Comparable()) // false
    fmt.Println(ta.Comparable()) // true
    fmt.Println(tc.Comparable()) // true
}
```

在上面这个例子中，我们使用方法Elem来得到某些类型的元素类型。 实际上，此方法也可以用来得到一个指针类型的基类型。

```go
type T []interface{m()}
func (T) m() {}

func main() {
    tp := reflect.TypeOf(new(interface{}))
    tt := reflect.TypeOf(T{})
    fmt.Println(tp.Kind(), tt.Kind()) // ptr slice

    // 使用间接的方法得到表示两个接口类型的reflect.Type值。
    ti, tim := tp.Elem(), tt.Elem()
    fmt.Println(ti.Kind(), tim.Kind()) // interface interface

    fmt.Println(tt.Implements(tim))  // true
    fmt.Println(tp.Implements(tim))  // false
    fmt.Println(tim.Implements(tim)) // true

    // 所有的类型都实现了任何空接口类型。
    fmt.Println(tp.Implements(ti))  // true
    fmt.Println(tt.Implements(ti))  // true
    fmt.Println(tim.Implements(ti)) // true
    fmt.Println(ti.Implements(ti))  // true
}
```

通过反射列出一个函数类型的各个输入参数和返回结果类型

```go
type F func(string, int) bool
func (f F) Validate(s string) bool {
    return f(s, 32)
}

func main() {
    var x struct {
        n int
        f F
    }
    tx := reflect.TypeOf(x)
    fmt.Println(tx.Kind())     // struct
    fmt.Println(tx.NumField()) // 2
    tf := tx.Field(1).Type
    fmt.Println(tf.Kind())               // func
    fmt.Println(tf.IsVariadic())         // false
    fmt.Println(tf.NumIn(), tf.NumOut()) // 2 1
    fmt.Println(tf.NumMethod())          // 1
    ts, ti, tb := tf.In(0), tf.In(1), tf.Out(0)
    fmt.Println(ts.Kind(), ti.Kind(), tb.Kind()) // string int bool
}
```

动态地创建出来一些非定义组合类型

```go
func main() {
    ta := reflect.ArrayOf(5, reflect.TypeOf(123))
    fmt.Println(ta) // [5]int
    tc := reflect.ChanOf(reflect.SendDir, ta)
    fmt.Println(tc) // chan<- [5]int
    tp := reflect.PtrTo(ta)
    fmt.Println(tp) // *[5]int
    ts := reflect.SliceOf(tp)
    fmt.Println(ts) // []*[5]int
    tm := reflect.MapOf(ta, tc)
    fmt.Println(tm) // map[[5]int]chan<- [5]int
    tf := reflect.FuncOf([]reflect.Type{ta},
                []reflect.Type{tp, tc}, false)
    fmt.Println(tf) // func([5]int) (*[5]int, chan<- [5]int)
    tt := reflect.StructOf([]reflect.StructField{
        {Name: "Age", Type: reflect.TypeOf("abc")},
    })
    fmt.Println(tt)            // struct { Age string }
    fmt.Println(tt.NumField()) // 1
}
```

### `reflect.Value`类型和值

我们可以通过调用reflect.ValueOf函数，从一个非接口类型的值创建一个reflect.Value值。 此reflect.Value值代表着此非接口值。 和reflect.TypeOf函数类似，`reflect.ValueOf`函数也只有一个`interface{}`类型的参数。 当我们将一个接口值传递给一个`reflect.ValueOf`函数调用时，此调用返回的是代表着此接口值的动态值的一个`reflect.Value`值。 我们必须通过间接的途径获得一个代表一个接口值的`reflect.Value`值。

一个`reflect.Value`值的`CanSet`方法将返回此reflect.Value值代表的Go值是否可以被修改（可以被赋值）。 如果一个Go值可以被修改，则我们可以调用对应的`reflect.Value`值的`Set`方法来修改此Go值。 注意：`reflect.ValueOf`函数直接返回的`reflect.Value`值都是不可修改的。

```go
func main() {
    n := 123
    p := &n
    vp := reflect.ValueOf(p)
    fmt.Println(vp.CanSet(), vp.CanAddr()) // false false
    vn := vp.Elem() // 取得vp代表的指针引用的值的代表值
    fmt.Println(vn.CanSet(), vn.CanAddr()) // true true
    vn.Set(reflect.ValueOf(789)) // <=> vn.SetInt(789)
    fmt.Println(n)               // 789
}
```

一个结构体值的非导出字段不能通过反射来修改

```go
func main() {
    var s struct {
        X interface{} // 一个导出字段
        y interface{} // 一个非导出字段
    }
    vp := reflect.ValueOf(&s)
    // 如果vp代表着一个指针，下一行等价于"vs := vp.Elem()"。
    vs := reflect.Indirect(vp)
    // vx和vy都各自代表着一个接口值。
    vx, vy := vs.Field(0), vs.Field(1)
    fmt.Println(vx.CanSet(), vx.CanAddr()) // true true
    // vy is addressable but not modifiable.
    fmt.Println(vy.CanSet(), vy.CanAddr()) // false true
    vb := reflect.ValueOf(123)
    vx.Set(vb)     // okay, 因为vx代表的值是修改的。
    // vy.Set(vb)  // 会造成恐慌，因为vy代表的值是不可修改的。
    fmt.Println(s) // {123 <nil>}
    fmt.Println(vx.IsNil(), vy.IsNil()) // false true
}
```

从上两例中，我们可以得知有两种方法获取一个代表着一个指针所引用着的值的`reflect.Value`值：

1. 通过调用代表着被此指针值的`reflect.Value`值的`Elem`方法。
2. 将代表着被此指针值的`reflect.Value`值的传递给一个`reflect.Indirect`函数调用。 （如果传递给一个`reflect.Indirect`函数调用的实参*不代表着一个指针值，则此调用返回此实参的一个复制*。）

`reflect.Value.Elem`方法也可以用来获取一个代表着一个接口值的动态值的`reflect.Value`值

```go
func main() {
    var z = 123
    var y = &z
    var x interface{} = y
    v := reflect.ValueOf(&x)
    vx := v.Elem()
    vy := vx.Elem()
    vz := vy.Elem()
    vz.Set(reflect.ValueOf(789))
    fmt.Println(z) // 789
}
```

reflect标准库包中也提供了一些对应着内置函数或者各种非反射功能的函数。

```go
func InvertSlice(args []reflect.Value) (result []reflect.Value) {
    inSlice, n := args[0], args[0].Len()
    outSlice := reflect.MakeSlice(inSlice.Type(), 0, n)
    for i := n-1; i >= 0; i-- {
        element := inSlice.Index(i)
        outSlice = reflect.Append(outSlice, element)
    }
    return []reflect.Value{outSlice}
}

func Bind(p interface{}, f func ([]reflect.Value) []reflect.Value) {
    // invert代表着一个函数值。
    invert := reflect.ValueOf(p).Elem()
    invert.Set(reflect.MakeFunc(invert.Type(), f))
}

func main() {
    var invertInts func([]int) []int
    Bind(&invertInts, InvertSlice)
    fmt.Println(invertInts([]int{2, 3, 5})) // [5 3 2]

    var invertStrs func([]string) []string
    Bind(&invertStrs, InvertSlice)
    fmt.Println(invertStrs([]string{"Go", "C"})) // [C Go]
}
```

如果一个`reflect.Value`值代表着一个函数值，则我们可以调用此`reflect.Value`值的`Call`方法来调用此函数。 每个`Call`方法调用接受一个`[]reflect.Value`类型的参数（表示传递给相应函数调用的各个实参）并返回一个同类型结果。

```go
    var square = func(a int) int {return a * a }
    var vsq = reflect.ValueOf(square)
    res := vsq.Call([]reflect.Value{reflect.ValueOf(3)})
    fmt.Println(reflect.TypeOf(res))
    fmt.Println(res)
    fmt.Println(res[0])
```

```go
type T struct {
    A, b int
}

func (t T) AddSubThenScale(n int) (int, int) {
    return n * (t.A + t.b), n * (t.A - t.b)
}

func main() {
    t := T{5, 2}
    vt := reflect.ValueOf(t)
    vm := vt.MethodByName("AddSubThenScale")
    results := vm.Call([]reflect.Value{reflect.ValueOf(3)})
    fmt.Println(results[0].Int(), results[1].Int()) // 21 9

    neg := func(x int) int {
        return -x
    }
    vf := reflect.ValueOf(neg)
    fmt.Println(vf.Call(results[:1])[0].Int()) // -21
    fmt.Println(vf.Call([]reflect.Value{
        vt.FieldByName("A"), // 如果是字段b，则造成恐慌
    })[0].Int()) // -5
}
```

映射反射值

```go
func main() {
    valueOf := reflect.ValueOf
    m := map[string]int{"Unix": 1973, "Windows": 1985}
    v := valueOf(m)
    // 第二个实参为Value零值时，表示删除一个映射条目。
    v.SetMapIndex(valueOf("Windows"), reflect.Value{})
    v.SetMapIndex(valueOf("Linux"), valueOf(1991))
    for i := v.MapRange(); i.Next(); {
        fmt.Println(i.Key(), "\t:", i.Value())
    }
}
```

数据通道反射值

```go
func main() {
    c := make(chan string, 2)
    vc := reflect.ValueOf(c)
    vc.Send(reflect.ValueOf("C"))
    succeeded := vc.TrySend(reflect.ValueOf("Go"))
    fmt.Println(succeeded) // true
    succeeded = vc.TrySend(reflect.ValueOf("C++"))
    fmt.Println(succeeded) // false
    fmt.Println(vc.Len(), vc.Cap()) // 2 2
    vs, succeeded := vc.TryRecv()
    fmt.Println(vs.String(), succeeded) // C true
    vs, sentBeforeClosed := vc.Recv()
    fmt.Println(vs.String(), sentBeforeClosed) // Go false
    vs, succeeded = vc.TryRecv()
    fmt.Println(vs.String()) // <invalid Value>
    fmt.Println(succeeded)   // false
}
```

`reflect.Value`类型的`TrySend`和`TryRecv`方法对应着只有一个`case`分支和一个`default`分支的`select`流程控制代码块。

`reflect.Select`函数在运行时刻来模拟具有不定`case`分支数量的`select`流程控制代码块

```go
func main() {
    c := make(chan int, 1)
    vc := reflect.ValueOf(c)
    succeeded := vc.TrySend(reflect.ValueOf(123))
    fmt.Println(succeeded, vc.Len(), vc.Cap()) // true 1 1

    vSend, vZero := reflect.ValueOf(789), reflect.Value{}
    branches := []reflect.SelectCase{
        {Dir: reflect.SelectDefault, Chan: vZero, Send: vZero},
        {Dir: reflect.SelectRecv, Chan: vc, Send: vZero},
        {Dir: reflect.SelectSend, Chan: vc, Send: vSend},
    }
    selIndex, vRecv, closed := reflect.Select(branches)
    fmt.Println(selIndex)    // 1
    fmt.Println(closed)      // true
    fmt.Println(vRecv.Int()) // 123
    vc.Close()
    // 再模拟select流程控制代码块。因为vc已经关闭了，
    // 所以需将最后一个case分支去除，否则它可能会造成一个恐慌。
    selIndex, _, closed = reflect.Select(branches[:2])
    fmt.Println(selIndex, closed) // 1 false
}
```

一些`reflect.Value`值可能表示着不合法的Go值。

```go
func main() {
    var z reflect.Value // 一个reflect.Value零值
    fmt.Println(z)      // <invalid reflect.Value>
    v := reflect.ValueOf((*int)(nil)).Elem()
    fmt.Println(v)      // <invalid reflect.Value>
    fmt.Println(v == z) // true
    var i = reflect.ValueOf([]interface{}{nil}).Index(0)
    fmt.Println(i)             // <nil>
    fmt.Println(i.Elem())      // <invalid reflect.Value>
    fmt.Println(i.Elem() == z) // true
}
```

`reflect.Value`类型的零值代表着一个不合法的Go值

使用空接口interface{}值做为中介，一个Go值可以转换为一个reflect.Value值。 逆过程类似，通过调用一个`reflect.Value`值的`Interface`方法得到一个`interface{}`值，然后将此`interface{}`断言为原来的Go值。

```go
func main() {
    vx := reflect.ValueOf(123)
    vy := reflect.ValueOf("abc")
    vz := reflect.ValueOf([]bool{false, true})

    x := vx.Interface().(int)
    y := vy.Interface().(string)
    z := vz.Interface().([]bool)
    fmt.Println(x, y, z) // 123 abc [false true]
}
```