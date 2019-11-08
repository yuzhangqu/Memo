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