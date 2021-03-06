# 基本概念
- Python是一门面向对象的语言
- 在Python中严格区分大小写
- Python中的每一行就是一条语句，每条语句以换行结束
- 一条语句可以分多行编写，多行编写时语句后边以`\`结尾
- Python是缩进严格的语言，所以在Python中不要随便写缩进
- 在Python中使用`#`来表示注释

# 基本数据类型
- 数字
    - 有三种：整数、浮点数、复数。可根据值自动识别
    - 数字范围无限制
    - 数字过长可用下划线分隔，如：`123_456_789`
    - 二进制以`0b`开头，八进制为`0o`，十六进制为`0x`
    - `int()`、`float()`可将合法的字符串转换为整数、浮点数
- 布尔
    - 布尔逻辑用的英文（`and`,`or`,`not`）而不是符号
    - `bool()`可将所有表示空(`0`、`None`、`''`)的对象转成`False`，其余是`True`
- 字符串
    - 三重引号（`'''`、`"""`）可以换行，并且保留格式
    - 可以用`+`拼接字符串，但是不能和数字相加
    - `print()`支持多参数，以打印效果以空格分隔；可通过`end`参数指定打印完成时末尾添加的字符串(默认为换行符)
    - 格式字符串中的占位符可后接`% (arg1, arg2...)`替换，一个参数可省略括号
    - 格式字符串前添加`f`可使其额外支持`{VAR}`，用来引用变量的值
    - `STR*N`，可将字符串`STR`重复`N`次
    - 是不可变序列
    - 可用`len()`方法取长度
    - `str()`可将其他类型转成字符串
    - `input(STR)`函数可以读取用户输入的字符串作为返回值。`STR`为提示文本
    - `r`前缀代表原始字符串（屏蔽转义）
    - `str.split(sep=None, maxsplit=-1)`：按照分隔符分割，返回一个list
    - `str.partition(sep)`：按照第一个出现分隔符分割，返回一个3-Tuple
- 空值
    - `None`

# 运算符
- `/`：运算结果总会是个浮点数
- `//`：整除运算符，操作数都是整数时，结果也是整数
- `**`：幂运算符
- `+=`：`a += 1`会先引用a，因此必须先对a赋值，否则报错
- `==`、`!=`：比较的是对象的值
- 注：比较运算符可以连写(`10 < 20 > 15`、`a == b == 1`等)
- `is`、`is not`：比较的是对象的`id`
- `not`：会将操作数转换为`bool`类型再取反
- `and`、'or'：是短路运算，不会将操作数转换为`bool`类型
- 三元运算符：`EXP1 if COND else EXP2`

# 流程控制
- if-elif-else语句：注意缩进，注意关键词
    ```python
    if COND1:
        EXP1
    elif COND2:
        EXP2
    else:
        EXP3
    ```
- while循环：
    ```python
    while COND1:
        EXP1
    else:
        EXP2
    ```
- for循环：
    ```python
    for ITERATING_VAR in SEQUENCE:
        EXP1
    else:
        EXP2
    ```
- `pass`可作为占位符，`continue`、`break`作用不赘述

# 容器
- range()
    - 生成自然数序列
    - 一个参数是结束位置（不包含），两个参数是起始和结束位置，三个参数是起始位置、结束位置和步长
