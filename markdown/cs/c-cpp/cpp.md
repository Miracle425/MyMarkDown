# 语法

## 作用域限定符`::`

- 命名空间限定符：

:: 可以用来访问命名空间中的变量、函数或类型，以及全局作用域中的符号。
示例：

```cpp
namespace NS {
    int var = 10;
    void func() {
        // Do something
    }
}

int main() {
    int var = 5;
    std::cout << var << std::endl;        // 输出局部变量 var 的值，即 5
    std::cout << NS::var << std::endl;    // 输出命名空间 NS 中的变量 var 的值，即 10

    NS::func();  // 调用命名空间 NS 中的函数 func
    
    return 0;
}
```

- 全局作用域限定符：

在全局作用域中使用 :: 表示全局命名空间，用于引用全局变量或函数。
示例：

```cpp
int var = 100;  // 全局变量

int main() {
    int var = 5;  // 局部变量
    std::cout << var << std::endl;    // 输出局部变量 var 的值，即 5
    std::cout << ::var << std::endl;  // 输出全局变量 var 的值，即 100

    return 0;
}
```

- 类作用域：

在类的成员函数定义或实现外部时，用 :: 表示类的作用域。
示例：

```cpp
class MyClass {
public:
    static int var;
};

int MyClass::var = 50;  // 类外定义静态成员变量 var

int main() {
    std::cout << MyClass::var << std::endl;  // 使用类作用域访问静态成员变量 var，输出 50

    return 0;
}
```

## 模板特例化

对某个类型的类模板进行特例化，可以为该类型提供特定的实现。

```cpp
template <>
class Storage<int> {
private:
    int item;

public:
    Storage(int t) : item(t) {}

    void print() {
        std::cout << "Specialized storage for int: " << item << std::endl;
    }
};template <>
class Storage<int> {
private:
    int item;

public:
    Storage(int t) : item(t) {}

    void print() {
        std::cout << "Specialized storage for int: " << item << std::endl;
    }
};
```

# 思想/结构
