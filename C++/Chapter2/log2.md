# 2.1 进入C++
表2.1：头文件命名约定  
| 头文件类型 | 约定 | 示例 | 说明 |  
|---|---|---|---|  
|C++旧式风格|以.h结尾|iostream.h|C++程序可以使用|  
|C旧式风格|以.h结尾|math.h|C、C++程序可以使用|  
|C++新式风格|没有扩展名|iostream|C++程序可以使用，使用namespace std|  
|转换后的C|加上前缀c，没有扩展名|cmath|C++程序可以使用，可以使用不是C的特性，如namespace std|

一行代码中不可分割的元素叫做标记token，空格、制表符和回车统称为空白white space。
<br><br>

# 2.2 C++语句
声明语句指出存储类型（需要的内存）并提供位置标签（内存单元的名称）。  
程序中的声明语句叫做定义声明defining declaration，简称为定义definition。

赋值从右向左进行。
<br><br>

# 2.4 函数
全部的函数特性：
- 有函数头和函数体
- 接受参数
- 返回一个值
- 需要一个原型

**关于call和invoke：call一般就用于函数调用，invoke更多的是，invoke an object，你总不能call an object。关于后者可以再看看“函数对象”和重载运算符()相关的内容。**

