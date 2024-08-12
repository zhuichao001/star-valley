
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
