<template>
  <div class="chartContainer">
    <h2>图表</h2>
    <div class="chart" id="oneChart"></div>
  </div>
</template>
  
  <script>
import { inject, onMounted, reactive } from "vue";

export default {
  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios");

    // 初始化数据
    let data = reactive({});
    let xdata = reactive([]);
    let ydata = reactive([]);

    function setData() {
      xdata = data.data.chartData.chartData.map((v) => v.title);
      ydata = data.data.chartData.chartData.map((v) => v.num);
      console.log("xdata", xdata);
      console.log("ydata", ydata);
    }

    // axios请求
    async function getState() {
      data = await $http({ url: "/one/data" });
    }

    onMounted(() => {
      let myChart = $echarts.init(document.getElementById("oneChart"));
      getState().then(() => {
        setData();

        myChart.setOption({
          grid: {
            top: "3%",
            // right: "",
            left:"1%",
            bottom:"3%",
            containLabel:true,
          },
          xAxis: {
            type: "value",
            axisLine: {
              lineStyle: {
                color: "#fff",
              },
            },
          },
          yAxis: {
            type: "category",
            data: xdata,
            axisLine: {
              lineStyle: {
                color: "#fff",
              },
            },
          },
          series: [
            {
              type: "bar",
              data: ydata,
              itemStyle: {
                normal: {
                  barBorderRadius: [0, 20, 20, 0],
                  // 渐变颜色
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

      // 输出
      return {
        getState,
        data,
        xdata,
        ydata,
        setData,
      };
    });
  },
};
</script>
  
  <style scoped>
h2 {
  /* 48像素 */
  margin-top: 0.25rem;
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