- List：可变序列。像数组一样是连续存储的，但是可以动态调整大小，并且可以存储不同类型的元素(内部实现是对象指针的数组)
    ```python
    xs = [3, 1, 2]    # Create a list
    print(xs, xs[2])  # Prints "[3, 1, 2] 2"
    print(xs[-1])     # Negative indices count from the end of the list; prints "2"
    xs[2] = 'foo'     # Lists can contain elements of different types
    print(xs)         # Prints "[3, 1, 'foo']"
    xs.append('bar')  # Add a new element to the end of the list
    print(xs)         # Prints "[3, 1, 'foo', 'bar']"
    x = xs.pop()      # Remove and return the last element of the list
    print(x, xs)      # Prints "bar [3, 1, 'foo']"
    ```
    - Slicing：访问List的子集
        - 步长不为1时，对Slicing赋值需要元素个数匹配
        ```python
        nums = list(range(5))     # range is a built-in function that creates a list of integers
        print(nums)               # Prints "[0, 1, 2, 3, 4]"
        print(nums[2:4])          # Get a slice from index 2 to 4 (exclusive); prints "[2, 3]"
        print(nums[2:])           # Get a slice from index 2 to the end; prints "[2, 3, 4]"
        print(nums[:2])           # Get a slice from the start to index 2 (exclusive); prints "[0, 1]"
        print(nums[:])            # Get a slice of the whole list; prints "[0, 1, 2, 3, 4]"
        print(nums[:-1])          # Slice indices can be negative; prints "[0, 1, 2, 3]"
        nums[2:4] = [8, 9]        # Assign a new sublist to a slice
        print(nums)               # Prints "[0, 1, 8, 9, 4]"
        ```
    - Loops
        ```python
        animals = ['cat', 'dog', 'monkey']
            for animal in animals:
        print(animal)
        # Prints "cat", "dog", "monkey", each on its own line.
        
        for idx, animal in enumerate(animals):
        print('#%d: %s' % (idx + 1, animal))
        # Prints "#1: cat", "#2: dog", "#3: monkey", each on its own line
        ```
    - List comprehensions：可将List中的元素转换类型，甚至可以带条件
        ```python
        nums = [0, 1, 2, 3, 4]
        squares = [x ** 2 for x in nums]
        print(squares)   # Prints [0, 1, 4, 9, 16]
        
        even_squares = [x ** 2 for x in nums if x % 2 == 0]
        print(even_squares)  # Prints "[0, 4, 16]"
        ```
    - 排序：`list.sort(*, key=None, reverse=False)`，其中`key`接受一个函数用来由元素生成比较的键。排序都是用的`<`
- Dictionary：存放键值对， 键必须是不可变对象
    - `dict.setdefault(key, value)`：如果`key`不存在，则添加键值对；存在则不做处理。函数总是返回`key`对应的值
    - `dict.update(other)`：用其他的字典更新该字典，`key`重复则覆盖，不重复则添加
    - 3.7版本后，`dict.popitem()`会删除最后一个添加的键值对，并作为Tuple返回
    - `dict.pop(key[, default])`：可以删除指定`key`返回`value`，指定`default`时删除不存在的`key`不会报错，会返回`default`
    - 注意：`copy()`是浅复制
    - `dict.keys()`返回包含所有键的序列，`dict.values()`返回包含所有值的序列，`dict.items()`返回包含双值子序列(键值对)的序列
    ```python
    d = {'cat': 'cute', 'dog': 'furry'}  # Create a new dictionary with some data
    d = dict(cat='cute', dog='furry')    # Same as the above line
    d = dict([['cat', 'cute'], ['dog', 'furry']]) # 双值子序列可转换为字典
    print(d['cat'])       # Get an entry from a dictionary; prints "cute"
    print('cat' in d)     # Check if a dictionary has a given key; prints "True"
    d['fish'] = 'wet'     # Set an entry in a dictionary
    print(d['fish'])      # Prints "wet"
    # print(d['monkey'])  # KeyError: 'monkey' not a key of d
    print(d.get('monkey', 'N/A'))  # Get an element with a default; prints "N/A"
    print(d.get('fish', 'N/A'))    # Get an element with a default; prints "wet"
    del d['fish']         # Remove an element from a dictionary
    print(d.get('fish', 'N/A')) # "fish" is no longer a key; prints "N/A"
    ```
    - Loops
        ```python
        d = {'person': 2, 'cat': 4, 'spider': 8}
        for animal in d:
            legs = d[animal]
            print('A %s has %d legs' % (animal, legs))
        # Prints "A person has 2 legs", "A cat has 4 legs", "A spider has 8 legs"

        for animal, legs in d.items():
            print('A %s has %d legs' % (animal, legs))
        # Prints "A person has 2 legs", "A cat has 4 legs", "A spider has 8 legs"
        ```
    - Dictionary comprehensions
        ```python
        nums = [0, 1, 2, 3, 4]
        even_num_to_square = {x: x ** 2 for x in nums if x % 2 == 0}
        print(even_num_to_square)  # Prints "{0: 0, 2: 4, 4: 16}"

        query_string = 'id=1&name=tom&age=26'
        d = {k:v for k,_,v in map(lambda x : x.partition('='), query_string.split('&'))}
        ```
