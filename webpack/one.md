地址：https://webpack.docschina.org/guides/asset-management/

基础命令 webpack

## 基本配置：
```json
  {
    "name": "webpack-demo",
    "version": "1.0.0",
    "description": "",
    "private": "true",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "build": "webpack"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "devDependencies": {
      "webpack": "^5.70.0",
      "webpack-cli": "^4.9.2"
    },
    "dependencies": {
      "lodash": "^4.17.21"
    }
  }

```

## 资源配置

```javaScript
module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
```
应保证 loader 的先后顺序：'style-loader' 在前，而 'css-loader' 在后。如果不遵守此约定，webpack 可能会抛出错误。

## 基本插件
 plugins：
  HtmlWebpackPlugin html管理 https://github.com/jantimon/html-webpack-plugin
