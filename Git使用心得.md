# Git使用心得
Git来管理代码是必须的，这里记录下来常用的命令。
## 首次配置
```bash
git config --global user.name "yuzhangqu"
git config --global user.email yuzhangqu@qq.com
git config credential.helper store
```

## 提交更改
```bash
git add .
git commit -m "XXX"
git push
```

## 放弃本地更改
```bash
git clean -df
git reset --hard
```

## 回退文件到某个版本
```bash
git checkout VERSION -- file1/to/restore file2/to/restore
```
