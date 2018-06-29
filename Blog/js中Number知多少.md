### js中Number知多少
date: 2017-10-12 17:51:27

- js数字类型的实现基于 IEEE 754(浮点数)，使用“双精度”格式(即64位二进制)；
- 特别大／小的数字 默认以指数格式显示, 相当于toExponential()转化成指数的结果；

- js的“机器精度”值，定义在 Number.EPSILON = 2^-52 = Math.pow(2, -52)，即 2.220446049250313e-16；
- js中最大浮点数定义在 Number.MAX_VALUE = 1.798e + 308 (约等于)；
- js中最小浮点数定义在 Number.MIN_VALUE = 5e - 324 (约等于，不是负数，无限接近于0的数)；
- js中能够被安全呈现的最大整数定义在 Number.MAX_SAFE_INTEGER = 2^53 - 1 = Math.pow(2, 53) - 1，即 9007199254740991；
- js中能够被安全呈现的最大整数定义在 Number.MIN_SAFE_INTEGER = -9007199254740991；

关于最大安全数字举例：
问题：js处理一些比较大的数字时出现的偏差，如数据库中的64位ID等。
原因：JS的数字类型无法精确呈现64位数。
解决方案：将其转换为字符串。

##### 0.1 + 0.2 == 0.3 ？


- 怎样来判断该语句返回为true呢？
方法：设置一个误差范围值，通常称为“机器精度”(machine epsilon)，对于js的数字来说，这个值通常是2^-52(2.220446049250313e-16)
对于ES6,该值定义在Number.EPSILON中，ES5兼容写法：
```
if (!Number.EPSILON) {
    Number.EPSILON = Math.pow(2, -52);
}
```
判断两个数字是否相等时，在指定的误差内，可以用Number.EPSILON，来比较
```
function numbersCloseToEqual(n1, n2) {
    return Math.abs(n1 - n2) < Number.EPSILON;
}
var a = 0.1 + 0.2;
var b = 0.3;
numbersCloseToEqual(a,b);	// true
```

- 检测一个值是否为整数？
1. 正则；
2. ES6: Number.isInteger();
```
Number.isInteger(42); // true;
Number.isInteger(42.00); // true;
Number.isInteger(42.35); // false;
```
3. ES6之前版本
```
if (!Number.isInteger) {
    Number.isInteger = function(num) {
        return type num == "number" && num % 1 == 0;
    }
}
```

- 检测一个值是否为安全范围内的整数？
1. ES6: Number.isSafeInteger()
```
Number.isSafeInteger(Number.MAX_SAFE_INTEGER); // true;
Number.isSafeInteger(2^53 - 1); // true;
Number.isSafeInteger(2^53); // false;
```
2. ES6之前版本
```
if (!Number.isSafeInteger) {
    Number.isSafeInteger = function(num) {
        return Number.isInteger(num) && Math.abs(num) <= Number.MAX_SAFE_INTEGER;
    }
}
```

- 检测一个值是否为NaN?
1. window.isNaN()  // 存在缺陷，只检测值 not a number;
```
var a = 2 / "foo";  // NaN
var b = "foo";
window.isNaN( a ); // true;
window.isNaN( b ); // true;
```
2. ES6 : Number.isNaN()
```
if (!Number.isNaN) {
    Number.isNaN = function() {
        return (
            typeof n === "number" && window.isNaN(n)
        );
    };
}
var a = 2 / "foo";  // NaN
var b = "foo";
window.isNaN( a ); // true;
window.isNaN( b ); // false;
```
3. NaN 是js 中唯一一个不等于自身的值
```
if (!Number.isNaN) {
    Number.isNaN = function(n) {
        return n !== n
    }
}
```
