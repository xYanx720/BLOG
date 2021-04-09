### 简介

使用 nodejs 时 当前端发起请求时 其实在network可以看到有两次请求：

**！！** 当第一次`OPTIONS`请求200时，才会执行接下来的 `POST` || `GET` 请求 **！！**

#### 解决方法

```javascript
const http = require('http');

const PORT = 5000;
const server = http.createServer((req, res) => {
  // 处理 OPTIONS 请求
  if (req.method === 'OPTIONS') {
    // 回复OPTIONS
    res.writeHead(200, {
      'Content-Type': 'text/plain',
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Headers':
        'Content-Type, Content-Length, Authorization, Accept, X-Requested-With , yourHeaderFeild, sessionToken',
      'Access-Control-Allow-Methods': 'PUT, POST, GET, DELETE, OPTIONS',
    });
    res.end('');
    return;
  }
});
server.listen(PORT, () => {
  console.log('serve running at port 5000');
});

```

