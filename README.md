#### ajax
Jesse James Garrett 将如下技术取名叫做 AJAX：异步的 JavaScript 和 XML
（async javascript and xml）

1. 使用 XMLHttpRequest 发请求
2. 服务器返回 XML 格式的字符串
3. JS 解析 XML，并更新局部页面
* 注：以前前是返回并解析xml格式，现在用的是json格式

#### 同源策略 & CORS

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