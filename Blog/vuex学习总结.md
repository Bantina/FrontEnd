#### 使用Vuex的优劣
###### 优势：
- 跨组件使用数据
- 统一管理数据规范

#### 图解Vuex内部的数据流动：
![image](https://github.com/Bantina/FrontEnd/blob/master/assets/img/vuex01.png)
【数据流动的单向性：】
- 组件可以调用actions；
- Actions用来分发mutations；
- 只有mutations可以修改状态；
- store是反应式的，即状态改变，组件内部改变；

#### 普通项目store结构:
![image](https://github.com/Bantina/FrontEnd/blob/master/assets/img/vuex02.png)
- state.js 所有共享的状态，存放数据；
- getters.js 处理输出。类似store的计算属性，当多个组件都是用处理/过滤后的数据，例如饼状图组件和曲线图组件，那抽取该数据来共享，放在getters里；
- mutations.js 变更状态的commit；
- actions.js 组件内分发mutations的函数；
- mutation-types.js 存放常量的js；


#### 按功能模块划分项目store结构:
![image](https://github.com/Bantina/FrontEnd/blob/master/assets/img/vuex03.png)


#### 源码解析：
参考https://segmentfault.com/a/1190000009390515
1. vuexInit
```
function vuexInit () {
	const options = this.$options
	if (optins.store) {
		this.$store = typeof options.store === 'function' ? options.store() : options.store
	} else if (options.parent && options.parent.$store) {
		this.$store = options.parent.$store
	}
}
```