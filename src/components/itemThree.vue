<template>
  <div>
    <h2>图表</h2>
    <div class="chart" id="myPieChart"></div>
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
        console.log(data)
        let myChart = $echarts.init(document.getElementById("myPieChart"));
        myChart.setOption({
          grid:{
            top:"20%",
            // bottom:"20%",
            left:"30%"
          },
          // legend: {
          //   //设置图例
          //   top: "bottom", //放到最下面
          // },
          series: [
            {
              // name: 'Nightingale Chart',
              type: "pie", //饼图
              radius: [10, 100], //饼图的半径数组的第一项是内半径，第二项是外半径
              center: ["50%", "45%"], //饼图的中心（圆心）坐标，数组的第一项是横坐标，第
              // 二项是纵坐标。
              roseType: "area", //设置成玫瑰图
              itemStyle: {
                borderRadius: 10, //用于指定饼图扇形区块的内外圆角半径，
              },
              data: data.data.chartThree.chartData, //数据
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
h2 {
  /* 48像素 */
  height: 1rem;
  color: #fff;
  line-height: 1rem;
  text-align: center;
  font-size: 0.8rem;
}
.chart {
  /* 高度360 */
  height: 14rem;
  /* background-color: gray; */
}
</style>