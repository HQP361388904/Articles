> 本章描述JavaScript的编程环境和基本的编程模块。

# 一、JavaScript环境

1. 浏览器里运行
2. 桌面程序执行
3. 服务器上执行

# 二、JavaScript编程实践

> 语言基本结构使用方法指南。

### 1. 声明和初始化变量

JavaScript中的变量默认是全局变量，严格地说，甚至不需要在使用前进行声明。如果对一个实现未予声明的JavaScript变量进行初始化，该变量就成了一个全局变量。

[tips：在使用变量前，先对其进行声明。](tips)

在JavaScript中声明变量，需要使用关键字`var`，后跟变量名，后面还可以跟一个赋值表达式。

```javascript
var name;
var greeting = 'Hello World!';
```

### 2. JavaScript中的算数运算和数学库函数

JavaScript使用标准的算术运算符：`+`（加）、`-`（减）、`*`（乘）、`/`（除）、`%`（取余）。

JavaScript同时拥有一个数学库，用来完成一些高级运算，比如平方根、绝对值和三角函数。算术运算符遵循标准的运算顺序，可以用括号来改变运算顺序。

```javascript
var x = 3;
var y = 2;

console.log(x + y); // 5
console.log(x - y); // 1
console.log(x * y); // 6
console.log(x / y); // 1.5
console.log(x % y); // 1

var z = 9;
console.log(Math.sqrt(z)); // 3

var w = -1;
console.log(Math.abs(w)); // 1
```

### 3. 判断语句

根据布尔表达式的值，判断结构让程序可以选择执行哪些程序语句：`if`语句和`switch`语句。

```javascript
/**
 * if语句
 */
var mid = 25;
var high = 50;
var low = 1;
var cur = 13;
var found = -1;

// 简单的if语句
if (cur < mid>) {
    mid = (cur - low) / 2;
}

// if-else语句
if (cur < mid>) {
    mid = (cur - low) / 2;
} else {
    mid = ( cur + high) / 2;
}

// if-else if语句
if (cur < mid) {
    mid = (cur - low) / 2;
} else if (cur > mid) {
    mid = (cur + high) / 2;
} else {
    found = cur;
}

/**
 * switch语句
 */
var verifyStatus = 2;
var verifyFormat = '';

switch (verifyStatus) {
    case 0:
        verifyFormat = '审核中';
    break;

    case 1:
        verifyFormat = '审核通过';
    break;

    case -1:
        verifyFormat = '审核不通过';
    break;

    default:
}
```

[tips：在有多个简单的选择时，使用`switch`语句的代码结构更加清晰。](tips)

### 4. 循环结构

本书涉及的多数算法，从本质上都具有循环的特性：`while`循环和`for`循环。

如果希望在条件为真时执行一组语句，就选择`while`循环。

```javascript
var number = 1;
var sum = 0;

while (number < 11) {
    sum += number;
    ++number;
}

console.log(sum); // 55
```

如果希望按执行次数执行一组语句，就选择`for`循环。

```javascript
//var number = 1;
var sum = 0;

for (var number = 1; number < 11; number++>) {
    sum += number;
}

console.log(sum); // 55

// for循环访问数组中的元素
var numbers = [3, 7, 12, 22, 100];
var sum = 0;

for (var i = 0; i < numbers.length; i++) {
    sum += numbers[i];
}

console.log(sum); // 144
```

### 5. 函数

JavaScript提供了两种定义函数的方式：有返回值和没有返回值（有时叫子程或void函数）。

```javascript
/**
 * 有返回值的函数
 */
functon factorial(number) {
    var product = 1;

    for (var i = number; i>= 1; i--) {
        product *= i;
    }

    return product;
}

console.log(factorial(4)); // 得到返回值：24

/**
 * 没有返回值的函数：JavaScript中的子程或void函数
 */
function curve(arr, amount) {
    for (var i = 0; i < arr.length; i++) {
        arr[i] += amount;
    }
}

var grades = [77, 73, 74, 81, 90];

curve(grades, 5);

console.log(grades); // [82, 78, 79, 86, 95]
```
使用没有返回值的函数，是为了执行函数中定义的操作。

### 6. 变量作用域

变量的作用域是指一个变量在程序中的哪些地方可以访问。JavaScript中的变量作用域被定义为函数作用域。这是指变量的值在定义该变量的函数内是可见的，并且定义在该函数内的嵌套函数中也可访问。

在主程序中，如果在函数外定义一个变量，那么该变量拥有全局作用域，在包括函数体内的程序的任何部分都可以访问该变量。

```javascript
/**
 * 全局变量
 */
function showScope() {
    return scope;
}

// 可以在程序的任意位置定义全局变量，如：在函数定义前或函数定以后。
var scope = 'global';

console.log(scope); // global
console.log(showScope()); // global

/**
 * 局部变量
 */
function showScope() {
    var scope = 'local';

    return scope;
}

var scope = 'global';

console.log(scope); // global
console.log(showScope()); // local
```

JavaScript允许在定义变量时不适用关键字var，此时定义的变量自动拥有了全局作用域，即使是在一个函数内定义的，也是全局变量。

```javascript
function showScope() {
    scope = 'local';

    return scope;
}

var scope = 'global';

console.log(scope); // global
console.log(showScope()); // local
console.log(scope); // local
```

### 7. 递归

JavaScript中允许函数递归调用。

```javascript
function factorial(number) {
    if (number === 1) {
        return number;
    } else {
        return number * factorial(number - 1);
    }
}

console.log(factorial(4)); // 24
```

当一个函数被递归调用，在递归没有完成时，函数的计算结果暂时被挂起。

```javascript
// factorial(4)函数执行过程
4 * factorial(3)
4 * 3 * factorial(2)
4 * 3 * 2 * factorial(1)
4 * 3 * 2 * 1
4 * 3 * 2
4 * 6

24
```
JavaScript都有能力处理递归层次较深的递归调用。但是当有的算法需要的递归深度超出了JavaScript的处理能力，这是就需要寻求该算法的一种迭代式解决方案。**任何可以被递归定义的函数，都可以被改写为迭代式的程序。**

# 三、对象和面向对象编程

对象通过如下方式创建：定义包含属性和方法声明的构造函数，并在构造函数后紧跟方法的定义。

```javascript
/**
 * 构造函数
 */
function Checking(amount) {
    // 属性
    this.balance = amount;
    // 方法
    this.deposit = deposit;
    this.withdraw = withdraw;
    this.toString = toString;
}

/**
 * 方法
 */
function deposit(amount) {
    this.balance += amount;
}

function withdraw(amount) {
    if (amount <= this.balance) {
        this.balance -= amount;
    } else {
        console.log('余额不足');
    }
}

function toString() {
    return 'Balance: ' + this.balance;
}

/**
 * 使用对象中的方法和属性
 */
var account = new Checking(500);

account.deposit(1000);
console.log(account.toString()); // Balance: 1500
account.withdraw(750);
console.log(account.toString()); // Balance: 750
account.withdraw(800); // 余额不足
console.log(account.toString()); // Balance: 750
```

# 四、小结

1. 在使用变量前，先对其进行声明。
2. 在有多个简单的选择时，`switch`语句比`if`语句的代码结构更加清晰。
3. 如果希望在条件为真时执行一组语句，就选择`while`循环；如果希望按执行次数执行一组语句，就选择`for`循环。
4. 使用没有返回值的函数，是为了执行函数中定义的操作。
5. JavaScript中的变量作用域被定义为函数作用域 —— 函数内可访问。
6. 