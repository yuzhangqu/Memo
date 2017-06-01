# Excel技巧
## 身份证最后一位校验
```
=EXACT(INDEX(Sheet2!B$1:B$11,MOD(MID(E6,1,1)*7+MID(E6,2,1)*9+MID(E6,3,1)*10+MID(E6,4,1)*5+MID(E6,5,1)*8+MID(E6,6,1)*4+MID(E6,7,1)*2+MID(E6,8,1)*1+MID(E6,9,1)*6+MID(E6,10,1)*3+MID(E6,11,1)*7+MID(E6,12,1)*9+MID(E6,13,1)*10+MID(E6,14,1)*5+MID(E6,15,1)*8+MID(E6,16,1)*4+MID(E6,17,1)*2,11)+1),MID(E6,18,1))
```

## 打印时每一份序号递增
```VB
Sub 打印()
Dim startnum, loopnum, N As Long                                '定义变量：起始编码，打印份数和循环值
startnum = Application.InputBox(Prompt:="起始号码？", Type:=1)  '定义起始号码
loopnum = Application.InputBox(Prompt:="多少份？", Type:=1)     '定义打印份数
For N = startnum To startnum + loopnum - 1                      '开始循环
Range("J1") = N                                                 '设置考号
ActiveSheet.PrintOut                                            '打印当前表格
Next N                                                          '下一个循环直到结束
End Sub
```