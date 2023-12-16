<template>
  <div>
    <h2>图表</h2>
    <div class="chart" id="chartDomd"></div>
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
      data = await $http({ url: "four/data" });
    }
    onMounted(() => {
      getState().then(() => {
        console.log("柱状图", data.data);
        let myChart = $echarts.init(document.getElementById("chartDomd"));
        myChart.setOption({
          xAxis: {
            // 设置坐标轴上文字颜色
            axisLine: {
              lineStyle: {
                color: "#fff",
              },
            },
            type: "category",
            data: data.data.chartFour.chartData.day,
          },
          yAxis: {
            // 设置坐标轴上文字颜色
            axisLine: {
              lineStyle: {
                color: "#fff",
              },
            },
            type: "value",
          },
          tooltip: {
            trigger: "axis",
            axisPointer: {
              //设置鼠标选中样式为阴影
              type: "shadow",
            },
          },
          legend: {}, //图例
          grid: {
            //位置
            left: "3%",
            right: "4%",
            bottom: "3%",
            containLabel: true, //设置包含坐标轴
          },
          series: [
            {
              name: "服饰",
              type: "bar",
              data: data.data.chartFour.chartData.num.Chemicals,
              stack: "total",
              label: {
                //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
                show: true,
              },
              emphasis: {
                //高亮的图形样式和标签样式。
                focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
              },
            },
            {
              name: "数码",
              type: "bar",
              data: data.data.chartFour.chartData.num.Clothes,
              stack: "total",
              label: {
                //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
                show: true,
              },
              emphasis: {
                //高亮的图形样式和标签样式。
                focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
              },
            },
            {
              name: "家电",
              type: "bar",
              data: data.data.chartFour.chartData.num.Electrical,
              stack: "total",
              label: {
                //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
                show: true,
              },
              emphasis: {
                //高亮的图形样式和标签样式。
                focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
              },
            },
            {
              name: "家居",
              type: "bar",
              data: data.data.chartFour.chartData.num.digit,
              stack: "total",

              // ##
              // 66.项目打包
              // vue项目中大家在运行的时候我们是需要用内置的devServer帮助我们自动项目 开发过程中没有问题
              label: {
                //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
                show: true,
              },
              emphasis: {
                //高亮的图形样式和标签样式。
                focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
              },
            },
            {
              name: "日化",
              type: "bar",
              data: data.data.chartFour.chartData.num.gear,
              stack: "total",
              label: {
                //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
                show: true,
              },
              emphasis: {
                //高亮的图形样式和标签样式。
                focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
              },
            },
          ],
        });
      });
      return {
        getState,
        data,
      };
    });
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