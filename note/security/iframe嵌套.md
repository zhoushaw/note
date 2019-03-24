
## 避免其他网站嵌入iframe

**配置http响应头**

> X-Frame-Options 响应头有三个可选的值:

* DENY:页面不能被嵌入到任何iframe或frame中；
* SAMEORIGIN:页面只能被本站页面嵌入到iframe或者frame中；
* ALLOW-FROM:页面允许frame或frame加载。

> 在服务端设置的方式如下:

```
//Java代码:
response.addHeader("x-frame-options","SAMEORIGIN");
// Nginx配置:
add_header X-Frame-Options SAMEORIGIN
//Apache配置:
Header always append X-Frame-Options SAMEORIGIN
```


