---
 title: JavaScriot 解构的用法实例
 base: 基于 ES6
 date: 2018-08-03
---

# JavaScriot 解构的用法实例

[toc]

## 1. 交换变量的值
 
```js
let x = 1;
let y = 2;

[x, y] = [y, x];
```

## 2. 从函数返回多个值

```js
// 返回一个数组

function example() {
    return [1, 2, 3];
  }
  let [a, b, c] = example();
  
  // 返回一个对象
  
  function example() {
    return {
      foo: 1,
      bar: 2
    };
  }
  let { foo, bar } = example();
```

## 3. 函数参数的定义

```js
// 参数是一组有次序的值
function f([x, y, z]) { ... }
f([1, 2, 3]);

// 参数是一组无次序的值
function f({x, y, z}) { ... }
f({z: 3, y: 2, x: 1});
```

## 4. 提取 JSON 数据

```js
let jsonData = {
    id: 42,
    status: "OK",
    data: [867, 5309]
  };
  
  let { id, status, data: number } = jsonData;
  
  console.log(id, status, number);
  // 42, "OK", [867, 5309]
```

## 5. 函数参数的默认值  ---

```js
jQuery.ajax = function (url, {
  async = true,
  beforeSend = function () {},
  cache = true,
  complete = function () {},
  crossDomain = false,
  global = true,
  // ... more config
  } = {}) {
   // ... do stuff
};
```

## 6. 遍历 Map 结构

```js
const map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world

// 获取键名
for (let [key] of map) {
    // ...
  }
  
  // 获取键值
  for (let [,value] of map) {
    // ...
  }
```

## 7. 输入模块的指定方法

```js
const { SourceMapConsumer, SourceNode } = require("source-map");
```

[原文链接](http://es6.ruanyifeng.com/#docs/destructuring)