- Set：元素的无序集合
    - 只能存储不可变对象(可哈希的类型)
    - 空集合通过`set()`创建
    - `set()`可将序列和字典转换为集合，转换字典时集合中为字典的keys
    - `update()`同样可以传序列和字典，传字典时只使用字典中的keys
    - `pop()`：随机删除并返回元素
    - `&`、`|`、`-`、`^`：交集、并集、差集、异或集
    - `<=`、`<`：检查前者是否为后者的子集、真子集
    ```python
    animals = {'cat', 'dog'}
    print('cat' in animals)   # Check if an element is in a set; prints "True"
    print('fish' in animals)  # prints "False"
    animals.add('fish')       # Add an element to a set
    print('fish' in animals)  # Prints "True"
    print(len(animals))       # Number of elements in a set; prints "3"
    animals.add('cat')        # Adding an element that is already in the set does nothing
    print(len(animals))       # Prints "3"
    animals.remove('cat')     # Remove an element from a set
    print(len(animals))       # Prints "2"
    ```
    - Loops：和List的遍历类似，但注意Set中的元素是无序的
        ```python
        animals = {'cat', 'dog', 'fish'}
        for idx, animal in enumerate(animals):
            print('#%d: %s' % (idx + 1, animal))
        # Prints "#1: fish", "#2: dog", "#3: cat"
        ```
    - Set comprehensions
        ```python
        from math import sqrt
        nums = {int(sqrt(x)) for x in range(30)}
        print(nums)  # Prints "{0, 1, 2, 3, 4, 5}"
        ```
- Tuple：不可变序列。是不可修改的、有序的、值的列表。
    - 可以作为Dictionary的键
    - 可以作为Set的元素
    - 不是空元组时括号可省略
    - 非空元组至少需要一个`,`
    - 解包需要数目一致，也可用`*VAR`解出剩余元素到一个List中
    ```python
    d = {(x, x + 1): x for x in range(10)}  # Create a dictionary with tuple keys
    t = (5, 6)        # Create a tuple
    print(type(t))    # Prints "<class 'tuple'>"
    print(d[t])       # Prints "5"
    print(d[(1, 2)])  # Prints "1"
    ```

# 对象
- 每个对象中都要保存三种数据
    - id：唯一标识，可通过`id()`查看
    - type：类型，可通过`type()`查看
    - value
- 变量中存储的是对象id（内存地址）
- 相同的不可变对象赋值给变量时，对象会复用
    ```python
    a = (1, 2, 3)
    b = (1, 2, 3)
    print(a is b) # True

    c = [1, 2, 3]
    d = [1, 2, 3]
    print(c is d) # False
    ```

# 函数
- `def`为声明函数的关键字
- 实参传递方式：位置参数、关键字参数
- 混合使用时，位置参数必须在关键字参数前
- 使用位置参数和关键字参数给同一个形参赋值会报错
- 函数调用时，不会检查实参的类型！
- 参数都是按引用传递，想按值传递可变对象可以通过其他方法（`copy()`、Slicing等）
- `def foo(a, *b, c, **d):`：按顺序分别为位置参数、Star参数、关键字参数、Double Star参数
    - `*b`：会将所有**位置实参**保存在一个Tuple中(Bare Star参数`*`不接受位置实参)，注意此时不`b`能再作为关键字参数
    - 此时`c`必须通过关键字参数传递
    - `**d`：将接收所有未定义的关键字参数，保存在字典中
    - python3.8引入了`/`，在`/`之前的参数只能通过位置参数传递
