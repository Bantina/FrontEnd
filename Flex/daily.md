# 学习内容

### 学习Flex弹性布局

##### 特性
设为flex布局的元素，子元素的float、clear、vertical-align属性将失效

##### 容器flex的属性
1. flex-direction【决定主轴即排列方向】 
	- row 水平方向，起点在左端
	- row-reverse 水平方向，起点在右端
	- column 垂直方向，起点在上沿
	- column-reverse 垂直方向，起点在下沿		
2. flex-wrap 【换行】
	- nowrap 不换行
	- wrap 换行，第一行在上方
	- wrap-reverse 换行，第一行在下方
3. flex-flow【1，2的结合】
4. justify-content【主轴上的对齐方式】
	- flex-start 左对齐
	- flex-end 右对齐
	- center 居中
	- space-between 两端对齐，两端无间距
	- space-around 整体对齐，两端有间距
5. align-items【交叉轴上的对齐方式】
	- strench 占满整个容器的高度
	- flex-start
	- flex-end
	- flex-center
	- stretch
	- baseline 
6. align-content【多根轴线的对齐方式】
	- stretch
	- flex-start
	- flex-end
	- center
	- stretch
	- space-between
	- space-around
##### 项目的属性

1. order【项目的排列顺序，数值越小，排列越靠前，默认为0】
2. flex-grow 【项目的放大比例，默认为0】
3. flex-shrink 【项目的缩小比例，默认为1】
	若它为0，其他项目为1，则空间不足时，前者不缩小。
4. flex-basis 
5. flex:[flex-grow,flex-shrink,flex-basis]
6. align-self【单个项目的align-items，相当于从一个项目中抽离】

##### 实践测试-见code/flexTest.html
	
### 初识Express
先来一个例子：
```
//express 数据请求api路由定义；
var express = require('express');
var app = express();
var apiRoutes = express.Router();

var appData = require('../data.json'); //请求的data数据
var seller = appData.seller;

apiRoutes.get('/seller',function(req,res){
	res.json({    //res.json()为express的响应方法
		errno:0,
		data:seller
	});
})

app.use('/api',apiRoutes);//在应用中加载路由模块 
//请求地址:../api/seller

```
1. 响应对象res的方法向客户端返回响应，终结请求响应的循环，否则一直挂起
- res.download()【提示下载文件】
- res.end()【终结响应处理流程】
- res.json()【发送一个json格式的响应】
- res.jsonP()【发送jsonP格式的响应】
- res.redirect()【重定向请求】
- res.render()【渲染视图模版】
- res.send()【发送各类型的响应】
- res.sendFile【以8位字节流形式发送文件】
- res.sendStatus()【设置响应状态代码】
2. express.Router类<br>
创建模块化、可挂载的路由句柄。<br>
必须使用 app.use() 挂载。

