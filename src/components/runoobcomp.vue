<template>
  <div id="runoobcomp">
    <div id="routertest">
      <p>
        <!-- 使用 router-link 组件来导航. -->
        <!-- 通过传入 `to` 属性指定链接. -->
        <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
        <router-link to="/foo">Go to Foo</router-link>
        <router-link to="/bar">Go to Bar</router-link>
      </p>
      <!-- 路由出口 -->
      <!-- 路由匹配到的组件将渲染在这里 -->
      <router-view></router-view>
    </div>

    <span>页面载入时，input 元素自动获取焦点：</span>
    <input v-focus><br>

    <!-- 判断class1的值，true则使用class1的样式 -->
    <label for="r1">修改颜色</label>
    <input type="checkbox" v-model="class1" id="r1"><br>
    <!-- v-bind 指令被用来响应地更新 HTML 属性，HTML 属性写在v-bind中 -->
    <div v-bind:class="{'class1': class1}">
      directiva v-bind:class
    </div>

    <!-- 自定义指令runoob -->
    <div v-runoob:hello.ab.="message"></div>
    <div v-setstyle="{ color: 'gray', text: 'my 指令' }"></div>

    <!-- 可以在 v-bind:style 直接设置样式 -->
    <div v-bind:style="{ color: 'green', fontSize: '20px' }">内嵌style</div>
    <!-- 可以直接绑定到一个样式对象，让模板更清晰。style对象在data块中定义-->
    <div v-bind:style="styleObjectl">绑定style</div>
    <!-- v-bind:style 可以使用数组将多个样式对象应用到一个元素上 -->
    <div v-bind:style="[styleObject, overrideStyle]">style数组</div>
    
    <!-- v-bind绑定href参数和url变量值 -->
    <pre><a v-bind:href="url">this is a link</a></pre>
    <!-- v-bind提供缩写 -->
    <pre><a :href="url">this is a link, too</a></pre>

    <!-- Vue.js 提供了完全的 JavaScript 表达式支持 -->
    {{ 5 + 5 }}
    {{ ok ? 'YES' : 'NO' }}
    {{ message.split('').reverse().join('') }}
    <a v-bind:id="'list-' + id">WTF</a>

    <!-- v-html 指令，输出html代码 -->
    <div v-html="vhtml"></div>

    <!-- v-if/v-else指令，判断if语句 -->
    <a v-if="Math.random() > 0.8">see me</a>
    <a v-else>see you</a>
    <!-- v-else-if 指令 -->
    <div v-if="type === 'A'"> A </div>
    <div v-else-if="type === 'B'"> B </div>
    <div v-else-if="type === 'C'"> C </div>
    <div v-else> Not A/B/C  </div>

    <!-- v-show 指令也可以来根据条件展示元素： -->
    <a v-show="ok"> ShowMe </a>

    <!-- v-for 循环指令 -->
    <!-- v-for 指令需要以 site in sites 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名。 -->
    <!-- v-for 可以绑定数据到数组来渲染一个列表 -->
    <ol>
      <li v-for="site in sites" :key="site.name"> {{site.name}} </li>
      <li>--------------</li>
    </ol>
    <!-- v-for 可以通过一个对象的属性来迭代数据 -->
    <ul>
      <li v-for="value in object" :key="value">{{value}}</li>
      <li>--------------</li>
    </ul>
    <!-- 提供第二个的参数为键名 -->
    <ul>
      <li v-for="(value,key) in object" :key="value">{{key}}:{{value}}</li>
      <li>--------------</li>
    </ul>
    <!-- 第三个参数为索引 -->
    <ul>
      <li v-for="(value, key, index) in object" :key="index"> {{ index }}. {{ key }} : {{ value }} </li>
      <li>--------------</li>
    </ul>
    <!-- v-for 也可以循环整数 -->
    <ul>
      <li v-for="n in 3" :key="n"> {{ n }} </li>
      <li>--------------</li>
    </ul>

    <!-- 计算属性 computed -->
    <p> 反转"HELLO"：{{reversedMessage2}}</p>

    <!-- 修饰符：以.指明的特殊后缀，用于指出一个指定应该以特殊方式绑定。
    例如，.prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()： -->
    <form v-on:submit.prevent="onSubmit"></form>

    <!-- v-model 指令，在input 输入框中实现双向数据绑定 -->
    <input v-model="message">

    <!-- v-on 指令，监听 DOM 事件，参数为事件名 
    例如：监听按钮事件，如下触发reverseMessage()，实现字符串反转-->
    <button v-on:click="reverseMessage">反转字符串</button>
    <!-- v-on提供缩写 -->
    <button @click="reverseMessage">反转2</button><br>
    <button @click="clicker += 1">+1s</button>
    <a> 总共加了{{clicker}}s</a><br>
  
    <!-- 过滤器，过滤器函数接受表达式的值作为第一个参数-->
    <!-- 在两个大括号中的过滤器 -->
    {{ message | capitalize }}<br>
    <!-- 在 v-bind 指令中的过滤器 -->
    <!-- <div v-bind:id="rawId | formatId"></div> -->
    <!-- 过滤器可以串联 -->
    {{ message | capitalize | capitalize2 }}<br>
    <!-- 过滤器是 JavaScript 函数，因此可以接受参数 -->
    <!-- {{ message | filterA('arg1', arg2) }} -->

    <p>{{ total }}</p>
    <!-- 插入组件button-counter，使用 $on(eventName) 监听事件 -->
    <button-counter v-on:increment="incrementTotal"></button-counter>
    <button-counter v-on:increment="incrementTotal"></button-counter>

    <!-- v-bind绑定class和样式 -->
    <div v-bind:class="{ active: isActive }"></div>
    <!-- 可以在对象中传入更多属性用来动态切换多个 class,
         text-danger 类背景颜色覆盖了 active 类的背景色： -->
    <div class="static"
      v-bind:class="{ active: isActive, 'text-danger': hasError }">
    </div>    
    <!-- 可以在这里绑定返回对象的计算属性。这是一个常用且强大的模式 -->
    <div v-bind:class="classObject"></div>
    <!-- 可以把一个数组传给 v-bind:class -->
    <div v-bind:class="[activeClass, errorClass]"></div>

    <!-- 直接的div class定义 -->
    <div class="active"></div>
    <div class="static active text-danger"></div>
    <div class="active text-danger"></div>

    <!-- 可以使用三元表达式来切换列表中的 class  -->
    <div v-bind:class="[errorClass ,isActive ? activeClass : '']"></div>

  </div>
