# 项目配置

下载脚手架 npx create-react-app 项目名称

## antd-mobile 配置

1. 移动端文档比较陈旧，看 pc 库文档进行配置
   pc 端：https://ant.design/docs/react/use-with-create-react-app-cn

移动端：https://mobile.ant.design/docs/react/introduce-cn

2. 安装依赖
   npm i antd-mobile
   npm i @craco/craco craco-less -D

3. 修改 package.json 中启动项目指令

```json
"scripts": {
   "start": "craco start",
   "build": "craco build",
   "test": "craco test",
}
```

4. 定义配置文件
   在项目根目录创建一个 `craco.config.js` 用于修改默认配置。

```js
// 配置文件：用来修改react脚手架配置
const CracoLessPlugin = require('craco-less')

module.exports = {
  plugins: [
    {
      // 自定义主题
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: {
              // 当前less变量是pc库的
              // '@primary-color': '#1DA57A'
              // 使用移动端的less变量
              // https://github.com/ant-design/ant-design-mobile/blob/master/components/style/themes/default.less
              '@brand-primary': '#e94f4f',
            },
            javascriptEnabled: true,
          },
        },
      },
    },
  ],
}
```

5. 全局引入 antd-mobile 样式文件

```js
// src/index.js
import 'antd-mobile/dist/antd-mobile.less'
```

6. 解决事件点透问题

```html
<!-- public/index.html -->
<meta
  name="viewport"
  content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no"
/>
<script src="https://as.alipayobjects.com/g/component/fastclick/1.0.6/fastclick.js"></script>
<script>
  if ('addEventListener' in document) {
    document.addEventListener(
      'DOMContentLoaded',
      function () {
        FastClick.attach(document.body)
      },
      false
    )
  }
  if (!window.Promise) {
    document.writeln(
      '<script src="https://as.alipayobjects.com/g/component/es6-promise/3.2.2/es6-promise.min.js"' +
        '>' +
        '<' +
        '/' +
        'script>'
    )
  }
</script>
```

7. 测试使用
   使用 Button 组件看效果

## viewport 适配

自动将 px 单位转换 viewport 单位
解决：使用 postcss 插件

1. 下载
   npm i postcss-px-to-viewport -D

2. 配置

```js
// craco.config.js
const pxtoviewport = require('postcss-px-to-viewport')

module.exports = {
  // ...
  style: {
    postcss: {
      plugins: [
        // https://www.npmjs.com/package/postcss-px-to-viewport
        pxtoviewport({
          // 设计稿的宽度
          viewportWidth: 375,
          // 求vw精确到小数点后几位
          unitPrecision: 3,
          propList: ['*'],
          // propList: ['width', 'font-size', 'margin', 'padding'],
        }),
      ],
    },
  },
}
```

3. 测试
   写 css 样式 px 单位，看是否会自动转换成 vw 单位

## react-router 配置

1. 下载
   npm i react-router-dom

2. 定义路由组件

- src/pages/Login/LoginCode
- src/pages/Login/LoginPassword
- src/pages/Register/RegisterPhone
- src/pages/Register/RegisterCode
- src/pages/Register/RegisterPassword

3. 配置

```js
// src/router/index.js
// 前端路由的配置文件
import LoginCode from '../pages/Login/LoginCode'
import LoginPassword from '../pages/Login/LoginPassword'
import RegisterPhone from '../pages/Register/RegisterPhone'
import RegisterCode from '../pages/Register/RegisterCode'
import RegisterPassword from '../pages/Register/RegisterPassword'

// 路由的配置项
const routes = [
  {
    path: '/login/code',
    component: LoginCode,
  },
  {
    path: '/login/password',
    component: LoginPassword,
  },
  {
    path: '/register/phone',
    component: RegisterPhone,
  },
  {
    path: '/register/code',
    component: RegisterCode,
  },
  {
    path: '/register/password',
    component: RegisterPassword,
  },
]

// 暴露出去
export default routes
```

4. 使用

```js
// App.jsx
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom'

import routes from './router'

function App() {
  return (
    <Router>
      <Switch>
        {
          // 遍历路由配置项，生成Route组件
          routes.map((route) => {
            return <Route {...route} key={route.path} />
          })
        }
      </Switch>
    </Router>
  )
}

export default App
```

5. 测试
   在浏览器输入地址访问，看是否能得到对应的路由组件

## 完成项目后打包

npm run build
打包后无法运行，需要下载
npm i serve -g
运行目录 serve 运行的目录
切换端口 serve 目录 -p 8888

## 懒加载

1.将组件单独打包，单独打包成一个 js 文件和 css 文件 
2.按需加载，需要用的时候加载

### 方法：

1.由引入 lazy
import { lazy } from 'react'
暴露路由 const LoginCode = lazy(() => import('../pages/Login/LoginCode'))

2.app 引入 Suspense 包裹元素
import { Suspense } from 'react'
Suspense 需要一个 loading 图
<Suspense fallback={<Icon type="loading"/>}><Suspense>
