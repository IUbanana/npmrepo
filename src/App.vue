<!-- 展示模板，写html -->
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <!-- 标签形式插入组件 -->
    <comptest></comptest>
    <runoobcomp></runoobcomp>
  </div>
</template>

<!-- 脚本代码，写JavaScript -->
<script>
//导入组件
import comptest from './components/CompTest'
import runoobcomp from './components/runoobcomp'

export default {
  name:'app',
  components:{ 
    comptest,
    runoobcomp
  }
}


</script>

<!-- 样式代码，写CSS -->
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
