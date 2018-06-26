# react-multi-page-config

> react 多页配置

## 配置

- 安装 [react-app-rewired](https://github.com/timarney/react-app-rewired) 并修改 `package.json` 里的启动配置：
``` bash
$ npm install react-app-rewired --save-dev
```
``` json
/* package.json */
"scripts": {
-   "start": "react-scripts start",
+   "start": "react-app-rewired start",
-   "build": "react-scripts build",
+   "build": "react-app-rewired build",
-   "test": "react-scripts test --env=jsdom",
+   "test": "react-app-rewired test --env=jsdom",
}
```

- 然后在项目根目录创建一个 config-overrides.js 用于修改默认配置。

``` js
module.exports = function override(config, env) {
  // do stuff with the webpack config...
  return config;
};
```

- 安装 react-multi-page-config ，并修改 config-overrides.js
``` bash
npm install react-multi-page-config --save-dev
```
``` js
+ const MultiPage = require('react-multi-page-config');
  module.exports = function override(config, env) {
+   config = MultiPage.init(config);
    return config;
  };
```

## 开发说明

### 如何声明一个页面

在 `src` 目录下创建以 `.page.js` 的页面入口文件。

### 如何为某个页面指定 `html` 模板

在 `xx.page.js` 同级目录下创建 `xx.html` 。

## 项目结构

```
src
├── App.css
├── App.js
├── App.test.js
├── index.css
├── index.page.js                // 页面入口文件，输出 build/index.html
├── logo.svg
├── pages
│   ├── home
│   │   ├── home.js
│   │   └── home.page.js         // 页面入口文件，输出 build/pages/home/home.html
│   ├── page1
│   │   ├── page1.html           // 为 page1.html 页面指定 html 模板
│   │   ├── page1.js
│   │   └── page1.page.js        // 页面入口文件，输出 build/pages/page1/page1.html
│   └── page2
│       ├── page2.css
│       ├── page2.js
│       └── page2.page.js        // 页面入口文件，输出 build/pages/page2/page2.html
└── registerServiceWorker.js
```
