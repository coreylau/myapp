<template>
  <div>
      <h2>销售总量</h2>
      <div class="chart" id="oneChart">
          图表的容器
        </div>
  </div>
</template>

<script>
import {inject,onMounted,reactive} from 'vue'
export default {
  setup(){
    let $echarts=inject("echarts")
    let $http=inject("axios")

    let data=reactive({})
    let xdata=reactive([])
    let ydata=reactive([])
    function setData(){
      xdata= data.data.chartData.chartData.map(v=>v.title)
      ydata= data.data.chartData.chartData.map(v=>v.num)
      // console.log("xdata",xdata)
    }

    async function getState(){
      data=await $http({url:"/one/data"})
      // console.log(oneData.data.chartData.chartData)
    }
    
    onMounted(()=>{
      let myChart=$echarts.init(document.getElementById("oneChart"))
      // 调用请求
      getState().then(()=>{
        setData()
        myChart.setOption({
          grid:{
            top:"1%",
            left:"1%",
            right:"10%",
            bottom:"15%",
            containLabel:true
          },
          xAxis:{
            type:"value",
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }},
          yAxis:{
            type:"category",
            data:xdata,
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }},
          series:[
            {
              data:ydata,
              type:"bar",
              itemStyle:{
                normal:{
                  barBorderRadius:[0,20,20,0],
                  color:new $echarts.graphic.LinearGradient(0,0,1,0,[
                  {
                    offset:0,
                    color:"#005eaa"
                  },
                  {
                    offset:0.5,
                    color:"#339ca8"
                  },
                  {
                    offset:1,
                    color:"#cda819"
                  }]
                  )
                }
              }

            }
          ]
        })
      })
    })
    return{
      getState,data,xdata,ydata,setData
    }
  }
}
</script>

<style scoped>
.chart{
  height:5rem;
}
h2{
  height:0.8rem;
  color: #fff;
  line-height: 0.5rem;
  font-size:0.35rem;
  text-align:center;
}
</style>