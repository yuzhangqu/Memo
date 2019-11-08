# 基本概念
- Python是一门面向对象的语言
- 在Python中严格区分大小写
- Python中的每一行就是一条语句，每条语句以换行结束
- 一条语句可以分多行编写，多行编写时语句后边以`\`结尾
- Python是缩进严格的语言，所以在Python中不要随便写缩进
- 在Python中使用`#`来表示注释

# 基本数据类型
- 数字
    ```python
    x = 3
    print(type(x)) # Prints "<class 'int'>"
    print(x)       # Prints "3"
    print(x + 1)   # Addition; prints "4"
    print(x - 1)   # Subtraction; prints "2"
    print(x * 2)   # Multiplication; prints "6"
    print(x ** 2)  # Exponentiation; prints "9"
    x += 1
    print(x)  # Prints "4"
    x *= 2
    print(x)  # Prints "8"
    y = 2.5
    print(type(y)) # Prints "<class 'float'>"
    print(y, y + 1, y * 2, y ** 2) # Prints "2.5 3.5 5.0 6.25"
    ```
- 布尔：布尔逻辑用的英文(`and`,`or`,`not`)而不是符号
    ```python
    t = True
    f = False
    print(type(t)) # Prints "<class 'bool'>"
    print(t and f) # Logical AND; prints "False"
    print(t or f)  # Logical OR; prints "True"
    print(not t)   # Logical NOT; prints "False"
    print(t != f)  # Logical XOR; prints "True"
    ```
- 字符串
    ```python
    hello = 'hello'    # String literals can use single quotes
    world = "world"    # or double quotes; it does not matter.
    print(hello)       # Prints "hello"
    print(len(hello))  # String length; prints "5"
    hw = hello + ' ' + world  # String concatenation
    print(hw)  # prints "hello world"
    hw12 = '%s %s %d' % (hello, world, 12)  # sprintf style string formatting
    print(hw12)  # prints "hello world 12"
    
    s = "hello"
    print(s.capitalize())  # Capitalize a string; prints "Hello"
    print(s.upper())       # Convert a string to uppercase; prints "HELLO"
    print(s.rjust(7))      # Right-justify a string, padding with spaces; prints "  hello"
    print(s.center(7))     # Center a string, padding with spaces; prints " hello "
    print(s.replace('l', '(ell)'))  # Replace all instances of one substring with another;
                                    # prints "he(ell)(ell)o"
    print('  world '.strip())  # Strip leading and trailing whitespace; prints "world"
    ```

# 容器
- List：像数组一样是连续存储的，但是可以动态调整大小，并且可以存储不同类型的元素(内部实现是对象指针的数组)
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
- Dictionary
    ```python
    d = {'cat': 'cute', 'dog': 'furry'}  # Create a new dictionary with some data
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