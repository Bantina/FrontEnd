### prototype遇到call的呐点事
date: 2017-10-12 09:59:15

##### 1.使用`Object.prototype.toString.call(value);`来判断数据类型

在使用typeof判断数据类型时，对于对象类型总是存在异议，eg:
```
typeof null;   // object
```
而使用`Object.prototype.toString.call(value);`会更加精确的判断数据类型，包括基本类型和原生饮用类型。

- 判断基本类型：
```
Object.prototype.toString.call(null); // ”[object Null]”
Object.prototype.toString.call(undefined); // ”[object Undefined]”
Object.prototype.toString.call(“abc”); // ”[object String]”
Object.prototype.toString.call(123); // ”[object Number]”
Object.prototype.toString.call(true); // ”[object Boolean]”
```
- 判断原生引用类型：
```
// 函数类型
Function fn(){console.log(“test”);}
Object.prototype.toString.call(fn); // ”[object Function]”

// 日期类型
var date = new Date();
Object.prototype.toString.call(date); // ”[object Date]”

// 数组类型
var arr = [1,2,3];
Object.prototype.toString.call(arr); // ”[object Array]”

// 正则表达式
var reg = /[hbc]at/gi;
Object.prototype.toString.call(arr); // ”[object Array]”

// 自定义类型
function Person(name, age) {
    this.name = name;
    this.age = age;
}
var person = new Person("Rose", 18);
Object.prototype.toString.call(arr); // ”[object Object]”
```

- 判断原生JSON对象：
```
var isNativeJSON = window.JSON && Object.prototype.toString.call(JSON);
console.log(isNativeJSON);
// 输出结果为”[object JSON]”说明JSON是原生的，否则不是；
```

##### 2.利用`Array.prototype.数组函数.call()`来处理字符串
```
// arr.join() 连接字符串；
var a = "foo";
var c = Array.prototype.join.call(a, "-");
console.log(c); // f-o-o

// arr.map()
var d = Array.prototype.map.call(a,function(v){
	return v.toUpperCase() + ".";
}).join("");
console.log(d); // F.O.O.

// arr.reverse() 反转字符串
// Array.prototype.reverse.call(a);
// => Chrome:Uncaught TypeError: Cannot assign to read only property '0' of object '[object String]'
var e = a.split("").reverse().join("");
console.log(e); // oof
```

##### 3.利用`Array.prototype.slice.call(arguments)`将类数组转化为数组
```
function foo(){
	var arr = Array.prototypt.slice.call( arguments );
	arr.push('add');
	console.log(arr);
}
foo('bar', 'baz'); // ['bar', 'baz', 'add']
// 在ES6中使用 Array.from( arguments ); 来实现此功能；
```
