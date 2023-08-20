# 11.1 + 11.2 运算符重载
运算符重载是一种形式的C++多态。  
通过**运算符函数**这种特殊函数形式来重载运算符：
operator**op**(argument-list)  
**op**必须是有效的运算符  
```c++
dis = sid + sara;
//如果“+”被重载，则编译器替换为：
dis = sid.operator+(sara);
```

**按照清单11.4和11.5的小时分钟求和的举例：**
```c++
class Time 
{
    Time Sum(const Time & t) const;        //旧的表现形式
    Time operator+(const Time & t) const ; //新的表现形式
}
//使用时：
total = a.operator+(b); //operator+表示法
total = a + b;          //运算符表示法，其中a是调用对象，b是参数
```

**P387页介绍了可进行重载的运算符和对重载的限制。**
<br><br>

# 11.3 友元（看多了字都不认识了，后面全部改为friend）
friend、friend类、**friend函数**

创建friend函数:  
1. 将其原型放在类声明中，并在原型声明前加上关键字friend  
```c++
class Time
{
    friend Time operator*(double m, const Time & t);
}
```
2. 编写定义  
```c++
//不是成员函数，不需要限定符
friend Time operator*(double m, const Time & t)
{}
```
**P393的friend判断有点乱，简单说就是看friend函数内部定义中，对哪个类对象的私有成员进行了访问，那它就是哪个类的friend。**

*只有在类声明的原型中才能使用friend关键字，除非函数定义也是原型。*
<br><br>

# 11.4 重载运算符：作为成员函数还是非成员函数
对于很多运算符可以选择成员函数或者非成员函数来实现运算符重载：  
```c++
class Time
{
    Time operator+(const Time & t) const;
    friend Time operator+(const Time & t1, const Time & t2);
}
```
上述两种格式都能和表达式 `T1 = T2 + T3;` 相匹配，因此必须只选其中一个以避免二义性错误。
<br><br>

# 11.5 再谈重载：一个矢量类
**一个详尽的例子。暂时跳过。**
<br><br>

# 11.6 类的自动转换和强制转换
**一开始这一段主要是通过利用构造函数，把类看作是一种基本类型，实现类和C++中的基本类型之间的转换。不用书上的例子，改用时间：**  
```c++
class Time
{
private:
    enum {min_per_hr = 60};
    int hour;
    double min_left;
    double minute;
public:
    Time(double min);
    Time(int hr, double min);
    Time();                    //默认构造函数
    ~Time();
    void show_hr() const;      //展示几小时几分钟，hh:mm
    void show_min() const;     //展示多少分钟，mm
}
```
那么直接利用构造函数 `Time(double min)` ，就可以实现浮点类型转换为Time类型：  
```c++
Time a;
a = 20.5;       //隐式转换
a = Time(20.5); //显式转换
a = (Time)20.5; //老式的显式转换
```
只有接收一个参数的构造函数才能作为转换函数。  
然而如果后面的参数提供默认值，那也可以。  
如果使用关键字explicit对函数作处理：`explict Time(double min)`，那么上面的隐式转换将非法。

在不加explicit修饰时，可将 `Time(double min)` 用于下述的隐式转换：  
- 将Time对象初始化为double值时
- 将double值赋给Time对象时
- 将double值传递给接受Time参数的函数时
- 返回值被声明为Time的函数试图返回double值时
- 上述任意一种情况下，使用可转换为double类型的内置类型时

基本类型转换为类类型使用构造函数，反过来需要转换函数。转换函数是用户定义的强制类型转换。要转换为typeName类型，使用如下形式的函数：  
```c++
operator typeName();
```
需要注意以下几点：
- 转换函数必须是类方法
- 转换函数不能指定返回类型
- 转换函数不能有参数

**也就是说类似于重载了之前的强制类型转换，如`double()`。不想看了，以后现学现卖吧。看吐了**