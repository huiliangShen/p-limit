# p-limit

> 多PromiseFunction并发控制包

## Install

```
$ npm install p-limit
```

## Usage

```js
import pLimit from 'p-limit';

const limit = pLimit(1);

const input = [
	limit(() => fetchSomething('foo')),
	limit(() => fetchSomething('bar')),
	limit(() => doSomething())
];

// 同时只会有一个Promise在跑
const result = await Promise.all(input);
console.log(result);
```

## API

### pLimit(concurrency)

Returns a `limit` function.
返回一个`limit`方法。

#### concurrency

Type: `number`\
Minimum: `1`\
Default: `Infinity`

Concurrency limit.

### limit(fn, ...args)

Returns the promise returned by calling `fn(...args)`.

#### fn

Type: `Function`

返回Promise的方法或者async方法

#### args

Any arguments to pass through to `fn`.

Support for passing arguments on to the `fn` is provided in order to be able to avoid creating unnecessary closures. You probably don't need this optimization unless you're pushing a *lot* of functions.

### limit.activeCount

正在执行的promises 数量

### limit.pendingCount

The number of promises that are waiting to run (i.e. their internal `fn` was not called yet).
正在等待执行的promises数量（fn内部尚未被执行的）

### limit.clearQueue()

清除正在等待执行的promises队列

Discard pending promises that are waiting to run.

This might be useful if you want to teardown the queue at the end of your program's lifecycle or discard any function calls referencing an intermediary state of your app.

Note: This does not cancel promises that are already running.

## FAQ

### 和[`p-queue`](https://github.com/sindresorhus/p-queue)包的差别?

This package is only about limiting the number of concurrent executions, while `p-queue` is a fully featured queue implementation with lots of different options, introspection, and ability to pause the queue.

## Related

- [p-queue](https://github.com/sindresorhus/p-queue) - Promise queue with concurrency control
- [p-throttle](https://github.com/sindresorhus/p-throttle) - Throttle promise-returning & async functions
- [p-debounce](https://github.com/sindresorhus/p-debounce) - Debounce promise-returning & async functions
- [p-all](https://github.com/sindresorhus/p-all) - Run promise-returning & async functions concurrently with optional limited concurrency
- [More…](https://github.com/sindresorhus/promise-fun)

---

<div align="center">
	<b>
		<a href="https://tidelift.com/subscription/pkg/npm-p-limit?utm_source=npm-p-limit&utm_medium=referral&utm_campaign=readme">Get professional support for this package with a Tidelift subscription</a>
	</b>
	<br>
	<sub>
		Tidelift helps make open source sustainable for maintainers while giving companies<br>assurances about security, maintenance, and licensing for their dependencies.
	</sub>
</div>
