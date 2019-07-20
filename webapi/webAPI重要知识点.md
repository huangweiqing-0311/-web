## webAPI重要知识点总结

### 找元素的方法

```js
document.getElementById(); //通过id找到元素，找到的就是元素，找不到返回null
document.getElementsByClassName(); //通过类名找到元素，永远得到伪数组，找到几个，伪数组里元素就有几个
document.getElementsByTagName(); //通过标签名找到元素，永远得到伪数组，找到几个，伪数组里元素就有几个
document.getElementsByName(); //通过Name属性值找到元素，永远得到伪数组，找到几个，伪数组里元素就有几个
document.querySelector(); //传入css选择器，找到第一个匹配的元素，只返回元素
document.querySelectorAll(); //传入css选择器，选择器能找到几个，这方法就找到几个，返回的是伪数组
```

### 操作行内属性

- 元素.id  获取或者设置id
- 元素.className  获取或设置class
- 元素.style.样式  获取或设置行内样式，如果css属性有-，就去掉-并把-后面首字母大写
  - 例：元素.style.width = "200px";    元素.style.backgroundColor = "red"
- **点语法只能操作自带属性，自定义的行内属性无法操作**
- 操作自定义行内属性
  - 元素.getAttribute(); 获取行内属性
  - 元素.setAttribute(); 设置行内属性
  - 元素.removeAttribute(); 删除行内属性



### 学过的事件

- 鼠标事件：
  - onclick：点击事件
  - ondblclick：双击事件
  - onmousedown：鼠标按下
  - onmouseup：鼠标弹起
  - onmouseover：鼠标移入
  - onmouseout：鼠标移出
  - onmousemove：鼠标移动
- 键盘事件：
  - onkeyup：键盘弹起
  - onkeydown：键盘按下
- 滚动事件：onscroll：在滚动就触发
- 尺寸发生改变事件：onresize
- window的两个事件：
  - window.onload: 页面资源加载完毕触发
  - window.onunload：页面关闭时触发
- 拖拽事件
  - 跟被拖拽元素有关的事件
    - ondragstart：拖拽开始
    - ondrag：拖拽中
    - ondragend：拖拽结束
  - 跟容器有关的事件
    - ondrop：在容器范围内松手触发
    - ondragover：配合ondrop使用



### 修改双标签内容

- innerHTML：获取或设置双标签内容，如果有标签，会把标签解析出来
- innerText：获取或设置双标签内容，设置的是纯文本



### 阻止a标签跳转

- 给a加点击事件，return false
- 把a标签的href改为： javascript:void(0)
- 给a加点击事件，点击事件里阻止事件默认行为： e.preventDefault()



### 元素操作

- parentNode：找到父元素
- children：找到所有子元素，返回的是伪数组
- removeChild：删除子元素
- appendChild：添加子元素
- document.createElement： 创建一个空元素



### 计时器

- setInterval：开启一个计时器，每隔一段时间触发一次。除非自己写代码停止，否则一直调用
- clearInterval：停止计时器
- setTimeout：开启一个计时器，这个计时器只执行一次，相当于延迟执行某段代码



### offset家族

- offsetWidth和offsetHeight ：获取盒子实际宽高
- offsetLeft和offsetTop：获取自身外边框到定位参照的父级元素内边框距离



### 获取元素最终样式

```js
window.getComputedStyle(元素)['样式名']; //不管是行内写的还是内嵌写的样式，只要是元素最终什么样，获取到的就是什么
```



### 浏览器存储

- localStorage： 本地存储，把数据存储在本地，只要自己不删就一直存在
- sessionStorage：临时存储，关掉浏览器自动删除
- 它们共同的方法有：
  - setItem： 保存数据
  - getItem：获取数据
  - removeItem：删除数据
  - clear：清空数据



### 事件对象有关

- 事件对象保存了触发事件时的相关信息
- 获取事件对象：在事件绑定函数里写一个形参e，名字随便写，建议叫e或者event
- 兼容写法：e = e || window.event;
- 坐标：
  - e.clientX e.clientY 获取到可视区域坐标
  - e.pageX e.pageY 获取到页面坐标



### 事件流

- 事件冒泡：默认就存在，指的是某个元素的事件被触发后，会依次调用所有父级元素的同名事件
- 事件捕获：跟冒泡相反，默认不存在，要用addEventListener 添加的事件，并且第三个参数写true才能看到

- 阻止冒泡： e.preventDefault();
- e.target： 获取到事件源（真正触发事件的元素）



### 添加事件的另一方法

addEventListener：添加事件，特点是给一个元素添加多个同名事件会依次触发

