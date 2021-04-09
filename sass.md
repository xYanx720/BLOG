### Sass

css预编译器

------

#### 注释

- /* sth */
- // sth 

#### 变量

> sass变量只能用 **$** 声明 ， $key:value 形式

- 全局变量

  在最外面写的就是全局变量，就像是 nodejs require一个模块一样  ， 模块总不可能写在函数里面require吧

- 局部变量

  ```scss
  .header{
  	$main:#fff; //局部变量
  }
  ```

- 默认变量

  假设test.scss里面

  ```
  $color:#fff;
  ```

  lalala.scss里面

  ```
  $color:#000;
  @import 'test.scss';
  ```

  那么结果就是 **test.scss** 里面的`$color`会覆盖 **lalala.scss** 里面的`$color`

  但是如果加了 **!default** 就不一样了  意思就是你这个是默认的  那么在 **lalala.scss** 里面  不管是在@import之前还是之后去改变都是会能改变的

- 修改全局变量

  讲真这块我没懂为什么有这个操作在  css 本来就不是写逻辑的  这种在局部改变全局变量的方式一般就 防抖 吧？  或者需要外部有个flag值来控制逻辑的行动，不过既然有还是记录一下

  ```scss
  $color: #333; // 全局变量
      .box{
          $color:#fff !global;// 局部修改全局变量
  
      }
  ```

- 别的用法

  ```
   $borderDirection:top;
      //应用于class和属性
      .border-#{$borderDirection}{
          border-#{$borderDirection}:1px solid #ccc;
      }
  ```

- 类 数组 ， 对象

  > 多值变量分为`list`类型和`map`类型，简单来说list类型有点像js中的数组，而map类型有点像js中的对象。

   ```scss
            //list类型
            $pd: 5px 10px 20px 30px;
            //使用
            .content{padding:$pd;}
            .btop{border-top:nth($pd,1);}
            //map类型
            $headings: (h1: 2em, h2: 1.5em, h3: 1.2em);
            //使用
            h1{font-size:map-get($headings,h1)}
   ```

#### 嵌套

不说了 就嵌套嘛 随便看看都会吧

#### mixin 混合器

 scss 这个应该跟 less 学学 

> sass中使用`@mixin`声明混合，通过@include来调用

```
    @mixin important-text {
        color: red;
        font-size: 25px;
        font-weight: bold;
        border: 1px solid blue;
    }

    @mixin bordered($width,$color) {
        border: $width solid $color;
    }

    @mixin max-screen($res){
      @media only screen and ( max-width: $res )
      {
        @content;
      }
    }

    // 使用
    h4{ @include important-text; }
    .myArticle {
        @include bordered(1px,blue);
    }
    @include max-screen(480px) {
      body { color: red }
    }
```

> PS：`@mixin`通过`@include`调用后解析出来的样式是以拷贝形式存在的，而下面的继承则是以联合声明的方式存在的，所以从3.2.0版本以后，建议传递参数的用`@mixin`，而非传递参数类的使用下面的继承`%`。

#### 占位选择器

```
    //占位符编译后不存在css样式中
    %ir{
        color: transparent;
        text-shadow: none;
        background-color: transparent;
        border: 0;
    }
    @extend %ir;
```

#### 导入

```
@import '*';
```

#### 函数

- 常用函数

  - `percentage($value)`：将一个不带单位的数转换成百分比值；
  - `round($value)`：将数值四舍五入，转换成一个最接近的整数；
  - `ceil($value)`：将大于自己的小数转换成下一位整数；
  - `floor($value)`：将一个数去除他的小数部分；
  - `abs($value)`：返回一个数的绝对值；
  - `min($numbers…)`：找出几个数值之间的最小值；
  - `max($numbers…)`：找出几个数值之间的最大值。
  - `lighten($color,$percent)` 通过改变颜$color色的亮度值（0% - 100%），让颜色变亮
  - `darken($color,$percent)`  通过改变颜$color色的亮度值（0% - 100%），让颜色变暗

- 自定义函数

  > 格式： @function 函数名

  ```
      $oneWidth: 10px;  
      $twoWidth: 40px;  
      
      @function widthFn($n) {  
          @return $n * $twoWidth + ($n - 1) * $oneWidth;  
      }  
      
      .leng {   
          width: widthFn($n : 5);  
      } 
  ```

  

#### 运算

> sass具有运算的特性，可以对数值型的Value(如：数字、颜色、变量等)进行**+-*/**四则运算 (请注意运算符前后请留一个空格，不然会出错)。

#### 判断

```
   @if $type == ocean {
        color: blue;
    } @else if $type == matador {
        color: red;
    } @else {
        color: black;
    }
```

#### 循环

```
    @for $var from <start> through <end>//（包含end值）
    @for $var from <start> to <end>//（不包含en值）
```

#### 编译

**gulp-sass**

```
npm install gulp-sass --save-dev
```

- 参数outputStyle:

  - nested			: 默认

  - expanded      : 展开

  - compact         : 单行

  - compressed  : 压缩

    ```
        gulp.task('sass', function () {
            return gulp.src('./sass/**/*.scss')
            .pipe(sass({outputStyle: 'compressed'}).on('error', sass.logError))
            .pipe(gulp.dest('./css'));
        });
    
        //文件监听（文件有修改自动编译）
        gulp.task('sassWatch',function(){
            gulp.watch('./src/sass/*.scss',gulp.series('sass'));
        });
    
    ```

    > 当scss文件以 `_`  开头时不会被编译成 css 文件	

**sass**

```
npm install sass -g
npm install sass --save-dev
```

​	编译命令

```
sass test.scss test.css
```

