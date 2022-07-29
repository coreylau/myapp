<template>
  <div>
    <header>
      <h1>数据大屏</h1>
    </header>
    <section class="container">
      <section class="itemLeft">
        <ItemPage >
          <ItemOne/>
        </ItemPage>
        <ItemPage >
          <ItemTwo/>
        </ItemPage>
      </section>
      <section class="itemCenter">
        
        <MapPage/>
      </section>
      <section class="itemRight">
        <ItemPage >
          <ItemThree/>
        </ItemPage>
        <ItemPage >
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
import MapPage from "@/components/mapPage.vue";

import {inject} from "vue";
export default {
  components: {
    ItemPage,
    ItemOne,
    ItemTwo,
    ItemThree,
    ItemFour,
    MapPage
},
  setup(){
    let $echarts=inject("echarts");
    let $http=inject("axios");
  }
};
</script>

<style lang="less">
// div{
//   font-size: 0.625rem;
// }
header {
  height: 1.2rem;
  width: 100%;
  background-color: rgba(0, 0, 255, 0.2);
  h1 {
    font-size: 0.5rem;
    color: #fff;
    text-align: center;
    line-height: 1rem;
  }
}

.container {
  min-width: 800px;
  max-width: 1600px;
  margin: 0 auto;
  padding: .05rem .05rem 0;
  // background-color: gray;
  display: flex;
  .itemLeft,
  .itemRight {
    flex: 3;
  }
  .itemCenter {
    flex: 5;
    height: 20rpx;
    border: 1px solid blue;
    padding:.0375rem;
    margin:.0375rem
  }
}
</style>