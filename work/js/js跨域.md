[http://query.yahooapis.com/v1/public/yql](http://query.yahooapis.com/v1/public/yql)

XMLHttpRequest2 进行跨域访问时需要服务器许可，不是任何域都接受跨域请求的。先来看一下从 Yahoo YQL 域返回的响应头（Response Header ）：

注意里面有一条标识 Access-Control-Allow-Origin:* ，这就表示允许跨域访问，所以可以正常访问该域，而对于其他没有该标识的域就会出现禁止访问提示。 

那么如何设置呢？如果要接受跨域访问请求，就必须在服务器端返回的资源中加入 Access-Control-Allow-Origin 头标识， Access-Control-Allow-Origin 的值可以是 URL 或 *，如果是 URL 则只会允许来自该 URL 的请求，* 则允许任何域的请求。比如，在 HTML 中可以设置：

在 HTML 中可以设置
```html
<meta http-equiv="Access-Control-Allow-Origin" content="*">
```

java code
```Java
response.setHeader("Access-Control-Allow-Origin", "*");
```


各种语言实现参考：[http://stackoverflow.com/questions/10143093/origin-is-not-allowed-by-access-control-allow-origin/10143166#10143166](http://stackoverflow.com/questions/10143093/origin-is-not-allowed-by-access-control-allow-origin/10143166#10143166)