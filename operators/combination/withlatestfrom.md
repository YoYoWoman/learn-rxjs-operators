# withLatestFrom

#### 签名: `withLatestFrom(other: Observable, project: Function): Observable`

## 还提供另一个 observable 的最新值。

---

:bulb: 如果你希望每当任意 observable 发出值时各个 observable 的最新值，请尝试 [combinelatest](combinelatest.md)！

---

### 示例

##### 示例 1: 发出频率更快的第二个 source 的最新值

( [jsBin](http://jsbin.com/fitekeseru/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/9c3pfgpk/) )

```js
// 每5秒发出值
const source = Rx.Observable.interval(5000);
// 每1秒发出值
const secondSource = Rx.Observable.interval(1000);
const example = source
  .withLatestFrom(secondSource)
  .map(([first, second]) => {
    return `First Source (5s): ${first} Second Source (1s): ${second}`;
  });
/*
  输出:
  "First Source (5s): 0 Second Source (1s): 4"
  "First Source (5s): 1 Second Source (1s): 9"
  "First Source (5s): 2 Second Source (1s): 14"
  ...
*/
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 第二个 source 发出频率更慢一些

( [jsBin](http://jsbin.com/vujekucuxa/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/bywLL579/) )

```js
// 每5秒发出值
const source = Rx.Observable.interval(5000);
// 每1秒发出值
const secondSource = Rx.Observable.interval(1000);
// withLatestFrom 的 observable 比源 observable 慢
const example = secondSource
  // 两个 observable 在发出值前要确保至少都有1个值 (需要等待5秒)
  .withLatestFrom(source)
  .map(([first, second]) => {
    return `Source (1s): ${first} Latest From (5s): ${second}`;
  });
/*
  "Source (1s): 4 Latest From (5s): 0"
  "Source (1s): 5 Latest From (5s): 0"
  "Source (1s): 6 Latest From (5s): 0"
  ...
*/
const subscribe = example.subscribe(val => console.log(val));
```


### 其他资源

* [withLatestFrom](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-withLatestFrom) :newspaper: - 官方文档
* [组合操作符: withLatestFrom](https://egghead.io/lessons/rxjs-combination-operator-withlatestfrom?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/operator/withLatestFrom.ts](https://github.com/ReactiveX/rxjs/blob/master/src/operator/withLatestFrom.ts)
