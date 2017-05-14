# Django学习笔记
这里记录Django框架的学习心得，以免以后忘记了。

## 安装Python3
Django是`python`框架，`python`肯定是要有的。虽然`Mac`自带`python 2.7`，但是作为一个刚刚入行的新手，完全应该顺应时代的召唤，安装最新版的`python`(我当时装的是`3.6.1`版本)。

```
brew update
brew doctor
brew install python3
```

安装好之后，有了`python3`和`pip3`，使用起来不是很方便。这要用到`python 3.6`自带的`venv`模块。

```
python3 -m venv /path/to/new/virtual/environment
```

激活虚拟环境之后，`python`和`pip`就是带`3`的版本了。

```
source /path/to/new/virtual/environment／bin/activate  // 激活
deactivate  // 去激活
```
## 安装Django
```
pip install Django
```