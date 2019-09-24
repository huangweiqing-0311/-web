### webpack-打包起步

[传送门](https://www.webpackjs.com/guides/getting-started/)

1. webpack是基于node的一个工具
2. 创建文件夹
   1. src: 写js代码
   2. dist: index.html(导入当前目录的main.js)(打包会生成的)
3. 初始化项目 npm init -y
4. 安装 webpack cnpm install webpack webpack-cli --save
5. 打包 npx webpack

###### webpack-配置文件

1. 设置webpack的打包方式

2. 项目根目录下新增一个文件 webpack.config.js

3. 执行 npx webpack --config webpack.config.js

4. 自动读取这个文件进行打包

   ```
   // 导入 path 路径模块
   const path = require('path')
   // 暴露出去
   module.exports = {
      // 打包入口(告诉webpack用到了什么东西)
      entry: './src/index.js',
      // 出口, 告诉webpack打包到哪里去
      output: {
        // 文件名
        filename: 'main.js',
        // 路径
        path: path.resolve(_dirname, 'dist')
      }  
     } 
   ```

###### webpack-dev-server

[传送门](https://www.webpackjs.com/guides/development/#%E4%BD%BF%E7%94%A8-webpack-dev-server)

1. dev 开发

2. server 服务器

3. 允许我们开启一个开发用的服务器,自动监听文件变化,自动打开浏览器.自动刷新浏览器

4. 装包 cnpm install --save-dev webpack-dev-server

5. webpack.config.js 中增加配置

6. 添加 packge.json 中的script

   ```
   "start": "webpack-dev-server --open"
   ```

###### webpack-loader

[传送门](https://www.webpackjs.com/loaders/)

1. 其他的文件默认不支持解析
2. 提供了一个机制loader,可以编译其他的文件
3. 让webpack拥有解析不同文件的能力
4. 不同文件对应的loader不一样
5. webpack默认只能够解析js

###### webpack-打包css

[传送门](https://www.webpackjs.com/guides/asset-management/#%E5%8A%A0%E8%BD%BD-css)

1. 装包 cnpm install --save-dev style-loader css-loader

2. 添加配置

3. ```
   const path = require('path')
   module.exports = {
     entry: './src/index.js',
     output: {
          filename: 'bundle.js',
          path: path.resolve(_dirname, 'dist')
     },
     module: {
         rules: [
              {
                  test: /\.css$/,
                  use: [
                      'style-loader',
                      'css-loader'
                  ]
              }
         ]
     }
     }
   ```

   

###### webpack-less

[传送门](https://www.webpackjs.com/loaders/less-loader/)

1. 装包 cnpm install --save-dev less-loader less

2. 配置规则

3. ```
   module.exports = {
      ...
       module: {
           rules: [{
               test: /\.less$/,
               use: [{
                   loader: "style-loader" // creates style nodes from JS strings
               }, {
                   loader: "css-loader" // translates CSS into CommonJS
               }, {
                   loader: "less-loader" // compiles Less to CSS
               }]
           }]
       }
   };
   ```

   