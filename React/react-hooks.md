## React 顶层 Api

- Hooks 调用规则
  - 不能再循环，嵌套，条件函数中调用`Hook`
  - 在`React`的最顶层函数中调用

* 基础 Hooks

  - `useState`
    - `const [count , setCount] = useState(0)`
  - `useEffect`
    - 执行方式
      - 异步
    - 执行时机
      - 第一次渲染以及每次更新之后都会执行
      - `DOM`更新完毕之后都会执行
    - 解决的痛点
      - 大量相关的逻辑分散在不同的生命周期
      - 大量不相干的逻辑放在同一个生命周期函数
    - 相当于三个声明周期的组合
      - `componentDidMount`
      - `componentDidUpdate`
      - `componentWillUnmount`
    - 清除操作
      - 返回一个函数 `return function() {}`
    * 性能优化
      - 第二个参数数组
    * [参考](https://react.docschina.org/docs/hooks-effect.html)
  - `useContext`

* 额外 Hooks

  - `useReducer`
  - `useCallback`
  - `useMemo`
  - `useRef`
  - `useImperativeHandle`
  - `useLayoutEffect`
  - `useDebugValue`

* 生命周期
  - `constructor`
    - 避免将`props`赋值给`state`，会导致 Bug
  * `static getDerivedStateFromProps(props,state)`
    - `render`方法之前调用
    - 初始化挂载以及后续更新都会被调用
    - 返回一个对象更新`state`，如果返回`null`则不更新
    - 只要父级重新渲染，这个函数也会被调用
* `ReactDOM`
  - `ReactDOM.createPortal(child, container)`
  - 用法
    - `render`中返回`ReactDOM.createPortal`
