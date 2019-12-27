# Socket
- Socket是一种通用的网络编程接口
- Socket是应用层与传输层之间的桥梁
- Python提供socket.py标准库，但是非常底层
- AF(Address Family)协议族
    - AF_INET：IPV4
    - AF_INET6：IPV6
    - AF_UNIX：Unix Domain Socket，Windows没有
- Socket类型
    - SOCK_STREAM：面向连接的流套接字。默认值，TCP协议
    - SOCK_DGRAM：无连接的数据报文套接字。UDP协议

## TCP模式
- 服务端
    ```python
    import socket

    server = socket.socket()
    server.bind(('0.0.0.0', 9999))
    server.listen()  # ss -tan 可以看到0.0.0.0:9999端口是LISTEN状态
    print('Waiting client...')
    conn, addr = server.accept()  # 阻塞直到有客户端连接，客户端连接时为其分配一个新socket，此时可以看到172.168.1.1:9999是ESTAB状态
    print(addr, 'has connected.')
    data = conn.recv(1024)  # 从缓冲区中取出最多1024字节的bytes数据，如果缓冲区为空，则阻塞。如果连接close了，读完缓冲区之后，返回b''
    while data:
        conn.send('RECEIVE:{}'.format(data.decode()).encode())  # 发送bytes对象到客户端。bytes.decode()得到str，str.encode()得到bytes
        data = conn.recv(1024)
    print('Server disconnected.')
    conn.close()  # 服务端先关闭，管道进入TIME-WAIT状态；如果客户端先关闭，管道进入CLOSE-WAIT状态
    server.close()
    ```
- 客户端
    ```python
    import socket
    client = socket.socket()
    client.connect(('172.168.1.1', 9999))
    msg = input('SEND:')
    while msg:
        client.send(msg.encode())  # 发送bytes对象到服务端
        data = client.recv(1024)  # 从缓冲区中取出最多1024字节的数据，如果缓冲区为空，则阻塞
        print(data.decode())
        msg = input('SEND:')
    print('Client disconnected.')
    client.close()
    ```

## socket库
- `socket.getsockname()`：获取自己的地址，返回二元组(ip, port)
- `socket.getpeername()`：获取远端的地址
- `socket.setblocking(flag)`：如果`flag`为0，则将套接字设为非阻塞模式
- `socket.setsockopt(level, optname, value)`：设置套接字选项的值。比如缓冲区大小等
- `socket.makefile(mode='r', buffering=None, *, encoding=None, errors=None, newline=None)`：用socket造一个文件，不用操作bytes了，可以用string

## HTTP协议
- 无状态：可以通过cookie、session来判断
- 有连接：基于TCP协议，面向连接的，需要3次握手、4次断开
- 短连接：自HTTP/1.1开始，支持`Connection: keep-alive`，默认开启，一个连接打开后，会保持一段时间（可配置），浏览器再访问该服务器就会用这个TCP连接
- cookie：键值对信息
    - 一般cookie信息是在服务端生成，返回给客户端的
    - 客户端可以自己设置cookie信息
    - 浏览器发起每一个请求，都会把cookie信息发给服务端
- url：uniform resource locator
    - `schema://host[:port#]/path/.../[?query-string][#anchor]`
- Request：浏览器向服务器发起的请求
    - 第一行是请求消息行：`请求方法（Method：GET、POST、HEAD等） 请求路径 协议版本CRLF`
    - 后面是各种键值对：`Host`、`User-Agent`、`Cookie`等（`X-`开头的是自己定义的）
    - 如果是表单提交，请求头中会有`Content-Type: application/x-www-form-urlencoded`，此时表单数据在最后一个键值对的两个`CRLF`之后(Body)
    - Restful风格，信息就在请求路径中
- Response：响应
    - 第一行是响应消息行：`协议版本 状态码 消息描述CRLF`
        - 1XX：提示信息，表示请求已被成功接收，继续处理
        - 2XX：表示正常响应
            - 200：正常返回了网页内容
        - 3XX：重定向
            - 301：页面永久性移走，永久重定向。返回新的URL，浏览器会根据返回的URL发起新的Request
            - 302：临时重定向
            - 304：资源未修改，浏览器使用本地缓存
        - 4XX：客户端请求错误
            - 400：请求语法错误
            - 401：请求要求身份验证（如：验证没通过）
            - 403：服务器拒绝请求（如：权限不够）
            - 404：Not Found，客户端请求的资源找不到
            - 405：Method Not Allowed
        - 5XX：服务端错误
            - 500：服务器内部错误
            - 502：上游服务器错误，例如Nginx反向代理的时候
    - 后面是各种键值对：`Content-Type: text/html;charset=utf-8`等

## WSGI协议
- WSGI解决的是WSGI Server与WSGI App之间的接口问题
- WSGI Server
    - 监听HTTP服务端口（TCPServer，默认端口80）
    - 接收浏览器端的HTTP请求并解析封装成environ环境数据（包含HTTP请求的Dict对象）
    - 负责调用应用程序，将environ和start_response(status, response_headers, exc_info=None)方法传入
    - 将应用程序响应的正文封装成HTTP响应报文返回浏览器端
- WSGI App需要响应状态码和响应头，返回一个可迭代对象，正文就是这个列表的元素
    - 应用程序需要是一个可调用对象：函数、类、实现了`__call__`方法的类的实例
    - 这个可调用对象应该接收两个参数
- wsgiref是一个WSGI参考实现库，一个简单的程序如下
```python
from wsgiref.simple_server import make_server, demo_app

with make_server('0.0.0.0', 8000, demo_app) as httpd:
    httpd.serve_forever()
```
- 测试命令curl
    - `-I`：HEAD方法
    - `-X`：指定方法`-X POST URL -d '{"key":value}'`
- `urllib.parse.parse_qs()`：解析查询字符串
- `webob`：封装了WSGI的请求响应对象
    - 请求
    ```python
    # Request(environ)
    from webob import Request
    request = Request(environ)
    print(request.method)
    print(request.path)
    print(request.GET)  # query string中的参数存在GetDict对象中
    print(request.POST)  # 表单中的参数存在MultiDict对象中
    print(request.params)  # 上面两个集中在这一个NestedMultiDict对象中
    ```
    - 响应
    ```python
    # Response(body=None, status=None, 略)
    res = Response()
    res.body = '<h1>Hello world!</h1>'.encode()
    return res(env, sr)
    ```
    - wsgify
    ```python
    # wsgify是一个类装饰器，将实例绑定到app上
    # wsgify实现了__call__魔术方法，满足wsgi协议，接收参数：environ和start_response
    # wsgify的__call__魔术方法利用environ构建Request实例，并调用被装饰函数
    # 被装饰函数可以直接返回Response的实例，也可以是str类型（会按照给定编码转成bytes）或bytes类型（会创建一个实例并将bytes写入body中），最终都会返回Response的实例
    # wsgify的__call__魔术方法调用Response实例并返回：return resp(environ, start_response)
    # Response的__call__魔术方法，满足了wsgi的接口要求（调用start_response并返回可迭代对象）
    from webob.dec import wsgify
    @wsgify
    def app(request):
        return Response('<h1>Hello World!</h1>')
    ```