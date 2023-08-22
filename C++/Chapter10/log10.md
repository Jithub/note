最重要的OOP特性：抽象、封装和数据隐藏、多态、继承、代码的可重用性。<br><br>
# 10.1 过程性编程和面向对象编程
前者首先考虑步骤，然后是数据；而后者首先考虑数据，及如何使用<br><br>
# 10.2 抽象和类
类也是一种类型，要指定类型就要完成三项工作：
- 决定数据对象需要的内存数量
- 决定如何解释内存中的位
- 决定可使用数据对象执行的操作或方法

类接口尽可能将共有接口与实现细节分开，共有接口表示设计的抽象组件。实现细节与抽象分开被称为封装。

*结构的默认访问类型是public，类为private*

```c++
void Stock::update() //我们称标识符update()具有类作用域
```

定义位于类声明中的函数自动成为内联函数；当然可以在类声明后面跟着进行单独定义（p.s. 内联函数要求在每个使用它们的文件中都对其进行定义）

```c++
Stock kate;
kate.show(); //句点"."为成员运算符
```

同一个类的所有对象共享同一组方法，即每种方法只有一个副本，执行同一个代码块。<br><br>
# 10.3 类的构造函数和析构函数
构造函数没有声明类型。程序声明对象时将自动调用构造函数。  
如果没有提供，则C++将自动提供默认构造函数。  
如果定义了构造函数，则必须定义默认构造函数。  
要定义默认构造函数，要么给所有参数提供默认值，要么没有参数。  
只能有一个默认构造函数。  
析构函数没有参数，原型必须为```~Stock();```   
编译器决定什么时候调用析构函数。

显式和隐式的调用构造函数：
```c++
Stock food = Stock(a,b);
Stock food(a,b);
```

**书上360页提到了大括号、析构函数、窗口环境的一个小trick，代码清单10.5 10.6**

使用构造函数对对象进行赋值时，构造函数总会创建一个临时对象，与初始化相比效率会变低。

C++11中可用列表初始化方法用于类：
```c++
Stock jock = {0, 'a'};
Stock jock {0, 'a'};
```
上述列表要有参数列表相匹配的构造函数

要想类方法不修改调用对象，应使用const成员函数：
```c++
void show() const； //函数声明
void Stock::show() const //函数头
```
<br>

# 10.4 this指针
this指针指向用来调用成员函数的对象。所有的类方法都将this指针设置为调用它的对象的地址。*this是该对象的别名。

*每个成员函数（包括构造和析构）都有一个this指针来指向调用对象。*
<br><br>

# 10.5 对象数组
可以使用构造函数来初始化对象数组元素：
```c++
Stock stocks[3] = {
    Stock(a, b),
    Stock(c, d),
    Stock(e, f)
};
```
<br>

# 10.6 类作用域
直接成员运算符（.）、间接成员运算符（->）、作用域解析运算符（::）

想要创建一个作用域为类的常量：  
1. 在类中声明一个枚举。用这种方式声明的枚举不是数据成员，因此不需要提供枚举名
```c++
enum {Month = 12};
```
2. 使用关键字static：  
```c++
static const int Month = 12;
```

C++11提供作用域内枚举，从而枚举量可以避免名称冲突：
```c++
enum class egg {small, medium, large, jumbo};
enum class t_shirt {small, medium, large, Xlarge};
//也可以使用关键字struct代替class。使用时都需要枚举名来限定枚举量：
egg choice = egg::small;
t_shirt child = t_shirt::small
```
作用域内枚举无法隐式地转换为整型。
<br><br>

# 10.7 抽象数据类型ADT
例如使用类来实现栈。私有部分必须标明数据存储发方式，共有接口应隐藏数据表示。