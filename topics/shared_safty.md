
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
shared_ptr<Foo> g(new Foo1); // 线程之间共享的 shared_ptr
shared_ptr<Foo> x; // 线程 A 的局部变量
shared_ptr<Foo> n(new Foo2); // 线程 B 的局部变量
-------------------------------------------
线程 A
x = g; （即 read g） //代码1 :赋值指针,赋值 引用计数
-------------------------------------------
线程 B
g = n;//代码2 :动作A 清空原来G指向Foo1, 动作B 然后重新赋值 Foo2

测试场景：

线程A 
  智能指针x 读取Foo1,然后还重置Foo1计数。

  线程 B:
   销毁了Foo1
   线程A
   重置计数是，foo1已经被销毁。
```
