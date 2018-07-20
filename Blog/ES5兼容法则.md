### ES5兼容法则
date: 2017-09-26 17:41:16

- ES5中提供的Object.create(要继承的原型)实现继承-可以理解为克隆
在不支持Object.create方法的浏览器中，兼容如下：
```
Object.create = Object.create || function(obj){
	var F = function(){};
	F.prototype = obj;

	return new F();
}
```
