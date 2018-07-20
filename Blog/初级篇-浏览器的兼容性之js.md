### 初级篇-浏览器的兼容性之js
date: 2016-12-11 15:16:14

### 1.window.onscroll 滚动条滚动时触发的事件
> 获取滚动条对象的兼容问题：IE-documentElement,谷歌-body;(clientWidth等属性与此相同)
> document.documentElement或document.body--IE7之前的版本；
```js
window.onscroll = function() {
  var osTop = document.documentElement.scrollTop || document.body.scrollTop;
}
```

### 2.addEvent 事件绑定
> 为了兼容IE使用统一的绑定事件的方法
```js
function addEvent(el, event, callbackFunction) {
  if (el.addEventListener) {
    el.addEventListener(event, callbackFunction, false); //元素作用域；
  } else if {
    el.attachEvent('on' + event, callbackFunction); //全局作用域
  }
}
```

<!-- -->
### 3.eventUtil 完整DOM事件 兼容写法
>
```js
var eventUtil = {
  //添加句柄
  addHandler: function(element, type, handler) {
    if (element.addEventListener) {
      element.addEventListener(type, handler, false);
    } else if (element.attachEvent) {
      element.attachEvent('on' + type, handler);
    } else {
      element['on' + type] = handler;
    }
  },
  //删除句柄
  removeHandler: function(element, type, handler) {
    if (element.removeEventListener) {
      element.removeEventListener(type, handler, false);
    } else if (element.detachEvent) {
      element.detachEvent('on' + type, handler);
    } else {
      element['on' + type] = null;
    }
  },
  //获取事件对象；
  getEvent: function(event) {
    return event ? event : window.event;
  },
  //获取事件类型；
  getType: function(event) {
    return event.type;
  },
  //获取事件来源元素；
  getElement: function(event) {
    return event.target || event.srcElement;
  },
  //阻止事件默认行为；
  preventDefault: function(event) {
    if (event.preventDefault) {
      event.preventDefault();
    } else {
      event.returnValue = false;
    }
  },
  //阻止事件冒泡；
  stopPropagation: function(event) {
    if (event.stopPropagation) {
      event.stopPropagation();
    } else {
      event.cancelBubble = true;
    }
  }
}
```

<!-- -->
### 4.getElement 获取事件目标
>
```js
function getElement(event) {
  return event.target || event.srcElement; //兼容IE 获取事件目标；
}
```

<!-- -->
### 5.获取元素通过类名
>
```js
/**
 * @param {classname} claName
 * @param {父元素的id，可选} parent
 **/
function getByClass(clsName, parent) {
  var oParent = parent ? document.getElementById(parent) : document;
  var eles = [];
  var elements = oParent.getElementsByTagName('*');
  for (var i = 0; i < elements.length; i++) {
    if (elements[i].className == clsName) {
      eles.push(elements[i]);
    }
  };
  return eles;
}
```

<!-- -->
### 6.透明度---js控制透明度；
> IE中CSS透明度通过filter:alpha(opacity:*)设置；
```js
function setAttr(el, attr, val) {
  if (attr == 'opacity') {
    el.style.filter = 'alpha(opacity:' + val + ')'; //针对IE浏览器的透明度写法
    el.style.opacity = val / 100; //针对谷歌、火狐浏览器的透明度写法,小数表示；
  }
}
```
> 注：IE与其他浏览器设置透明度时 值 需换算；
