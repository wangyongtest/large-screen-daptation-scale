<template>
  <section class="parentRoot">
    <section class="screen" id="screen">
      <section class="layoutLeft">
        <section class="container">
          <section class="chartItem">
            <chart-com :chart-options="option" />
          </section>
          <section class="chartItem">
            <chart-com :chart-options="option" />
          </section>
          <section class="chartItem">
            <chart-com :chart-options="option" />
          </section>
        </section>
      </section>
      <section class="layoutCenter"></section>
      <section class="layoutRight">
        <section class="container">
          <section class="chartItem">
            <chart-com :chart-options="option" />
          </section>
          <section class="chartItem">
            <chart-com :chart-options="option" />
          </section>
          <section class="chartItem">
            <chart-com :chart-options="option" />
          </section>
        </section>
      </section>
    </section>
  </section>
</template>
<script setup lang="ts">
import { onMounted } from "vue";
import { handleScreenAuto } from "@/utils/scale.ts";
import { option } from "./chart.ts";

import ChartCom from "@/components/chartCommon.vue";

onMounted(() => {
  handleScreenAuto();
  window.addEventListener("resize", () => {
    handleScreenAuto();
  });
});
</script>
<style lang="less" scoped>
.parentRoot {
  width: 100%;
  height: 100%;
  background-color: pink;
  position: relative;
  .screen {
    /*  设计稿的宽度 */
    width: 1920px;
    /* 设计稿的高度 */
    height: 960px;
    transform-origin: 0 0;
    position: absolute;
    left: 50%;
    top: 50%;
    // border: 10px solid red;
    .layoutLeft {
      width: 25%;
      height: 100%;
      position: absolute;
      left: 0;
      z-index: 1;
      .container {
        width: 100%;
        height: 100%;
        display: grid;
        grid-template-rows: repeat(3, 1fr);
        grid-row-gap: 10px;
        .chartItem {
          width: 100%;
          height: 100%;
        }
      }
    }
    .layoutCenter {
      width: 100%;
      height: 100%;
      position: absolute;
      background-color: #ccc;
    }
    .layoutRight {
      width: 25%;
      height: 100%;
      position: absolute;
      right: 0;
      z-index: 1;
      .container {
        width: 100%;
        height: 100%;
        display: grid;
        grid-template-rows: repeat(3, 1fr);
        grid-row-gap: 10px;
        .chartItem {
          width: 100%;
          height: 100%;
        }
      }
    }
  }
}
</style>
