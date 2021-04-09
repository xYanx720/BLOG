## JSON

#### 定义

`json` 是一种特殊的字符串个是，本质是一个字符串

```javascript
var jsonObj = '{ "name": "Jack", "age": 18, "gender": "男" }';
var jsonArr =
  '[{ "name": "Jack", "age": 18, "gender": "男" }, { "name": "Jack", "age": 18, "gender": "男" }, { "name": "Jack", "age": 18, "gender": "男" }]';
```

就是对象内部的 `key` 和 `value` 都用双引号包裹的字符串（必须是双引号）

#### 方法

- `JSON.parse`将 JSON 格式转换为对象或者数组（具体看 json 本身的格式）

  ```js
  var jsonObj = '{ "name": "Jack", "age": 18, "gender": "男" }';
  var jsonArr =
    '[{ "name": "Jack", "age": 18, "gender": "男" }, { "name": "Jack", "age": 18, "gender": "男" }, { "name": "Jack", "age": 18, "gender": "男" }]';

  var obj = JSON.parse(jsonStr);
  var arr = JSON.parse(jsonArr);

  console.log(obj);
  console.log(arr);
  ```

- `JSON.stringify`将对象或者数组转为 json 格式

  ```javascript
  var obj = {
    name: 'Jack',
    age: 18,
    gender: '男',
  };
  var arr = [
    {
      name: 'Jack',
      age: 18,
      gender: '男',
    },
    {
      name: 'Jack',
      age: 18,
      gender: '男',
    },
    {
      name: 'Jack',
      age: 18,
      gender: '男',
    },
  ];

  var jsonObj = JSON.stringify(obj);
  var jsonArr = JSON.stringify(arr);

  console.log(jsonObj);
  console.log(jsonArr);
  ```

## this

- 在全局作用域之下 **`this`** 指向全局 （若 js 作用于 html 中，则指向 winodw）

  ```js
  function fn() {
    console.log(this);
  }
  fn();
  // 此时 this 指向 window
  ```

  ```js
  var obj = {
    fn: function () {
      console.log(this);
    },
  };
  obj.fn();
  // 此时 this 指向 obj
  ```

- 处理例如延时器 `setTimeout` 或者定时器 `setInterval` 时

  ```js
  setTimeout(function () {
    console.log(this);
  }, 0);
  // 此时定时器处理函数里面的 this 指向 window
  ```

- 处理事件指向事件源

  ```js
  div.onclick = function () {
    console.log(this);
  };
  // 当你点击 div 的时候，this 指向 div
  ```

- 自调用函数指向 window

  ```js
  (function () {
    console.log(this);
  })();
  // 此时 this 指向 window
  ```

###### 附属：强行改变 this 指向的方法

- **call / apply / bind**
- 这三个方法都会用第一个参数去调用前面的方法 实现代替执行的效果 所以会强制改变 this 的指向

## let 和 const 关键字

- 我们以前都是使用 `var` 关键字来声明变量的

- 在 ES6 的时候，多了两个关键字 `let` 和 `const`，也是用来声明变量的

- 只不过和 var 有一些区别

  1.  `let` 和 `const` 不允许重复声明变量

  ```javascript
  // 使用 var 的时候重复声明变量是没问题的，只不过就是后面会把前面覆盖掉
  var num = 100;
  var num = 200;
  ```

  ```javascript
  // 使用 let 重复声明变量的时候就会报错了
  let num = 100;
  let num = 200; // 这里就会报错了
  ```

  ```javascript
  // 使用 const 重复声明变量的时候就会报错
  const num = 100;
  const num = 200; // 这里就会报错了
  ```

  2. `let` 和 `const` 声明的变量不会在预解析的时候解析（也就是没有变量提升）

     ```javascript
     // 因为预解析（变量提升）的原因，在前面是有这个变量的，只不过没有赋值
     console.log(num); // undefined
     var num = 100;
     ```

     ```javascript
     // 因为 let 不会进行预解析（变量提升），所以直接报错了
     console.log(num); // undefined
     let num = 100;
     ```

     ```javascript
     // 因为 const 不会进行预解析（变量提升），所以直接报错了
     console.log(num); // undefined
     const num = 100;
     ```

  3. `let` 和 `const` 声明的变量会被所有代码块限制作用范围

     ```javascript
     // var 声明的变量只有函数能限制其作用域，其他的不能限制
     if (true) {
       var num = 100;
     }
     console.log(num); // 100
     ```

     ```javascript
     // let 声明的变量，除了函数可以限制，所有的代码块都可以限制其作用域（if/while/for/...）
     if (true) {
       let num = 100;
       console.log(num); // 100
     }
     console.log(num); // 报错
     ```

     ```javascript
     // const 声明的变量，除了函数可以限制，所有的代码块都可以限制其作用域（if/while/for/...）
     if (true) {
       const num = 100;
       console.log(num); // 100
     }
     console.log(num); // 报错
     ```

