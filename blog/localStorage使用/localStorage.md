## What is localStorage

在HTML5中，新加入一个localStorage属性，这个特性主要是用来作为本地存储来使用的，解决了cookie存储空间不足的问题（cookie中每条cookie的存储空间为4k），localStorage中一般浏览器支持的是5M大小，这个在不同的浏览器中localStorage会有所不同。

### localStorage 的特性

#### 优势

- localStorage拓展了cookie的4K限制
- localStorage会可以将第一次请求的数据直接存储到本地，这个相当于一个5M大小的针对于前端页面的数据库，相比于cookie可以节约带宽，但是这个却是只有在高版本的浏览器中才支持的

#### 局限

- 浏览器的大小不统一，并且在IE8以上的IE版本才支持localStorage这个属性
- 目前所有的浏览器中都会把localStorage的值类型限定为string类型，这个在对我们日常比较常见的JSON对象类型需要一些转换
- localStorage在浏览器的隐私模式下面是不可读取的
- localStorage本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，会导致页面变卡
- localStorage不能被爬虫抓取到
   localStorage与sessionStorage的唯一一点区别就是localStorage属于永久性存储，而sessionStorage属于当会话结束的时候，sessionStorage中的键值对会被清空
   这里我们以localStorage来分析

### 代码层使用

#### 写入

localStorage的写入，localStorage的写入有三种方法

**Tips:** 这里要特别说明一下localStorage的使用也是遵循同源策略的，所以不同的网站直接是不能共用相同的localStorage

```js
if(！window.localStorage){
            alert("浏览器不支持localstorage");
            return false;
        }else{
            var storage=window.localStorage;
            //写入a字段
            storage["a"]=1;
            //写入b字段
            storage.b=1;
            //写入c字段
            storage.setItem("c",3);
            console.log(typeof storage["a"]);
            console.log(typeof storage["b"]);
            console.log(typeof storage["c"]);
        }
```

![13387321-525ffd58aa27a7aa](H:\博客\localStorage使用\13387321-525ffd58aa27a7aa.webp)![13387321-7cae0ef66c51e2ac](H:\博客\localStorage使用\13387321-7cae0ef66c51e2ac.webp)

#### 读取

localStorage 只能存储 `String` 类型的数据即使你在赋值的时候给的是 `int` 数据

官方推荐 `getItem` \ `setItem` 两种方法进行存取

下来是3种读取的方法

```js
if(!window.localStorage){
            alert("浏览器不支持localstorage");
        }else{
            var storage=window.localStorage;
            //写入a字段
            storage["a"]=1;
            //写入b字段
            storage.b=1;
            //写入c字段
            storage.setItem("c",3);
            console.log(typeof storage["a"]);
            console.log(typeof storage["b"]);
            console.log(typeof storage["c"]);
            //第一种方法读取
            var a=storage.a;
            console.log(a);
            //第二种方法读取
            var b=storage["b"];
            console.log(b);
            //第三种方法读取
            var c=storage.getItem("c");
            console.log(c);
        }
```

#### 修改

改这个就比较好理解了 既然阔以像对象一样获取和设置 那改也是一样的

```js
if(!window.localStorage){
            alert("浏览器支持localstorage");
        }else{
            var storage=window.localStorage;
            //写入a字段
            storage["a"]=1;
            //写入b字段
            storage.b=1;
            //写入c字段
            storage.setItem("c",3);
            console.log(storage.a);
            // console.log(typeof storage["a"]);
            // console.log(typeof storage["b"]);
            // console.log(typeof storage["c"]);
            /*分割线*/
            storage.a=4;
            console.log(storage.a);
        }
```

这个在控制台上面我们就可以看到已经a键已经被更改为4了

#### 删除

删除所有localStorage里面的数据

```js
var storage=window.localStorage;
            storage.a=1;
            storage.setItem("c",3);
            console.log(storage);
            storage.clear();
            console.log(storage);
```

删除某个特定的键值对删除

```js
var storage=window.localStorage;
            storage.a=1;
            storage.setItem("c",3);
            console.log(storage);
            storage.removeItem("a");
            console.log(storage.a);
```

#### key()

参数：index

```
var storage=window.localStorage;
            storage.a=1;
            storage.setItem("c",3);
            for(var i=0;i<storage.length;i++){
                var key=storage.key(i);
                console.log(key);
            }
//使用key()方法，向其中输入索引即可获取对应的键
```

### 注意事项

一般我们会将JSON存入localStorage中，但是在localStorage会自动将localStorage转换成为字符串形式

这个时候我们可以使用JSON.stringify()这个方法，来将JSON转换成为JSON字符串



代码图片来源：https://www.jianshu.com/p/5f02331f5386