</template>

<script>
import Vue from 'vue'
import Router from 'vue-router'

// 0. 如果使用模块化机制编程，導入Vue和Router，要调用 Vue.use(Router)
Vue.use(Router)
// 1. 定义（路由）组件。
// 可以从其他文件 import 进来
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }
 
// 2. 定义路由
// 每个路由应该映射一个组件。 其中"component" 可以是
// 通过 Vue.extend() 创建的组件构造器，
// 或者，只是一个组件配置对象。
// 我们晚点再讨论嵌套路由。
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]
 
// 3. 创建 router 实例，然后传 `routes` 配置
const router = new Router({
  routes // （缩写）相当于 routes: routes
})
 
// 4. 创建和挂载根实例。
// 记得要通过 router 配置参数注入路由，从而让整个应用都有路由功能
const routertest = new Vue({
  router
})

Vue.component('button-counter',{
  template:'<button v-on:click="incrementHandler">{{counter}}</button>',
  data:function(){
    return{
      counter:0
    } 
  },
  methods: {
    incrementHandler: function () {
      this.counter += 1
      // 使用 $emit(eventName) 触发事件
      this.$emit('increment')
    }
  },
})

// directive注册一个全局自定义指令 v-focus
// Vue.directive('focus', {
//   // 当绑定元素插入到 DOM 中。
//   inserted: function (el) {
//     // 聚焦元素
//     el.focus()
//   }
// })
//自定义v-setstyle指令
Vue.directive('setstyle', function (el, binding) {
	// 简写方式设置文本及背景颜色
	el.innerHTML = binding.value.text
	el.style.backgroundColor = binding.value.color
})

export default {
  //参数
  data () {
    return {
      class1: false,
      vhtml:'v-html test',
      ok: true,
      message: 'runoob',
      id : 1,
      url:'www.baidu.com',
      type:'C',
      isActive:true,
      hasError:true,
      error: null,
      activeClass: 'active',
      errorClass: 'text-danger',
      clicker: 0,
      total: 0,
      //数组定义格式
      sites: [
      { name: 'Runoob' },
      { name: 'Google' },
      { name: 'Taobao' }
    ],
      //对象定义格式
      object: {
        name: 'ss',
        url: 'http://www.ss.com',
        slogan: 'just ss'
      },
      //绑定样式的style对象定义格式
      styleObject: {
        color: 'green',
        fontSize: '20px'
      },
      overrideStyle: {
        color: 'red',
        fontSize: '20px',
        'font-weight': 'bold'
      }
    }
  },
  //方法
  methods: {
    //reverseMessage(): 反转字符串的JS方法
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    },
    //定义方法count()
    greet:function(event){
      //this 表示当前vue实例
      alert('Hello' + this.name + '!')
      if(event)
        alert(greet.target.tagName)
    },
    incrementTotal: function () {
      this.total += 1
    }
  },
  //过滤器
  filters: {
    //capitalize(value): 将输入的第一个字母转为大写的过滤器
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    },
    //capitalize(value): 将输入的第二个字母转为大写的过滤器
    capitalize2: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0)+value.charAt(1).toUpperCase() + value.slice(2)
    }
  },
  //计算属性
  computed: {
    reversedMessage2: function () {
      return "HELLO".split('').reverse().join('')
    },
    site:{
      //getter
      get:function(){
        return this.name + ' ' + this.url
      },
        //setter
      set:function(newValue){
        var names = newValue.split(' ')
        this.name = newValue[0]
        this.url = names[names.length - 1]
      },
      classObject: function () {
        return {
          active: this.isActive && !this.error,
          'text-danger': this.error && this.error.type === 'fatal',
        }
      }
    }
  },
  //自定义局部指令
  directives: {
    // 注册一个局部的自定义指令 v-focus
    focus: {
      // 指令的定义
      inserted: function (el) {
        // 聚焦元素
        el.focus()
      }
    },
    runoob: {
      //钩子函数bind，指令第一次绑定到元素时调用，定义在绑定时执行一次的初始化动作。
      bind: function (el, binding, vnode) {
        var s = JSON.stringify
        el.innerHTML =
        'name: '       + s(binding.name) + '<br>' +
        'value: '      + s(binding.value) + '<br>' +
        'expression: ' + s(binding.expression) + '<br>' +
        'argument: '   + s(binding.arg) + '<br>' +
        'modifiers: '  + s(binding.modifiers) + '<br>' +
        'vnode keys: ' + Object.keys(vnode).join(', ')
      }
    },
    // setstyle: {
    //   //指令函数可以引入一切JavaScript对象
    //   function (el, binding) {
    //   // 简写方式设置文本及背景颜色
    //   el.innerHTML = binding.value.text
    //   el.style.backgroundColor = binding.value.color
    //   }
    // }
  }
}

</script>

<style>
.class1{
  background: #444;
  color: #eee;
}
.active {
	width: 20px;
	height: 20px;
	background: green;
}
.text-danger {
    background: red;
}
</style>