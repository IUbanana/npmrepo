<template>
  <div id="runoobcomp">
    <h2>Runoob Test</h2>    

    <!-- 判断class1的值，true则使用class1的样式 -->
    <label for="r1">修改颜色</label>
    <input type="checkbox" v-model="class1" id="r1"><br>
    <!-- v-bind 指令被用来响应地更新 HTML 属性，HTML 属性写在v-bind中 -->
    <div v-bind:class="{'class1': class1}">
      directiva v-bind:class
    </div>

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

    <!-- 可以在 v-bind:style 直接设置样式 -->
    <div v-bind:style="{ color: 'green', fontSize: '20px' }">内嵌style</div>
    <!-- 可以直接绑定到一个样式对象，让模板更清晰。style对象在data块中定义-->
    <div v-bind:style="styleObject">绑定style</div>
    <!-- v-bind:style 可以使用数组将多个样式对象应用到一个元素上 -->
    <div v-bind:style="[styleObject, overrideStyle]">style数组</div>
    
    <!-- v-bind绑定href参数和url变量值 -->
    <pre><a v-bind:href="url">this is a link</a></pre>
    <!-- v-bind提供缩写 -->
    <pre><a :href="url">this is a link, too</a></pre>

    <!-- Vue.js 提供了完全的 JavaScript 表达式支持 -->
    {{5+5}}
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
    <button @click="reverseMessage">反转2</button>
    <button @click="count"></button><br>

    <!-- 过滤器，过滤器函数接受表达式的值作为第一个参数-->
    <!-- 在两个大括号中的过滤器 -->
    {{ message | capitalize }}<br>
    <!-- 在 v-bind 指令中的过滤器 -->
    <!-- <div v-bind:id="rawId | formatId"></div> -->
    <!-- 过滤器可以串联 -->
    {{ message | capitalize | capitalize2 }}<br>
    <!-- 过滤器是 JavaScript 函数，因此可以接受参数 -->
    <!-- {{ message | filterA('arg1', arg2) }} -->

  </div>
</template>
 
<script>

export default {
  //参数
  data () {
    return {
      class1: false,
      vhtml:'v-html test',
      ok: true,
      message: 'dunoob',
      id : 1,
      url:'www.baidu.com',
      type:'C',
      isActive:true,
      hasError:true,
      error: null,
      activeClass: 'active',
      errorClass: 'text-danger',
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