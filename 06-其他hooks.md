### useContext 

```js
-- context.js
import React from 'react'
export default React.createContext()


-- App.js
export default class App extends Component {
  render() {
    return (
      <testContext.Provider value={{ name: 'zs' }}>
        <Test></Test>
        <Test1></Test1>
      </testContext.Provider>
    )
  }
}

-- Test.js
import React, { useContext } from 'react'
import testContext from './context'
export default function Test() {
  const context = useContext(testContext)
  console.log(context)
  return <div></div>
}


```

### useReducer

```js
import React, { useReducer } from 'react'

const initialState = { count: 0, msg: '哈哈' }

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {
        ...state,
        count: state.count + 1,
      }
    case 'decrement':
      return {
        ...state,
        count: state.count - 1,
      }
    default:
      throw new Error()
  }
}
export default function Test1() {
  const [state, dispatch] = useReducer(reducer, initialState)
  return (
    <>
      Count: {state.count}
      msg: {state.msg}
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
    </>
  )
}

// useReduder的第三个参数:

function init(initialCount) {
  return {count: initialCount};
}

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    case 'reset':
      return init(action.payload);
    default:
      throw new Error();
  }
}

function Counter({initialCount}) {
  const [state, dispatch] = useReducer(reducer, initialCount, init);
  return (
    <>
      Count: {state.count}
      <button
        onClick={() => dispatch({type: 'reset', payload: initialCount})}>
        Reset
      </button>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}


```

### useCallBack

```js
点击 Button1 的时候只会更新 Button1 和 Button3 后面的内容; 因为父组件更新了,子组件也更新
点击 Button2 会将三个按钮后的内容都更新; 因为button2监听了count2的变化,只要count2没有变化,Button组件就不会更新
点击 Button3 的也是只更新 Button1 和 Button3 后面的内容。 因为父组件更新了,子组件也更新


-- App.js
import React, { useState, useCallback } from 'react';
import Button from './Button';

export default function App() {
  const [count1, setCount1] = useState(0);
  const [count2, setCount2] = useState(0);
  const [count3, setCount3] = useState(0);

  const handleClickButton1 = () => {
    setCount1(count1 + 1);
  };

  const handleClickButton2 = useCallback(() => {
    setCount2(count2 + 1);
  }, [count2]);

  return (
    <div>
      <div>
        <Button onClickButton={handleClickButton1}>Button1</Button>
      </div>
      <div>
        <Button onClickButton={handleClickButton2}>Button2</Button>
      </div>
      <div>
        <Button
          onClickButton={() => {
            setCount3(count3 + 1);
          }}
        >
          Button3
        </Button>
      </div>
    </div>
  );
}

--Button.js
import React from 'react';

const Button = ({ onClickButton, children }) => {
  return (
    <>
      <button onClick={onClickButton}>{children}</button>
      <span>{Math.random()}</span>
    </>
  );
};

export default React.memo(Button); //React.memo 相当于就是类组件的PureComponent
```

#### React.memo

```js
--App.js  注意: 这里App要使用类组件(如果App.js使用了函数组件,并使用了useState.即便不使用React.memo也有优化效果,但是效果可能会比较混乱)

import React, { useState, useEffect } from 'react'
import Test from './Test'
function getRandomIntInclusive(min, max) {
  min = Math.ceil(min)
  max = Math.floor(max)
  return Math.floor(Math.random() * (max - min + 1)) + min //含最大值，含最小值
}
class App extends React.Component {
  state = {
    count: 0,
  }
  render() {
    console.log('app渲染了')
    return (
      <div>
        <button
          onClick={() => {
            this.setState({
              count: getRandomIntInclusive(1, 2),
            })
          }}
        >
          按钮
        </button>
        <Test count={this.state.count}></Test>
      </div>
    )
  }
}

export default App


-- Test.js 
import React from 'react'

function Test(props) {
  console.log('Test组件渲染了-' + props.count)
  return <div>{props.count}</div>
}
export default React.memo(Test)
```





### useMemo

>会缓存一个计算的结果,如果没有变化,则不会重新执行计算

