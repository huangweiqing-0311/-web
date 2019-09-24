# vue



#### 知识点总结

- 1.v-text,也叫胡子语法,{{}}插值表达式,类似innerText操作

- 2.v-html,类似于innerHtml操作,支持HTML标签解析

- 3.v-on,事件绑定,简写是@, 调用methods中的方法

- 4.v-bind:动态绑定HTML标签的属性,简写就是一个 : 冒号, 将data里面的数据绑定到标签的行内属性上

- 5.v-model: 表单双向数据绑定,表单输入会赋值给data,data也会改变表单的值

- 6.v-for: 循环遍历数组,v-for="(item, index) in items"

- 7.v-if和v-show,判断显示,v-if若是false则什么都不做,v-show若是false其本质只是改变了display的属性值为none

- 8.v-cloak、v-one、v-pre了解

- 9.v-bind使用

  - 1.操作元素class列表和内联样式是数据绑定的一个常见需求,他们都是属性,所以我们可以用v-bind处理他们: 只需要通过表达式计算出字符串结果即可.表达式结果也可以是对象或字符串

  - 2.使用对象来绑定我们希望操作的class属性

    - ```
      <li class="box" :class="{red: isRed}"></li>
      ```

    - a.当isred为true时,有red这个类名,反则没有

    - b.默认的class, 和 :class 不会冲突,后面的会作为追加,或者移除来解析

  - 3.style的使用和class基本一样,要注意的是对象属性的name需要按照驼峰方式来命名

    - ```
      <div :style="{fontSize: size + 'px'}"></div>
      ```


#### 表达式的作用域

- 表达式会在vue实例的数据作用域下作为JavaScript被解析
  - js表达式里面的变量作用域是vue实例,这些变量是vue实例能够访问到的
  - js表达式里面的变量必须定义在data和methods里面

#### 初识vue生命周期钩子函数

- 1.生命周期钩子函数其本质就是在: vue实例化及执行过程中对应关键节点的回调函数
- 2.updated钩子函数执行时间是data数据更改DOM更新完成后,需要执行的回调函数
- 3.需要注意的是: updated不常用,因为他检测的是所有的data相关数据更新,会造成不必要的消耗

#### vue生命周期钩子-mounted

- 1.执行时机是: vue解析完了所有的页面内容后,将data和其他computed属性都解析到了页面上之后执行的一个回调函数,钩子函数
- 2.当我们遇到凡是需要依赖页面已经加渲染完成后的操作都应该使用mounted这个钩子函数
- 3.只会执行一次,在渲染挂载完毕以后
- 4.如果说数据发生改变我们需要执行的操作,应该放在updated中

##### vue的计算属性

- 1.使用computed关键字进行定义
- 2.使用函数定义return新的值
- 3.Vue实例化过程中,计算属性会默认依赖相关的data变量调用一次并返回初始化的数据
- 4.vue执行过中,计算属性依赖相关的data变量每次发生变化,都会自动调用并返回新值
- 5.计算属性也可以依赖其他计算属性进行自动调用更新

###### 如何在Vue中排查Bug

- 1.点击右键 => 检查 => 开发者工具栏,也可以直接按F12快捷键打开
- 2.语法语义类错误,会在开发者工具栏直接标红报错
  - 1.变量名调用错误,比如: 把{{messge}}写成了{{mesage}}
  - 2.语法格式使用错误,比如: 在行内表达式中使用了{{}}引入数据
- 3.逻辑性错误,一般不会直接报错的错误
  - 1.使用console.log或者alert,打印异步获取到的数据,判断执行逻辑,查看数据类型是否是我们想要的结果
  - 2.推荐一个神器,Chrome-vue-tools调试工具,Vue专用开发者工具

###### Chrome Vue DevTools

- 1.翻墙,前往Chrome商店,插件地址,下载crx安装文件
- 2.打开Chrome浏览器, 更多选项 => 更多工具 => 拓展程序, 使用拖拽的方式就能直接安装
- 3.安装成功后,浏览器右上角出现一个vue图标,点击打开开发者模式,就可以使用了OK



