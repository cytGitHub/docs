## Promise

### 特点

- `Promise`的状态分为三种，`pendding`，`fulfilled`，`rejected`
- `Promise`状态的改变分为两种
  - `pendding`到`fulfilled`
  - `pendding`到`rejected`
  - 状态是不可逆的，会一直保持这个状态

### 缺点

- 需要回调函数来收集内部抛出的错误
- 无法取消`promise`
- 对于进行到那个阶段，不好感知

### `resolve` `reject`

- 调用`resolve`，`reject`并不会阻挡后面的代码执行
- `resolve`，`reject`的`Promise`是在本轮事件循环的末尾执行，总是晚于同步任务
- 一旦调用`resolve`，`reject`，`Promise`的使命已经完成，后续操作应该放到`then`里面， 所以最好在`resolve`，`reject`前面添加`return`

### `then(resolve , reject)`

- 定义在`prototype`上
- `promise`函数状态改变的时候的回调函数
- 第一个参数是`resolved`状态的回调，第二个参数是`rejected`状态的回调
- 返回一个全新的`Promise`

### `catch`

- `then(null，rejection)` 的别名，指定发生错误的时候回调
- 如果没有`catch`，`Promise`内部抛出错误，并不会影响后续代码执行，`Promise`会吃掉错误
- 如果`Promise`的状态已经`resolve`，那么在抛出错误是无效的

* `catch`返回一个`promise`，可以继续调用`then`
* 如果`catch`内部报错，并没有`catch`接收的话，也会报错

### `Promise.try`

- 不知道一个函数是同步还是异步，可以用`promise.try`来实现
