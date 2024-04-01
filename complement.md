- 如何实现一个长连接推送，长连接要注意哪些事项？以IM为背景
- 陈述一个多线程消息队列的实现，如何优化瓶颈?
- 给一个简单的单例实现？
```
class Singleton {
 private:
     static Singleton* instance;
     // 私有构造函数，防止从其他地方创建对象。
     Singleton() {}

 public:
     // 静态访问方法。
     static Singleton* getInstance() {
         if (instance == 0) {
             instance = new Singleton();
         }
         return instance;
     }
};

// 初始化指针为零，这样在第一次调用getInstance时可以初始化
Singleton* Singleton::instance = 0;

int main() {
    // 创建一个新的Singleton对象。
    Singleton* s = Singleton::getInstance();

    // 使用Singleton对象。

    return 0;
}
```
- 对象之间的关系有哪几种，分别是怎么实现？
