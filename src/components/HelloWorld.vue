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
        <el-date-picker v-model="value1" :type="type" range-separator="至" start-placeholder="开始日期" end-placeholder="结束日期"
          style="width:100%;">
        </el-date-picker>
      </div>
      <el-button @click="handle">点击弹出</el-button>
      <el-dialog :visible.sync="view">1111111</el-dialog>
    </el-card>
    <div ref="change" style="width:300px; height:300px; border:1px solid red;" @mousemove="onchange"></div>
    <div class="toggle">
      <div class="wrapper" style="width:110px;height:30px;border-radius:20px;border:1px solid #f0f1f2;background-color:#f0f1f2;justify-content: space-around;">
        <div :class="{'isactive':isshow==true}" style="width:70px;height:28px;border-radius:20px;" class="flex j-center a-center"
          @click="changeday">天</div>
        <div :class="{'isactive':isshow==false}" style="width:70px;height:28px;border-radius:20px;" class="flex j-center a-center"
          @click="changemonth">月</div>
      </div>
    </div>
    <div class="circle">

    </div>
    <div class="circle3">

    </div>
    <div class="circle2">

    </div>
  </div>

</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
        items: [{
            value: 1,
            label: "日"
          },
          {
            value: 2,
            label: "月"
          }
        ],
        cycle: 1,
        value1: [],
        type: "daterange",
        view: false,
        timer: null,
        isshow: true
      }
    },
    mounted() {
      this.drawLine()
    },
    methods: {
      drawLine() {
        console.log(1)

        var data = [120, 200, 150, 80, 70, 110, 130]
        var max = data.sort(function(a,b){
          return b-a
        })

        max.length = 2

        console.log(max)

        let echart = this.$echarts.init(this.$refs["option"])
        console.log(echart)
        let option = {
          xAxis: {
            type: 'category',
            data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
          },
          yAxis: {
            type: 'value'
          },
          series: [{
            data: [120, 200, 150, 80, 70, 110, 130],
            type: 'bar',
            label: {
              show: true,
              position: ['40%', '5%'],
              color: '#eee',
               formatter:function(e){
                if(max.indexOf(e.value)>-1){
                  return 'x'
                }else{
                  return 's'
                }
               }
            },
            itemStyle:{
              color:function(e){
                if(max.indexOf(e.value)>-1){
                   return '#000000'
                 }else{
                   return '#eee'
                 }
                }
              }
            }]
       
        };

        echart.setOption(option)
      },
      handle() {
        this.view = true
      },
      changeday() {
        this.isshow = true
      },
      changemonth() {
        this.isshow = false
      },
      onchange(e) {
        const that = this
        //清除定时器会直接跳到最后的结果，而不显示过程
        clearTimeout(that.timer)
        that.timer = setTimeout(() => {
          let div = that.$refs.change
          div.innerHTML = `(${e.clientX},${e.clientY})`
        }, 1000)

      }
    },
    watch: {
      cycle() {
        if (this.cycle === 1) {
          console.log(1)
          this.type = "daterange"
        } else {
          console.log(2)
          this.type = "monthrange"
        }
      }
    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1,
  h2 {
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

  .select {
    padding: 0;
    width: 65px;
  }

  .time {
    width: 30%;
  }

  .isactive {
    color: #3A8EE6;
    background-color: white;
  }

  .wrapper {
    display: flex;
    align-items: center;
  }

  .circle {
    width: 100px;
    height: 100px;
    border: 1px solid #000000;
    border-radius: 50%;
  }

  .circle2 {
    width: 100px;
    height: 100px;
    border: 2px solid #000000;
    border-radius: 50%;
  }

  .circle3 {
    width: 100px;
    height: 100px;
    border: 2px solid #000000;
    border-radius: 50%;
    transform: scale(0.4);
  }
</style>
