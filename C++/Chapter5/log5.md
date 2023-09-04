# 5.1 for循环
for循环是入口条件（entry-condition）循环，这意味着在每轮循环之前，都将计算测试表达式的值。

C++中每个表达式都有值。`1+1`的值为2，`x=20`的值为20。  
`int total;`不是表达式

for循环原来的句法为：
```c++
for(expression; experssion; expression)
    statement
```
由于C++允许for循环在初始化部分中使用非表达式的声明语句，于是句法修改为：
```c++
for(for-init-statement; condition; expression)
    statement
```

## 副作用和顺序点
副作用side effect是在计算表达式时对某些东西（如存储在变量中的值）进行了修改  
顺序点sequence point是程序执行过程中的一个点，在这里，进入下一步之前将确保对所有的副作用都进行了评估

C++中语句后面的分号就是一个顺序点。任何完整的表达式末尾都是一个顺序点。

递增递减运算符的前缀后缀格式，对于内置类型，采用哪种格式不会有差别；但对于用户自定义的类型，如果有用户自定义的递增和递减运算符，则前缀格式的效率更高。
<br><br>

# 5.2 while循环
**类型别名**  
*C++使用两种方式为类型建立别名*  
```c++
#define BYTE char  //使用预处理器
typedef char BYTE; //使用关键字typedef，这种方式能处理更复杂的类型别名
```
<br><br>

# 5.5 基于范围的for循环（C++11）
```c++
double prices[5] = {1, 2, 3, 4, 5};
for (double x: prices){
    cout << x;
}
//要修改数组元素的话：
for (double &x: prices){
    x *= 0.8;
}
//也可以：
for (int x: {1,2,3}){
    cout << x;
}
```