- 参数解包：传递实参时，在序列前加`*`，可将序列中的元素解包传给位置参数；字典前加`**`，可以将字典解包传给关键字参数(字典用`*`解包，只解出key)
- 文档字符串：形参名后面跟`:TYPE`可说明形参需要的类型，函数头的`:`前写`-> TYPE`可说明函数返回值类型，在函数内部可用`'''`多行编写注释。可用help(FUNC)打印出来。
- 作用域：全局作用域、函数作用域。函数内部使用`global VAR`，其后对该变量的引用都是全局变量。
- 命名空间：一个存储变量的字典。`locals()`可以获取当前作用域的命名空间，`globals()`可以获取全局作用域的命名空间。
- 高阶函数：接受函数作为参数或者返回函数的函数。
    - `filter(function, iterable)`
    - `map(function, iterable)`函数，返回一个能yield结果的迭代器，惰性求值
    - `sorted(iterable, *, key=None, reverse=False)`，效果同`list.sort()`，但是这个内置函数可以用于其他数据类型，返回一个list
- lambda表达式：lambda 参数列表:返回值
- 闭包：外部函数将内部函数作为返回值返回形成的。闭包可以访问外部函数的局部变量
- 装饰器：
    - 本质：装饰器接受被装饰函数作为参数，然后装饰器的返回值（一般情况下是一个函数）绑定给被装饰函数名
    - 思想：基于开闭原则（OCP），应该对扩展是开放的，对修改是关闭的，即在不修改函数的情况下对函数进行扩展
    - 利用参数的装包解包，可以实现以上要求
    - 可以对一个函数使用多个装饰器（内层装饰器先起作用，然后是外层）
    ```python
    def foo(func):
        def bar(*args, **kwargs):
            # ...do some stuff
            result = func(*args, **kwargs)
            # ...do other stuff
            return result
        return bar

    @foo
    def xxx():
        pass
    ```
    - 带参数的装饰器会立刻执行，只要返回结果还是一个装饰器就可以继续装饰函数
    - 类装饰器：类的构造函数（`__init__`）接受被装饰函数作为参数，实例化对象绑定给被装饰函数。重载`__call__`函数达到装饰器效果
    - 带参数的类装饰器：类的构造函数接受参数保存起来，重载`__call__`函数接受被装饰函数作为参数返回一个函数
    - 被`@property`装饰的函数不再是个函数，而是`property`对象。
    ```python
    class Person:
        def __init__(self, name):
            self._name = name

        @property
        def name(self):
            return self._name

        @name.setter
        def name(self, name):
            self._name = name
    ```

# 类
- 用`class`关键字去定义一个类`Foo`，实际上是定义一个`type`类型的对象`Foo`
- foo = Foo()实例化对象：实际上是创建一个`Foo`类型的对象`foo`
- isinstance(foo, Foo)：判断对象`foo`是不是类`Foo`的实例
- issubclass(A, B)：判断类A是不是类B的子类
- 属性和方法的查找流程：先在实例对象中找，然后去类对象去找
- 类属性：在类中定义的属性。类属性可以通过类或者类的实例访问，但是只能通过类修改
- 实例属性：通过实例对象添加的属性。只能通过实例对象访问和修改
- 实例方法：在类中定义的，以`self`为第一个参数的方法。通过实例调用时，python将调用对象作为self传入；通过类调用时，需要手动传入`self`参数
- 类方法：在类中用`@classmethod`来装饰的方法，以`cls`为第一个参数。通过类调用时，python将调用的类对象作为cls传入；通过实例调用时，找到实例的类型并传入；两者效果没区别
- 静态方法：在类中用`@staticmethod`来装饰的方法。同样可以通过类对象和实例对象调用。一般是一些工具方法，作为静态方法放在类中，避免放在全局。

# 封装、继承和多态
- 封装：确保对象中的数据安全
    - `__属性名`：是对象的隐藏属性，隐藏属性只可以在类的内部访问。（其实也可以在外部访问，隐藏属性只是把属性名改为了`_类名__属性名`）
    - `_属性名`：由于隐藏属性实际上也能在外部访问，因此私有属性一般用单下划线开头，表明不希望被访问，全靠程序员自觉
