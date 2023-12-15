<template>
  <div>
    <header>
      <h1>数据可视化</h1>
    </header>
    <section class="container">
      <section class="itemLeft">
        <ItemPage>
            <ItemOne/>
        </ItemPage>

        <ItemPage>
            <ItemTwo/>
        </ItemPage>
      </section>

      <section class="itemCenter"></section>
      <section class="itemRight">
        <ItemPage>
            <ItemThree/>
        </ItemPage>
        <ItemPage>
            <ItemFour/>
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
export default {
  components: { 
    ItemPage, ItemOne,ItemTwo,ItemThree,ItemFour
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
    line-height: 1.5rem;
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
    height: 30rem;
    padding: 0.625rem ;
    margin: .25rem;
    border: 1px solid blue;
    flex: 5;
  }
}
</style>