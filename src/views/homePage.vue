<template>
  <div>
    <header>
      <h1>数据可视化</h1>
    </header>
    <section class="container">
      <!-- 左盒子 -->
      <section class="itemLeft">
        <ItemPage>
          <ItemOne />
        </ItemPage>

        <ItemPage>
          <ItemTwo />
        </ItemPage>
      </section>
      <!-- 中 -->
      <section class="itemCenter">
        <MapPage />
      </section>
      <!-- 右边盒子 -->
      <section class="itemRight">
        <ItemPage>
          <ItemThree />
        </ItemPage>
        <ItemPage>
          <ItemFour />
        </ItemPage>
      </section>
    </section>
  </div>
</template>

<script>
import ItemPage from "@/components/itemPage.vue";

import ItemOne from "@/components/itemOne.vue";
import ItemTwo from "@/components/itemTwo.vue";
import ItemThree from "@/components/itemThree.vue";
import ItemFour from "@/components/itemFour.vue";
import MapPage from "@/components/mapPage.vue";
import { inject } from "vue";
export default {
  components: {
    ItemPage,
    ItemOne,
    ItemTwo,
    ItemThree,
    ItemFour,
    MapPage,
  },

  setup() {
    // let $echarts=inject("echarts");
    // let $http=inject("axios")
  },
};
</script>

<style lang="less">
header {
  height: 2.5rem;
  width: 100%;
  background-color: rgba(0, 0, 255, 0.2);
  h1 {
    font-size: 1.5rem;
    color: #fff;
    line-height: 2.5rem;
    text-align: center;
  }
}

//大容器样式设置
.container {
  min-width: 1200px;
  max-width: 2048px;
  margin: 0 auto;
  padding: 0.125rem 0.125rem 0;
  //   background-color: gray;
  display: flex;
  // 设置左右配置
  .itemLeft,
  .itemRight {
    flex: 3;
  }
  .itemCenter {
    height: 30.25rem;
    padding: 0.625rem;
    margin: 0.25rem;
    border: 1px solid blue;
    flex: 5;
  }
}
</style>