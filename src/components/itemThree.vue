
<template>
  <div>
    <h2>库存统计</h2>
    <div class="chart" id="chart">图标的容器</div>
  </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";
export default {
  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios");

    let data = reactive({});

    async function getState() {
      data = await $http({ url: "/three/data" });
    }

    onMounted(() => {
      getState().then(() => {
        console.log("饼状图", data.data.chartThree.chartData);

        let myChart = $echarts.init(document.getElementById("chart"));
        myChart.setOption({
          legend:{
            top:"bottom"
          },
          tooltip:{
            show:true,
          },
          series: [
            {
              type: "pie",
              data: data.data.chartThree.chartData,
              radius:[10,100],
              center:["50%","45%"],
              roseType:"area",
              itemStyle:{
               
                borderRadius:10
              },
              
            },
          ],
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
