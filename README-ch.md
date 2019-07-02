# Javascript 状态机

[![NPM version](https://badge.fury.io/js/javascript-state-machine.svg)](https://badge.fury.io/js/javascript-state-machine)
[![Build Status](https://travis-ci.org/jakesgordon/javascript-state-machine.svg?branch=master)](https://travis-ci.org/jakesgordon/javascript-state-machine)

一个 JS 有限状态机的库

有限状态机模型要点
<br>
![matter state machine](examples/matter.png)


### 用户须知

> **VERSION 3.0** 是早期版本的重大改写。
  现有 2.x 用户建议阅读升级指南，确保已升级。 [Upgrade Guide](docs/upgrading-from-v2.md).

<br>

# 安装

在浏览器里使用:

```html
  <script src='state-machine.js'></script>
```

> 下载完整文件来源：[source](dist/state-machine.js) ，或者压缩版 [minified version](dist/state-machine.min.js)

用 npm 安装:

```shell
  npm install --save-dev javascript-state-machine
```

在 Node.js 使用:

```javascript
  var StateMachine = require('javascript-state-machine');
```

# Usage

一个状态机可以这样构造出来（new 操作符） ：
  * init 初始的状态值
  * transitions.name 变化名称
  * transitions.from 变化允许来自的状态值 (可以为数组)
  * transitions.to 变化成什么状态

```javascript
  var fsm = new StateMachine({
    init: 'solid',
    transitions: [
      { name: 'melt',     from: 'solid',  to: 'liquid' },
      { name: 'freeze',   from: 'liquid', to: 'solid'  },
      { name: 'vaporize', from: 'liquid', to: 'gas'    },
      { name: 'condense', from: 'gas',    to: 'liquid' }
    ],
    methods: {
      onMelt:     function() { console.log('I melted')    },
      onFreeze:   function() { console.log('I froze')     },
      onVaporize: function() { console.log('I vaporized') },
      onCondense: function() { console.log('I condensed') }
    }
  });
```

... 经过上诉步骤，返回值 fsm 拥有一个 property 名为 state (不可通过赋值直接变更):

  * `fsm.state`

... 经过上诉步骤，返回值 fsm 拥有以下的方法 (变化函数) ，让 state 变化成不同值:

  * `fsm.melt()`
  * `fsm.freeze()`
  * `fsm.vaporize()`
  * `fsm.condense()`

... 以下函数，会在转化状态变化，完成时，被调用 :

  * `onMelt()`
  * `onFreeze()`
  * `onVaporize()`
  * `onCondense()`

... 当然，还有以及以下的 helper 方法:

  * `fsm.is(s)`            - 当 status 和 s 相等时候，返回 true，否则 false。
  * `fsm.can(t)`           - 当前状态可运行变化名称 t 时，返回 true，否则 false。
  * `fsm.cannot(t)`        - return true if transition `t` cannot occur from the current state
  * `fsm.transitions()`    - return list of transitions that are allowed from the current state
  * `fsm.allTransitions()` - return list of all possible transitions
  * `fsm.allStates()`      - return list of all possible states

# Terminology

示例代码中，状态机有下列有效状态 [**States**](docs/states-and-transitions.md)

  * solid
  * liquid
  * gas

示例代码中，状态机可以变化自己的状态，用以下方法 [**Transitions**](docs/states-and-transitions.md)

  * melt
  * freeze
  * vaporize
  * condense

示例代码中，状态机，在变化过程中，可以触发一些动作(运行一些函数) [**Lifecycle Events**](docs/lifecycle-events.md)

  * onBeforeMelt
  * onAfterMelt
  * onLeaveSolid
  * onEnterLiquid
  * ...

状态机也可以设置任意的其他数据，和方法 [**Data and Methods**](docs/data-and-methods.md).

你可以用 machine factory 来封装出具有固定参数的状态机，便于生成多个实例 [**State Machine Factory**](docs/state-machine-factory.md).

# 其他文档

阅读更多

  * [状态和变化关系](docs/states-and-transitions.md)
  * [其他数据和方法](docs/data-and-methods.md)
  * [生命周期](docs/lifecycle-events.md)
  * [异步的变化](docs/async-transitions.md)
  * [构造时候初始化，和构造之后初始化状态](docs/initialization.md)
  * [错误事件处理](docs/error-handling.md)
  * [状态历史记录，状态回退](docs/state-history.md)
  * [变更记录转化成可视化数据](docs/visualization.md)
  * [状态机工厂](docs/state-machine-factory.md)
  * [从 2.x 升级](docs/upgrading-from-v2.md)

# 贡献

你可以为 [Contribute](docs/contributing.md) 这个库贡献 issues 或者 pull requests.

# 发行说明

请看 [RELEASE NOTES](RELEASE_NOTES.md) 文件.

# 执照

请看 [MIT LICENSE](https://github.com/jakesgordon/javascript-state-machine/blob/master/LICENSE) 文件.

# 联系我

如果你有一些建议，反馈，请求要求，bug 上报，你可以用以下方式联系到我 [jake@codeincomplete.com](mailto:jake@codeincomplete.com), 或者我的个人网站 : [Code inComplete](http://codeincomplete.com/)
