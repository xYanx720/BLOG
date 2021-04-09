![image-20210304164641152](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\apply&call.png)![image-20210312151109162](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210312151109162.png)

# 前言

Js 中的.call() 和 .apply()的区别

#### .call()定义

```js
.call( obj , arg1 , arg2 , arg3 )
```

传入的第一个值为对象，后面为参数，参数之间使用逗号分隔

#### .apply()定义

```js
.apply( obj , args[arg1,arg2,arg3] )
```

传入的第一个值为对象，后面为参数数组；

#### .bind()定义

```js
.bind( obj , arg1 , arg2 ,arg3 )
```



------

##### 相同点：

- .call **/** .apply 都可以用传入的对象代替执行 .call **/** .apply 前面的方法
- 
  ```js
  function test1() {
          let temp = [].slice.call(arguments); //转化为真数组
          console.log(temp);
        }
        test1(1, 2, 3, 45);
  //输出:(4) [1, 2, 3, 45]
  
  function test2() {
          let temp = [].slice.apply(arguments); //转化为真数组
          console.log(temp);
        }
        test2('a','b','c','d');
  //输出: (4) ["a", "b", "c", "d"]
  
  ```

##### 不同点：

- 当需要往代替执行的函数中传参的时候

- ```js
   function test1() {
          let temp = [].slice.call(arguments, 0, 2); //转化为真数组
          console.log(temp); 
        }
        test1(1, 2, 3, 45);
  //输出:(2) [1, 2]  
  
    function test2() {
          let temp = [].slice.apply(arguments, [0, 3]); //转化为真数组
          console.log(temp);
        }
        test2('a', 'b', 'c', 'd');
  //输出: (3) ["a", "b", "c"]
  ```

  

### 新增bind



![image-20210312152231541](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210312152231541.png)

![image-20210312152318787](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210312152318787.png)