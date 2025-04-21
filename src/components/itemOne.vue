
<template>
  <div>
    <h2>销售总量</h2>
    <div class="chart" id="oneChart">图标的容器</div>
  </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";
export default {
  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios");

    let data = reactive({});
    let xData = reactive([]);
    let yData = reactive([]);

    function setData() {
      xData = data.data.chartOne.chartData.map((v) => v.title);
      yData = data.data.chartOne.chartData.map((v) => v.num);
      console.log("xData", xData);
      console.log("yData", yData);
    }

    async function getState() {
      data = await $http({ url: "/one/data" });
      // console.log(oneData.data.chartOne.chartData);
    }

    onMounted(() => {
      //调用请求函数
      getState().then(() => {
        setData();
        myChart.setOption({
          grid:{
            top:"3%",
            left:"1%",
            right:"6%",
            bottom:"3%",
            containLabel:true
            
          },
          xAxis: {
            type: "value",
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }
          },
          yAxis: {
            type: "category",
            data: xData,
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }
          },
          series: [
            {
              data: yData,
              type: "bar",
              itemStyle: {
                normal: {
                  barBorderRadius:[0,20,20,0],
                  color: new $echarts.graphic.LinearGradient(0, 0, 1, 0, [
                    {
                      offset: 0,
                      color: "#005eaa",
                    },
                    {
                      offset: 0.5,
                      color: "#339ca8",
                    },
                    {
                      offset: 1,
                      color: "#cda819",
                    },
                  ]),
                },
              },
            },
          ],
        });
      });
      let myChart = $echarts.init(document.getElementById("oneChart"));
    });
    return {
      getState,
      setData,
      data,
      xData,
      yData,
    };
  },
};
</script>
<style scoped>
.chart {
  height: 4.5rem;
}
h2 {
  height: 0.6rem;
  color: white;
  line-height: 0.6rem;
  font-size: 0.25rem;
  text-align: center;
}
</style>
