---
description: python 내장 되어 있는 심플 http 서버
---

# simple cgi server

simple http server

```text
$ python -m http.server --cgi 8080
```

web browser 에서 [http://localhost:8080](http://localhost:8080) 을 입력한다.

### Directory listing for /

* .android/
* .AnySign4PC/
* .atom/
* .bash\_history
* .bash\_profile
* .bash\_sessions
* .config/
* .cups/
* .dbeaver-drivers/
* .dbeaver4/
* .delfino.conf

## python script 

```text
import http.server
import socketserver

Handler = http.server.CGIHTTPRequestHandler

http = socketserver.TCPServer(("", 8080), Handler)
http.server_name = "localhost"
http.server_port = 8080
http.serve_forever()
```



