对象是由多个键/值对组成的无序的集合。对象中每个属性可以是任意类型的值。

定义对象可以使用构造函数或字面量的形式：

```
var obj = new Object;  //obj = {}
obj.name = "张三";  //添加描述
obj.say = function(){};  //添加行为

```

除了以上添加属性的方式，还可以使用`Object.defineProperty`定义新属性或修改原有的属性。

### Object.defineProperty()

#### 语法：

```
Object.defineProperty(obj, prop, descriptor)

```

**参数说明：**

1. obj：必需。目标对象
2. prop：必需。需定义或修改的属性的名字
3. descriptor：必需。目标属性所拥有的特性

**返回值：**

传入函数的对象。即第一个参数obj；

------

针对属性，我们可以给这个属性设置一些特性，比如是否只读不可以写；是否可以被for…in或Object.keys()遍历。

给对象的属性添加特性描述，目前提供两种形式：`数据描述`和`存取器描述`。

当修改或定义对象的某个属性的时候，给这个属性添加一些特性：

#### 数据描述：

```
var obj = {
    test:"hello"
}
//对象已有的属性添加特性描述
Object.defineProperty(obj,"test",{
    configurable:true | false,
    enumerable:true | false,
    value:任意类型的值,
    writable:true | false
});
//对象新添加的属性的特性描述
Object.defineProperty(obj,"newKey",{
    configurable:true | false,
    enumerable:true | false,
    value:任意类型的值,
    writable:true | false
});

```

数据描述中的属性都是可选的，来看一下设置每一个属性的作用。

**value**

属性对应的值,可以使任意类型的值，默认为undefined

```
var obj = {}
//第一种情况：不设置value属性
Object.defineProperty(obj,"newKey",{

});
console.log( obj.newKey );  //undefined
------------------------------
//第二种情况：设置value属性
Object.defineProperty(obj,"newKey",{
    value:"hello"
});
console.log( obj.newKey );  //hello

```

**writable**

属性的值是否可以被重写。设置为true可以被重写；设置为false，不能被重写。默认为false。

```
var obj = {}
//第一种情况：writable设置为false，不能重写。
Object.defineProperty(obj,"newKey",{
    value:"hello",
    writable:false
});
//更改newKey的值
obj.newKey = "change value";
console.log( obj.newKey );  //hello

//第二种情况：writable设置为true，可以重写
Object.defineProperty(obj,"newKey",{
    value:"hello",
    writable:true
});
//更改newKey的值
obj.newKey = "change value";
console.log( obj.newKey );  //ch

```

**enumerable**

此属性是否可以被枚举（使用for…in或Object.keys()）。设置为true可以被枚举；设置为false，不能被枚举。默认为false。

```
var obj = {}
//第一种情况：enumerable设置为false，不能被枚举。
Object.defineProperty(obj,"newKey",{
    value:"hello",
    writable:false,
    enumerable:false
});

//枚举对象的属性
for( var attr in obj ){
    console.log( attr );  //console不出来
}
//第二种情况：enumerable设置为true，可以被枚举。
Object.defineProperty(obj,"newKey",{
    value:"hello",
    writable:false,
    enumerable:true
});

//枚举对象的属性
for( var attr in obj ){
    console.log( attr );  //newKey
}

```

**configurable**

是否可以删除目标属性或是否可以再次修改属性的特性（writable, configurable, enumerable）。设置为true可以被删除或可以重新设置特性；设置为false，不能被可以被删除或不可以重新设置特性。默认为false。

这个属性起到两个作用：

目标属性是否可以使用delete删除

目标属性是否可以再次设置特性

```
//-----------------测试目标属性是否能被删除------------------------
var obj = {}
//第一种情况：configurable设置为false，不能被删除。
Object.defineProperty(obj,"newKey",{
    value:"hello",
    writable:false,
    enumerable:false,
    configurable:false
});
//删除属性
delete obj.newKey;
console.log( obj.newKey ); //hello

//第二种情况：configurable设置为true，可以被删除。
Object.defineProperty(obj,"newKey",{
    value:"hello",

```

除了可以给新定义的属性设置特性，也可以给已有的属性设置特性

```
//定义对象的时候添加的属性，是可删除、可重写、可枚举的。
var obj = {
    test:"hello"
}

//改写值
obj.test = 'change value';

console.log( obj.test ); //'change value'

Object.defineProperty(obj,"test",{
    writable:false
})


//再次改写值
obj.test = 'change value again';

console.log( obj.test ); //依然是：'change value'

```

提示：一旦使用Object.defineProperty给对象添加属性，那么如果不设置属性的特性，那么configurable、enumerable、writable这些值都为默认的false

```
var obj = {};
//定义的新属性后，这个属性的特性中configurable，enumerable，writable都为默认的值false
//这就导致了neykey这个是不能重写、不能枚举、不能再次设置特性
//
Object.defineProperty(obj,'newKey',{

});

//设置值
obj.newKey = 'hello';
console.log(obj.newKey);  //undefined

//枚举
for( var attr in obj ){
    console.log(attr);
}

```

### 存取器描述：

注：当使用了getter或setter方法，不允许使用writable和value这两个属性

```
var obj = {};
var initValue = 'hello';
Object.defineProperty(obj,"newKey",{
    get:function (){
        //当获取值的时候触发的函数
        return initValue;    
    },
    set:function (value){
        //当设置值的时候触发的函数,设置的新值通过参数value拿到
        initValue = value;
    }
});
//获取值
console.log( obj.newKey );  //hello

//设置值
obj.newKey = 'change value';

console.log( obj.newKey ); //change value

```

![defineProperty](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\defineProperty.png)

##### 总结：

对于对象上已经有的属性，可以通过Object.defineProperty() 第三个参数设置该属性的一些特性，即是否可写，是否可迭代等。
对于对象上没有的属性，我们可以通过Object.defineProperty()来给该对象添加属性。