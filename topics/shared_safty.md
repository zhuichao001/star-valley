
## shared_ptr线程安全性
```
boost官方文档中有如下结论：
https://www.boost.org/doc/libs/1_57_0/libs/smart_ptr/shared_ptr.htm#ThreadSafety
```
- 1）同一个shared_ptr被多个线程“读”是安全的；
- 2）同一个shared_ptr被多个线程“写”是不安全的；
- 3）共享引用计数的不同的shared_ptr被多个线程”写“ 是安全的；
```
 A shared_ptr instance can be "read" (accessed using only const operations) simultaneously by multiple threads.
 Different shared_ptr instances can be "written to" (accessed using mutable operations such as operator= or reset) simultaneously 
 by multiple threads (even when these instances are copies, and share the same reference count underneath.)
 Any other simultaneous accesses result in undefined behavior.
 ```

## 举例
```
shared_ptr<Foo> g(new Foo(1)); // 线程之间共享的 shared_ptr
shared_ptr<Foo> m; // 线程 A 的局部变量
shared_ptr<Foo> n(new Foo(2)); // 线程 B 的局部变量
-------------------------------------------
线程 A
m = g; （即 read g） //代码1 :赋值指针, 赋值引用计数
-------------------------------------------
线程 B
g = n; （即 write g）//代码2 :清空原来G指向Foo1, 然后重新赋值 Foo2
```

- 测试场景：
```
线程A 
  智能指针m 读取Foo1, 即将增加Foo1计数。

线程 B:
  减少Foo1的引用计数，并且销毁了Foo1
```
