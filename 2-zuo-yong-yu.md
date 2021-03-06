# 2 作用域

## 2.1 和静态变量

在 `.c` 文件中定义一个不需要被外部引用的变量时，可以将它们放在匿名命名空间或声明为 `static` 。但是不要在 `.h` 文件中这么做。

**定义:**

> 所有置于匿名命名空间的声明都具有内部链接性，函数和变量可以经由声明为 `static` 拥有内部链接性，这意味着你在这个文件中声明的这些标识符都不能在另一个文件中被访问。即使两个文件声明了完全一样名字的标识符，它们所指向的实体实际上是完全不同的。

**结论:**

> 推荐、鼓励在 `.c` 中对于不需要在其他地方引用的标识符使用内部链接性声明，但是不要在 `.h` 中使用。

## 2.2 非成员函数

> 如果必须定义非成员函数, 又只是在 `.c` 文件中使用它, 可使用=`static` 链接关键字 \(如 `static int Foo() {...}`\) 限定其作用域.

## 2.3 局部变量

将函数变量尽可能置于最小作用域内, 并在变量声明时进行初始化.

C++ 允许在函数的任何位置声明变量. 我们提倡在尽可能小的作用域中声明变量, 离第一次使用越近越好. 这使得代码浏览者更容易定位变量声明的位置, 了解变量的类型和初始值. 特别是，应使用初始化的方式替代声明再赋值, 比如:

> ```c
> int i;
> i = f(); // 坏——初始化和声明分离
> ```
>
> ```c
> int j = g(); // 好——初始化时声明
> ```

属于 `if`, `while` 和 `for` 语句的变量应当在这些语句中正常地声明，这样子这些变量的作用域就被限制在这些语句中了，举例而言:

> ```c
> while (const char* p = strchr(str, '/')) str = p + 1;
> ```

