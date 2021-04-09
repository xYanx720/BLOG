#### 安装

```
npm install mysql
```

#### 引入

```js
const mysql = require('mysql');
```

#### 初始化

**db.js**

```js
let MYSQL_CONFIG = {};


MYSQL_CONFIG = {
  
    host: 'localhost',
    user: 'root',
    password: 'adminadmin',
    port: 3306,
    database: 'homework',
  
};

module.exports = {
  MYSQL_CONFIG
}
```

**mysql.js**

```js
const { MYSQL_CONFIG } = require('../config/db');

// 创建连接对象
const connection = mysql.createConnection(MYSQL_CONFIG);
```

#### 连接

```js
connection.connect();
```

#### 封装执行sql语句

```js
/**
 * @param {string} sql sql语句
 * @return {Promise}
 *注：mysql这里的回调函数就是先err再result的
 */
function execSQL(sql) {
  const promise = new Promise((resolve, reject) => {
    connection.query(sql, (err, result) => {
      if (err) {
        reject(err);
        return;
      }

      resolve(result);
    });
  });
  return promise;
}
```

#### 关闭连接

```js
// 关闭连接
connection.end();
```

#### 抛出方法模块

```js
module.exports = {
  execSQL,
};
```

