<template>
  <div id="app">
    <img src="./assets/logo.png">
    <el-radio-group v-model="water">
        <el-radio :label="0">进水</el-radio>
        <el-radio :label="1">出水</el-radio>

      </el-radio-group>
    <In :water="water"></In>
    <router-view/>
  </div>
</template>

<script>
  import In from "./components/in"
export default {
  name: 'App',
  components:{In
},
  data(){
    return{
      water:0
    }
  }

}
</script>

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
