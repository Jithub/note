# 4.1 数组
C++11的列表初始化：
```c++
double earnings[4] {1.0, 2.0, 3.0, 4.0}; //可以省略等于号
unsigned int counts[10] {}; //可不包含任何东西，初始化为0
//列表初始化禁止缩窄转换
```
<br><br>

# 4.2 字符串
C风格的字符串的特殊性质：以空字符null character来标记结尾
<br><br>

# 4.3 string类简介
ISO/ANSI C++98标准通过添加string类扩展了C++库

未被初始化的string类对象长度为0

新的char类型对应的数组和字符串字面值：
```c++
wchar_t title[] = L"Chief Astrogator";
char16_t name[] = u"Felonia Ripova";
char32_t car[] = U"Humber Super Snipe";
```
原始字符串：使用 "( 和 )" 作为定界符，使用R作为前缀来进行标识；定界符可以自定义
```c++
cout << R"(whatever inside will be printed directly)";
```
<br><br>

# 4.3 结构简介
C++允许在声明结构变量时省略关键字struct
```c++
struct inflatable
{
    char name[20];
    float volume;
    double price;
};
struct inflatable goose; // C
inflatable vincent;      // C++
```
可以使用赋值运算符=将结构赋给另一个同类型的结构，这种赋值称为成员赋值。
<br><br>

# 4.5 共用体
```c++
union one4all
{
    int int_val;
    long long_val;
    double double_val;
};
one4all pail;
```
可以使用pail来存储int、long或double，只能存一个。共用体的长度为其最大成员的长度。

可以去掉上述的one4all，成为匿名共用体。P95的例子很清楚

常用于节省内存、操作系统数据结构或硬件数据结构
<br><br>

# 4.6 枚举
```c++
enum spectrum
{
    red,
    orange,
    yellow,
    green,
    blue,
    violet,
    indigo,
    ultraviolet
};
```
在不进行强制类型转换的情况下，只能将定义枚举时使用的枚举量赋给这种枚举的变量：
```c++
spectrum band;
band = blue; //valid
band = 2000; //invalid
```
对于枚举，只定义了赋值运算符，没有算术运算符
```c++
band = orange;       // valid
band++;              //invalid
band = orange + red; //invalid，后者可以加，但是得到的结果为int，不能赋给枚举类型
```
枚举量是整型，可被提升为int，但int不能自动转换为枚举类型

## 设置枚举的值
必须是整数；  
第一个值默认为0；  
最后面没有初始化的量将比前面的加1；  
可以创建多个值相同的枚举量；

## 枚举的取值范围
每个枚举都有取值范围range，通过强制类型转换，可以将取值范围中的任何整数值赋给枚举变量，即使这个值不是枚举值：
```c++
enum bits {one = 1, two = 2, eight = 8};
bits myflag = bits(6); //valid
```
取值范围的定义，不看了。

选择用多少空间来存储枚举由编译器决定。
<br><br>

# 4.7 指针和自由存储空间
**P98的指针与OOP基本原理：**  
*OOP相比传统的过程性编程，更强调在运行阶段（而不是编译阶段）进行决策。例如，内存分配。*

*运算符被称为间接值（indirect value）或解除引用（dereferencing）运算符。

指针和数组名之间的根本差别：  
不能修改数组名的值。但指针是变量，可以修改它的值。比如`p3 = p3 + 1;`  
<br><br>

# 4.8 指针、数组和指针算术
指针和数组基本等价的原因在于指针算术和C++内部处理数组的方式。

C++将数组名解释为地址。对于数组表达式`stack[1]`，C++编译器将其看作是`*(stack + 1)`

多数情况下数组名被解释为数组第一个元素的地址，也有例外：  
对数组名使用sizeof时得到的是数组的长度  
```c++
short tell[20];
cout << tell << endl;  //打印&tell[0]，一个2字节内存块的地址
cout << &tell << endl; //打印整个数组（一个20个字节内存块）的地址
short (*pas)[20] = &tell; //pas的类型为short(*)[20]
```

*在cout和多数C++表达式中，char数组名、char指针以及用双引号括起的字符串常量都被解释为字符串第一个字符的地址。*

C++不能保证字符串字面值被唯一地存储。也就是说，如果在程序中多次使用“wren”，则编译器可能存储该字符串的多个副本，也可能只存储一个副本。

