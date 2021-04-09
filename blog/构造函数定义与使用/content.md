![image-20210317211723201](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210317211723201.png)

## 构造函数的定义和使用

思路来源:https://www.jianshu.com/p/7e21e23ffba9

##### 意义

假如现在需要录入60个同学的属性，写60次对象 则意味着name，age，gender之类的属性名需要写很多次，体力活没意义；

所以如果有一个函数能通过传入的参数返回一个独立的对象个体那就很 **彳亍**

然后就出现了构造函数

```
//old
var p1 = { name: 'zs', age: 6, gender: '男', hobby: 'basketball' };
var p2 = { name: 'ls', age: 6, gender: '女', hobby: 'dancing' };
var p3 = { name: 'ww', age: 6, gender: '女', hobby: 'singing' };
var p4 = { name: 'zl', age: 6, gender: '男', hobby: 'football' };
```

```
//new
function Person(name, gender, hobby) {
    this.name = name;
    this.gender = gender;
    this.hobby = hobby;
    this.age = 6;
}

var p1 = new Person('zs', '男', 'basketball');
var p2 = new Person('ls', '女', 'dancing');
var p3 = new Person('ww', '女', 'singing');
var p4 = new Person('zl', '男', 'football');
```

#### 执行过程

当函数创建好之后如果不加 **new** 关键字 则就不知道是不是构造函数 ，所以只有 **new** 了我们才能称之为构造函数

```
function Person(name, gender, hobby) {
 this.name = name;
 this.gender = gender;
 this.hobby = hobby;
 this.age = 6;
}

var p1 = new Person('zs', '男', 'basketball');
```

此时，构造函数会有以下几个执行过程：

1. 当以 new 关键字调用时，会创建一个新的内存空间，标记为 Animal 的实例。
2. 函数体内部的 this 指向该内存

通过以上两步，我们就可以得出这样的结论。

```
var p2 = new Person('ls', '女', 'dancing');  // 创建一个新的内存 #f2
var p3 = new Person('ww', '女', 'singing');  // 创建一个新的内存 #f3
```

每当创建一个实例的时候，就会创建一个新的内存空间(#f2, #f3)，创建 #f2 的时候，函数体内部的 this 指向 #f2, 创建 #f3 的时候，函数体内部的 this 指向 #f3。

3. 执行函数体内的代码
 通过上面的讲解，你就可以知道，给 this 添加属性，就相当于给实例添加属性。

4. 默认返回 this

由于函数体内部的this指向新创建的内存空间，默认返回 this ，就相当于默认返回了该内存空间，也就是上图中的 #f1。此时，#f1的内存空间被变量p1所接受。也就是说 p1 这个变量，保存的内存地址就是 #f1，同时被标记为 Person 的实例。

以上就是构造函数的整个执行过程。

#### 构造函数的返回值

 构造函数执行过程的最后一步是默认返回 this 。言外之意，构造函数的返回值还有其它情况。下面我们就来聊聊关于构造函数返回值的问题。

**Ps**  没有手动添加返回值，默认返回 this

- 手动添加一个基本数据类型的返回值，最终还是返回 this

  ```
  function Person2() {
   this.age = 28;
   return 50;
  }
  
  var p2 = new Person2();
  console.log(p2.age);   // 28
  p2: {
   age: 28
  }
  ```

- 手动添加一个复杂数据类型(对象)的返回值，最终返回该对象

  ```
  function Person3() {
   this.height = '180';
   return ['a', 'b', 'c'];
  }
  
  var p3 = new Person3();
  console.log(p3.height);  // undefined
  console.log(p3.length);  // 3
  console.log(p3[0]);      // 'a'
  ```

  ```
  function Person4() {
    this.gender = '男';
    return { gender: '中性' };
  }
  
  var p4 = new Person4();
  console.log(p4.gender);  // '中性'
  ```

  

------

### 为构造函数添加方法

1. 在Person.prototype里添加方法

   ```
   function Person(name, age) {
           this.name = name;
           this.age = age;
         }
         Person.prototype = {
           say() {
             console.log(this.name);
           },
           print() {
             console.log(this);
           },
         };
   ```

2. 在构造函数内部使用 this.\__proto__ (个人喜欢把东西都放在构造函数内 但是似乎这么写不好)

   ```
   function Hero(name, age) {
           this.name = name;
           this.age = age;
           this.__proto__ = {
             say() {
               console.log(this.name);
             },
             print() {
               console.log(this);
             },
           };
         }
   ```

   

### 对象中的两个关键字

- **isPrototypeOf( 实例 )** 判断当前原型对象 是否在传入实例对象的原型链上面

  ```js
  //检测一个对象是否存在于另一个对象的原型链中，如果存在就返回 true，否则就返回 false
  
  prototypeObject.isPrototypeOf(object);
  ```

  

- **instanceof** 判断一个对象是否是一个构造函数的实例

  ```js
  object instanceof constructor
  
  //object：某个实例对象     constructor：某个构造函数
  
  //用来检测  constructor.prototype 是否存在于参数  object 的原型链上。
  ```

  

