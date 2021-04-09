## 构造函数、对象原型、实例对象三者之间的关系

- 每创建一个 **function** 都会自带一个 **prototype** 属性，该属性指向一个对象，就是原型对象

  ```
  function => prototype
  ```

- 原型对象上有一个属性 **constructor** ，指向相关联的构造函数

  ```
  原型对象 => constructor
  ```

- **构造函数** 产生的 **实例对象**， 拥有一个内部属性，指向原型对象，这样子 **实例对象** 就可以访问到 **原型对象** 上的所有方法和属性



------



### 上代码！！！！

```
function People(name){
	this.name = name;
}
People.prototype.print = function(){
	console.log(this.name);
}

let son = new People('儿子');
son.print();//儿子
```

> 上方代码定义了构造函数**People()** , **People.prototype**指向原型对象，原型对象有个 **construtor** 属性又指回 **People()**
>
>
> 使用 **People()**  new出来的实例对象由于自带的内部指针指向了原型对象，所以实例对象也能访问我们设置在原型对象上的**print**方法

之间的关系大概就是下面的样子

















![image-20210317201803490](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210317201803490.png)