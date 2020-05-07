<template>
  <div class="hello">

  <el-card style="height:600px;margin-bottom:100px;">
    <div id="echart" style="width:300px;height:300px" ref="option"></div>
    <div class="select">
      <el-select v-model="cycle">
        <el-option v-for="item in items" :value="item.value" :label="item.label" :key="item.value"></el-option>
      </el-select>
    </div>
    <div class="time">
       <el-date-picker
            v-model="value1"
            :type="type"
            range-separator="至"
            start-placeholder="开始日期"
            end-placeholder="结束日期" style="width:100%;">
          </el-date-picker>
    </div>
    <el-button @click="handle">点击弹出</el-button>
    <el-dialog :visible.sync="view">1111111</el-dialog>
  </el-card>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      items:[
        {value:1,label:"日"},
        {value:2,label:"月"}
      ],
      cycle:1,
      value1:[],
      type:"daterange",
      view:false
    }
  },
  mounted(){
    this.drawLine()
  },
  methods:{
    drawLine(){
      console.log(1)
      let echart=this.$echarts.init(this.$refs["option"])
      console.log(echart)
      let option={
        title:{
          text:'销量集合'
        },
         xAxis: {
                  data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子'],
                  show:false
                },
        yAxis: {show:false},
        tooltip:{
                trigger:'item'
        },
        series: [{
                 name: '销量',
                 type: 'line',
                 data: [5, 20, 36, 10, 10, 20]
                 }]
      }
      echart.setOption(option)
    },
    handle(){
      this.view=true
    }

  },
  watch:{
    cycle(){
      if(this.cycle===1){
        console.log(1)
        this.type="daterange"
      }else{
        console.log(2)
        this.type="monthrange"
      }
    }
  }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.select{
  padding:0;
  width:65px;
}
.time{
  width:30%;
}

</style>
