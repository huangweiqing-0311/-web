# node 

###  常见终端

- cmd   /   powershell   都是微软出的,都有自己的独特语法
- git bash   支持很多通用的命令,Linux系统中的, 很多命令在这里都可以用
- cmder  集成了很多终端,功能是相通的,内部写的很多命令,在Linux / Mac / iOS上面都可以写

### 终端常用命令

- 1.路径切换
  - cd 路径名
- 2.显示文件
  - ls 
- 3.显示当前路径
  - pwd
- 4.清屏
  - clear
- 5.删除文件
  - rm -rf 文件名/文件夹/*
- 6.新建文件
  - touch 文件名
- 7.使用vscode打开
  - code 文件名/文件夹
- 8.创建文件夹
  - mkdir 文件名



###  同步与异步

###### 同步

- 代码从上往下执行

###### 异步

- 代码同时执行

- 定时器/回调函数

###### 注意

- 1.绝大多数的代码都是同步的

- 2.如果有回调函数,大部分情况都是异步

  - 定时器

  - fs读写文件

  - ajax请求

  - jQuery动画回调函数

    ```
    $('div').animate({height:100},function(){})
    ```

### node.js中的路径

- 相对路径

  - 相对的是小黑框(终端)中所处的没用的路径,不是js文件

- 绝对路径

  - 不同用户的电脑盘符信息不通,不能写死/用到下面的全局变量

  - __dirname: 执行的js文件所处的文件夹的绝对路径

  - __filename: 执行的js文件自己的绝对路径

  - 我们用__dirname来拼接一个完整的绝对路径

  - ```
    const fs = require('fs')
    //使用__dirname来拼接一个要读文件的绝对路径,这样子在谁的电脑上都不会有问题
    fs.readFile(__dirname, '\\和js文件所在同一目录的文件名\\index.html', 'utf-8', (err, data)=>{
          if(err == null){
               console.log(data)
          }else{
              console.log(err) 
          }
    })
    ```

    

###    path 模块

- ###### 路径生成

  - 先导入path模块

  - ```
    const path = require('path')
    ```

  - 拼接路径

  - ```
    path.join(__dirname, '要导入的文件夹名称', '文件夹里面的文件名称')
    ```

    

###     http模块

-  1.引入http模块

  ```
  const http = require('http')
  ```

- 2.创建一个服务器

  ```
  const server = http.createServer((request, response) => {
       // 设置返回给用户的内容
       response.end('hello word')
  })
  ```

- 3.开启一个服务器(参数1是端口号, 参数2是开启成功后的回调函数)

  ```
  server.listen(3999, () => {
      console.log('服务器开启成功啦')
   }   
  ```



### 端口

- ######  物理端口

  - 电脑上的接口 USB网线

- ###### 虚拟端口

  - 看不到的,让系统,软件和外界通讯的一个通道
  - 比较靠前的基本被使用了,靠后的基本没有用
  - 建议用靠后一点的端口 1000+



###  静态资源服务器

- ###### 实现步骤

  - 1.导入模块

    ```
    const http = require('http')
    const fs = require('fs')
    const path = require('path')
    ```

  - 2.创建服务器

    ```
    const server = http.createServer((request, response) => {
           // 获取用户请求的文件(url) request.url
         const fullPath = path.join(__dirname, '文件夹名字', request.url)
         // 读取文件
         fs.readFile(fullPath, (err, data) => {
               if(err == null){
                   response.end(data) 
               }else{
                   response.end(err) 
               }
         })
    })
    ```

  - 3.开启服务器

    ```
    server.listen(4399, () => {
         console.log('服务器开启啦')
      }
    ```



###   NPM第三方模块的使用

- 1.新建一个文件夹(不要用中文, 名字不要用express)
- 2.终端中进入文件夹 输入命令 npm init -y
- 3.找到你要用的第三方模块
  - 在npm上面找
  - 输入命令 npm i 模块的名字(回车下载)
  - 导入模块
  - 使用模块













