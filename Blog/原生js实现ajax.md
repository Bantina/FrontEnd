### 1. ES5-原生js封装ajax
```
/**
 * 1. ES5-原生js封装ajax
 * ajax({
 *  url: '',
 *  type: 'POST',
 *  data: { name: 'aaa', age: 12},
 *  dataType: 'json',
 *  success: function (response, xml) {},
 *  error: function (status) {}
 * })
 */
function ajax(options) {
  var xhr
  var params = formatParams(options.data)
  options = options || {}
  options.type = (options.type || 'GET').toUpperCase()
  options.dataType = options.dataType || 'json'

  // 1. 创建对象
  xhr = new XMLHttpRequest() || new ActiveXObject('Microsoft.XMLHTTP')

  // 2. 连接并发送
  if (options.type === 'GET') {
    xhr.open('GET', options.url + '?' + params, true)
    xhr.send(null)
  } else if (options.type === 'POST') {
    xhr.open('POST', options.url, true)
    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
    xhr.send(params)
  }

  // 3. 接收返回值
  xhr.onreadystatechange = function () {
    if (xhr.readyState !== 4) return
    var status = xhr.status
    if (status >= 200 && status < 300 || status === 304) {
      options.success && options.success(xhr.responseText, xhr.responseXML)
    } else {
      options.error && options.error(status)
    }
  }
}

/** 格式化参数 */
function formatParams (data) {
  var arr = []
  for (var name in data) {
    arr.push(encodeURIComponent(name) + '=' + encodeURIComponent(data[name]))
  }
  arr.push(('v=' + Math.random()).replace('.'))
  return arr.join('&')
}
```

### 2. ES6-promise实现ajax
```
/**
 * 2. ES6-promise实现ajax
 * getJSON(({
 *  url: '',
 *  type: 'POST',
 *  data: { name: 'aaa', age: 12},
 *  dataType: 'json',
 *  success: function (response, xml) {},
 *  error: function (status) {}
 * }).then(function (json) {}, function (error) {})
 */
const getJSON = function (options) {
  const promise = new Promise(function (resolve, reject){
    const params = formatParams(options.data)
    options = options || {}
    options.type = (options.type || 'GET').toUpperCase()
    options.dataType = options.dataType || 'json'

    // 1. 创建对象
    const xhr = new XMLHttpRequest() || new ActiveXObject('Microsoft.XMLHTTP')

    // 2. 连接并发送
    if (options.type === 'GET') {
      xhr.open('GET', options.url + '?' + params, true)
      xhr.send(null)
    } else if (options.type === 'POST') {
      xhr.open('POST', options.url, true)
      xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
      xhr.send(params)
    }

    // 3. 接收返回值
    xhr.onreadystatechange = function () {
      if (this.readyState !== 4)  return
      if (this.status === 200) {
        resolve(this.response)
      } else {
        reject(new Error(this.statusText))
      }
    }
  })

  return promise
}
```