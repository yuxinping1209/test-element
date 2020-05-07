<template>
  <div>
   <p>进水</p>
   <div v-if="show">这是进水的标签</div>
   <div v-else>这是出水的标签</div>

  </div>
</template>

<script>
  export default{
    data(){
      return {
       show:true
      }
    },
    props:['water'],
    watch:{
        water(value){
          console.log(value)
          this.show=!this.show

      }
    }


  }
</script>

<style>
.el-radio__inner{
  width:20px;
  height:20px;
}
</style>