- 继承：保证了对象的可扩展性
    - 如果创建类时省略父类，则默认父类为object
    - `类名.__bases__`：获取类的父类
    - 父类的所有方法都会被子类继承，包括特殊方法
    - `super()`：获取实例的父类部分（也是一个实例）
    - 多重继承：`class Foo(A, B):`，如果多个父类中有同名方法，则在前面的父类的方法会覆盖后面的父类的
- 多态：保证了程序的灵活性
    - 由于没有类型检查，所以使用的是`duck typing`（`If it walks like a duck, swims like a duck, and quacks like a duck, then it probably is a duck.`）
    - 只要传入函数的对象提供所需的全部方法和属性，就可以调用，而不会做`type checking`
    - 例如：一个类型的对象能传入`len()`函数，只需要该类型提供`__len__(self)`函数

# 垃圾回收
- 垃圾：没有被引用的对象就是垃圾
- Python有自动的垃圾回收机制
- `del VAR`：只是删除变量
- 对象没有被任何对象引用则会触发垃圾回收

# 特殊方法
- 也叫魔术(magic)方法、双下（dunder）方法
- `__new__(cls[, ...])`：静态方法，一般返回类的实例，如果返回实例，接下来以这个实例调用`__init__`；如果不返回实例，`__init__`不会被调用
- `__init__(self[, ...])`：会在创建实例时立刻执行
- `__del__(self)`：会在垃圾回收前调用
- `__repr__(self)`：建议返回能描述对象的无歧义的字符串。在交互模式下输入变量，会调用此方法。也可通过`repr()`函数调用
- `__str__(self)`：此方法默认实现是调用`__repr__`。建议返回能简要描述对象的字符串。可通过`str()`函数调用，也可以在`print()`、`format()`时自动调用
- `__lt__(self, other) & __gt__(self, other)`：如果只实现其中一个，则另一个会调用已实现的函数，结果取反。
- `__le__(self, other) & __ge__(self, other)`：同上。注意：实现了`__lt__`和`__eq__`并不代表支持`<=`
- `__eq__(self, other) & __ne__(self, other)`：如果实现了`__eq__`，则`__ne__`会调用`__eq__`，结果取反。**反过来不成立**。
- 如果比较操作符右边的操作数是左边的子类，则子类中相应的反射函数（`__lt__`和`__le__`是`__gt__`和`__ge__`的反射，`__eq__`和`__ne__`都是自身的反射）优先
- `__len__(self)`：函数`len()`调用，建议返回一个非负数，表示对象的长度。
- `__bool__(self)`：函数`bool()`调用，或者真值检测时自动调用。如果没实现，则调用`__len__`，根据结果是否为0检测真值。如果都没实现，所有实例都是真
- `__iter__(self)`：在需要容器的迭代器的时候被调用，返回一个可迭代的对象（`yield from`）
- 还有很多运算符的特殊方法，不赘述了，根据需要实现

# 模块和包
- 模块
    - 可以多次引入同一个模块，但是模块的实例只会创建一次
    - 模块引入：`import 模块名[ as 别名]`，模块名就是文件名
    - 可以通过`__name__`获取模块的名字，主模块的名字固定为`__main__`
- 包：也是一个模块。
    - 普通模块是一个文件，而包是一个文件夹。
    - 包引入：`import 包名`
    - 包的子模块引入：`from 包名 import 子模块名`
    - `__init__.py`：包中的此文件会在引入包或包的子模块时执行
    - `__pycache__`：存放编译之后的缓存文件

# 标准库
- sys：访问解释器的变量、与解释器交互
    - `sys.argv`：命令行的参数
    - `sys.modules`：已加载的模块
    - `sys.path`：模块的搜索路径，第一个元素是被执行的脚本所在的目录
    - `sys.platform`：判断兼容性时用
    - `sys.exit('MSG')`：退出程序
- os：提供操作系统相关的功能
    - `os.environ`：系统环境变量
    - `os.system(command)`：可以执行操作系统的命令
- pprint：提供美观的打印
    - `pprint.pprint()`
- logging：日志
    - 日志级别由低到高：`NOTSET, DEBUG, INFO, WARNING, ERROR, CRITICAL`
    - root logger默认是WARNING级别
    - `logging.basicConfig(format=FORMAT, level=logging.INFO)`
    - 内置`%(asctime)s %(message)s`等
