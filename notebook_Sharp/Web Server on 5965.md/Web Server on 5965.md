# Web Server on 5965

```html
kali㉿kali $ curl -v http://10.10.10.219:5985/
*   Trying 10.10.10.219:5985...
* Connected to 10.10.10.219 (10.10.10.219) port 5985 (#0)
> GET / HTTP/1.1
> Host: 10.10.10.219:5985
> User-Agent: curl/7.74.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 404 Not Found
< Content-Type: text/html; charset=us-ascii
< Server: Microsoft-HTTPAPI/2.0
< Date: Sat, 17 Apr 2021 12:34:59 GMT
< Connection: close
< Content-Length: 315
< 
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN""http://www.w3.org/TR/html4/strict.dtd">
<HTML><HEAD><TITLE>Not Found</TITLE>
<META HTTP-EQUIV="Content-Type" Content="text/html; charset=us-ascii"></HEAD>
<BODY><h2>Not Found</h2>
<hr><p>HTTP Error 404. The requested resource is not found.</p>
</BODY></HTML>
* Closing connection 0
```