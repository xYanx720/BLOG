# [forEach、map、filter、reduce的区别]

1.相同点：

- 都会循环遍历数组中的每一项；
- map()、forEach()和filter()方法里每次执行匿名函数都支持3个参数，参数分别是：当前元素、当前元素的索引、当前元素所属的数组；
- 匿名函数中的this都是指向window；
- 只能遍历数组。

2.不同点：

- map()速度比forEach()快；
- **map()和filter()会返回一个新数组，不对原数组产生影响；forEach()不会产生新数组，返回undefined；**reduce()函数是把数组缩减为一个值(比如求和、求积)；
- reduce()有4个参数，第一个参数为初始值。

3.forEach使用



```
let array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});
```

4.map使用

```
let array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

5.filter使用

```
let words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

6.reduce使用

```
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

![image-20210304164240182](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210304164240182.png)