- threading：多线程
    - `threading.Thread(group=None, target=None, name=None, args=(), kwargs={}, *, daemon=None)`：创建线程
    - `start()`：开始线程活动
    - `run()`：线程的活动代码
    - `treading.Event().wait(TIMEOUT)`：通过线程的方式等待一段时间
- datetime：日期
    - `datetime.datetime.now()`
    - `time.strftime(format)`：%Y/%m/%d-%H:%M:%S
- json：JSON相关库
    - `load`：将支持read()的类文件对象转成JSON
    - `loads`：将str或bytes转成JSON
    - 一般来说，JSON的`object`转成Python的`dict`
    - JSON字符串要使用双引号

# 异常
```python
try:
    pass
except NameError as e:  # 捕获NameError类型的异常，对象绑定到e
    pass
except IndexError:  # 捕获IndexError类型的异常
    pass
except:  # 捕获其他类型的异常，等同于except Exception
    pass
else:  # 程序正常时执行下面的代码块
    pass
finally:  #无论是否有异常都执行
    pass
```
- `try`语句是必须的
- `except`和`finally`必须要有一个
- `else`可有可无
- 所有异常都是BaseException的子类
- 绝大多数异常都是Exception的子类
- 自定义的异常建议继承Exception类
- `raise Exception('MSG')`：抛出异常

# 文件
- 打开文件
    - `open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)`
    - 打开文本文件一般指定编码为`'utf-8'`
    - 默认模式(`'r'`)或`'r+'`模式，文件不存在时打开会报错
- 读取文件：
    - `file_obj.read(size=-1, /)`：接受一个位置参数，表示要读取的字符数（换行符也算一个）
    - 不够要求的字符数则读到EOF
    - 参数为负数或省略，则读取到EOF
    - 直接读到EOF则返回空串
    - `file_obj.readline(size=-1, /)`：读取一整行（包括最后换行符），参数同上，如果参数大于当前行的总字符数，也只会读完这一行
    - `file_obj.readlines(hint=-1, /)`：读取多行，返回一个字符串list。如果读取一行之后字符数超过`hint`，则读取结束
    - file_obj也是可以迭代的，迭代的每一个元素为一行
- 写入文件
    - `'w'`或`'w+'`模式：一打开就会清空内容
    - `'a'`或`'a+'`模式：追加模式
    - `'x'`或`'x+'`模式：新建文件，文件已存在则报错
    - 没`+`都是不能读的
- 二进制文件
    - 模式后加`b`
    - 二进制模式下读取长度参数以字节为单位
- 位置控制
    - `file_obj.tell()`：获取当前的流位置
    - `file_obj.seek(cookie, whence=0, /)`：改变流位置，第一个参数是字节偏移量；第二个参数为0表示相对开头，为1表示相对当前位置，为2表示相对末尾
    - utf-8编码下中文占3个字节
- 关闭文件：`file_obj.close()`，手动关闭容易遗漏，最佳实践是使用`with语句`
    ```python
    with open(file_name) as file_obj
        print(file_obj.read())
    ```
- 其他操作
    - `os.listdir(path=None)`：获取指定路径的目录结构，返回一个字符串的list，每一个元素是目录下的文件或子目录
    - `os.getcwd()`：获取当前目录
    - `os.chdir(path)`：切换到指定目录
    - `os.mkdir(path)`：创建目录，目录存在会报错
    - `os.rmdir(path)`：删除目录，目录非空会报错
    - `os.remove(path)`：删除文件
    - `os.rename(src, dst)`：其实是类似于Linux的mv操作

# Numpy

# Python和Sublime的整合
- 在Sublime中执行Python代码，`ctrl + b` 自动在Sublime内置的控制台中执行
- 使用SublimeREPL来运行python代码，安装完成，设置快捷键，希望按f5则自动执行当前的Python代码
```
{
    "keys": ["f5"],
    "caption": "SublimeREPL:Python",
    "command": "run_existing_window_command",
    "args":
    {
        "id": "repl_python_run",
        "file": "config/Python/Main.sublime-menu"
    }
},
```