- `let` 和 `const` 的区别

  1. `let` 声明的变量的值可以改变，`const` 声明的变量的值不可以改变

     ```javascript
     let num = 100;
     num = 200;
     console.log(num); // 200
     ```

     ```javascript
     const num = 100;
     num = 200; // 这里就会报错了，因为 const 声明的变量值不可以改变（我们也叫做常量）
     ```

  2. `let` 声明的时候可以不赋值，`const` 声明的时候必须赋值

     ```javascript
     let num;
     num = 100;
     console.log(num); // 100
     ```

     ```javascript
     const num; // 这里就会报错了，因为 const 声明的时候必须赋值
     ```

## 箭头函数

#### 特点

- 没有内部 **`this`** 意思是不会改变 this 指向 原来指向哪里 还是指向哪里
- 没有**`arguments`**
- 当只需要传一个参数的时候可以不写 **`()`**
- 当函数内只有一句语句时 可以不用写 **`return`**

## 解构赋值

#### 对象

```js
// ES5 的方法向得到对象中的成员
const obj = {
  name: 'Jack',
  age: 18,
  gender: '男',
};

let name = obj.name;
let age = obj.age;
let gender = obj.gender;
```

```js
// 解构赋值的方式从对象中获取成员
const obj = {
  name: 'Jack',
  age: 18,
  gender: '男',
};

// 前面的 {} 表示我要从 obj 这个对象中获取成员了
// name age gender 都得是 obj 中有的成员
// obj 必须是一个对象
let { name, age, gender } = obj;
```

#### 数组

```js
// ES5 的方式从数组中获取成员
const arr = ['Jack', 'Rose', 'Tom'];
let a = arr[0];
let b = arr[1];
let c = arr[2];
```

```js
// 使用解构赋值的方式从数组中获取成员
const arr = ['Jack', 'Rose', 'Tom'];

// 前面的 [] 表示要从 arr 这个数组中获取成员了
// a b c 分别对应这数组中的索引 0 1 2
// arr 必须是一个数组
let [a, b, c] = arr;
```

###### 注意

- `{}` 是专门解构对象使用的
- `[]` 是专门解构数组使用的
- 不能混用

## 展开运算符

- ES6 里面号新添加了一个运算符 `...` ，叫做展开运算符

- 作用是把数组展开

  ```javascript
  let arr = [1, 2, 3, 4, 5];
  console.log(...arr); // 1 2 3 4 5
  ```

- 合并数组的时候可以使用

  ```javascript
  let arr = [1, 2, 3, 4];
  let arr2 = [...arr, 5];
  console.log(arr2);
  ```

- 也可以合并对象使用

  ```javascript
  let obj = {
    name: 'Jack',
    age: 18,
  };
  let obj2 = {
    ...obj,
    gender: '男',
  };
  console.log(obj2);
  ```

- 在函数传递参数的时候也可以使用

  ```javascript
  let arr = [1, 2, 3];
  function fn(a, b, c) {
    console.log(a);
    console.log(b);
    console.log(c);
  }
  fn(...arr);
  // 等价于 fn(1, 2, 3)
  ```

![image-20210312153121490](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\ES5&es6.png)

