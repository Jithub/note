ANSI C（C99）只保证名称中前63个字符有意义。

C++提供一套整型的标准：
- short至少16位
- int至少与short一样长
- long至少32位，且至少与int一样长
- long long至少64位，且至少与long一样长

头文件climits包含了关于整型限制的信息。具体地说它定义了各种限制的符号名称，例如INT_MAX为int的最大取值，SHRT_MAX为short的最大取值，CHAR_BIT为字节的位数。

sizeof为运算符，对类型名使用时应将类型名的名称放在括号中，但是变量名则为可选：`sizeof(int); sizeof n_short;`

**表 3.1 climits中的符号常量**

C++独特于C的初始化语法：
```c++
int wrens(432);
```
C++11初始化方式：
```c++
int hamburgers = {24};
int emus{7};
int rocs = {}; // init to 0
int psychics{}; // init to 0
```
C++11使得可将大括号初始化用于任何类型。

C++使用前一到两位来标识数字常量的基数。第一位为1-9则为十进制decimal，第一位是0而第二位是1-7则为八进制octal，前两位为0x或0X则为十六进制hex。

iostream提供控制符dec、hex和oct来指示cout显示的进制。`cout << hex;` 修改格式之前，原来的格式将一直有效。

除非有理由存储为其他类型，否则C++将整型常量存储为int。

后缀是放在数字常量后面的的字母，用来表示类型。有`l/L, u/U, u/U和l/L无序组合, ll/LL, ull/Ull/uLL/ULL`

对于字符，C++实现使用的是其主机系统的编码，不过一般是ASCII字符集。

可以基于字符的八进制和十六进制编码来使用转义序列，例如Ctr+Z的ASCII码为26，则可用\032或\x1a表示。**十进制不行，试过了**

与int不同，char在默认情况下，是否有符号由C++实现决定。

宽字符类型wchar_t有足够的空间，可以表示系统使用的最大扩展字符集。

C++11新增无符号类型char16_t和char32_t，其长度和特征不随实现变化而变化。分别用u和U作为前缀。

const相比于#define的好处：
- 能够明确指定类型
- 可以使用C++的作用域规则将定义限制在特定的函数或文件中
- 可以将const用于更复杂的类型
<br><br>

# 3.3 浮点数
计算机将带有小数的数字分为基准值和缩放因子两部分存储（先不考虑符号），以十进制为例，3.14可以分为0.314和10。C++内部表示浮点数采用2的幂次作为缩放因子。单精度浮点类型float一般使用4字节共32比特位，其中1位为符号位，8位为指数位，23位为尾数位。

C++的3种浮点类型及其有效位数：
- float至少32位
- double至少48位，且不少于float
- long double至少和double一样多

浮点常量可以加f/F或l/L后缀。
<br><br>

# 3.4 C++运算符
从左到右的结合性(associativity)意味着如果两个优先级相同的运算符被同时用于同一个操作数，则首先应用左侧的运算符。

## 类型转换
使用大括号{}的初始化称为列表初始化list-initialization，不允许缩窄narrowing，即变量的类型可能无法表示赋给它的值。

表达式中的转换有个整型提升的概念：在计算表达式时，C++将低等级的整型值转换为int。
```c++
short chickens = 20;
short ducks = 30;
short fowl = chickens + ducks; //chickens和ducks都先转为int，算出结果后再转为short赋给fowl
```
### 强制类型转换
```c++
(long) thorn //来自C语言
long (thorn) //C++，使其像函数一样使用
```
C++还引入了4个强制类型转换运算符，在第15章。其中static_cast<>可用于将值从一种数值类型转换为另一种数值类型：
```c++
static_cast<long> (thorn)
```
