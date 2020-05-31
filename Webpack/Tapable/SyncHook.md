## Tapable SyncHook 源码分析

### 示例

```
import {SyncHook} from "tapable";
let Car = new SyncHook();
Car.tap('01',(args) => { console.log(args) });
Car.call();
```

##### 分析

- 1，SyncHook 是一个类，这个类上有 3 个自己定义的方法，tapAsync，\* tapPromise，compile。
- 2，SyncHook 继承了 Hook 类上的属性和方法，
- 3，Hook 类上面绑定了很多的方法，如\_createCall，tap 等
- 4，Car.tap 实际上是调用的 Hook 上面的 tap 的方法
- 5，tap 方法内部实现

```js

tap(options, fn) {
		if (typeof options === "string") options = { name: options };
		if (typeof options !== "object" || options === null)
			throw new Error(
				"Invalid arguments to tap(options: Object, fn: function)"
			);
		options = Object.assign({ type: "sync", fn: fn }, options);
		if (typeof options.name !== "string" || options.name === "")
			throw new Error("Missing name for tap");
		options = this._runRegisterInterceptors(options);
		this._insert(options);
	}

```

内部做一些参数处理，同时调用了内部私有函数`_runRegisterInterceptors` 返回一个新的 options

```
_runRegisterInterceptors(options) {
		for (const interceptor of this.interceptors) {
			if (interceptor.register) {
				const newOptions = interceptor.register(options);
				if (newOptions !== undefined) options = newOptions;
			}
		}
		return options;
	}
```

然后调用内部函数`_insert`去注册方法，`insert`内部实现

```
_insert(item) {
		this._resetCompilation();
		let before;
		if (typeof item.before === "string") before = new Set([item.before]);
		else if (Array.isArray(item.before)) {
			before = new Set(item.before);
		}
		let stage = 0;
		if (typeof item.stage === "number") stage = item.stage;
		let i = this.taps.length;
		while (i > 0) {
			i--;
			const x = this.taps[i];
			this.taps[i + 1] = x;
			const xStage = x.stage || 0;
			if (before) {
				if (before.has(x.name)) {
					before.delete(x.name);
					continue;
				}
				if (before.size > 0) {
					continue;
				}
			}
			if (xStage > stage) {
				continue;
			}
			i++;
			break;
		}
		this.taps[i] = item;
	}
```

##### Car.call() 调用分析

- Hook 类内部绑定的属性如下

```
class Hook {
	constructor(args) {
		this.call = this._call;
		...
	}

```

我们可以看到`this.call = this._call`，有个内部私有属性赋值到了`this.call`上面去,那么`this._call`是什么东西呢？我们继续往下看

```
Object.defineProperties(Hook.prototype , "_call" , {
	value:createCompileDelegate("call" , "sync")
	configurable: true,
	writable: true
})

```

通过这种方式，在`Hook.prototype`的原型上定义了一个私有属性`_call`，该属性的值是`createCompileDelegate`，这是一个方法，接收两个参数，那么这个方法执行的返回值是什么呢？继续往下看

```
function createCompileDelegate(name, type) {
	return function lazyCompileHook(...args) {
		this[name] = this._createCall(type);
		return this[name](...args);
	};
}
```

这个方法返回的是一个函数，同时这个函数接收一些参数，这些参数 也就是`Car.call(arg)`中的`args`参数

在这个函数内部，调用了一个`this._createCall`的函数，这个函数返回的是`compile`函数的执行结果

在`compile`函数的内部执行的逻辑

```
compile(options) {
	factory.setup(this, options);
	return factory.create(options);
}
```

`factory`是一个类，根据传入的参数，通过字符串拼接的方式生成要执行的`js`代码,然后通过`New Function`的形式来执行代码
