
<template>
  <div>
    <h2>库存统计图</h2>
    <div class="chart" id="myChartFour">图标的容器</div>
  </div>
</template>

<script>
import { inject, reactive, onMounted } from "vue";
export default {
  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios");

    let data = reactive({});

    async function getState() {
      data = await $http({ url: "/four/data" });
    }

    onMounted(() => {
      getState().then(() => {
        console.log("柱状图4", data);

        let myChart = $echarts.init(document.getElementById("myChartFour"));
        myChart.setOption({
          grid:{
            left:"3%",
            right:"4%",
            bottom:"3%",
            containLabel:true
          },
          xAxis: {
            type: "category",
            data:data.data.chartFour.chartData.day,
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }
          },
          yAxis: {
            type:"value",
            axisLine:{
              lineStyle:{
                color:"#fff"
              }
            }
          },
          legend:{},
          tooltip:{
            trigger:"axis",
            axisPointer:{
              type:"shadow"
            }
          },
          series:[
            {
              name:"日化",
              type:"bar",
              data:data.data.chartFour.chartData.num.Chemicals,
              stack:"total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
            {
              name:"家具",
              type:"bar",
              data:data.data.chartFour.chartData.num.gear,
              stack:"total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
            {
              name:"服饰",
              type:"bar",
              data:data.data.chartFour.chartData.num.Clothes,
              stack:"total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
            {
              name:"数码",
              type:"bar",
              data:data.data.chartFour.chartData.num.digit,
              stack:"total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
            {
              name:"家电",
              type:"bar",
              data:data.data.chartFour.chartData.num.Electrical,
              stack:"total",
              label:{
                show:true
              },
              emphasis:{
                focus:"series"
              }
            },
          ]
        });
      });
    });

    return {
      getState,
      data,
      
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
