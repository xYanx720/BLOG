### 简介

cookies操作示范



#### 代码

**安装**

```
npm install cookies
```

**引入**

```js
const Cookies = require('cookies');
```

**使用**

```js
	// cookies进行签名（加密）
    let keys = ['keyboardCat'];

    let cookies = new Cookies(req, res, { keys: keys });
    // console.log(cookies);

    // 设置cookie('键名','值','有效期')
    cookies.set('LastVisit', new Date().getTime(), { signed: true });
    cookies.set('k1', 'v1', { signed: true,maxAge:0 }); //永久有效
    cookies.set('k3', 'v3', { signed: true,maxAge:-1 }); //删除cookie
    cookies.set('k2', 'v2',{ signed: true,maxAge:60000*60*24*7 }); //单位毫秒，有效期为7天

    // 获取cookie,new Cookies时设置了签名，获取时也要进行签名认证
    let lastVisit = cookies.get('LastVisit', { signed: true });
    // let lastVisit2 = cookies.get('LastVisit' );
    console.log(lastVisit);
    // console.log(lastVisit2);
```