#### 网络请求库axios

- [官网地址](https://github.com/axios/axios)

- 1.jQuery的ajax请求远程数据,需要引入整个包,降低性能,浪费资源

- 2.vue提供了一个轻量,便捷的新的数据请求工具 => axios

- 3.使用流程

  - 1.到官网去下包/导包

    - ```
      <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
      ```

  - 2.用包

    - ```
      const axios = require('axios')
      //1.发get请求
      axios.get('/user?ID=12345')
        .then(function (response) {
          //成功执行的回调函数
          console.log(response);
        })
        .catch(function (error) {
          //失败执行的回调函数
          console.log(error);
        })
        .finally(function () {
          //完成以后执行的回调函数,总是会被执行
        });
        
        //2.post请求
        axios.post('/user', {
          firstName: 'Fred',
          lastName: 'Flintstone'
        })
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
      ```

#### ajax和axios的区别

- 1.ajax使用的是success,error回调函数作为参数来使用的
- 2.axios使用的是链式调用,返回的结果是一个promise对象,会承诺向服务器发出异步请求,然后根据请求的结果链式执行相应的逻辑
- 3.axios在链式调用的参数方法定义中,使用箭头函数确保能够绑定到当前vue实力上并能获取到vue声明的属性和方法



##### vue实战-天知道

- 1.第一步 需求分析: 
  - 1.当用户在输入搜索关键字,回车或点击搜索按钮,loading显示
  - 2.发送ajax请求,获取远程数据
  - 3.将返回的数据渲染到页面上
  - 4.点击预设的几个地址关键字,请求新数据并渲染到页面
- 2.第二部 对照样式设计
- 3.第三部: 设计核心相关需要的data直接手动输入初始化的值并代替页面静态部分
  - 1.输入框输入的数据需要一个data属性searchCitys来保存(字符串)
  - 2.渲染到页面的天气列表需要一个data属性searchList,这是一个数组
  - 3.预设的几个searchCitys,我们定义一个数组initCitys来保存
- 4.第四步: 分析用户操作逻辑,用真实数据渲染
  - 1.输入框用户输入的数据
  - 2.异步axios请求的数据
- 5.第五步: 相关优化
  - 1.数据反馈异常的兼容优化
  - 2.动画效果的优化
  - 3.代码结构的优化



#### vue动画-单个元素动画

- [官网地址](https://cn.vuejs.org/v2/guide/transitions.html#%E5%8D%95%E5%85%83%E7%B4%A0-%E7%BB%84%E4%BB%B6%E7%9A%84%E8%BF%87%E6%B8%A1)

- 1.transition如果不包裹元素,是没有动画效果的,同时transition和tag标签配合包裹动画元素

- 2.name属性和动画的css设置样式,开头部分一致name-xx

- 3.元素在显示和隐藏触发条件下才会出现动画

  - 条件渲染(使用v-for)
  - 条件展示(使用v-show)

- 4.vue动画其实本质是: 再触发动画时,动态的修改当前transition的class类名,然后配合css3事先定义好的动画效果来实现的

- 5.动画的各个阶段的类名是不同的,在进入/离开的过渡中,一共会有6个class切换

  - 1.v-enter: 定义进入过度的开始状态,在元素被插入之前生效,在元素被插入之后的下一帧移除
  - 2.v-enter-active: 定义进入过度生效时的状态,在整个进入过度的阶段中应用,在元素被插入之前生效,在过度/动画完成之后移除,这个类可以被用来定义进入过度的过程时间,延迟和曲线函数
  - 3.v-enter-to: 2.1.8版及以上 定义进入过度的结束状态,在元素被插入之后下一帧生效(与此同时v-enter被移除),在过度/动画完成之后移除
  - 4.v-leave: 定义离开过度的开始状态,在离开过度被触发时立即生效,下一帧被移除
  - 5.v-leave-active: 定义离开过度生效时的状态,在整个离开过度的阶段中应用,在离开过度被触发时立即生效,在过度/动画完成之后移除,这个类可以被用来定义离开过度的过渡时间,延迟和曲线函数
  - 6.v-leave-to: 2.1.8版及以上 定义离开过度的结束状态,在离开过渡被触发之后下一帧生效(与此同时v-leave被移除),在过渡/动画完成之后后移除.

  vue-cli 脚手架安装  
 淘宝镜像: npm install -g cnpm --registry=https://registry.npm.taobao.org

## component组件

###### 概念

1. 把一段公共的代码抽取出来,形成一个组件,以达到复用的目的

###### 作用

1. 可以实现组件的复用(包含视图, 逻辑)

###### 注意

1. 全局注册的行为必须在根Vue实例(new Vue)创建之前发生
   - 全局组件  Vue.component( )  不加s
   - 局部组件  new Vue({ components: { } })
2. 组件中的复用代码( 模板 ) 必须被一个根标签包裹住
3. 组件的作用域是隔离的

###### 

###### 难点

- 组件中返回的data不是一个对象,而是一个函数,并且函数中返回一个新的对象
- 原因
  - 对象是值应用类型,栈中存放地址,堆中存放数据,若改变数据就是改变栈中的地址
  - 而组件可能会被多个实例进行引用,如果data值为对象,将导致对个实例共享一个对象,其中一个组件改变data的属性值,其他实例也会受到影响
  - 当data为函数的时候,通过return返回对象的拷贝,使每个实例都有自己独立的对象,实例之间可以互不影响的改变data属性值

#### 注册组件的方法

1. 先定义,然后注册,最后注册的标签写在body上

   - ```
     //01-先定义一个组件
      let loginComponent = Vue.extend({ template: '<div> 代码 </div>})
      
      //02-注册组件
      Vue.component( 'login', loginComponent)
      
      //03-创建Vue实例对象
      const app = new Vue({
            el: '#app'
      })
     ```

   2.定义注册合二为一,定义的组件标签写在body上

   - ```
     Vue.component('login', {
            template: '<div>代码</div>',
            data:{ },
            methods: { },
          })  
     ```

   3.定义注册合二为一,复用代码写在template中,通过他的id进行绑定

   - ```
     Vue.component('login', {
             template: 'id',
             data: { },
             methods: { }
           })  
     ```

   4.定义注册合二为一,复用代码写在script标签中,通过他的id进行绑定

   - ```
     Vue.component('login', {
          template: 'id',
          data: { },
          methods: { }
        })  
     ```

   5.单文件组件

   - 命名    组件名.vue 
   - 组成    template模板   script逻辑  style样式

   

####   父子组件传值

- 1.子组件中写模板, 父组件中导入子组件, 并注册局部组件, 父组件中的HTML中添加组件标签
- 2.父组件传值给子组件
  - 父组件中， 在组件标签里通过属性名和属性值，进行传出数据
  - 子组件中， 通过props获取父组件中定义的属性名， props： {‘name': 'jack, 'age': 18}
- 3.子组件传值给父组件
  - 子组件中， 通过this.$emit(事件名, 载荷对象)
  - 父组件中,   在组件中定义的事件名与子组件中保持一致,写函数时,通过形参获取到子组件传过来的载荷对象

#### 知识点

- 1.数组的filter方法

  - 语法: array.filter((数组中每项元素) => { return 布尔值 }, this.value)

  - 作用: 根据条件来过滤旧数组, 组成一个新数组并返回

  - ```
    const newArr = this.arr.filter( (item) => {
         return item.name.includes(this.search)
    })
    ```

    

#### vue发送请求

- 1.vue-resouce(要挂载到vue实例上)

  - vue-resouce基于vue,必须要在vue导入之后,再导入vue-resouce, 挂载到vue实例上,使用的时候用this.$http

  - 获取参数    response.body

  - this中的参数说明, 第一个参数是成功回调,第二个参数是错误回调

  - ```
    get请求
     const url = 'http://127.0.0.1:3000/api/login?      username=admin&password=123456'
     
     this.$http.get(url).then.( response => {
          console.log(response.body) 
     }, error => { })
     
     
    post请求
      const url = 'http://127.0.0.1:3000/api/post/postLogin'
      this.$http.post(url, {参数}).then.( response => {
             console.log(response.body)
      }, error => { })
    ```

     

- 2.axios

  - axios不基于vue,在导入的时候,没有顺序,并且也不用挂载到vue实例上,直接使用

  - 获取参数 response.data

  - ```
    get请求
     axios.get(url).then( response => {
           console.log(response.data)
     }, error => { })
     
    post请求
    axios.post( url, {参数}).then( response => {
          console.log(response.data)
    }, error => { })
    ```

#### vuex-基本使用

1. 下包

2. 导包

   要Vue.use(vuex)

3. 实例化vuex对象

4. 挂载到vue的对象里

5. $store.state.属性名

##### vuex-state

1. 管理仓库数据源
2. 所有组件都可以用
3. $store.state.xxx
4. 代码中使用this.$store.state.xxx
5. 可以结合计算属性使用

##### vue-mutation

1. 所有组件中都可以修改数据
2. this.$store.commit('方法名', 参数)
3. 方法定义在仓库的mutations的内部
4. 在Chrome中可以看到每次提交的内容方便调试

##### vue-getters

1. vuex中计算属性

###### vue-cli功能-快速原型开发

1. 装包: cnpm install -g @vue/cli-service-global
2. 直接把一个xxx.vue跑起来
3. vue serve xxx.vue (xxx是文件名)

#### vue组件的封装-在子组件上使用v-model(v-model本质)

[传送门](https://cn.vuejs.org/v2/guide/components.html#%E5%9C%A8%E7%BB%84%E4%BB%B6%E4%B8%8A%E4%BD%BF%E7%94%A8-v-model)

在子组件中 绑定两个东西

```
Vue.component('base-checkbox', {
  model: {
      prop: 'checked',
      event: 'change'
    },
    props: {
       checked: Boolean
       },
    template: `
       <input
        type="checbox"
        v-bind:checked="checked"
        v-on:change="$emit('change',      $event.target.checked)" >
        `
    }
```

v-model本质就是v-bind和v-on的组合

v-model会跟子组件里的model属性进行一一对应,event里面写了什么(例如change), 就相当于给父组件加了一个@change, 子组件里面对应的时机, 用$emit就可以把数据推给父组件了

#### vue-组件封装-插槽

[传送门](https://cn.vuejs.org/v2/guide/components.html#%E9%80%9A%E8%BF%87%E6%8F%92%E6%A7%BD%E5%88%86%E5%8F%91%E5%86%85%E5%AE%B9)

##### A具名插槽

1. [传送门](https://cn.vuejs.org/v2/guide/components-slots.html#%E5%85%B7%E5%90%8D%E6%8F%92%E6%A7%BD)
2.   给插槽取名字 (slot标签里写一个name属性)
3. 在使用这个子组件的地方, 要包一个template, 用 v-slot: name 名绑定, 告诉它填充到那个插槽
4. name名不用加引号

##### B作用域插槽

1. [传送门](https://cn.vuejs.org/v2/guide/components-slots.html#%E4%BD%9C%E7%94%A8%E5%9F%9F%E6%8F%92%E6%A7%BD)
2. 让插槽可以使用组件内部的数据
3. 把子组件暴露的数据在父组件传入的结构中获取
4. 

#### vue组件的数据传递-bus模式

[传送门](https://cn.vuejs.org/v2/guide/migration.html#dispatch-%E5%92%8C-broadcast-%E6%9B%BF%E6%8D%A2)

1. bus可以实现兄弟传值
2. 实例化一个vue作为传递的中间对象
3. 通过它来传递对象
4. 需要在多个组件中监听和触发事件

### vue  - mixin 混入

[传送门](https://cn.vuejs.org/v2/guide/mixins.html)

```
// 定义一个混入对象
var myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}

// 定义一个使用混入对象的组件
var Component = Vue.extend({
  mixins: [myMixin]
})

var component = new Component() // => "hello from mixin!"
```

1. 把组件内部公共的部分抽取出来
2. 每次要创建组件时, 可以把这部分内容合并进去

### vue-keep-alive

[传送门](https://cn.vuejs.org/v2/api/#keep-alive)

1. 作用: 使组件不被销毁
2. 是两个新的钩子
3. 包裹之后组件不会被销毁, 会被保存到内存中
4. 再次显示时, 状态还在
5. deactivated  钩子
6. activated  钩子
7. 这两个钩子必须结合keep-alive才可以使用

### vue.set

[传送门](https://cn.vuejs.org/v2/api/#Vue-set)

1. 本来data中没有的属性, 通过.语法添加上去之后
2. vue不能够跟踪数据的改变
3. 如果必须要动态的增加属性, 可以使用 this.$set
4. 如果直接给data的属性赋值,内部会对这些属性全部set一下
5. 赋值之后再去 .xxx=xxx 这种不会再去设置了
6. 注意: 
   1. 动态增加属性无法更新
   2. 找到 Vue.set
   3. set 的本质是Vue双向绑定原理,Object.defineProperty

#### Vue.use

[传送门](https://cn.vuejs.org/v2/api/#Vue-use)

1. 执行插件对象的 install 方法
2. 把 vue 的构造函数传入
3. 内部就可以为构造函数添加原型属性
4. 或者是注册全局的组件 过滤器等
5. 饿了么UI就是这么做的
6. 用它的时候要use
   1. $message设置给原型
   2. el-input这些组件都是全局注册



### vue虚拟DOM $ vue的diff算法 $ key的作用

[传送门1-官方解释](https://cn.vuejs.org/v2/guide/render-function.html#%E8%8A%82%E7%82%B9%E3%80%81%E6%A0%91%E4%BB%A5%E5%8F%8A%E8%99%9A%E6%8B%9F-DOM)

[传送门2-官方解释](https://cn.vuejs.org/v2/api/#key)

[Vue-虚拟dom--diff算法](https://www.jianshu.com/p/af0b398602bc)

1. 虚拟dom是用js对象在内存中描述出一个类似于dom树的结构
2. 数据改变时,现在内存中的用js表示的虚拟dom上,进行计算匹配对比,最终匹配出所有更改的元素
3. 再同步到页面上
4. beforeUpdate
5. updated
6. dom元素非常多,为了尽可能高效的计算出结果,所以给个key唯一的标记
7. 不给key可能会浪费一些性能



### vue数据响应式原理

[传送门](https://cn.vuejs.org/v2/guide/reactivity.html)

1. Object.defineProperty为对象动态的增加一个属性
2. 我们在为这个对象的属性 取值 或者赋值时
3. 会触发get 和 set 方法
4. 在这个方法中就可以去执行自定义的逻辑了
5. 比如操纵dom元素
6. vue2.x的数据响应原理

### vue数据响应式原理 3-proxy

[传送门](https://www.jianshu.com/p/2a8ec76e0090)

1. proxy设置之后

2. 所有对这个对属性的取值和赋值都会触发 get 和 set

3. 无论属性名是什么

4. 当vue3用了proxy之后,就不需要Vue.set了

5. ```
    let data = {}
     
     // new proxy对象
     let proxyData = new Proxy(data,{
       get(obj,prop){
         console.log('get')
         console.log(obj)
         console.log(prop)
         return obj[prop]
       },
       set(obj,prop,value){
         obj[prop]= value
         console.log('set')
         console.log(obj)
         console.log(prop)
         console.log(value)
       }
     })
   ```

   



### 自己搭建项目

1.先创建一个项目的源文件    src / main.js

2.项目根目录创建一个webpack的配置文件  

- webpack.config.js   module.exports(导出) 
  - mode:  模式, production(生产模式)   development(开发模式)
  - entry:   指定打包的入口文件
  - output:  出口,打包之后存放稳健的地方
  - module:  写rules, 里面配置loader, 将不同类型的文件进行转换成能够识别的js文件
  - plugins: 插件,协助打包

3.生成项目描述文件 

- npm init -y
- package.json

4.main.js中导入其他的js文件, css, sacc文件

- 1.安装: 
  - css:  npm i style-loader css-loader -D
  - sass:  npm i sass-loader node-sass -D
- 2.在main.js中通过require的相对路径引入
  - require('./modela.js')
  - require('./statics/css/base.css')
- 3.配置
  - 在module中的rules中配置 { test: /\.css$/, use: ['style-loader', 'css-loader'] }

5.打包之前删除掉dist目录,并重新生成

- 安装包  cnpm i clean-webpack-plugin webpack -D
- 配置
  - 1,导入模块,  const CleanWebpackPlugin = require('clean-webpack-plugin')
  - 2.在 plugin中配置  new CleanWebpackPlugin('dist')

6.根据template.html模板生成index.html, 并导入boundle.js 

- 安装包  cnpm i html-webpack-plugin webpack -D

- 准备文件, 准备一个template.html文件, 并把html标准代码用  ! +Tab生成

- 配置

  - 1.导入模块

    - ```
      const HtmlWebPackPlugin = require('html-webpack-plugin')
      ```

    2.在plugins中配置

    - ```
      new HtmlWebpackPlugin({
          template: './template.html',  //模板文件
          filename: 'index.html'       //在dist根目录下生成
      })
      ```

    

    

    

### router路由

作用: 前端可以实现单页面应用(SPA) single page application

###### 使用

- html如下

- ```
  <div id="app">
      <router-link to="/foo" > go to Foo <router-link>
      <router-link to="/bar" > go to Bar <router-link>
      
      //路由出口, 路由匹配的组件将渲染到这里
      <router-view><router-view>
   </div>
      
    //通过to指定链接, router-link默认会被渲染成一个<a>标签  
  ```

- js中如下

- ```
  //1.定义一个组件
    const Foo = Vue.extend({
         template: '<div>我是foo组件</div>',
    })
   
  //2.创建路由对象,设置路由规则
   const router = new VueRouter({
      //routes是一个数组, 发送的路径和定义的组件 要一一匹配
      routes: [
        {path: '/foo', component: Foo},
        {path: '/bar', component: Bar}
       ] 
   })
  //路由重定向   {path: '/', redirect: '/foo'}
  //params传参  {path: '/detail/:id', component: Detail}
  
  //3.创建vue实例对象
   const app = new Vue({
        router: router, 
   }).mount('#app')
   
  ```

- $router与$route

  - 1.this.$router.push在Vue实例内部(文件后缀为.vue), 可以通过$router访问路由实例,因此可以调用this.$router.push
  - 2.获取路径中的参数, 不管是通过params还是query, 在watch中监控$route的变化
  - 3.路由守卫
    - router.beforeEach((to, from, next) => { })
  - 4.路由元信息
    - meta: {needLogin: true}
    - {path: '/order', component: order, meta: {needLogin: true}



### 项目打包

- 1.项目做完要上线
- 2.打包
  1. 压缩合并html
  2. 压缩合并css
  3. 压缩合并js
  4. 添加兼容性代码等等
- 3.一般用的是webpack来打包
- 4.我们的项目是vue-cli搭建的,vue-cli的内部就是基于webpack的封装
- 5.我们只需要npm run build
- 6.打包好之后
  1. 给后端
  2. 或者是运维
- 7.上线的本质是把本地的代码上传到远程服务器
- 8.所有的资源的路径都是网站的根目录

### 打包设置

1. 项目根目录下创建一个vue.config.js(默认不存在的)与packge.json同级

2. 内部通过暴露的对象的语法,添加自己的设置即可

3. 比如这里

   ```
   module.exports = {
      // 打包的根路径 使用的是相对
      publicPath: './
     }
   ```

4. 移除map文件

   1. 在vue.config.js文件里增加一组键值对 productionSourceMap:  false



#### vue项目首次加载提速(路由懒加载)

1. 如果所有的文件都合并到了一起,用户不一定会都打开
2. 而我却都加载了
3. 组件在导入时, 使用const Foo = () => import('./Foo.vue')即可实现懒加载
4. 本质上只是把时间分开了
5. 总时间没有变

#### vue项目加载提速02-CDN加速

[vue-cli中合并webpack配置](https://cli.vuejs.org/zh/guide/webpack.html#%E7%AE%80%E5%8D%95%E7%9A%84%E9%85%8D%E7%BD%AE%E6%96%B9%E5%BC%8F)

1. 抽取不再需要打包的文件到到index.html中

2. 增加vue.config.js

3. 输入内容

   ```
   module.exports = {
     // 这里直接写webpack的配置即可
     configureWebpack: {
         // 告诉打包程序: vue, vue-router, axios,             // element-ui不要打包生成
         externals {
             // 键: 模块名字
             // 值: 导入后它叫什么名字
             'vue': 'vue',
             'vue-router': 'VueRouter',
             'axios': 'axios',
             // element-ui这里的名字要大写
             'element-ui': 'ELEMENT'
         }
     }
     }
   ```

4. 网络第三方库查找

   1. bootcdn
   2. 模块的官网

5. 没有打包第三方模块文件更小了

6. 第一次加载速度更快一些

7. 把第三方模块的引入, 从本地, 变成网络资源

###### CDN

1. 缺点
   1. 所有的服务器都需要同步相同的内容
   2. 更新了网站之后
   3. 全网同步需要时间
   4. 一般在半夜更新
   5. 运维
2. 把一个服务器中的内容, 放到多个不同的地域的服务器中
3. 用户访问时就近原则

#### vue项目加载提速03-通用方案

1. 充钱买带宽!服务器返回的数据的速度更快
2. 使用静态资源服务器
   1. 网站的静态资源专门用一个服务器存放
   2. 图片
   3. 用户在请求时
      1. 图片一个服务器的流量
      2. 网站一个服务器的流量
   4. 七牛云
   5. 所有图片 使用静态资源服务器的网络地址 相对路径
3. gzip压缩（压缩比更大的压缩格式)
   1. 服务器用到的一种压缩资源格式
   2. 需要运维开启一个设置
4. webp文件格式
   1. 谷歌推出的一种格式
   2. 图片精度不大的情况下,容量小了不少
   3. UI转成这个格式即可
5. 减少请求
   1. 不打包第三方模块,CDN加速有冲突
   2. 降低自己服务器的压力
   3. 自己的项目逻辑, 合并到一起,所有的css合并到一起
6. base64: 编码格式, 用它代表一个图片, 直接用base64不用把图片存到服务器
7. 懒加载
8. js少用递归, 闭包, 嵌套循环, 少用全局变量





### 项目上线

[传送门](https://www.cnblogs.com/zhaowy/p/8400405.html)



### 传送门

[Vue.delete](https://cn.vuejs.org/v2/api/#Vue-directive)

[vue原理剖析](https://juejin.im/user/59ee29a36fb9a0451c3990e5/posts)

[es6,7,8,9,10新特性一览](https://juejin.im/post/5ca2e1935188254416288eb2)

[iView-基于Vue的ui框架](https://www.iviewui.com/)

[Cube-ui-移动端Vue组件库](https://didi.github.io/cube-ui/#/zh-CN/example)

[Mint-ui -饿了么团队开发的移动端Vue组件库](http://mint-ui.github.io/#!/zh-cn)

[mui  HBuilder团队开发的移动端框架](http://dev.dcloud.net.cn/mui/)

[D2-admin 现成的后台管理界面](https://d2admin.fairyever.com)

[iView-admin 基于iView搭建的后台管理页面](http://admin.iviewui.com/login)

[Element - admin 基于Elementui实现的后台管理页面](https://panjiachen.github.io/vue-element-admin-site/zh/)

[vue-resource（早期结合Vue的网络请求库）](https://github.com/pagekit/vue-resource)

