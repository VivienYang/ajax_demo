#### AJAX
Jesse James Garrett 将如下技术取名叫做 AJAX：异步的 JavaScript 和 XML
（async javascript and xml）

1. 使用 XMLHttpRequest 发请求
2. 服务器返回 XML 格式的字符串
3. JS 解析 XML，并更新局部页面
* 注：以前前是返回并解析xml格式，现在用的是json格式

#### 同源策略 & CORS
只有 协议+端口+域名 一模一样才允许发 AJAX 请求
一模一样一模一样一模一样一模一样一模一样一模一样一模一样一模一样

1. http://baidu.com 可以向 http://www.baidu.com 发 AJAX 请求吗 no
2. http://baidu.com:80 可以向 http://baidu.com:81 发 AJAX 请求吗 no

突破同源策略 === 跨域(Cross-Origin Resource Sharing)
* C O源 R S
* 跨源资源共享

jack.com在响应的时候，header里面加上Access-Control-Allow-Origin:http://www.frank.com:8001就可以让frank.com请求jack.com了
```
response.setHeader('Access-Control-Allow-Origin','http://www.frank.com:8001')
response.setHeader('Access-Control-Allow-Origin',*)
```
##### 浏览器必须保证
1. 只有 协议+端口+域名 一模一样才允许发 AJAX 请求
2. CORS 可以告诉浏览器，我俩一家的，别阻止他
#### 原生js发送ajax
```
let request = new XMLHttpRequest()  //step1:new一个XMLHttpRequest对象
request.open('get','/xxx')  //step2:配置request
request.send()  //step3:发送这个请求
request.onreadystatechange=()=>{  //step4:监听readystate变化
  if(request.readyState===4){  //readystate为4表示已经完整收到了响应
    if(request.status >= 200 && request.status<300){  //判断status
      let string = request.responseText  //获取响应的字符串
      let object = window.JSON.parse(string)  //将json格式的字符串转化为js对象
    }
  }
}
```