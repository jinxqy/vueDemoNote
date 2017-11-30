### 1.安装node环境，(c)npm。

### 2.安装vuecli:

`cnpm install -g vue-cli`

3.命令行切换到clone下来对应的盘符，初始化一个项目：

`vue init webpack Vue-Project`

其中，会弹出一些操作提示：

<br>Project name:vueProject   (项目名称)
<br>Project description: firsrProject (项目描述)
等等...

其中本人建议把Use EsLint To Your Code?设置为No(不使用ESLint代码规范，过于严格了，谁用谁头疼)。
<br>`cd Vue-Project `

启动Vue：
<br>`npm run dev`

如果浏览器打开之后，没有加载出页面，有可能是本地的 8080 端口被占用，需要修改一下配置文件 config>index.js 将dev下的port属性改成其他的即可。

运行
**0**
*开始*
先看一段最基本的代码，创建一个vue实例：

<br>`new Vue({`  
<br> ` el: '#app',`                                                          //将组建挂载到对应dom
<br>` template: '<div>{{ apple }}<div/>',`                     //组建的模板，html代码或片段
<br>    `data:{`                                                               //载入的数据
<br>        ` fruit： 'apple'`
<br>  ` }     `                                  
<br>`})`

data和template通过这样的一个方式，我们就可以完成最基本的渲染。
*声明：为了看起来简约，用data(){}.param 表示 组建内声明了一个名叫param的变量，
<br>即:export default {
    data(){
       param: ”param“
    }
}*

<br>**1**
*渲染*

可以通过小胡子形式渲染：
<br>`<div>{{ hello }}</div>`
<br>`data(){
<br>    return{
<br>       hello: 'hellow world!'
<br>   }
<br>}`
   vue1.x里，属性也可这样渲染：
   
<br>   `<p title={{hello}}>hello</div>`，而在2.0里会报错。
   vue2.0里，可这样进行渲染：
   
<br>  `<p :title="hello"></p>` 或 `<p v-bind:title="hello"></p>`
同时，也可以使用v-html或v-text的方式进行渲染：

<br>`<div v-html="hello"></div>`  

<br>`<div v-text="hello"></div>` 
若hello变量等于一段html标签：`<p>hello</p>` 那么，v-html在页面会渲染成`<p>hello</p>`；v-text则是hello。
同时，小胡子形式也可以通过一些表达式的形式渲染，诸如：

{{ statue ? "true" ： "false" }}、{{ num + 1 }}等。

**2**
*指令*
####v-for:####
   data(){}里将这样一个列表渲染到页面上：  
   
   list: [{
          name: 'apple',
          price: 34
       },
       {
         name: 'bananana',
         price: 20
     }]
我们可以这样渲染：
<br>`<p v-for="item in  list">{{ item.name }}  + {{item.price}}</p>`

绑定序号： 
<br>`<p v-for="(item,index) in  list">{{index }} + {{ item.name }}  + {{item.price}}</p>` 
注：2.0之前可以直接绑定index。
同样，也可以渲染对象:
objPerson：{
   name: jinxqy
   age: 18
}
渲染
<br> `<p v-for="(value, key) in objList">{{ value }}</p> `
也可以渲染组件：
<br>`<componentsA v-for= "(value, key) in objList"></componentsA>`

####v-on/@:可进行事件注册####
 template代码:
 
 <br>`<button v-on:click= "sayHello">sayhello</button>`
js代码：

<br>`export default{`
<br>    `methods:{`
<br>        `sayHello(){`
<br>         ` alert("hello!");`
<br>        ` list.push({name:‘1’，price:10 })；`
<br>       `}`
<br>   `}`
<br>`}`

如上，在vue里push，pop,sort等操作数组的方法会使数组发生更新。而如filter,concat,slince是不会触发数组更新的。

v-on/@还可以给子组建注册自定义事件,若comA为子组建:
  tempate：
  <br>`<comA @clickEvent="onComEvent">click</comA>`
  
  methods:
  <br>`onComEvent(param){
  
  <br>`}
子组建里template:
  <br>`<button @click="emitEvent">emit</button>`
  
  methods: 
 <br>` emitEvent(){`
     <br>`this.$emit("clickEvent", "a");`
  <br>`}`
*注：sayHello(){}是es6语法糖，即等于: sayHello:function(){}*

####v-bind\：  :####
  v-bind可用来绑定属性，如：data(){}.strClass = "font-red" 则：
 
 <br>`<p v-bind:class="strClass" class="yellow"></p>`
 这样渲染出来，class会同时存在font-red和yellow两个class。
如果strClass是一个对象，如：data(){}.strClass = { 'font-red': true, 'font-blue': false }，则只会绑定为true的属性，即：font-red。
  

####v-if、v-else 、v-show: ####
控制标签是否显示。

`data(){}.show1 = true；data(){}.show2 = true；`

<br>`<span v-if="show1">data</span>`
<br>`<span v-else>no data</span>`
<br>`<span v-show="!paramA">222</span>`

v-show=false是通过设置该元素的display:none；来控制元素的显示与否,v-if=false，则该元素不会加载在文档流里。


####v-model####
 v-model可以用来绑定表单控件:如果data（）{}.arr = ["pen", "pencial"]; data(){}.apple = "apple";
 则可以通过以下方式绑定:
 <br>`<input v-model="apple" type="text" value=""/>`
 
 <br>`<input v-model="arr" type="checkbox" value="pen"/>`
 
 <br>`<input v-model="arr" type="redio" value="pencial"/>`
 
  <br>`<select>
     <br>`<option v-for="item in arr">{{ item }}</option>
  <br>`</select>
 
 v-model后还可以加number,trim,lazy等修饰符做表单验证。
 如：input只能输入数字：
 <br>`<input v-model.number="apple" type="text" value=""/>`
 
**3**属性和事件

如果a变量随着b变量的值改变而更新，类似于高级语言里的get，可以通过计算属性实现：

  如：始终想要得到paramA + '1':
  
  template: 
  
  {{ computedParamA }}
  
  computed：
  <br>`computed：{
      <br>`computedParamA(){
         <br>`return this.paramA + '1';
      <br>`}
   <br>`}
   
相比之下，computed比事件监听更加高效、简单.在上面中，每当paramA更新后，computedParamA才会同步更新；

而使用事件则会在每一次调用后，更新参数，无论paramA是否变化。

####属性监听：####

有时候，我们希望当属性paramA改变后，去固定执行某个方法，则可以通过属性监听watch来完成:

  <br>`watch：{
     <br>`paramA： function(newParamA, oldParamA){
      <br>`  console.log("由" + oldParamA +"改为"+ newParamA);
     <br>`}
  <br>`}


**4**组件
####1引用####
   
  import comA from './components/comA';
  export default {
      componets:{
         comA
      }
  }
  *其中如果在componets里，comA = comA,则可以使用es6语法，简写为comA*
  
  ####2交互####
  子组建 => 父组件传值 通过$emit完成： 
  
  子组件comA代码：
  
  <br>`methods:{`
     
     <br>`submitParam（）{`
     
    <br>`this.$emit('getParam', "from comA");`
     
    <br>`}`
    
   <br>`}`
  
  父组建代码：
    
    <br>`methods:{`
     
     <br>`getParam（paramformA）{`
     
    <br>`  console.log("from paramA is" + paramformA);
 
    <br>`}`
    
   <br>`}`
   
   
   
**4**vue-router


**5**vuex


**6**扩展


**7**其他
