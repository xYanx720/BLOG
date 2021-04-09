![image-20210330201306333](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210330201306333.png)

#### 使用

- await后面接一个会return new promise的函数并执行它

- await只能放在async函数里

```
async function test(){
	let res = await fun();
}
```

#### 获取多个异步函数的结果

- await是直接获取多个promise的结果的，因为Promise.all()返回的也是一个promise所以如果要使用await拿到多个promise的值，可以直接await Promise.all()

```
async function test(){
    try{
        let n = await Promise.all([fun('str'),fun('str1')])
        console.log(n)
    }catch(error){
        console.log(error)
    }
}
test()
```

- async函数会返回一个promise，并且Promise对象的状态值是resolved（成功的）
  1. 如果你没有在async函数中写return，那么Promise对象resolve的值就是是undefined
  2. 如果你写了return，那么return的值就会作为你成功的时候传入的值

#### await 等到之后，干嘛？

await 右边表达式的结果 就是 await 要等待的东西

等到之后，两种情况

- ​	 `Promise` 对象
- 非 `Promise` 对象

> 不管是不是 Promise 对象 ，await 都会暂停函数内的后续代码（称之为 **阻塞** ）
>
> And then 
>
> 非 Promise ：把这个非 Promise 的东西 ， 作为 await 表达式的结果
>
> ​	 Promise：把 resolve 的参数作为 await 表达式的运算结果

#### 执行过程

**Tips**：如果Promise没有一个成功的值传入，对await来说都是失败的，下面的代码是不会执行的

所以不管await后面的代码是同步还是异步，await总是需要时间，从右向左执行，先执行右侧的代码，执行完后，发现有await关键字，于是让出线程，阻塞代码

```js
/* 这个代码因为fn是属于同步的，所以先打印出1，然后是3，但是因为没有resolve结果，所以await拿不到值，因此不会打印2 */
function fn(){
    return new Promise(resolve=>{
        console.log(1)
    })
}
async function f1(){
    await fn()
    console.log(2)
}
f1()
console.log(3)
//1
//3
```

```js
/* 这个代码与前面相比多了个resolve说明promise成功了，所以await能拿到结果，因此就是1 3 2 */
function fn(){
    return new Promise(resolve=>{
        console.log(1)
        resolve()
    })
}
async function f1(){
    await fn()
    console.log(2)
}
f1()
console.log(3)
//1
//3
//2
```

