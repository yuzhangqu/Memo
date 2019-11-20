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
        EXP
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
- 参数解包：传递实参时，在序列前加`*`，可将序列中的元素解包传给位置参数；字典前加`**`，可以将字典解包传给关键字参数(字典用`*`解包，只解出key)
- 文档字符串：形参名后面跟`:TYPE`可说明形参需要的类型，函数头的`:`前写`-> TYPE`可说明函数返回值类型，在函数内部可用`'''`多行编写注释。可用help(FUNC)打印出来。
- 作用域：全局作用域、函数作用域。函数内部使用`global VAR`，其后对该变量的引用都是全局变量。
- 命名空间：一个存储变量的字典。`locals()`可以获取当前作用域的命名空间，`globals()`可以获取全局作用域的命名空间。
- 高阶函数：接受函数作为参数或者返回函数的函数。
    - `filter(function, iterable)`
    - `map(function, iterable)`函数
    - `sorted(iterable, *, key=None, reverse=False)`，效果同`list.sort()`，但是这个内置函数可以用于其他数据类型，返回一个list
- lambda表达式：lambda 参数列表:返回值
- 闭包：外部函数将内部函数作为返回值返回形成的。闭包可以访问外部函数的局部变量
- 装饰器：
    - 本质：装饰器接受被装饰函数作为参数，然后装饰器的返回值（一般情况下是一个函数）赋值给被装饰函数
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
    - 类装饰器：类的构造函数（`__init__`）接受被装饰函数作为参数，实例化对象赋值给被装饰函数。重载`__call__`函数达到装饰器效果
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
- 属性和方法的查找流程：先在实例对象中找，然后去类对象去找
- 特殊方法：也叫魔术(magic)方法、双下（dunder）方法。`__init__`会在创建实例时立刻执行
- `__属性名`：是对象的隐藏属性，隐藏属性只可以在类的内部访问。（其实也可以在外部访问，隐藏属性只是把属性名改为了`_类名__属性名`）
- 由于隐藏属性实际上也能在外部访问，因此私有属性一般用单下划线开头（`_属性名`），表明不希望被访问，全靠程序员自觉
- 实例方法、类方法（`@classmethod`）、静态方法（`@staticmethod`）

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