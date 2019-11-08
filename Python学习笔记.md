# 基本概念
- Python是一门面向对象的语言
- 在Python中严格区分大小写
- Python中的每一行就是一条语句，每条语句以换行结束
- 一条语句可以分多行编写，多行编写时语句后边以`\`结尾
- Python是缩进严格的语言，所以在Python中不要随便写缩进
- 在Python中使用`#`来表示注释

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