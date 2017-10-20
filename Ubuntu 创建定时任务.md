# Ubuntu 创建定时任务
使用`crontab`模块可以实现定时任务要求
## crontab规则
```shell
#<分钟> <小时> <日> <月份> <星期> <命令>
```

## crontab用法
1. 创建自己的cron文件`MyCrontab`，输入自己的规则
2. `crontab MyCrontab`装载
3. `crontab -l`查看

## API获取IP地址
http://ip.chinaz.com/getip.aspx

```JSON
{
	ip:'121.60.106.130',
	address:'湖北省武汉市 电信'
}
```