```js
// 使用前
import React,{useState} from 'react';
 
export default function WithoutMemo() {
    const [count, setCount] = useState(1);
    const [val, setValue] = useState('');
 
    function expensive() {
        console.log('compute');
        let sum = 0;
        for (let i = 0; i < count * 100; i++) {
            sum += i;
        }
        return sum;
    }
 
    return <div>
        <h4>{count}-{val}-{expensive()}</h4>
        <div>
            <button onClick={() => setCount(count + 1)}>+c1</button>
            <input value={val} onChange={event => setValue(event.target.value)}/>
        </div>
    </div>;
}

// 使用后
export default function WithMemo() {
    const [count, setCount] = useState(1);
    const [val, setValue] = useState('');
    const expensive = useMemo(() => {
        console.log('compute');
        let sum = 0;
        for (let i = 0; i < count * 100; i++) {
            sum += i;
        }
        return sum;
    }, [count]);
 
    return <div>
        <h4>{count}-{expensive}</h4>
        {val}
        <div>
            <button onClick={() => setCount(count + 1)}>+c1</button>
            <input value={val} onChange={event => setValue(event.target.value)}/>
        </div>
    </div>;
}
```

### useRef

```js
function TextInputWithFocusButton() {
  const inputEl = useRef(null); // 传入的null表示inputEl.current的初始值
  const onButtonClick = () => {
    // `current` 指向已挂载到 DOM 上的文本输入元素
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

### useImperativeHandle

>`useImperativeHandle` 可以让你在使用 `ref` 时自定义暴露给父组件的实例值. `useImperativeHandle` 应当与 [`forwardRef`]一起使用

```js
--App.js
import React, { useState, useEffect } from 'react'
import FancyInput from './FancyInput'

const inputRef = React.createRef()
class App extends React.Component {
  render() {
    return (
      <div>
        <button
          onClick={() => {
            
            console.log(inputRef.current.focus())
          }}
        >
          按钮
        </button>
        <FancyInput ref={inputRef}></FancyInput>
      </div>
    )
  }
}

export default App


--FancyInput.js
import React, { useRef, useImperativeHandle, forwardRef } from 'react'
function FancyInput(props, ref) {
  const inputRef = useRef()
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus()
    },
  }))
  return <input ref={inputRef} />
}
FancyInput = forwardRef(FancyInput)
export default FancyInput


```

### useLayoutEffect

>作用与 `useEffect` 相同，但它会在所有的 DOM 变更之后同步调用 effect。可以使用它来读取 DOM 布局并同步触发重渲染。在浏览器执行绘制之前，`useLayoutEffect` 内部的更新计划将被同步刷新。

```js
useEffect
这个是在render结束后,你的callback函数执行,但是不会阻塞浏览器渲染

useLayoutEffect
这个是用在处理DOM的时候,当你的useEffect里面的操作需要处理DOM,并且会改变页面的样式,就需要用这个,否则可能会出现出现闪屏问题, useLayoutEffect里面的callback函数会在DOM更新完成后立即执行,但是会在浏览器进行任何绘制之前运行完成,阻塞了浏览器的绘制

import React, { useEffect, useLayoutEffect, useRef } from 'react'
import TweenMax from 'gsap' // npm i gsap@3.7.0
import './index.css'

const Animate = () => {
  const REl = useRef(null)
  useLayoutEffect(() => {
    /*下面这段代码的意思是当组件加载完成后,在0秒的时间内,将方块的横坐标位置移到600px的位置*/
    TweenMax.to(REl.current, 0, { x: 600 })
  }, [])
  return (
    <div className="animate">
      <div ref={REl} className="square">
        square
      </div>
    </div>
  )
}

export default Animate
```

### useDebugValue

```js
useDebugValue 可用于在 React 开发者工具中显示自定义 hook 的标签

import { useState, useDebugValue } from 'react'
function getRandomIntInclusive(min, max) {
  min = Math.ceil(min)
  max = Math.floor(max)
  return Math.floor(Math.random() * (max - min + 1)) + min //含最大值，含最小值
}

export default function useFriendStatus() {
  const [isOnline, setIsOnline] = useState(null)

  setTimeout(() => {
    let result = getRandomIntInclusive(0, 1)
    console.log(result)
    setIsOnline(result ? 'online' : 'offline')
  }, 1000)

  // 在react开发者工具中的这个 Hook 旁边显示标签
  // "FriendStatus: Online"
  useDebugValue(isOnline)

  return isOnline
}

```

