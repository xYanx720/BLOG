### onreadystatechange

```js
let request = new XMLHttpRequest();
```

在 `onreadystatechange` 中 打印 `request.readyState` 会输出3个值：2、3、4

### onload

在 `onload` 中 打印 `request.readyState` 只会出现 **4** 原因是onload只会在可以响应的时候触发

#### readyState 状态码

- 0：请求未初始化
- 1：服务器连接已建立
- 2：请求已接收
- 3：请求处理中
- 4：请求已完成，且响应已就绪

#### HTTP 状态码

- 200：服务器成功返回网页
- 404：请求的网页不存在
- 503：服务器暂时不可用