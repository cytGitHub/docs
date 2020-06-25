## Webpackk Tapable

- #### SyncHook 同步钩子

  - 注册方式：`tap`注册
  - 调用方式：`call`调用

- #### AsyncHook 异步钩子

  - `tapAsync`

    - 注册方式：`tapAsync`
    - 调用方式：`callAsync`

  - `tapPromise`
    - 注册方式：`tapPromise`
    - 调用方式：`callPromise`

### Api 解析

- `SyncHooks`

  - `SyncHook`同步执行，不关心返回值

  ```
    let Car = new SyncHook();
    Car.tap("tapable",() => { console.log(`tapable`) })
    Car.tap("webpack",() => { console.log(`webpack`)})
  ```

  - `SyncBailHook` 如果监听的函数返回值不是`undefined`，则不执行后面的函数

  ```
    let Car = new SyncBailHook();
    Car.tap("tapable",() => {
      console.log(`tapable`)
      return xx
    })
    Car.tap("webpack",() => { console.log(`webpack`)})

    Car.call()
    webpack函数不会执行
  ```

* `SyncWaterfallHook`，上一个监听函数的返回值可以传递给下一个

```
  let Car = new SyncWaterfallHook(['args']);
  Car.tap("tapable",() => {
    console.log(`tapable`)
    return "参数传递"
  })
  Car.tap("webpack",(args) => { console.log(args)})
  Car.call();
```

- `SyncLoopHook`，当监听函数返回`true`，会一直执行，直到返回`undefined`，退出循环

- `AsyncHooks Parall`

  - `AsyncParalleHook`，异步并发，不关心返回值

  ```
  let Car = new AsyncParalleHook(['arg']);

  Car.tapAsync('01', (args , cb) => { console.log(args); cb()});
  Car.tapAsync('02', (args , cb) => { console.log(args); cb()});
  Car.callAsync('test', () => {})
  ```

* `AsyncParalleBailHook`异步并发，只要监听函数不是返回`undefined`，就会直接跳到`callAsync`等触发函数绑定的回调函数，然后执行这个回调

* `AsyncHooks Series`
  - `AsyncSeriesHook`，异步串行，不关心`callback`的参数
  - `AsyncSeriesBailHook`，异步串行，当返回值不为`undefined`，直接跳转到`callAsync`等绑定的回调函数中，并触发该函数
  - `AsyncSeriesWaterfallHook` , 异步串行，将返回值传递给下一个函数
