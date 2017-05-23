# Base64使用记录
## 下载动态生成的CSV文件
用JS代码，设置`<a>`标签的`href`为`"data:application/csv;charset=UTF-8,BASE64"`

## 播放Beep音效
```js
var snd = new Audio("data:audio/wav;base64,BASE64");
snd.play();
```

## 如何将wav文件转为Base64
将普通字符串转换为Base64有很多在线的工具可用。那么如何转换文件呢？使用Python是其中一种方法。

```python
from base64 import b64encode

f = open("beep.wav", "rb")
enc = b64encode(f.read())  // enc中存放着Base64
f.close()

output = open("output.txt", "wb")
output.write(enc)
output.close()
```