### 简介

 `POST` 数据有时候会是很大的数据流 那如果后端不做 **异步** 接收数据的话就会拖性能  ，那就需要异步处理数据

#### 处理

一开始我是想着进了`routes`之后再接收数据这样子  ，一来是觉得匹配不上路由就没必要接收了  ，**BUT**这么写的话就会多次调用代码很不美观写的也很烦  ，最后还是在服务器的处理函数上写了

```javascript
const http = require('http');

const PORT = 5000;
const server = http.createServer((req, res) => {
  // 统一处理接收post数据
  const handlePostData = function () {
    console.log(
      '====================     handlePostData     ===================='
    );
    const promise = new Promise((resolve, reject) => {
    //创建一个空变量
      let data = '';
      req.on('data', (chunk) => {
        data += chunk.toString();
      });
      req.on('end', () => {
        if (!data) {
          resolve({});
          return;
        }
        resolve(JSON.parse(data));
        return;
      });
    });
    return promise;
  };

  handlePostData(req).then((postData) => {
    req.body = postData;

    // 博客相关的路由
    const apiDataPromise = handleRoute(req, res);
    
    // 未匹配到任何路由
    res.writeHead(404, { 'Content-Type': 'text/html; charset=utf-8' });
    res.write('404 not Found');
    res.end();
  });
});
server.listen(PORT, () => {
  console.log('serve running at port 5000');
});

```

**Tips:**可以这么理解post请求中如果传参的参数太大会 分批 接收数据  ，当最后一次接收的时候就会走`req.on('end',function(){})`表示接收完毕  ，我这里稍微处理了一下因为有些请求确实没有传参数  ，data就还是为空那么判断一下如果是空的话就`resolve({})`  ，并且在后面把`data`放进`req`里面带到路由处理器中  ，以便后续代码使用这个`data`