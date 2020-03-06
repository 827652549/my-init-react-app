# my-init-react-app

&emsp;&emsp;从零创建一个React应用，不使用脚手架工具。

### 文件结构
```
.
├── LICENSE
├── README.md
├── package.json
├── public
│   └── index.html
├── src
│   ├── App.css
│   ├── App.js
│   └── index.js
├── webpack.config.js
├── .gitignore
└── .babelrc
```

### 实现过程：

以下是在mac终端中实现的，具体文件的内容可直接粘贴本项目对应的文件

1. 初始化`npm`项目，生成`package.json`。

2. 初始化`git`，创建`.gitignore`忽略指定文件(node_modules等)。

3. 添加`public/index.html`。

4. 安装`Babel`，创建`.babelrc`进行配置。

5. 安装`webpack`，创建`webpack.config.js`进行配置。

6. 安装`react`、`react-dom`、热更新`react-hot-loader`。

7. 添加`src/index.js`、`src/App.js`、`src/App.css`。

8. 配置`package.json`，修改启动命令。

9. 启动项目。

### 分部步骤：

&emsp;准备：确保本机上已经安装`npm`、`node`、(`git`)

> 如果你不打算添加版本控制，所有git操作均可忽略。


1. **初始化`npm`项目，生成`package.json`。**

```
npm init -y
```

2. **初始化`git`，创建`.gitignore`忽略指定文件(node_modules等)。**

```
git init
touch .gitignore
```

`.gitignore`
```
#这个文件是让git过滤的列表

#过滤依赖
/node_modules

#过滤生产
/dist/
/build/

#苹果系统的隐藏文件
.DS_Store
```

3. **添加`public/index.html`。**

```
mkdir public
cd public
touch index.html
```

`index.html`
```html
<!-- sourced from https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <title>React Starter</title>
</head>

<body>
  <div id="root"></div>
  <noscript>
    You need to enable JavaScript to run this app.
  </noscript>
  <script src="../dist/bundle.js"></script>
</body>

</html>
```

&emsp;&emsp;这里引入的`bundle.js`后面会用到。

4. **安装`Babel`，创建`.babelrc`进行配置**。

```
cd ..
npm install -D @babel/core@7.1.0 @babel/cli@7.1.0 @babel/preset-env@7.1.0 @babel/preset-react@7.0.0.
touch .babelrc
```

`.babelrc`
```json
{
  "presets": ["@babel/env", "@babel/preset-react"]
}
```

5. **安装`webpack`，创建`webpack.config.js`进行配置。**

```
npm install -g -D webpack webpack-cli webpack-dev-server style-loader css-loader babel-loader
touch webpack.config.js
```

`webpack.config.js`
```javascript
const path = require("path");
const webpack = require("webpack");

module.exports = {
  entry: "./src/index.js",
  mode: "development",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /(node_modules|bower_components)/,
        loader: "babel-loader",
        options: { presets: ["@babel/env"] }
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  resolve: { extensions: ["*", ".js", ".jsx"] },
  output: {
    path: path.resolve(__dirname, "dist/"),
    publicPath: "/dist/",
    filename: "bundle.js"
  },
  devServer: {
    contentBase: path.join(__dirname, "public/"),
    port: 3000,
    publicPath: "http://localhost:3000/dist/",
    hotOnly: true
  },
  plugins: [new webpack.HotModuleReplacementPlugin()]
};
```

6. **安装`react`、`react-dom`、热更新`react-hot-loader`。**

```
npm install -D react react-dom react-hot-loader
```

7. **添加`src/index.js`、`src/App.js`、`src/App.css`。**

```
mkdir src
cd src
touch index.js
touch App.js
touch App.css
```

`index.js`
```javascript
import React from "react";
import ReactDOM from "react-dom";
import App from "./App.js";
ReactDOM.render(<App />, document.getElementById("root"));
```

`App.js`
```javascript
import React, { Component} from "react";
import {hot} from 'react-hot-loader';
import "./App.css";

class App extends Component{
  render(){
    return(
      <div className="App">
        <h1> Hello</h1>
      </div>
    );
  }
}

export default hot(module)(App);
```

`App.css`
```css
.App {
  margin: 1rem;
  font-family: Arial, Helvetica, sans-serif;
  border: 1px solid red;
}
```

8. **配置`package.json`，修改启动命令。**

&emsp;&emsp;在package.json里配置scripts字段。

```json
"scripts": {
    "start": "webpack-dev-server --mode development",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
```

9. **启动项目。**

```
npm start
```

&emsp;&emsp;在浏览器键入[http://localhost:3000](http://localhost:3000)以启动项目

### 额外说明

[参考链接](https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658)

