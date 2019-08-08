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

  - 注意:

    1. 获取用户请求的url地址 (文件名) request.url
    2. 文件存在与否取决于 err的值 err==null  => 成功



###   NPM第三方模块的使用

- 1.新建一个文件夹(不要用中文, 名字不要用express)
- 2.终端中进入文件夹 输入命令 npm init -y
- 3.找到你要用的第三方模块
  - 在npm上面找
  - 输入命令 npm i 模块的名字(回车下载)
  - 导入模块
  - 使用模块

## express实现静态资源服务器

1. 装包

2. 导包

3. 用包

   ```
   //导入express
   const express = require('express')
   //创建服务器对象
   const app = express()
   
   //暴露public文件夹 让外面访问
   app.use(express.static('public))
   
   //开启服务器
   app.listen(4399, ()=> {
         console.log('服务器开启了')
   })
   ```



#### get数据获取

1. 使用req.query可以获取到用户get提交的数据
2. 数据的格式对象
   1. 使用 .语法
   2. es6结构也可以 如 const {name} = req.query

#### post数据获取

1. 使用body-parser这个第三方模块获取post提交的数据
   1. 下载body-parser
   2. 导入
   3. 通过req.body可以获取到用户提交的数据
   4. body-parser的作用
      1. 把post文件数据放到req.body中

#### post数据-文件获取

1. 接收formData上传的文件,要通过multer这个第三方模块
   1. 下包 npm i multer
   2. 导包
   3. 用包
2. 注意: 
   1. req.file获取文件的信息
   2. req.body获取文本信息



#### 中间件

中间件是请求和响应之间额外注册的回调函数

1. 服务器接收请求的时候,会执行注册的回调函数
2. 执行的顺序,按照编写的顺序执行
3. next() 执行下一个回调函数, 如果不写,程序就不会往下执行,卡在某个函数
4. 中间件中的req对象是共享的,添加的属性,后面也可以用



### jQuery里用formData

1. 如果使用formData提交表单数据,要在请求体里设置
   1. contentType: false,
   2. processData: false,
2. 为啥? 
   1. 因为jQuery他会帮我们自动设置请求头
   2. jQuery会把data后面给的对象转成 参数=值 形式的字符串





#### 跨域概念

1. 浏览器使用ajax时,如果请求了的接口地址和当前打开的页面地址不同源称之为跨域

#### 跨域-同源

1. 协议: http://
2. 地址: 127.0.0.1
3. 端口: 4399
4. 两个地址的协议,地址,端口都一样称之为 同源

不同源

- 两个http地址的 , 协议, 地址, 端口任何一个不一样,称之为不同源

跨域访问

- 浏览器使用ajax,向不同源的接口发送请求,称之为跨域访问

 

#### 跨域-解决方案-cors

- 原理 :  服务器在返回响应报文的时候,在响应头中 设置一个允许的header

- 自己实现

  1. 响应数据时,额外设置header Access-Control-Allow-Origin: *

- 使用中间件来设置cors

  1. 写一个中间件,res是共享的

  2. 中间件中设置一次允许即可

  3. ```
     app.use((req, res, next) => {
           console.log('我是中间体')
           res.setHeader('Access-Control-Allow-Origin:'*')
           next()
     })
     ```

#### 跨域-解决方案-jsonp

1. HTML元素的src属性支持跨域请求 => 只支持get请求
2. 利用script标签的src属性, 向一个不同源的接口, 发送一个get请求
3. 发送请求时,额外携带了一个callback的参数, 值是一个页面中定义好的 函数
4. 服务器接收到参数之后,拼接成一个函数的调用并且返回给浏览器
5. 浏览器接收到这个结果解析为js代码并执行
   1. 函数是浏览器定义的,处理逻辑浏览器写
   2. 数据是服务器返回的,到底是什么数据,服务器决定

