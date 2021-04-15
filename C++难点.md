# 随机数生成
```C++
uniform_int_distribution<int> dist(0, 999);
random_device rd;
mt19937 engine(rd());
for (int i = 0; i < 100; ++i) {
    cout << dist(engine) << endl;
}
```

# 虚函数实现机制
- 每个类有一个虚函数表
- 每个类对象有一个虚表指针
- 如果子类重写了父类的虚方法，子类虚函数表将保存重写的虚函数的地址，而不是父类的虚函数地址

# new vs malloc
- new在自由存储区上分配（甚至可以不分配`new(addr) type`），malloc在堆上分配；
- new返回对象类型的指针，malloc返回`void *`；
- 分配失败时，new抛出`bac_alloc`异常，malloc返回NULL
- new根据类型自动计算分配内存大小，malloc需要手动指定大小；
- new/delete会调用构造/析构函数，malloc/free则不会；
- new[]/delete[]支持数组类型，malloc/free需要自行管理数组；
- new/delete可以被重载
- malloc分配的内存可以用`realloc`扩容

# sizeof vs strlen
- sizeof是操作符，参数可以是类型或变量，计算数据类型占内存的大小
- strlen是库函数，计算以`\0`结尾的字符串的长度
- sizeof在编译时计算，strlen在运行时才能计算

# 可重入函数
- 重入：一个函数被多个执行流调用，有可能在第一次调用还没有返回时，再次进入这个函数
- 遵循下面原则的是可重入函数
    + 不在函数内部使用静态或全局数据
    + 不返回静态或全局数据，所有数据都由函数的调用者提供
    + 使用本地数据，或者通过制作全局数据的本地拷贝来保护全局数据
    + 如果必须访问全局变量，利用互斥机制来保护全局变量
    + 不调用不可重入函数

# volatile
- 阻止编译器优化（`-O3`）被volatile修饰的对象，对这些对象的读取总是从内存中读，而不是从临时的寄存器中，因为这些对象的修改可能无法完全被编译器确定；
- 例如：Memory-mapped I/O。声明为volatile才能每次读到最新的数据；
- 例如：多线程通过全局变量的方式共享内存。声明为volatile才能在另一个线程修改的时候读到最新的值

# 异常
- 遇到cache语句之后，开始stack unwind的流程，从异常抛出点到cache语句，逐层析构创建的自动对象

# 智能指针
- RAII思想：将基本类型指针封装为类，析构时自动释放内存
- 不可以将基本类型指针隐式转换为智能指针
- 不可以用非堆内存初始化智能指针
- auto_ptr：会出现所有权转让（摒弃）
- shared_ptr：采用引用计数，在引用计数为0时才释放。用于需要多个指针指向同一个对象
- unique_ptr：也是所有权模型，将源unique_ptr赋值给另一个时，如果源unique_ptr时临时右值(OK)，否则编译不通过。
- 循环引用：两个shared_ptr互相引用，在超出范围时都不会释放内存。
- weak_ptr：也可以共享，但是实际上不拥有对象，必须通过lock()函数得到shared_ptr

# Move Constrctor
- 消除两个对象交互时不必要的对象拷贝，节省运算存储资源，提高效率。

# vector的push_back与容量增长
- 扩容因子1.5。因为1.5的时候扩容几次之后可以利用之前的空间
- 均摊之后，时间复杂度是常数。等比数列求和
- 扩容时涉及到拷贝操作

# vector与list的效率比较
- push_back：vector效率高(vector扩容时申请了更多空间，list每次都要申请，申请内存耗时的)
- insert、remove：list效率高(链表的随机插入删除)
- 随机位置访问：vector效率高(vector的随机访问)

# 虚函数表
- 虚函数表指针在实例中最前面的位置，因此同一个类的不同实例，前64位的内容是一样的(指向同一个虚函数表)
- 虚函数表的每一个节点是一个虚函数指针，按声明顺序存储
- 子类继承父类的情况下，首先是父类的虚函数指针(如果有覆盖则替换为子类的)，然后是子类没覆盖的
- 多重继承：子类有多个虚函数表，子类实例有多个虚表指针，子类未覆盖的虚函数放在第一个虚函数表中，覆盖的虚函数会替换所有覆盖的虚函数

# 继承
- 可见性由高到低是：public、protected、private
- 只有public和protected成员可以被继承，private成员不能被继承
- public继承、protected继承、private继承：决定了继承过来的成员的可见性上限

# 静态多态 vs 动态多态
- 静态多态通过模板定义接口来实现，动态多态通过基类虚函数定义接口来实现
- 静态多态在编译器完成，效率高，但是不能够处理异质对象集合
- 动态多态在运行时绑定，有运行时开销，但是可以处理同一继承体系下异质对象集合

# friend函数
- 友元函数是可以直接访问类的私有成员的非成员函数。
- `friend Complex operator+(Complex &c1,Complex &c2);`

# istream、ostream重载
- `friend ostream & operator <<(ostream &output, T &t);`
- `friend istream & operator >>(istream &input, T &t);`

# 特殊成员变量的初始化
- const成员、引用成员：初始化列表中初始化
- static成员：在类外初始化
- static const整型成员：可以在类内部、类外初始化
- static const非整型成员：在类外初始化，用constexpr修饰可在类内部初始化

# STL的空间配置器
- 第一层配置器处理大于128B的内存申请，实际调用malloc、free等
- 小于128B的由第二层配置器的内存池管理
- 内存池由一系列的free_list组成，大小从8B到128B
- free_list都是8B的整数倍：效率高，64位系统的地址是8B

# Qt的信号槽机制
- 信号索引、槽索引

# 迭代器实现原理
- 封装了指针

# 宏展开
- 参数涉及到`#`或`##`操作，那么参数的宏不会在此操作之前展开
