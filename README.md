### 1.安装node环境，(c)npm。

### 2.安装vuecli:

`cnpm install -g vue-cli`

3.命令行切换到clone下来对应的盘符，初始化一个项目：

`vue init webpack Vue-Project`

其中，会弹出一些操作提示：
Project name:vueProject   (项目名称)
Project description: firsrProject (项目描述)
等等...

其中本人建议把Use EsLint To Your Code?设置为No(不使用ESLint代码规范，过于严格了，谁用谁头疼)。
`cd Vue-Project `

启动Vue：
`npm run dev`

如果浏览器打开之后，没有加载出页面，有可能是本地的 8080 端口被占用，需要修改一下配置文件 config>index.js 将dev下的port属性改成其他的即可。

运行
**0**
*开始*
先看一段最基本的代码，创建一个vue实例：
`new Vue({`  
 ` el: '#app',`                                                          //将组建挂载到对应dom
` template: '<div>{{ apple }}<div/>',`                     //组建的模板，html代码或片段
    `data:{`                                                               //载入的数据
         ` fruit： 'apple'`
   ` }     `                                  
`})`

data和template通过这样的一个方式，我们就可以完成最基本的渲染。
*声明：为了看起来简约，用data(){}.param 表示 组建内声明了一个名叫param的变量，即:export default {
    data(){
       param: ”param“
    }
}*
**1**
*渲染*

可以通过小胡子形式渲染：
`<div>{{ hello }}</div>`
`data(){
    return{
       hello: 'hellow world!'
   }
}`
   vue1.x里，属性也可这样渲染：
   `<p title={{hello}}>hello</div>`，而在2.0里会报错。
   vue2.0里，可这样进行渲染：
  `<p :title="hello"></p>` 或 `<p v-bind:title="hello"></p>`
同时，也可以使用v-html或v-text的方式进行渲染：
`<div v-html="hello"></div>`  
`<div v-text="hello"></div>`  
若hello变量等于一段html标签：<p>hello</p> 那么，v-html在页面会渲染成<p>hello</p>；v-text则是hello。
同时，小胡子形式也可以通过一些表达式的形式渲染，诸如：
{{ statue ? "true" ： "false" }}、{{ num + 1 }}等。

**2**
*指令*
v-for:
   data(){}里将这样一个列表渲染到页面上：  
   list: [{
          name: 'apple',
          price: 34
       },
       {
         name: 'bananana',
         price: 20
     }]
我们可以这样渲染：`<p v-for="item in  list">{{ item.name }}  + {{item.price}}</p>`
绑定序号： `<p v-for="(item,index) in  list">{{index }} + {{ item.name }}  + {{item.price}}</p>` 注：2.0之前可以直接绑定index。
同样，也可以渲染对象:
objPerson：{
   name: jinxqy
   age: 18
}
渲染： `<p v-for="(value, key) in objList">{{ value }}</p> `
也可以渲染组件：`<componentsA v-for= "(value, key) in objList"></componentsA>`

v-on:可进行事件注册
 template代码:
 `<button v-on:click= "sayHello">sayhello</button>`
js代码：
`export default{`
    `methods:{`
        `sayHello(){`
          ` alert("hello!");`
         ` list.push({name:‘1’，price:10 })；`
       `}`
   `}`
`}`
如上，在vue里push，pop,sort等操作数组的方法会使数组发生更新。而如filter,concat,slince是不会触发数组更新的。

*注：sayHello(){}是es6语法糖，即等于: sayHello:function(){}*
v-bind\：  :
  v-bind可用来绑定属性，如：data(){}.strClass = "font-red" 则：`<p v-bind:class="strClass" class="yellow"></p>`这样渲染出来，class会同时存在font-red和yellow两个class。
如果strClass是一个对象，如：data(){}.strClass = { 'font-red': true, 'font-blue': false }，则只会绑定为true的属性，即：font-red。

v-if、v-else 、v-show:
控制标签是否显示。
data(){}.show1 = true；data(){}.show2 = true；
<span v-if="show1">111</span><span v-else="paramA">222</span>






**3**组建


**4**vue-router


**5**vuex


**6**扩展


**7**其他
