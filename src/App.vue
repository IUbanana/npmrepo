<!-- 展示模板，写html -->
<template>
  <div id="app">
    <img src="./assets/logo.png">

    <el-button @click="visible = true">按钮</el-button>
    <el-dialog :visible.sync="visible" title="Hello world">
      <p>欢迎使用 Element</p>
    </el-dialog>

    <!-- 标签形式插入组件 -->
    <globalcomp></globalcomp>
    <input v-model="parentMsg">
    <localcomp v-bind:msg="parentMsg"></localcomp>
    <comptest></comptest>
    <runoobcomp></runoobcomp>
  </div>
</template>

<!-- 脚本代码，写JavaScript -->
<script src="//unpkg.com/vue/dist/vue.js"></script>
<script src="//unpkg.com/element-ui/lib/index.js"></script>
<script>
//导入Vue
import Vue from 'vue'
import Element from 'element-ui'
//导入组件
import comptest from './components/CompTest'
import runoobcomp from './components/runoobcomp'

Vue.use(Element, { size: 'small' })

var Main = {
  data() {
    return {
      visible: false
    }
  }
}
var Ctor = Vue.extend(Main)
new Ctor().$mount('#app')

//注册全局组件，可在html中直接标签导入
Vue.component('globalcomp',{
  template:'<h2>自定义全局组件</h2>'
  //声明props，传递数据
})

//定义局部组件
var local = {
  // template: '<h2>自定义局部组件</h2>',
  props: ['msg'],
  template: '<span>props传递的数据：{{msg}}</span>'
}

export default{
  // name:'app',
  data () {
    return {
      parentMsg: 'parentContent'
    }
  },
  components: { 
    //注册局部组件
    'localcomp': local,
    //import的组件也要注册
    comptest,
    runoobcomp
  }

}
</script>

<!-- 样式代码，写CSS -->
<style>
@import url("//unpkg.com/element-ui/lib/theme-chalk/index.css");
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */

</style>
