<template>
  <div class="map" id="map"></div>
</template>

<script>
import axios from "axios";
import { inject, onMounted, reactive } from "vue";

export default {
  setup() {
    let $echarts = inject("echarts");
    // 2.设置请求 并且创建变量接收获取来的数据 不要忘了报漏
    let mapData = reactive({});
    async function getState() {
      mapData = await axios.get("http://localhost:8080/map/china.json");
    }
    onMounted(() => {
      // 3发送请求
      let myChart = $echarts.init(document.getElementById("map"));
      getState().then(() => {
        $echarts.registerMap("china", mapData.data);

        myChart.setOption({
          title: {
            text: "城市销售量",
            left: "45%",
            textStyle: {
              color: "#fff",
              fontSize: 20,
              textShadowBlur: 10, //文字本身的阴影长度。
              textShadowColor: "#33ffff",
            },
          },
          geo: {
            map: "china",
            itemStyle: {
              //地图区域的多边形 图形样式
              areaColor: "#0099ff", //地图区域的颜色。
              borderColor: "#00ffff", //图形的描边颜色。
              shadowColor: "rgba(230,130, 70, 0.5)", //橙色
              shadowBlur: 30, //图形阴影的模糊大小
              emphasis: {
                //高亮状态下的多边形和标签样式。
                focus: "self", //在高亮图形时，是否淡出其它数据的图形已达
              },
            },
          },
          series: [
            {
              type: "scatter", //类型散点图
              itemStyle: {
                //散点图的颜色
                color: "red",
              },
              name: "所在城市销售额",
              coordinateSystem: "geo", //该系列使用的坐标系 geo使用地理坐标系
              data: [
                { name: "北京", value: [116.46, 39.92, 4367] },
                { name: "上海", value: [121.48, 31.22, 8675] },
                { name: "深圳", value: [114.07, 22.62, 2461] },
                { name: "广州", value: [113.23, 23.16, 187] },
                { name: "西安", value: [108.45, 34, 3421] },
              ],
            },
          ],
          tooltip: {
            //提示框组件。
            trigger: "item",
          },
          visualMap: {
            //是视觉映射组件就是地图左下角的选择器
            type: "continuous", // 连续型
            min: 100, // 值域最小值，必须参数
            max: 5000, // 值域最大值，必须参数
            calculable: true, // 是否启用滑动空间
            inRange: {
              color: ["#50a3ba", "#eac736", "#d94e5d"], // 指定数值从低到高时的颜色变
              // 化
            },
            textStyle: {
              color: "#fff", // 值域控件的文本颜色
            },
          },
        });
      });
    });
    return {
      mapData,
    };
  },
};
</script>

<style lang="less">
.map {
  width: 100%;
  height: 100%;
}
</style>