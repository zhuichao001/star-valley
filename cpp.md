- C++构造函数有哪几种？分别有什么用途？
- 阐述一下代码会发生什么？
```
class A{
    public:
        A(double i);  
        // explicit A(double i);  
        //virtual ~A(){}
};
A a = 2;
```
- 写一个C++类，可以实现无类型操作，例如a=1, a='abc', a=3.134
- std::deque的底层实现,  std::queue的实现
- std::make_shared的原理，
- shared_from_this的作用
- T&、std::unique_ptr<T>、std::unique_ptr<T> &, std::unique_ptr<T> &&的区别?
- shared_ptr是线程安全的吗？如何做到线程安全?
