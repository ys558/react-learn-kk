### **React所有核心接口可参见:**
[React Api](https://github.com/facebook/react/blob/master/packages/react/index.js)
+ 这里抽其中的3个接口模拟实践: 
    + [ReactDom.render](https://github.com/facebook/react/blob/master/packages/react-dom/src/client/ReactDOM.js): 属于客户端渲染的ReactDom.render,另外还有服务端渲染,这里不做展开。
    + React.Component: `import React {Component} from 'react';`的接口
    + [React.createElement](https://github.com/facebook/react/blob/master/packages/react-dom/src/client/ReactDOMComponent.js): class组件里render()函数,实质上是调用`React.createElement`接口实现
    + [setState]()

+ 阅读步骤:
0. `create-react-app .` 创建该项目

1. 导入需要提供的伪代码文件,里面包含这两个接口实现的伪代码:`src/components/react-source-code-study/src/kkreact/`

2. 将src里所有文件删掉, 并新建`src/components/react-source-code-study/src/index.js`

3. 内容见具体文件:index.js及其
[注释0.](https://github.com/ys558/react-kaikeba/blob/master/src/components/react-source-code-study/src/index.js)

4. **自行实现核心接口`React.createElement()`**
    + 创建`src/components/react-source-code-study/src/kreact.jsx`
    + 具体内容见该文件及
    [注释1.2.3.](https://github.com/ys558/react-kaikeba/blob/master/src/components/react-source-code-study/src/kreact.js)

5. 返回index.js,创建多一个类组件,见
[注释2.3.](https://github.com/ys558/react-kaikeba/blob/master/src/components/react-source-code-study/src/index.js)

6. **实现render()**
    + 新建`src/components/react-source-code-study/src/kreact-dom.js`
    + [注释1.2.3](https://github.com/ys558/react-kaikeba/blob/master/src/components/react-source-code-study/src/kreact-dom.js)

7. 新建`src/components/react-source-code-study/src/kvdom.js`,
[注释1.](https://github.com/ys558/react-kaikeba/blob/master/src/components/react-source-code-study/src/kvdom.js)

8. `src/components/react-source-code-study/src/index.js`
[注释4.](https://github.com/ys558/react-kaikeba/blob/master/src/components/react-source-code-study/src/index.js)

9. `src/components/react-source-code-study/src/kreact.js`
[注释4.5.6.7.](https://github.com/ys558/react-kaikeba/blob/master/src/components/react-source-code-study/src/kreact.js)

10. **将虚拟dom操作转换为真实dom**
    + `src/components/react-source-code-study/src/kvdom.js`
[注释2.3.4.5.](https://github.com/ys558/react-kaikeba/blob/master/src/components/react-source-code-study/src/kvdom.js)

+ 总结



+ ### **PureComponent**
    + 继承Component，主要是设置了shouldComponentUpdate生命周期
  ```jsx
  import shallowEqual from './shallowEqual'
  import Component from './Component'
  export default function PureComponent(props, context) {
    Component.call(this, props, context)
  }

  PureComponent.prototype = Object.create(Component.prototype)
  PureComponent.prototype.constructor = PureComponent
  PureComponent.prototype.isPureReactComponent = true
  PureComponent.prototype.shouldComponentUpdate = shallowCompare

  function shallowCompare(nextProps, nextState) {
    return !shallowEqual(this.props, nextProps) ||
    !shallowEqual(this.state, nextState)
  }
  ```

+ ### **diff算法和setState**
    + ### **setState**
    + setState并没有直接操作去渲染，而是执行了一个异步的updater队列 我们使用一个类来专门管理，./kkreact/Component.js
    + 具体代码见`src/components/react-source-code-study/src/kkreact/Component.js`的
    [注释](https://github.com/ys558/react-kaikeba/blob/master/src/components/react-source-code-study/src/kkreact/Component.js)