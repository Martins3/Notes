## chapter 5 : 右值引用，移动语义，完美转发

移动语义让创建 move only 类型的对象成为可能，包括 std::unique_ptr, std::future, std::thread.

形参是 左值, 即使其类型是右值引用。
```cpp
void f(Widget && a);
```

- 如果想要移动一个对象，就不要将其声明为常量, 常量对象将移动操作会一声不响的转换为复制操作
- std::move 只是保证转换之后的对象可以移动

- std::forward 的操作，当且仅当其实参是使用右值完成初始化时，他才会将执行向右值类型的强制类型转换

- [ ] P155 论述 std::forward 为什么不可以替代 std::move

- 如果看到 `T &&`, 但是没有涉及该类型的类型推导，那么就是右值引用。

- 万能引用的常见场景是在 auto 和 template 上, 是不是万能引用的关键在于 类型推导

- 使用右值来初始化万能引用，将会得到右值引用，采用左值来初始化万能引用，将会得到一个左值引用

