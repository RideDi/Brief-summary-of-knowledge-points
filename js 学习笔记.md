js 学习笔记

变量提升：任何对变量和函数的生命都会被提升到函数顶部

但是 只有声明会提升，初始化不会

var x 会

var x = 8 不会

var x = 8 ==> var x;  x = 8;

------

var let const三种声明方式

var 声明的会挂载在window上，let和const不会

var 声明的有变量提升，另外两种没有

let 和 const 声明形成块作用域

```js
if(1){
    var a = 10;
    let b = 10;
    const c = 10;
}
console.log(a); //10
console.log(b); // b not define
console.log(c); // c not define
```

var 可以重复声明

暂存死区

![image-20210208144459110](C:\Users\49353\AppData\Roaming\Typora\typora-user-images\image-20210208144459110.png)

![image-20210208144518026](C:\Users\49353\AppData\Roaming\Typora\typora-user-images\image-20210208144518026.png)

