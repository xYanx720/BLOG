## PHP

#### （1）PHP文件的书写

- 所有的 php 代码都要写在一个 php 的范围内

- 要求以 `<?php` 开头

- 要求以 `?>` 结尾

  ```php
  <?php
  #代码
  
  
  ?>
  ```

  

#### **（2）语法**

- 每一句后面必须加`;`

- 在 php 中没有 `var` 关键字给我们定义变量
- 直接使用 `$` 来确定一个变量

```php
<?php
	
  # 下面就是一个定义了一个变量，并且赋值为 100
  # 变量名就是 $num
  $num = 100;
  
  $boo = true;
  
  # 下面是一个字符串
  $str = "你好 php";
  
?>
```

#### 	(3)输出

- `echo`
  - 只能输出字符串
- `var_dump()`
  - 什么都能输出，并且会把每一个数据的数据类型输出出来
- `print_r()`
  - 什么都能输出，但是不会输出数据的数据类型

#### （4）条件语句

- 和js差不多

  ```php
  <?php
     	$boo = true;
      if($boo){
  		echo '欢迎登陆！';
      }else{
      	echo '您还没有登录，请登录';
  	}
  ?>
  ```

#### （5）循环结构

```php
<?php
    $num = 5;
	#for循环
    for ($i = 0; $i < $num; $i++) {
      echo 'hello php';
    }	
	#while循环
    while($num >= 0){
        $num--;
        echo '你好呀';
    }
?>
```

#### （6）数组

```
<?php

  # 创建一个数组
  $arr = array(1, 2, 3);

  print_r($arr);
  # Array ( [0] => 1 [1] => 2 [2] => 3 )
  # 这个就类似于我们 js 中的数组，按照索引来的

  # 创建一个关联数组
  $arr2 = array('name' => 'Jack', 'age' => 18, 'gender' => '男')
  print_r($arr2)
  # Array ( [name] => Jack [age] => 18 [gender] => 男 )
  # 这个就类似于我们 js 中的 对象，键值对的形式
  
   # 把4这个值添加到 $arr1 这个数组中
   array_push($arr1,4);
?>
```

------

### 数据库

#### 链接数据库

```
<?php
 	// 假定数据库用户名：root，密码：123456，数据库：students 
	$con=mysqli_connect("localhost","root","123456","students");  
?>
```

#### 执行sql语句操作数据库

```
<?php
  # 下面就是使用 sql 语句对数据库进行操作
  # mysqli_query($con,"你要执行的SQL语句");  
    $res = mysqli_query($con,'SELECT * FROM `student`');
?>
```

#### 获取结果并解析

- 以上步骤 中`$res`就是  根据执行的mysql语句得到的结果，但是这个结果是我们看不懂的处理信息

- 需要使用 `mysql_fetch_row` || `mysql_fetch_assoc` 解析一下结果才能看得懂

#### 关闭对数据库的连接

```
<?php
   mysqli_close($con);
?>
```

##### 总结：完整步骤(好奇怪都只解析第一句？)

```php
<?php
  $con=mysqli_connect("localhost","root","123456","students");  
  $res =mysqli_query($con，'SELECT * FROM `student`');
  $row = mysqli_fetch_assoc($res);
  mysqli_close($con);

  print_r($row);
?>
```

- mysqil_fetch_row() ` 解析你结果中的第一条，以 索引型数组 的形式返回 
- `mysqli_fetch_array() `解析你结果中的第一条，以 组合型数组 的形式返回 就是把你的字段名称 + 值全部放在数组里面 
- `mysqli_fetch_assoc()  `解析你结果中的第一条，以 关联型数组 的形式返回 

**虽然这些方法都只返回一条数据，但是这些方法再执行第二次的时候，都会从上一次结束的位置开始 

#### 常用sql语句

- 增

  ```php
  <?php
    # 向表中增加一条数据，再增加的时候主键不能由我们书写，而是 mysql 数据库自己递增
    $sql = 'INSERT INTO `student` VALUES(null, "张三",  "男",18)';
      
    # 插入固定几个键的数据，其他的用默认值
    $sql = 'INSERT INTO `student` (`name`, `age`) VALUES("李四", 22)';
  ?>
  ```

  

- 删

  ```php
  <?php
    # 删除表中 id 为 1的数据
    $sql = 'DELETE FROM `student` WHERE `id`=1';
  
    # 删除表中 name 为 张三 的数据
    $sql = 'DELETE FROM `student` WHERE `name`="张三"'
  ?>
  ```

  

- 改

  ```php
  <?php
    # 更新一条 id 为 1的数据中的 name 字段的值和 age 字段的值
    $sql = 'UPDATE `student` SET `name`="张三", `age`=10 WHERE `id`=1'
      
    # 更新数据的时候让所有的数据增加一些内容
    $sql = 'UPDATE `student` SET `age`=age+1'
  ?>
  ```

  

- 查

  ```php
  <?php
    # 查询 student 这个表里面的所有数据
    $sql = 'SELECT * FROM `student`';
      
    # 查询 student 表中的数据里面 gender 为 男 的数据
    $sql = 'SELECT * FROM `student` WHERE `gender`="男"';
      
    # 查询 student 表中的数据里面 age 大于 18 的数据
    $sql = 'SELECT * FROM `student` WHERE `age`>18';
      
    # 查询 student 表中的数据里面 age 大于 18 且 gender 为 男 的数据
    $sql = 'SELECT * FROM `student` WHERE `age`>18 AND `gender`="男"';
  
    # 查询 student 表中的数据里面 age 小于 22 或者 age 大于 28 的数据
    $sql = 'SELECT * FROM `student` WHERE `age`<22 OR `age`>28';
  
    # 查询 student 表中的数据里面从 第几条开始 查询多少条
    $sql = 'SELECT * FROM `student` LIMIT 0, 10';
      
    # 先按照条件筛选出数据以后再进行分页查询
    # 下面是查询表中所有 age>18 且 性别为男的所有数据，查出来以后从第 10 条开始查 10 条
    $sql = 'SELECT * FROM `student` WHERE `age`>18 AND `gender`="男" LIMIT 10, 10';
  
    # 查询表的模糊查询
    # 下面表示查询表中所有数据里面 name 字段中包含 "三" 字的数据
    $sql = 'SELECT * FROM `student` WHERE `name` LIKE "%三%"';
  
    # 查询排序，查询的时候按照某一个字段升序或降序排序
    $sql = 'SELECT * FROM `student` ORDER BY `age` ASC';
    $sql = 'SELECT * FROM `student` ORDER BY `age` DESC';
  ?>
  ```

  