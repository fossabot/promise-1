# 🍁深入`Promise`内部结构，一步一步实现一个完整的、能通过所有`Test case`的`Promise`类

## `Promise`标准解读
### 1. 只有一个`then`方法，没有`catch，race，all`等方法，甚至没有构造函数
`Promise`标准中仅指定了`Promise`对象的`then`方法的行为，其它一切我们常见的方法/函数都并没有指定，包括`catch`，`race`，`all`等常用方法，甚至也没有指定该如何构造出一个`Promise`对象，另外`then`也没有一般实现中（Q, $q等）所支持的第三个参数，一般称`onProgress`.

### 2. `then`方法返回一个新的`Promise`
`Promise`的`then`方法返回一个新的`Promise`，而不是返回`this`
```js
var promise2 = promise1.then(/*your code*/)
var promise2 !== promise1   // true
```
### 3. 不同`Promise`的实现需要可以相互调用(interoperable)
### 4. `Promise`的初始状态为`pending`，它可以由此状态转换为`fulfilled`（`resolved`）或者`rejected`，一旦状态确定，就不可以再次转换为其它状态，状态确定的过程称为`settle`
### 5. 更多规范参照[Promise官方英文文档](https://promisesaplus.com/)