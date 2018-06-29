### ES6到ES5的转化
date: 2017-09-26 17:32:08

1. “机器精度”(machine epsilon)值，2^-52(2.220446049250313e-16)。
ES6,该值定义在Number.EPSILON中，
ES5兼容写法：
```
if (!Number.EPSILON) {
    Number.EPSILON = Math.pow(2, -52);
}
```
